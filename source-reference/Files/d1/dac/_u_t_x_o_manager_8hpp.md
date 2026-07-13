---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/UTXOManager.hpp
summary: In-memory and persisted UTXO state manager with reservation and checkpoint helpers. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/UTXOManager.hpp



In-memory and persisted UTXO state manager with reservation and checkpoint helpers.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::OutPointHash](/source-reference/Classes/d5/d40/structsgns_1_1_out_point_hash/)** <br/>Hash functor for using [OutPoint](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/) keys in unordered containers.  |
| class | **[sgns::UTXOManager](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/)** <br/>Owns the local UTXO set, supports coin selection, validation, persistence, reservations, and deterministic snapshot hashing.  |
| struct | **[sgns::UTXOManager::UTXOEntry](/source-reference/Classes/d5/d7d/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_entry/)** <br/>Metadata tracked for each outpoint in the local registry.  |
| struct | **[sgns::UTXOManager::UTXOCheckpoint](/source-reference/Classes/dc/d6b/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_checkpoint/)** <br/>Persisted checkpoint snapshot used to audit finalized UTXO state at a given epoch.  |

## Detailed Description

In-memory and persisted UTXO state manager with reservation and checkpoint helpers. 

**Date**: 2026-01-20 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef SGNS_UTXO_MANAGER_HPP
#define SGNS_UTXO_MANAGER_HPP

#include "GeniusUTXO.hpp"
#include "UTXOStructs.hpp"

#include "base/logger.hpp"
#include "crdt/globaldb/globaldb.hpp"
#include "storage/rocksdb/rocksdb.hpp"

#include <optional>
#include <shared_mutex>
#include <unordered_map>
#include <unordered_set>

namespace sgns
{
    struct OutPointHash
    {
        size_t operator()( const OutPoint &outpoint ) const
        {
            size_t seed = std::hash<base::Hash256>{}( outpoint.txid_hash_ );
            boost::hash_combine( seed, outpoint.output_idx_ );
            return seed;
        }
    };

    class UTXOManager
    {
    public:
        enum class UTXOState : uint8_t
        {
            UTXO_READY = 0,        
            UTXO_CONSUMED = 1,     
            UTXO_RESERVED = 2      
        };

        enum class UTXOType : uint8_t
        {
            UTXO_NORMAL = 0, 
            UTXO_BRIDGE = 1  
        };

        using UTXOData = std::pair<UTXOState, GeniusUTXO>;

        struct UTXOEntry
        {
            UTXOState                    state{ UTXOState::UTXO_READY }; 
            GeniusUTXO                   utxo;                           
            uint64_t                     created_epoch{ 0 };             
            std::optional<uint64_t>      spent_epoch;   
            std::optional<base::Hash256> spent_by_txid; 
            UTXOType                     type{ UTXOType::UTXO_NORMAL }; 
        };

        struct UTXOCheckpoint
        {
            std::string owner_address; 
            uint64_t    epoch{ 0 };    
            base::Hash256
                last_finalized_tx{}; 
            base::Hash256 registry_hash{};    
            base::Hash256 utxo_merkle_root{}; 
            uint64_t      utxo_count{ 0 };    
            uint64_t      created_at_ms{ 0 }; 
        };

        using UTXOOutPointMap = std::unordered_map<OutPoint, UTXOEntry, OutPointHash>;
        using AddressOutPointList = std::unordered_map<std::string, std::vector<OutPoint>>;
        using SignFunc = std::function<std::vector<uint8_t>( const std::vector<uint8_t> &data )>;
        using VerifySignatureFunc = std::function<bool( const std::string          &address,
                                                        const std::vector<uint8_t> &signature,
                                                        const std::vector<uint8_t> &data )>;

        UTXOManager( std::string address, SignFunc sign, VerifySignatureFunc verify_signature ) :
            address_( std::move( address ) ),
            sign_( std::move( sign ) ),
            verify_signature_( std::move( verify_signature ) )
        {
        }

        [[nodiscard]] uint64_t GetBalance() const;

        [[nodiscard]] uint64_t GetBalance( const std::string &address ) const;

        uint64_t GetBalance( const TokenID &token_id ) const;

        uint64_t GetBalance( const TokenID &token_id, const std::string &address ) const;

        outcome::result<bool> PutUTXO( GeniusUTXO         new_utxo,
                                       const std::string &address,
                                       UTXOType           type = UTXOType::UTXO_NORMAL );

        outcome::result<bool> PutUTXO( const GeniusUTXO &new_utxo )
        {
            return PutUTXO( new_utxo, address_ );
        }

        outcome::result<void> DeleteUTXO( const base::Hash256 &utxo_id,
                                          uint32_t             output_idx,
                                          const std::string   &address );

        outcome::result<bool> ConsumeUTXOs( const std::vector<InputUTXOInfo> &infos,
                                            const std::string                &address,
                                            UTXOType                          type = UTXOType::UTXO_NORMAL );

        outcome::result<bool> ConsumeUTXOs( const std::vector<InputUTXOInfo> &infos,
                                            UTXOType                          type = UTXOType::UTXO_NORMAL )
        {
            return ConsumeUTXOs( infos, address_, type );
        }

        std::vector<GeniusUTXO> GetUTXOs( const std::string &address ) const;

        std::vector<GeniusUTXO> GetUTXOs() const
        {
            return GetUTXOs( address_ );
        }

        std::vector<GeniusUTXO> GetUnconsumedUTXOs( const std::string &address ) const;

        std::optional<GeniusUTXO> GetUnconsumedUTXO( const base::Hash256 &txid, uint32_t output_idx ) const;

        std::unordered_map<std::string, std::vector<UTXOData>> GetAllUTXOs() const;

        outcome::result<void> SetUTXOs( const std::vector<GeniusUTXO> &utxos, const std::string &address );

        outcome::result<void> SetUTXOs( const std::vector<GeniusUTXO> &utxos )
        {
            return SetUTXOs( utxos, address_ );
        }

        outcome::result<UTXOTxParameters> CreateTxParameter( uint64_t    amount,
                                                             std::string dest_address,
                                                             TokenID     token_id );

        outcome::result<UTXOTxParameters> CreateTxParameter( const std::vector<OutputDestInfo> &destinations,
                                                             const TokenID                     &token_id );

        void ReserveUTXOs( const std::vector<InputUTXOInfo> &inputs,
                           const std::string                &reservation_id,
                           UTXOType                          type = UTXOType::UTXO_NORMAL );

        void RollbackUTXOs( const std::vector<InputUTXOInfo> &inputs,
                            const std::string                &reservation_id,
                            UTXOType                          type = UTXOType::UTXO_NORMAL );

        bool VerifyParameters( const UTXOTxParameters &params ) const
        {
            return VerifyParameters( params, address_ );
        }

        bool VerifyParameters( const UTXOTxParameters &params, const std::string &address ) const;

        std::optional<UTXOState> GetOutPointState( const base::Hash256 &utxo_id, uint32_t output_idx ) const;

        bool IsOutPointConsumed( const base::Hash256 &utxo_id, uint32_t output_idx ) const;

        bool IsOutPointReserved( const base::Hash256 &utxo_id, uint32_t output_idx ) const;

        [[nodiscard]] base::Hash256 ComputeUTXOMerkleRoot() const;

        [[nodiscard]] base::Hash256 ComputeUTXOMerkleRoot( const std::string &address ) const;

        [[nodiscard]] base::Hash256 ComputeUTXOMerkleRootFromSnapshot( const std::vector<GeniusUTXO> &utxos ) const;

        outcome::result<bool> LoadUTXOs( std::shared_ptr<storage::rocksdb> db );

        void ReleaseStorage();

        outcome::result<void> StoreUTXOs( const std::string &address );

        outcome::result<void> CreateCheckpoint( uint64_t             epoch,
                                                const base::Hash256 &last_finalized_tx,
                                                const base::Hash256 &registry_hash );

        outcome::result<void> CreateCheckpoint( const std::string   &address,
                                                uint64_t             epoch,
                                                const base::Hash256 &last_finalized_tx,
                                                const base::Hash256 &registry_hash );

        outcome::result<std::optional<UTXOCheckpoint>> LoadLatestCheckpoint() const
        {
            return LoadLatestCheckpoint( address_ );
        }

        outcome::result<std::optional<UTXOCheckpoint>> LoadLatestCheckpoint( const std::string &address ) const;

    private:
        static constexpr std::string_view DB_PREFIX = "/utxo";
        static constexpr std::string_view CHECKPOINT_PREFIX = "/utxo-checkpoint";

        std::shared_ptr<storage::rocksdb> AcquireStorage() const;

        outcome::result<std::pair<std::vector<InputUTXOInfo>, uint64_t>> SelectUTXOs( uint64_t       required_amount,
                                                                                      const TokenID &token_id );

        void SignInputs( std::vector<InputUTXOInfo> &inputs ) const;

        base::Logger logger_ = base::createLogger( "UTXOManager" );

        std::string         address_;          
        SignFunc            sign_;             
        VerifySignatureFunc verify_signature_; 
        std::shared_ptr<storage::rocksdb> db_; 

        mutable std::shared_mutex utxos_mutex_;       
        UTXOOutPointMap           utxo_outpoints_;    
        AddressOutPointList       address_outpoints_; 
        std::unordered_map<OutPoint, std::string, OutPointHash> local_reservations_;
    };

}

#endif // SGNS_UTXO_MANAGER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

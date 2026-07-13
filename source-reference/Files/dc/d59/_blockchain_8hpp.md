---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/blockchain/Blockchain.hpp
summary: Header file for the Blockchain class, which provides an interface for block storage operations. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/blockchain/Blockchain.hpp



Header file for the Blockchain class, which provides an interface for block storage operations.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/)** <br/>Manages genesis/account-creation blocks and consensus integration.  |

## Functions

|                | Name           |
| -------------- | -------------- |
| | **[OUTCOME_HPP_DECLARE_ERROR_2](/source-reference/Files/dc/d59/_blockchain_8hpp/#function-outcome_hpp_declare_error_2)**([sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/) , Blockchain::Error )<br/>Macro for declaring error handling in the IBasicProof class.  |

## Detailed Description

Header file for the Blockchain class, which provides an interface for block storage operations. 

**Date**: 2025-10-16 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 

## Functions Documentation

### function OUTCOME_HPP_DECLARE_ERROR_2

```cpp
OUTCOME_HPP_DECLARE_ERROR_2(
    sgns ,
    Blockchain::Error 
)
```

Macro for declaring error handling in the IBasicProof class. 



## Source code

```cpp


#ifndef SGNS_BLOCKCHAIN_HPP
#define SGNS_BLOCKCHAIN_HPP

#include <memory>
#include <map>
#include <functional>
#include <string>
#include <string_view>
#include <vector>
#include <cstdint>
#include <atomic>
#include <optional>
#include <unordered_map>
#include "outcome/outcome.hpp"
#include "crdt/globaldb/globaldb.hpp"
#include "crdt/proto/delta.pb.h"
#include "account/GeniusAccount.hpp"
#include "blockchain/impl/proto/SGBlockchain.pb.h"
#include "blockchain/Consensus.hpp"
#include "base/buffer.hpp"
#include "crdt/crdt_callback_manager.hpp"
#include "base/sgns_version.hpp"

namespace sgns
{
    class ValidatorRegistry;

    class Migration3_5_0To3_6_0;
    class Migration3_6_0To3_7_0;

    class Blockchain : public std::enable_shared_from_this<Blockchain>
    {
    public:
        enum class Error
        {
            GENESIS_BLOCK_CREATION_FAILED = 0,           
            GENESIS_BLOCK_INVALID_SIGNATURE,             
            GENESIS_BLOCK_UNAUTHORIZED_CREATOR,          
            GENESIS_BLOCK_SERIALIZATION_FAILED,          
            GENESIS_BLOCK_MISSING,                       
            ACCOUNT_CREATION_BLOCK_MISSING,              
            ACCOUNT_CREATION_BLOCK_CREATION_FAILED,      
            ACCOUNT_CREATION_BLOCK_INVALID_SIGNATURE,    
            ACCOUNT_CREATION_BLOCK_SERIALIZATION_FAILED, 
            ACCOUNT_CREATION_BLOCK_INVALID_GENESIS_LINK, 
            VALIDATOR_REGISTRY_CREATION_FAILED,          
            BLOCKCHAIN_NOT_INITIALIZED,                  
        };

        using BlockchainCallback = std::function<void( outcome::result<void> )>;

        static std::shared_ptr<Blockchain> New( std::shared_ptr<crdt::GlobalDB>            global_db,
                                                std::shared_ptr<GeniusAccount>             account,
                                                std::shared_ptr<ipfs_pubsub::GossipPubSub> pubsub,
                                                BlockchainCallback                         callback );

        ~Blockchain();

        outcome::result<void> Start();
        outcome::result<void> Stop();

        outcome::result<void> OnGenesisBlockReceived( const base::Buffer &serialized_genesis );

        outcome::result<void> OnAccountCreationBlockReceived( const base::Buffer &serialized_account_creation );

        static void SetAuthorizedFullNodeAddress( const std::string &pub_address );

        static const std::string &GetAuthorizedFullNodeAddress();

        outcome::result<std::string> GetGenesisCID() const;
        outcome::result<std::string> GetAccountCreationCID() const;
        std::shared_ptr<ValidatorRegistry> GetValidatorRegistry() const;

        void SetFullNodeMode();

        bool RegisterSubjectHandler( std::string_view subject_type, ConsensusManager::SubjectHandler handler );
        void UnregisterSubjectHandler( std::string_view subject_type );
        bool RegisterCertificateHandler( std::string_view                            subject_type,
                                         ConsensusManager::CertificateSubjectHandler handler );
        void UnregisterCertificateHandler( std::string_view subject_type );
        bool RegisterProposalCleanupHandler( std::string_view                         subject_type,
                                             ConsensusManager::ProposalCleanupHandler handler );

        void RegisterSlotKeyHandler( std::string_view subject_type, ConsensusManager::SlotKeyHandler handler );

        void SetSlotHashPopulator( ConsensusManager::SlotHashPopulator populator );

        void UnregisterSlotKeyHandler( std::string_view subject_type );

        outcome::result<ConsensusManager::Subject> CreateConsensusNonceSubject(
            const std::string                             &account_id,
            uint64_t                                       nonce,
            const std::string                             &tx_hash,
            const EmbeddedTransaction                     &transaction,
            const std::optional<UTXOTransitionCommitment> &utxo_commitment,
            const std::optional<UTXOWitness>              &utxo_witness );

        outcome::result<ConsensusManager::Proposal> CreateConsensusProposal(
            const std::string                             &account_id,
            uint64_t                                       nonce,
            const std::string                             &tx_hash,
            const EmbeddedTransaction                     &transaction,
            const std::optional<UTXOTransitionCommitment> &utxo_commitment,
            const std::optional<UTXOWitness>              &utxo_witness );

        outcome::result<void> SubmitProposal( const ConsensusManager::Proposal &proposal );

        outcome::result<void> TryResumeProposal( const std::string &hash );
        outcome::result<void> TryResumePendingDependency( const ConsensusManager::PendingDependencyKey &dependency );
        bool CheckCertificate( const std::string &subject_hash ) const;
        bool CheckCertificateStrict( const ConsensusManager::Subject &subject ) const;
        outcome::result<ConsensusManager::Certificate> GetCertificateBySubjectHash(
            const std::string &subject_hash ) const;
        const std::string &BestHash( const std::string &a, const std::string &b ) const;

    protected:
        friend class Migration3_5_0To3_6_0;
        friend class Migration3_6_0To3_7_0;
        friend class MultiAccountTestAccess;

        static outcome::result<void> MigrateCids( const std::shared_ptr<crdt::GlobalDB> &old_db,
                                                  const std::shared_ptr<crdt::GlobalDB> &new_db );

    private:
        Blockchain( std::shared_ptr<crdt::GlobalDB> global_db,
                    std::shared_ptr<GeniusAccount>  account,
                    BlockchainCallback              callback );

        outcome::result<void> InitGenesisCID();
        outcome::result<void> InitAccountCreationCID( const std::string &address );
        outcome::result<void> SaveGenesisCID( const std::string &cid );
        outcome::result<void> SaveAccountCreationCID( const std::string &address, const std::string &cid );

        std::vector<uint8_t> ComputeSignatureData( const GenesisBlock &g ) const;
        std::vector<uint8_t> ComputeSignatureData( const AccountCreationBlock &ac ) const;
        bool VerifySignature( const GenesisBlock &g ) const;
        bool VerifySignature( const AccountCreationBlock &ac ) const;

        outcome::result<void> CreateGenesisBlock();
        outcome::result<void> VerifyGenesisBlock( const std::string &serialized_genesis );

        outcome::result<void> CreateAccountCreationBlock();
        outcome::result<void> VerifyAccountCreationBlock( const std::string &serialized_account_creation );

        std::optional<std::vector<crdt::pb::Element>> FilterGenesis( const crdt::pb::Element &element );
        std::optional<std::vector<crdt::pb::Element>> FilterAccountCreation( const crdt::pb::Element &element );
        bool ShouldReplaceGenesis( const GenesisBlock &existing, const GenesisBlock &candidate ) const;
        bool ShouldReplaceAccountCreation( const AccountCreationBlock &existing,
                                           const AccountCreationBlock &candidate ) const;

        outcome::result<void> GenesisReceivedCallback( const crdt::CRDTCallbackManager::NewDataPair &new_data,
                                                       const std::string                            &cid );
        outcome::result<void> AccountCreationReceivedCallback( const crdt::CRDTCallbackManager::NewDataPair &new_data,
                                                               const std::string                            &cid );
        outcome::result<void> InformBlockchainResult( outcome::result<void> result ) const;
        outcome::result<void> InformGenesisResult( outcome::result<std::string> result );
        outcome::result<void> InformAccountCreationResponse( outcome::result<std::string> creation_result );
        void WatchCIDDownload( const std::string &cid, Error error_on_failure, uint64_t timeout_ms );
        outcome::result<void> EnsureValidatorRegistry() const;

        static constexpr std::string_view BLOCKCHAIN_TOPIC =
            "gnus-blockchain"; 
        static constexpr std::string_view DEFAULT_FULL_NODE_PUB_ADDRESS =
            "8a33bdf1445a68736429d1773be8682362753a0efc6fb9d8b3e8dffe3b74fc91e26b203fd521547a5219eddf1d3ac51fd17a7646c9bca5ef065da131add4e5a2"; 
        static constexpr std::string_view GENESIS_KEY =
            "gnus-genesis-block"; 
        static constexpr std::string_view GENESIS_CID_KEY =
            "gnus-genesis-block-cid"; 
        static constexpr std::string_view ACCOUNT_CREATION_KEY_PREFIX =
            "gnus-account-creation-"; 
        static constexpr std::string_view ACCOUNT_CREATION_CID_KEY_PREFIX =
            "gnus-account-creation-cid-";                          
        static constexpr uint64_t TIMEOUT_GENESIS_BLOCK_MS = 8000; 
        static constexpr uint64_t TIMEOUT_ACC_CREATION_BLOCK_MS =
            8000; 

        std::shared_ptr<crdt::GlobalDB> db_;      
        std::shared_ptr<GeniusAccount>  account_; 

        BlockchainCallback   blockchain_processed_callback_; 
        GenesisBlock         genesis_block_;                 
        AccountCreationBlock account_creation_block_;        

        struct BlockchainCIDs
        {
            std::optional<std::string> genesis_; 
            std::unordered_map<std::string, std::string>
                account_creation_; 

            bool hasGenesis() const
            {
                return genesis_.has_value();
            }

            bool hasAccount( const std::string &address ) const
            {
                return account_creation_.find( address ) != account_creation_.end();
            }

            bool hasAnyAccount() const
            {
                return !account_creation_.empty();
            }

            bool isCompleteFor( const std::string &address ) const
            {
                return hasGenesis() && hasAccount( address );
            }
        };

        BlockchainCIDs cids_; 

        static std::string &AuthorizedFullNodeAddressStorage();

        std::shared_ptr<ValidatorRegistry> validator_registry_; 

        base::Logger logger_ = base::createLogger( "Blockchain" ); 

        bool              created_successfully_ = false; 
        bool              filters_registered_   = false; 
        bool              callbacks_registered_ = false; 
        std::atomic<bool> validator_registry_initialized_{ false }; 
        bool              genesis_ready_          = false;          
        bool              account_creation_ready_ = false;          

        std::shared_ptr<ConsensusManager> consensus_manager_; 
    };

}

OUTCOME_HPP_DECLARE_ERROR_2( sgns, Blockchain::Error );

#endif // SGNS_BLOCKCHAIN_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/GeniusAccount.hpp
summary: Header file of the Genius account class. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/GeniusAccount.hpp



Header file of the Genius account class.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[boost::multiprecision](/source-reference/Namespaces/d2/d0c/namespaceboost_1_1multiprecision/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/)**  |

## Detailed Description

Header file of the Genius account class. 

**Date**: 2024-03-11 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef SGNS_GENIUS_ACCOUNT_HPP
#define SGNS_GENIUS_ACCOUNT_HPP

#include <array>
#include <deque>
#include <memory>
#include <string>
#include <vector>
#include <shared_mutex>
#include <mutex>
#include <condition_variable>
#include <chrono>
#include <functional>
#include <optional>
#include <set>
#include <string_view>

#include <boost/multiprecision/cpp_int.hpp>
#include <boost/filesystem/path.hpp>
#include <WalletCore/PrivateKey.h>

#include <ProofSystem/EthereumKeyGenerator.hpp>

#include "account/TokenID.hpp"
#include "storage/rocksdb/rocksdb.hpp"
#include "local_secure_storage/ISecureStorage.hpp"
#include "outcome/outcome.hpp"
#include "UTXOManager.hpp"

#include <unordered_set>

namespace sgns
{
    using namespace boost::multiprecision;

    class AccountMessenger;
    class TransactionManager;

    class GeniusAccount : public std::enable_shared_from_this<GeniusAccount>
    {
    public:
        using StorageWithAddress = std::pair<std::shared_ptr<ISecureStorage>, ethereum::EthereumKeyGenerator>;

        static const std::array<uint8_t, 32> ELGAMAL_PUBKEY_PREDEFINED;      
        static constexpr int64_t             NONCE_CACHE_DURATION_MS = 5000; 

        using SecureStorageFactory = std::function<std::shared_ptr<ISecureStorage>( const std::string &identifier )>;

        static void SetSecureStorageFactory( SecureStorageFactory factory );

        static const SecureStorageFactory &GetSecureStorageFactory();

        static std::shared_ptr<GeniusAccount> New( TokenID                        token_id,
                                                   const boost::filesystem::path &base_path,
                                                   bool                           full_node = false );

        static std::shared_ptr<GeniusAccount> NewFromPrivateKey( TokenID                        token_id,
                                                                 const char                    *eth_private_key,
                                                                 const boost::filesystem::path &base_path,
                                                                 bool                           full_node = false );

        static std::shared_ptr<GeniusAccount> NewFromPublicKey( TokenID          token_id,
                                                                std::string_view public_key,
                                                                bool             full_node = false );

        static std::shared_ptr<GeniusAccount> NewFromMnemonic( TokenID                        token_id,
                                                               const std::string             &mnemonic,
                                                               const boost::filesystem::path &base_path,
                                                               bool                           full_node = false );

        static std::pair<std::shared_ptr<GeniusAccount>, std::string> NewFromRandomMnemonic(
            TokenID                        token_id,
            const boost::filesystem::path &base_path,
            bool                           full_node = false );

        static std::vector<std::string> GetAvailableAccounts( const boost::filesystem::path &base_path );

        static outcome::result<void> DeleteAccount( std::string_view               public_address,
                                                    const boost::filesystem::path &base_path );

        static std::string_view NormalizeAddress( std::string_view address ) noexcept;

        static bool IsValidPublicKey( std::string_view key ) noexcept;

        bool InitMessenger( std::shared_ptr<ipfs_pubsub::GossipPubSub> pubsub );

        bool ConfigureDatabaseDependencies( std::shared_ptr<crdt::GlobalDB> global_db );

        void DeconfigureDatabaseDependencies();

        ~GeniusAccount();

        [[nodiscard]] std::string GetAddress() const;

        [[nodiscard]] TokenID GetToken() const;

        [[nodiscard]] std::string GetNonce() const
        {
            return std::to_string( GetProposedNonce() );
        }

        static bool VerifySignature( const std::string          &address,
                                     std::string_view            sig,
                                     const std::vector<uint8_t> &data );

        std::vector<uint8_t> Sign( const std::vector<uint8_t> &data ) const;

        std::vector<InputUTXOInfo> CreateInputsFromUTXOs( const std::vector<GeniusUTXO> &utxos ) const;

        void SetPeerConfirmedNonce( uint64_t nonce, const std::string &address, const std::string &tx_hash = "" );

        void RollBackPeerConfirmedNonce( uint64_t nonce, const std::string &address );

        outcome::result<uint64_t> GetPeerNonce( const std::string &address ) const;

        outcome::result<uint64_t> GetLocalConfirmedNonce() const;

        outcome::result<std::string> GetLocalConfirmedTxHash( uint64_t nonce ) const;

        outcome::result<uint64_t> GetConfirmedNonce( uint64_t timeout_ms ) const;

        outcome::result<std::optional<uint64_t>> FetchNetworkNonce( uint64_t timeout_ms ) const;

        uint64_t GetProposedNonce() const;

        uint64_t ReserveNextNonce();

        void ReleaseNonce( uint64_t nonce );

        outcome::result<void> RequestGenesis(
            uint64_t                                            timeout_ms = 8000,
            std::function<void( outcome::result<std::string> )> callback   = nullptr ) const;
        outcome::result<void> RequestAccountCreation(
            uint64_t                                            timeout_ms,
            std::function<void( outcome::result<std::string> )> callback ) const;
        outcome::result<void> RequestValidatorRegistry(
            uint64_t                                            timeout_ms,
            std::function<void( outcome::result<std::string> )> callback ) const;
        outcome::result<void> RequestRegularBlock(
            uint64_t                                            timeout_ms,
            const std::string                                  &cid,
            std::function<void( outcome::result<std::string> )> callback = nullptr ) const;
        outcome::result<void> RequestTransaction(
            uint64_t                                            timeout_ms,
            const std::string                                  &tx_hash,
            std::function<void( outcome::result<std::string> )> callback = nullptr ) const;
        outcome::result<std::unordered_set<std::string>> RequestUTXOs( uint64_t           timeout_ms,
                                                                       const std::string &address,
                                                                       uint64_t           silent_time_ms = 150 ) const;
        outcome::result<void> RequestHeads( const std::unordered_set<std::string> &topics ) const;

        static outcome::result<StorageWithAddress> GenerateGeniusAddress( const char *eth_private_key,
                                                                          const boost::filesystem::path &base_path );

        static outcome::result<StorageWithAddress> GenerateGeniusAddress( const TW::PrivateKey          &private_key,
                                                                          const boost::filesystem::path &base_path );

        outcome::result<void> SaveInSecureStorage( const std::string                      &key,
                                                   const ISecureStorage::SecureBufferType &buffer )
        {
            return storage_->Save( key, buffer );
        }

        outcome::result<ISecureStorage::SecureBufferType> LoadFromSecureStorage( const std::string &key )
        {
            return storage_->Load( key );
        }

        const UTXOManager &GetUTXOManager() const
        {
            return utxo_manager_;
        }

        UTXOManager &GetUTXOManager()
        {
            return utxo_manager_;
        }

    protected:
        friend class Blockchain;
        friend class TransactionManager;
        void SetGetBlockChainCIDMethod(
            std::function<outcome::result<std::string>( uint8_t, const std::string & )> method );
        void ClearGetBlockChainCIDMethod();
        void SetHasBlockCidMethod( std::function<outcome::result<bool>( const std::string & )> method );
        void ClearHasBlockCidMethod();
        void SetGetValidatorWeightMethod(
            std::function<outcome::result<std::optional<uint64_t>>( const std::string & )> method );
        void ClearGetValidatorWeightMethod();
        void SetGetTransactionCIDMethod( std::function<outcome::result<std::string>( const std::string & )> method );
        void ClearGetTransactionCIDMethod();
        void SetNonceStore( std::shared_ptr<storage::rocksdb> db );

    private:
        struct ConfirmedTxRecord
        {
            uint64_t    nonce;
            std::string hash;
        };

        static constexpr size_t SIGNATURE_EXP_SIZE               = 64; 
        static constexpr size_t LOCAL_CONFIRMED_TX_HISTORY_LIMIT = 5;

        static outcome::result<StorageWithAddress> LoadGeniusAccount( const boost::filesystem::path &base_path );

        static outcome::result<StorageWithAddress> LoadGeniusAccount( std::string_view public_key );

        static std::shared_ptr<GeniusAccount> CreateInstanceFromResponse( TokenID            token_id,
                                                                          StorageWithAddress response_value,
                                                                          bool               full_node );

        TokenID                         token;         
        std::shared_ptr<ISecureStorage> storage_;      
        bool                            is_full_node_; 

        std::shared_ptr<ethereum::EthereumKeyGenerator> eth_keypair_;      
        std::unordered_map<std::string, uint64_t>       confirmed_nonces_; 
        mutable std::shared_mutex                       nonce_mutex_;      
        std::set<uint64_t>                              pending_nonces_;   
        std::optional<uint64_t>                         local_confirmed_nonce_; 
        std::deque<ConfirmedTxRecord>                   local_confirmed_transactions_; 
        std::shared_ptr<AccountMessenger>               messenger_;                    
        UTXOManager                                     utxo_manager_;

        // Nonce request tracking
        mutable std::mutex              nonce_request_mutex_; 
        mutable std::condition_variable nonce_request_cv_;    
        mutable bool nonce_request_in_progress_;              
        mutable std::optional<outcome::result<uint64_t>>
            cached_nonce_result_; 
        mutable std::chrono::steady_clock::time_point
                   cached_nonce_timestamp_; 
        std::mutex get_cids_mutex_;         
        std::function<outcome::result<std::string>( uint8_t, const std::string & )>
            get_cids_method_; 
        std::function<outcome::result<bool>( const std::string & )> has_cid_method_; 
        std::function<outcome::result<std::vector<std::string>>( const std::string & )>
            get_utxos_method_; 
        std::function<outcome::result<std::optional<uint64_t>>( const std::string & )>
            get_validator_weight_method_; 
        std::function<outcome::result<std::string>( const std::string & )>
                                          get_transaction_cid_method_; 
        std::shared_ptr<storage::rocksdb> nonce_db_;                   

        static constexpr std::string_view NONCE_KEY_PREFIX                      = "gnus-confirmed-nonce-";
        static constexpr std::string_view LOCAL_CONFIRMED_TX_HISTORY_KEY_PREFIX = "gnus-local-confirmed-tx-history-";

        void               LoadConfirmedNonces();
        void               PersistConfirmedNonce( const std::string &address, uint64_t nonce );
        static std::string SerializeConfirmedTxHistory( const std::deque<ConfirmedTxRecord> &history );
        static std::deque<ConfirmedTxRecord> DeserializeConfirmedTxHistory( const std::string &serialized );
        void UpdateLocalConfirmedTxHistoryLocked( uint64_t nonce, const std::string &tx_hash );
        void RollbackLocalConfirmedTxHistoryLocked( uint64_t nonce );

        uint64_t GetNextNonceLocked() const;

        GeniusAccount( std::shared_ptr<ethereum::EthereumKeyGenerator> eth_keypair,
                       TokenID                                         token_id,
                       std::shared_ptr<ISecureStorage>                 storage,
                       bool                                            full_node );
    };
}

#endif // SGNS_GENIUS_ACCOUNT_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/TransactionManager.hpp
summary: Transaction coordination, CRDT sync, and lifecycle tracking for outgoing and incoming account activity. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/TransactionManager.hpp



Transaction coordination, CRDT sync, and lifecycle tracking for outgoing and incoming account activity.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::TransactionManager](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/)** <br/>Coordinates transaction creation, CRDT propagation, verification, and status tracking.  |
| struct | **[fmt::formatter< sgns::TransactionManager::State >](/source-reference/Classes/d5/d76/structfmt_1_1formatter_3_01sgns_1_1_transaction_manager_1_1_state_01_4/)**  |

## Types

|                | Name           |
| -------------- | -------------- |
| using std::pair< std::string, base::Buffer > | **[EscrowDataPair](/source-reference/Files/de/d54/_transaction_manager_8hpp/#using-escrowdatapair)**  |

## Detailed Description

Transaction coordination, CRDT sync, and lifecycle tracking for outgoing and incoming account activity. 

**Date**: 2024-03-13 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 
## Types Documentation

### using EscrowDataPair

```cpp
using sgns::EscrowDataPair = std::pair<std::string, base::Buffer>;
```





## Source code

```cpp

#ifndef _TRANSACTION_MANAGER_HPP_
#define _TRANSACTION_MANAGER_HPP_

#include <memory>
#include <deque>
#include <cstdint>
#include <chrono>
#include <unordered_map>
#include <unordered_set>
#include <optional>

#include <boost/format.hpp>

#include "crdt/globaldb/globaldb.hpp"
#include "crdt/atomic_transaction.hpp"
#include "account/proto/SGTransaction.pb.h"
#include "account/GeniusTransaction.hpp"
#include "account/GeniusAccount.hpp"
#include "account/GeniusInputValidator.hpp"
#include "account/InputValidators.hpp"
#include "account/PublicChainInputValidator.hpp"
#include "base/logger.hpp"
#include "base/buffer.hpp"
#include "crypto/hasher.hpp"

#include "blockchain/Blockchain.hpp"
#include "processing/proto/SGProcessing.pb.h"
#include "outcome/outcome.hpp"

namespace sgns
{
    using namespace boost::multiprecision;
    using EscrowDataPair = std::pair<std::string, base::Buffer>;

    class TransactionManager : public std::enable_shared_from_this<TransactionManager>
    {
    public:
        static constexpr std::string_view GNUS_FULL_NODES_TOPIC        = "SuperGNUSNode.TestNet.FullNode";
        static constexpr std::string_view GNUS_FULL_NODES_TOPIC_LEGACY = "SuperGNUSNode.TestNet.FullNode.963";
        static constexpr uint64_t         NONCE_REQUEST_TIMEOUT_MS =
            5000; 

        enum class State : uint8_t
        {
            CREATING = 0, 
            INITIALIZING, 
            SYNCING,      
            READY,        
        };

        using TransactionPair  = std::pair<std::shared_ptr<GeniusTransaction>, std::optional<std::vector<uint8_t>>>;
        using TransactionBatch = std::vector<TransactionPair>;
        using TransactionItem  = std::pair<TransactionBatch, std::optional<std::shared_ptr<crdt::AtomicTransaction>>>;
        using StateChangeCallback = std::function<void( const State &previous, const State &current )>;

        enum class TransactionStatus : uint8_t
        {
            CREATED,   
            SENDING,   
            CONFIRMED, 
            VERIFYING, 
            UNCONFIRMED, 
            FAILED,    
            INVALID    
        };

        static std::shared_ptr<TransactionManager> New(
            std::shared_ptr<crdt::GlobalDB>          processing_db,
            std::shared_ptr<boost::asio::io_context> ctx,
            std::shared_ptr<GeniusAccount>           account,
            std::shared_ptr<crypto::Hasher>          hasher,
            std::shared_ptr<Blockchain>              blockchain,
            bool                                     full_node           = false,
            uint16_t                                 subnet_id           = 0,
            std::chrono::milliseconds                timestamp_tolerance = std::chrono::milliseconds( 300000 ),
            std::chrono::milliseconds                mutability_window   = std::chrono::milliseconds( 0 ) );

        ~TransactionManager();

        void Start();
        void RegisterTopicNames();
        void StartListeningTopics();
        void StartCore();

        void PrintAccountInfo() const;

        std::vector<std::vector<uint8_t>> GetOutTransactions() const;
        std::vector<std::vector<uint8_t>> GetInTransactions() const;
        std::vector<std::vector<uint8_t>> GetTransactions(
            std::optional<TransactionStatus> tx_status = std::nullopt ) const;
        std::vector<std::vector<uint8_t>> GetTransactions() const;

        outcome::result<std::string> TransferFunds( uint64_t amount, std::string destination, TokenID token_id );

        outcome::result<std::string> MintFunds( uint64_t    amount,
                                                std::string transaction_hash,
                                                std::string chainid,
                                                TokenID     tokenid,
                                                std::string destination = "" );

        outcome::result<std::string> MigrationFunds( uint64_t    amount,
                                                     std::string from_version,
                                                     TokenID     tokenid,
                                                     std::string destination = "" );

        outcome::result<std::pair<std::string, EscrowDataPair>> HoldEscrow( uint64_t           amount,
                                                                            const std::string &dev_addr,
                                                                            uint64_t           peers_cut,
                                                                            const std::string &job_id );
        outcome::result<std::string>                            PayEscrow( const std::string                       &escrow_path,
                                                                           const SGProcessing::TaskResult          &task_result,
                                                                           std::shared_ptr<crdt::AtomicTransaction> crdt_transaction );

        // Wait for an incoming transaction to be processed with a timeout
        TransactionStatus WaitForTransactionIncoming( const std::string        &txId,
                                                      std::chrono::milliseconds timeout ) const;
        // Wait for an outgoing transaction to be processed with a timeout
        TransactionStatus WaitForTransactionOutgoing( const std::string        &txId,
                                                      std::chrono::milliseconds timeout ) const;

        TransactionStatus WaitForEscrowRelease( const std::string        &originalEscrowId,
                                                std::chrono::milliseconds timeout ) const;

        static std::string GetTransactionPath( uint16_t base, const std::string &tx_hash );
        static std::string GetTransactionPath( const GeniusTransaction &element );
        static std::string GetTransactionPath( const std::string &tx_hash );
        static std::string GetTransactionProofPath( const GeniusTransaction &element );

        static outcome::result<std::shared_ptr<GeniusTransaction>> FetchTransaction(
            const std::shared_ptr<crdt::GlobalDB> &db,
            std::string_view                       transaction_key );
        static outcome::result<std::shared_ptr<GeniusTransaction>> DeSerializeTransaction(
            const base::Buffer &tx_data );

        State GetState() const
        {
            return state_m;
        }

        TransactionStatus GetOutgoingStatusByTxId( const std::string &txId ) const;
        TransactionStatus GetIncomingStatusByTxId( const std::string &txId ) const;

        outcome::result<std::shared_ptr<GeniusTransaction>> GetConflictingTransaction(
            const GeniusTransaction &element ) const;

        void Stop();

        void RegisterStateChangeCallback( StateChangeCallback callback );
        void UnregisterStateChangeCallback();

        static std::string StateToString( State state )
        {
            switch ( state )
            {
                case State::CREATING:
                    return "CREATING";
                case State::INITIALIZING:
                    return "INITIALIZING";
                case State::SYNCING:
                    return "SYNCING";
                case State::READY:
                    return "READY";
                default:
                    return "UNKNOWN";
            }
        }

        static std::string GetBlockChainBase( uint16_t network_id );

        static std::string GetBlockChainBase();

        outcome::result<void> QueryTransactions();

        outcome::result<void> FetchAndProcessTransaction( const std::string          &tx_key,
                                                          std::optional<base::Buffer> tx_data = std::nullopt );

        static outcome::result<std::shared_ptr<GeniusTransaction>> DeSerializeTransaction( std::string tx_data );

        static outcome::result<std::shared_ptr<GeniusTransaction>> DeSerializeEmbeddedTransaction(
            const EmbeddedTransaction &embedded );

    protected:
        friend class GeniusNode;
        friend class Migration3_6_0To3_7_0;
        friend class CertificateFallbackTestAccess;
        friend class TransactionManagerPendingLifecycleTestAccess;
        void EnqueueTransaction( TransactionPair element );
        void EnqueueTransaction( TransactionItem element );

        void SetTimeFrameToleranceMs( uint64_t timeframe_tolerance );
        void SetMutabilityWindowMs( uint64_t mutability_window );

    private:
        static constexpr std::string_view TRANSACTION_BASE_FORMAT = "/bc-%hu/";

        struct TrackedTx
        {
            std::shared_ptr<GeniusTransaction> tx;
            TransactionStatus                  status;
            uint64_t                           cached_nonce; // Cache nonce to avoid dereferencing tx
        };

        struct ReplayProtectionResult
        {
            ConsensusManager::ValidationResult validation = ConsensusManager::ValidationResult::Approve();
        };

        struct AccountUTXOState
        {
            uint64_t      version{ 0 };
            base::Hash256 root{};
            bool          initialized{ false };
        };

        TransactionManager( std::shared_ptr<crdt::GlobalDB>          processing_db,
                            std::shared_ptr<boost::asio::io_context> ctx,
                            std::shared_ptr<GeniusAccount>           account,
                            std::shared_ptr<crypto::Hasher>          hasher,
                            std::shared_ptr<Blockchain>              blockchain,
                            bool                                     full_node,
                            std::chrono::milliseconds                timestamp_tolerance,
                            std::chrono::milliseconds                mutability_window );

        TransactionManager( std::shared_ptr<crdt::GlobalDB>          processing_db,
                            std::shared_ptr<boost::asio::io_context> ctx,
                            std::shared_ptr<GeniusAccount>           account,
                            std::shared_ptr<crypto::Hasher>          hasher,
                            std::shared_ptr<Blockchain>              blockchain,
                            bool                                     full_node,
                            uint16_t                                 subnet_id,
                            std::chrono::milliseconds                timestamp_tolerance,
                            std::chrono::milliseconds                mutability_window );

        // Parser function pointer alias: returns a set of topic strings or an error
        using TransactionParserFn =
            outcome::result<void> ( TransactionManager::* )( const std::shared_ptr<GeniusTransaction> & );

        SGTransaction::DAGStruct FillDAGStruct( std::optional<std::string> other_chain_hash = std::nullopt );
        std::string              GetOutgoingPreviousHash( uint64_t nonce ) const;
        std::string              GetTrackedOutgoingPreviousHash( uint64_t nonce ) const;
        std::string              GetPersistedOutgoingPreviousHash( uint64_t nonce ) const;
        std::string              QueryOutgoingPreviousHashFromCRDT( uint64_t nonce ) const;

        outcome::result<void> SendTransactionItem( TransactionItem &item );

        outcome::result<void> RollbackTransactions( TransactionItem &item_to_rollback );

        static std::vector<uint16_t> GetMonitoredNetworkIDs();

        static outcome::result<std::string> GetExpectedProofKey( const std::string                        &tx_key,
                                                                 const std::shared_ptr<GeniusTransaction> &tx );

        static outcome::result<std::string> GetExpectedTxKey( const std::string &proof_key );

        outcome::result<bool> CheckProof( const std::shared_ptr<GeniusTransaction> &tx );

        outcome::result<void> ParseTransaction( const std::shared_ptr<GeniusTransaction> &tx );

        outcome::result<void> RevertTransaction( const std::shared_ptr<GeniusTransaction> &tx );
        bool                  DoesTransactionMutateUTXOState( const std::shared_ptr<GeniusTransaction> &tx ) const;
        std::unordered_set<std::string> CollectTouchedAccounts( const std::shared_ptr<GeniusTransaction> &tx ) const;
        AccountUTXOState                GetOrInitAccountUTXOState( const std::string &address ) const;
        void UpdateAccountUTXOState( const std::unordered_set<std::string> &addresses, bool increment_version );

        void InitializeUTXOs();

        void InitTransactions();

        bool CheckNonce() const;

        void SyncNonce();

        void RequestRelevantHeads();

        outcome::result<bool> CheckTransactionValidity( const std::set<uint64_t> &nonces_to_check );

        outcome::result<void> DeleteTransaction( std::string tx_key, const std::unordered_set<std::string> &topics );

        std::shared_ptr<GeniusTransaction> GetTransactionByHash( const std::string &tx_hash ) const;

        std::shared_ptr<GeniusTransaction> GetTransactionByHashNoLock( const std::string &tx_hash ) const;

        std::shared_ptr<GeniusTransaction> GetTransactionByNonceAndAddress( uint64_t           nonce,
                                                                            const std::string &address ) const;
        std::optional<TrackedTx> GetTrackedTxByNonceAndAddress( uint64_t nonce, const std::string &address ) const;
        std::optional<TrackedTx> GetTrackedTxByHash( const std::string &tx_hash ) const;

        bool SetOutgoingStatusByNonce( uint64_t nonce, TransactionStatus s );

        void TickOnce();

        outcome::result<ConsensusManager::Check> OnConsensusCertificate( const std::string          &tx_hash,
                                                                         const ConsensusCertificate &certificate );
        void OnProposalTimeoutCleanup( const std::string &tx_hash );

        std::shared_ptr<crdt::GlobalDB> globaldb_m;

        std::shared_ptr<boost::asio::io_context> ctx_m;
        std::shared_ptr<GeniusAccount>           account_m;
        std::shared_ptr<crypto::Hasher>          hasher_m;
        std::shared_ptr<Blockchain>              blockchain_;
        bool                                     full_node_m;
        uint16_t                                 subnet_id_ = 0;    
        std::string                              full_node_topic_m; 
        State                                    state_m;
        std::mutex                               state_change_callback_mutex_;
        StateChangeCallback                      state_change_callback_;

        // Head request rate limiting (for reactive requests due to nonce gaps)
        std::optional<std::chrono::steady_clock::time_point> last_head_request_time_;

        // Periodic sync - request heads every 10 minutes to stay in sync across devices/instances
        std::chrono::steady_clock::time_point last_periodic_sync_time_;
        std::atomic<bool>                     received_first_periodic_sync_response_{
            false }; // Track if we've gotten at least one response

        static constexpr std::chrono::minutes PERIODIC_SYNC_INTERVAL         = std::chrono::minutes( 10 );
        static constexpr std::chrono::seconds INITIAL_PERIODIC_SYNC_INTERVAL = std::chrono::seconds( 30 );

        // for the SendTransactionItem thread support
        mutable std::mutex          mutex_m;
        std::deque<TransactionItem> tx_queue_m;

        mutable std::shared_mutex                                   tx_mutex_m;
        std::unordered_map<std::string, TrackedTx>                  tx_processed_m;
        mutable std::shared_mutex                                   account_utxo_state_mutex_;
        mutable std::unordered_map<std::string, AccountUTXOState>   account_utxo_state_;
        std::atomic<uint32_t>                                       utxo_state_tracking_suppression_{ 0 };
        std::unordered_map<std::string, ConsensusManager::Proposal> pending_proposals_;
        std::function<void()>                                       task_m;
        std::atomic<bool>                                           stopped_{ false };
        std::chrono::milliseconds                                   timestamp_tolerance_m;
        std::chrono::milliseconds                                   mutability_window_m;
        uint64_t                                                    nonce_window_m = DEFAULT_NONCE_WINDOW;

        // METRICS-01: Operational metrics counters
        // Atomic counters tracking vote rates, validation breakdown, and transaction lifecycle.
        // Flushed to log on TransactionManager destruction (per D-12/D-13/D-14).
        std::atomic<uint64_t> metrics_cert_fallback_success_{ 0 };
        std::atomic<uint64_t> metrics_cert_fallback_failure_{ 0 };
        std::atomic<uint64_t> metrics_validation_approve_{ 0 };
        std::atomic<uint64_t> metrics_validation_reject_{ 0 };
        std::atomic<uint64_t> metrics_tracking_insert_{ 0 };
        std::atomic<uint64_t> metrics_tracking_confirm_{ 0 };
        std::atomic<uint64_t> metrics_tracking_fail_{ 0 };

        static constexpr std::chrono::milliseconds TIMESTAMP_TOLERANCE  = std::chrono::seconds( 10 );
        static constexpr std::chrono::milliseconds MUTABILITY_WINDOW    = std::chrono::minutes( 15 );
        static constexpr uint64_t                  DEFAULT_NONCE_WINDOW = 5;

        std::mutex                                         cv_mutex_;
        std::condition_variable                            cv_;
        std::queue<crdt::CRDTCallbackManager::NewDataPair> new_data_queue_;
        std::queue<std::string>                            deleted_data_queue_;

        std::chrono::steady_clock::time_point last_loop_time_;
        std::atomic<bool>                     topic_names_registered_{ false };
        std::atomic<bool>                     listening_topics_started_{ false };
        std::atomic<bool>                     core_started_{ false };

        std::mutex                            missing_tx_mutex_;
        std::unordered_set<std::string>       missing_tx_hashes_;
        std::chrono::steady_clock::time_point last_init_tx_request_time_{};
        static constexpr uint64_t             k_init_tx_request_cooldown_ms = 5000;

        static constexpr std::string_view kBridgeExecutedPrefix = "/bridge/executed/";
        static constexpr std::string_view kBridgeKeySeparator   = ":";

        outcome::result<void> ParseTransferTransaction( const std::shared_ptr<GeniusTransaction> &tx );
        outcome::result<void> ParseMintTransaction( const std::shared_ptr<GeniusTransaction> &tx );
        outcome::result<void> ParseEscrowTransaction( const std::shared_ptr<GeniusTransaction> &tx );
        outcome::result<void> RevertTransferTransaction( const std::shared_ptr<GeniusTransaction> &tx );
        outcome::result<void> RevertMintTransaction( const std::shared_ptr<GeniusTransaction> &tx );
        outcome::result<void> RevertEscrowTransaction( const std::shared_ptr<GeniusTransaction> &tx );

        static const std::unordered_map<std::string, std::pair<TransactionParserFn, TransactionParserFn>>
            transaction_parsers;

        base::Logger m_logger = base::createLogger( "TransactionManager" );

        std::optional<std::vector<crdt::pb::Element>> FilterTransaction( const crdt::pb::Element &element );

        std::optional<std::vector<crdt::pb::Element>> FilterProof( const crdt::pb::Element &element );

        bool ShouldReplaceTransaction( const GeniusTransaction &existing_tx, const GeniusTransaction &new_tx ) const;

        static uint64_t GetCurrentTimestamp();

        int64_t GetElapsedTime( uint64_t timestamp, uint64_t current_timestamp ) const;

        int64_t GetElapsedTime( uint64_t timestamp ) const;

        bool IsTransactionImmutable( const GeniusTransaction &tx ) const;

        outcome::result<void> RemoveTransactionFromProcessedMaps( const std::string &transaction_key,
                                                                  bool               delete_from_crdt = false );

        outcome::result<void> AddTransactionToProcessedMaps( crdt::CRDTCallbackManager::NewDataPair new_data );

        outcome::result<void> StoreTransactionCID( const std::string &key, const std::string &cid );

        void ProcessDeletion( std::string deleted_key );
        void ProcessNewData( crdt::CRDTCallbackManager::NewDataPair new_data );

        void NewElementCallback( crdt::CRDTCallbackManager::NewDataPair new_data, std::string cid );

        void DeleteElementCallback( std::string deleted_key );

        void ChangeState( State new_state );

    public:
        enum class WitnessValidationResult : uint8_t
        {
            VALID,
            DRIFT,
            INVALID
        };

        outcome::result<std::string>             GetTransactionCID( const std::string &tx_hash ) const;
        outcome::result<ConsensusManager::ValidationResult> HandleNonceConsensusSubject(
            const ConsensusManager::Subject &subject );
        ConsensusManager::ValidationResult ValidateTransactionForConsensus(
            const std::shared_ptr<GeniusTransaction> &tx ) const;
        bool CheckTransactionWellFormed( const GeniusTransaction &tx ) const;
        bool CheckTransactionAuthorization( const GeniusTransaction &tx ) const;
        bool CheckTransactionTimestamp( const GeniusTransaction &tx ) const;
        bool CheckTransactionReplayProtection( const GeniusTransaction &tx ) const;
        ReplayProtectionResult EvaluateTransactionReplayProtection( const GeniusTransaction &tx ) const;
        bool CheckTransactionTypeRules( const std::shared_ptr<GeniusTransaction> &tx ) const;
        std::optional<UTXOTransitionCommitment> BuildUTXOTransitionCommitment(
            const std::shared_ptr<GeniusTransaction> &tx ) const;
        std::optional<UTXOWitness> BuildUTXOWitness( const std::shared_ptr<GeniusTransaction> &tx ) const;
        bool                       ApplyTransactionToUTXOSnapshot( const std::shared_ptr<GeniusTransaction> &tx,
                                                                   std::vector<GeniusUTXO>                  &snapshot ) const;
        WitnessValidationResult    ValidateWitnessForConsensus( const ConsensusSubject                   &subject,
                                                                const std::shared_ptr<GeniusTransaction> &tx ) const;
        bool ValidateUTXOParametersForConsensus( const UTXOTxParameters &params, const std::string &address ) const;
        void SetNonceWindow( uint64_t window );
        outcome::result<void> ChangeTransactionState( const std::shared_ptr<GeniusTransaction> &tx,
                                                      TransactionStatus                         new_status );
        bool                  HasConfirmedInputConflict( const std::shared_ptr<GeniusTransaction> &candidate_tx ) const;

        bool KeyExistsInDB( const std::string &key ) const;

        PublicChainInputValidator &GetPublicChainInputValidator() noexcept
        {
            return public_chain_input_validator_;
        }

        const PublicChainInputValidator &GetPublicChainInputValidator() const noexcept
        {
            return public_chain_input_validator_;
        }

    private:
        static constexpr std::string_view GENIUS_CHAIN_ID = "supergenius";

        std::string               GetValidationChainId( const std::shared_ptr<GeniusTransaction> &tx ) const;
        const IInputValidator    &GetInputValidator( const std::string &chain_id ) const;
        GeniusInputValidator      genius_input_validator_;
        PublicChainInputValidator public_chain_input_validator_;
    };
}

template <>
struct fmt::formatter<sgns::TransactionManager::State> : formatter<std::string_view>
{
    format_context::iterator format( sgns::TransactionManager::State s, format_context &ctx ) const;
};

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

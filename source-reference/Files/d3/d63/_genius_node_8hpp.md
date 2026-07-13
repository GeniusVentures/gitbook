---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/GeniusNode.hpp
summary: Top-level node orchestration API for account, transaction, blockchain, and processing services. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/GeniusNode.hpp



Top-level node orchestration API for account, transaction, blockchain, and processing services.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[GeniusNodeConfig](/source-reference/Classes/d2/d8e/struct_genius_node_config/)** <br/>Runtime configuration values used to bootstrap a Genius node instance.  |
| class | **[sgns::GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/)** <br/>High-level facade that initializes and coordinates account, networking, transaction, blockchain, and processing subsystems.  |

## Types

|                | Name           |
| -------------- | -------------- |
| typedef struct GeniusNodeConfig | **[GeniusNodeConfig](/source-reference/Files/d3/d63/_genius_node_8hpp/#typedef-geniusnodeconfig)** <br/>Runtime configuration values used to bootstrap a Genius node instance.  |

## Functions

|                | Name           |
| -------------- | -------------- |
| | **[OUTCOME_HPP_DECLARE_ERROR_2](/source-reference/Files/d3/d63/_genius_node_8hpp/#function-outcome_hpp_declare_error_2)**([sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/) , GeniusNode::Error ) |

## Attributes

|                | Name           |
| -------------- | -------------- |
| [GeniusNodeConfig](/source-reference/Classes/d2/d8e/struct_genius_node_config/) | **[gGeniusNodeConfig](/source-reference/Files/d3/d63/_genius_node_8hpp/#variable-ggeniusnodeconfig)**  |
| uint64_t | **[kDefaultTimestampToleranceMs](/source-reference/Files/d3/d63/_genius_node_8hpp/#variable-kdefaulttimestamptolerancems)**  |
| uint64_t | **[kBridgeCatchupScanDepth](/source-reference/Files/d3/d63/_genius_node_8hpp/#variable-kbridgecatchupscandepth)**  |

## Defines

|                | Name           |
| -------------- | -------------- |
|  | **[OUTGOING_TIMEOUT_MILLISECONDS](/source-reference/Files/d3/d63/_genius_node_8hpp/#define-outgoing_timeout_milliseconds)**  |
|  | **[INCOMING_TIMEOUT_MILLISECONDS](/source-reference/Files/d3/d63/_genius_node_8hpp/#define-incoming_timeout_milliseconds)**  |

## Detailed Description

Top-level node orchestration API for account, transaction, blockchain, and processing services. 

**Date**: 2024-03-11 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 
## Types Documentation

### typedef GeniusNodeConfig

```cpp
typedef struct GeniusNodeConfig GeniusNodeConfig;
```

Runtime configuration values used to bootstrap a Genius node instance. 


## Functions Documentation

### function OUTCOME_HPP_DECLARE_ERROR_2

```cpp
OUTCOME_HPP_DECLARE_ERROR_2(
    sgns ,
    GeniusNode::Error 
)
```



## Attributes Documentation

### variable gGeniusNodeConfig

```cpp
GeniusNodeConfig gGeniusNodeConfig;
```


### variable kDefaultTimestampToleranceMs

```cpp
uint64_t kDefaultTimestampToleranceMs = 300000;
```


### variable kBridgeCatchupScanDepth

```cpp
uint64_t kBridgeCatchupScanDepth = 10000;
```



## Macros Documentation

### define OUTGOING_TIMEOUT_MILLISECONDS

```cpp
#define OUTGOING_TIMEOUT_MILLISECONDS 50000
```


### define INCOMING_TIMEOUT_MILLISECONDS

```cpp
#define INCOMING_TIMEOUT_MILLISECONDS 150000
```


## Source code

```cpp

#ifndef _GENIUS_NODE_HPP_
#define _GENIUS_NODE_HPP_

#include <chrono>
#include <memory>
#include <cstdint>
#include <functional>
#include <vector>
#include <thread>
#include <optional>
#include <mutex>
#include <atomic>

#include <boost/asio.hpp>
#include <spdlog/sinks/basic_file_sink.h>
#include <libp2p/log/logger.hpp>
#include <libp2p/multi/multibase_codec/multibase_codec_impl.hpp>
#include <libp2p/multi/content_identifier_codec.hpp>

#include "account/GeniusAccount.hpp"
#include "base/buffer.hpp"
#include "account/PublicChainInputValidator.hpp"
#include "account/TransactionManager.hpp"
#include "account/BridgeRelayer.hpp"
#include "account/ChainRpcEndpointProvider.hpp"
#include "eth/eth_watch_service.hpp"
#include <ipfs_lite/ipfs/graphsync/graphsync.hpp>
#include "crypto/hasher/hasher_impl.hpp"
#include "processing/impl/processing_core_impl.hpp"
#include "processing/impl/processing_subtask_result_storage_impl.hpp"
#include "processing/processing_service.hpp"
#include "singleton/IComponent.hpp"
#include "processing/processing_task_queue.hpp"
#include "coinprices/coinprices.hpp"
#include "blockchain/Blockchain.hpp"
#include <boost/algorithm/string/replace.hpp>
#include <ipfs_lite/ipfs/graphsync/impl/network/network.hpp>
#include <processingbase/ProcessingManager.hpp>
#include <libp2p/peer/peer_info.hpp>
#include <libp2p/event/bus.hpp>
#include <libp2p/network/connection_manager.hpp>

typedef struct GeniusNodeConfig
{
    std::string   Addr;             
    std::string   Cut;              
    std::string   TokenValueInGNUS; 
    sgns::TokenID TokenID;          
    std::string   BaseWritePath;    
    sgns::ChainlistFetcher chainlist_fetcher{}; 
} GeniusNodeConfig;

extern GeniusNodeConfig gGeniusNodeConfig;

constexpr uint64_t kDefaultTimestampToleranceMs = 300000; // ±5 minutes
constexpr uint64_t kBridgeCatchupScanDepth      = 10000;  // Max historical blocks to scan for unprocessed burns (D-20)

#define OUTGOING_TIMEOUT_MILLISECONDS 50000  // just communication time
#define INCOMING_TIMEOUT_MILLISECONDS 150000 // communication + verify proof

namespace sgns
{
    class MigrationManager;

    class GeniusNode : public IComponent, public IBridgeInitObserver, public std::enable_shared_from_this<GeniusNode>
    {
    public:
        static std::shared_ptr<GeniusNode> New( const GeniusNodeConfig &dev_config,
                                                bool                autodht      = true,
                                                uint16_t            base_port    = 40001,
                                                bool                is_full_node = false );

        static std::shared_ptr<GeniusNode> NewFromPrivateKey( const GeniusNodeConfig &dev_config,
                                                              const char         *eth_private_key,
                                                              bool                autodht      = true,
                                                              uint16_t            base_port    = 40001,
                                                              bool                is_full_node = false );

        static std::shared_ptr<GeniusNode> NewFromMnemonic( const GeniusNodeConfig &dev_config,
                                                            const std::string  &mnemonic,
                                                            bool                autodht      = true,
                                                            uint16_t            base_port    = 40001,
                                                            bool                is_full_node = false );

        ~GeniusNode() override;

        enum class NodeState : uint8_t
        {
            CREATING = 0,              
            MIGRATING_DATABASE,        
            INITIALIZING_DATABASE,     
            INITIALIZING_BLOCKCHAIN,   
            INITIALIZING_TRANSACTIONS, 
            INITIALIZING_PROCESSING,   
            INITIALIZING_RPC_CATCH_UP, 
            READY,                     
        };

        enum class Error : uint8_t
        {
            INSUFFICIENT_FUNDS        = 1,  
            DATABASE_WRITE_ERROR      = 2,  
            INVALID_TRANSACTION_HASH  = 3,  
            INVALID_CHAIN_ID          = 4,  
            INVALID_TOKEN_ID          = 5,  
            TOKEN_ID_MISMATCH         = 6,  
            PROCESS_COST_ERROR        = 7,  
            PROCESS_INFO_MISSING      = 8,  
            INVALID_JSON              = 9,  
            INVALID_BLOCK_PARAMETERS  = 10, 
            NO_PROCESSOR              = 11, 
            NO_PRICE                  = 12, 
            TRANSACTIONS_NOT_READY    = 13, 
            TRANSACTION_NOT_FINALIZED = 14, 
            TRANSACTION_FAILED        = 15, 
        };

#ifdef SGNS_DEBUG
        static constexpr std::chrono::milliseconds TIMEOUT_ESCROW_PAY{ 50000 }; 
        static constexpr std::chrono::milliseconds TIMEOUT_TRANSFER{ 50000 };   
        static constexpr std::chrono::milliseconds TIMEOUT_MINT{ 50000 };       
#else
        static constexpr std::chrono::milliseconds TIMEOUT_ESCROW_PAY{ 30000 }; 
        static constexpr std::chrono::milliseconds TIMEOUT_TRANSFER{ 30000 };   
        static constexpr std::chrono::milliseconds TIMEOUT_MINT{ 30000 };       
#endif
        std::vector<std::string> GetAvailableAccounts();

        outcome::result<void> AddAccountWithKey( const char *private_key ) const;

        outcome::result<void> AddAccountWithMnemonic( const std::string &mnemonic ) const;

        outcome::result<std::string> AddAccountWithRandomMnemonic() const;

        outcome::result<void> SelectAccount( std::string_view public_address );

        outcome::result<void> TransferAccount( std::string_view public_address );

        outcome::result<void> DeleteAccount( std::string_view public_address );

        outcome::result<void> MergeAccount( std::string_view public_address );

        outcome::result<void> SetPayoutAddress( std::string_view payout_address );

        outcome::result<std::string> ProcessImage( const std::string &jsondata );

        std::vector<std::string> GetMyTaskIds( size_t limit = 50, size_t offset = 0 ) const;

        outcome::result<SGProcessing::TaskResult> GetTaskResult( const std::string &taskId );

        uint64_t GetProcessCost( std::shared_ptr<sgns::sgprocessing::ProcessingManager> &procmgr );

        outcome::result<double> GetGNUSPrice();

        std::string GetName() override
        {
            return "GeniusNode";
        }

        std::string GetVersion();

        void LoadLogConfig();

        outcome::result<std::string> MintTokens( uint64_t           amount,
                                                 const std::string &transaction_hash,
                                                 const std::string &chainid,
                                                 TokenID            tokenid,
                                                 std::string        destination = "" );

        outcome::result<std::pair<std::string, uint64_t>> MintTokens( uint64_t                  amount,
                                                                      const std::string        &transaction_hash,
                                                                      const std::string        &chainid,
                                                                      TokenID                   tokenid,
                                                                      std::string               destination,
                                                                      std::chrono::milliseconds timeout );

        void AddPeer( const std::string &peer );

        void RefreshUPNP( uint16_t pubsubport );

        uint64_t GetBalance();

        uint64_t GetBalance( TokenID token_id );

        uint64_t GetBalance( const std::string &address );

        uint64_t GetBalance( TokenID token_id, const std::string &address );

        [[nodiscard]] std::vector<std::vector<uint8_t>> GetInTransactions() const;

        [[nodiscard]] std::vector<std::vector<uint8_t>> GetOutTransactions() const;

        [[nodiscard]] const std::vector<std::vector<uint8_t>> GetTransactions(
            std::optional<TransactionManager::TransactionStatus> tx_status = std::nullopt ) const;

        std::string GetAddress() const;

        std::optional<std::string> GetMnemonicOfActiveAccount() const;

        [[nodiscard]] TokenID GetTokenID() const
        {
            return dev_config_.TokenID;
        }

        [[nodiscard]] std::pair<float, std::string> GetInitializationStatus() const;

        [[nodiscard]] processing::ProcessingServiceImpl::ProcessingStatus GetProcessingStatus() const
        {
            return processing_service_ == nullptr ? processing::ProcessingServiceImpl::ProcessingStatus(
                                                        processing::ProcessingServiceImpl::Status::DISABLED,
                                                        0.0f )
                                                  : processing_service_->GetProcessingStatus();
        }

        outcome::result<std::pair<std::string, uint64_t>> TransferFunds( uint64_t                  amount,
                                                                         const std::string        &destination,
                                                                         TokenID                   token_id,
                                                                         std::chrono::milliseconds timeout );

        outcome::result<std::string> TransferFunds( uint64_t amount, const std::string &destination, TokenID token_id );

        outcome::result<std::string> PayDev( uint64_t amount, TokenID token_id );

        outcome::result<std::pair<std::string, uint64_t>> PayDev( uint64_t                  amount,
                                                                  TokenID                   token_id,
                                                                  std::chrono::milliseconds timeout );

        outcome::result<std::pair<TransactionManager::TransactionStatus, uint64_t>> WaitForFinalized(
            const std::string        &tx_id,
            std::chrono::milliseconds timeout );

        std::optional<TransactionManager::TransactionStatus> IsFinalized( const std::string &tx_id );

        std::shared_ptr<ipfs_pubsub::GossipPubSub> GetPubSub()
        {
            return pubsub_;
        }

        void ResetProcessingMembers();

        outcome::result<std::string> FormatTokens( uint64_t amount, TokenID tokenId );

        outcome::result<uint64_t> ParseTokens( const std::string &str, TokenID tokenId );

        void PrintDataStore() const;

        void StopProcessing();

        void StartProcessing();

        outcome::result<std::map<std::string, double>> GetCoinprice( const std::vector<std::string> &tokenIds );

        outcome::result<std::map<std::string, std::map<int64_t, double>>> GetCoinPriceByDate(
            const std::vector<std::string> &tokenIds,
            const std::vector<int64_t>     &timestamps );

        outcome::result<std::map<std::string, std::map<int64_t, double>>> GetCoinPricesByDateRange(
            const std::vector<std::string> &tokenIds,
            int64_t                         from,
            int64_t                         to );

        TransactionManager::TransactionStatus WaitForTransactionIncoming( const std::string        &txId,
                                                                          std::chrono::milliseconds timeout );

        TransactionManager::TransactionStatus WaitForTransactionOutgoing( const std::string        &txId,
                                                                          std::chrono::milliseconds timeout );

        TransactionManager::TransactionStatus WaitForEscrowRelease( const std::string        &originalEscrowId,
                                                                    std::chrono::milliseconds timeout );

        TransactionManager::State GetTransactionManagerState() const;

        void ConfigureRpcEndpoint( const std::string &chain_id, std::vector<WeightedRpcEndpoint> endpoints );

        TransactionManager::TransactionStatus GetTransactionStatus( const std::string &txId ) const;

        void SetAuthorizedFullNodeAddress( const std::string &pub_address );

        const std::string &GetAuthorizedFullNodeAddress() const;

        NodeState GetState() const
        {
            return state_.load();
        }

    protected:
        friend class TransactionSyncTest;
        friend class MultiAccountTestAccess;

        void SendTransactionAndProof( std::shared_ptr<GeniusTransaction> tx, std::vector<uint8_t> proof );

        void ConfigureTransactionFilterTimeoutsMs( uint64_t timeframe_limit_ms, uint64_t mutability_window_ms );

        std::string                    write_base_path_; 
        std::shared_ptr<GeniusAccount> account_;         

    private:
        std::shared_ptr<boost::asio::io_context> io_; 
        boost::asio::executor_work_guard<boost::asio::io_context::executor_type>
                                                   io_work_guard_;       
        std::shared_ptr<crdt::GlobalDB>            tx_globaldb_;         
        std::shared_ptr<crdt::GlobalDB>            job_globaldb_;        
        std::shared_ptr<ipfs_pubsub::GossipPubSub> pubsub_;              
        std::shared_ptr<TransactionManager>        transaction_manager_; 
        std::shared_ptr<MigrationManager> migration_manager_; 
        mutable std::mutex                migration_mutex_;   
        std::shared_ptr<eth::EthWatchService>                 eth_watch_service_;   
        std::shared_ptr<BridgeRelayer>                        bridge_relayer_;      
        std::shared_ptr<processing::ProcessingTaskQueue>      task_queue_;          
        std::vector<std::string>                             my_task_ids_;         
        static constexpr size_t                              kMyTasksMemoryLimit = 50; 
        std::shared_ptr<processing::ProcessingCoreImpl>       processing_core_;     
        std::shared_ptr<processing::ProcessingServiceImpl>    processing_service_;  
        std::shared_ptr<processing::SubTaskResultStorageImpl> task_result_storage_; 
        std::shared_ptr<soralog::LoggingSystem>               logging_system_;      
        bool                                                  autodht_;     
        bool                                                  isprocessor_; 
        bool                           is_full_node_;              
        base::Logger                   node_logger_;               
        GeniusNodeConfig                   dev_config_;                
        bool                           catchup_scan_done_ = false; 
        bool                           catchup_scan_in_progress_ = false; 
        std::vector<ChainContractPair> catchup_chains_; 
        mutable std::mutex             catchup_mutex_;
        std::shared_ptr<ChainRpcEndpointProvider>
                                            rpc_endpoint_provider_;    
        std::atomic<uint64_t>          bridge_init_generation_{ 0 };
        std::string                         gnus_network_full_path_;   
        std::string                         processing_channel_topic_; 
        std::string                         processing_grid_chanel_topic_; 
        std::vector<std::string>            bootstrap_peers_;
        uint16_t                       subnet_id_ = 0; 
        std::vector<std::string>            bootstrap_fullnodes_;
        std::vector<libp2p::peer::PeerInfo> bootstrap_fullnode_infos_;
        std::unordered_set<libp2p::peer::PeerId> bootstrap_fullnode_ids_;
        std::vector<libp2p::peer::PeerInfo>      bootstrap_peer_infos_;
        std::unordered_set<libp2p::peer::PeerId> bootstrap_peer_ids_;
        uint16_t                                 pubsubport_; 
        std::shared_ptr<Blockchain>              blockchain_; 

        GeniusNode( const GeniusNodeConfig            &dev_config,
                    std::shared_ptr<GeniusAccount> account,
                    bool                           autodht,
                    uint16_t                       base_port,
                    bool                           is_full_node );

        void InitOpenSSL();

        void LoadSgnsConfig();

        bool InitLoggers( const std::string &base_path );

        base::Logger ConfigureLogger( const std::string        &tag,
                                      const std::string        &logdir,
                                      spdlog::level::level_enum level );

        bool InitNetwork( uint16_t base_port, bool is_full_node );

        void LoadCrdtConfig();

        bool InitUPNP();

        bool InitDatabase();

        bool InitProcessingModules();

        void BeginDBInitialization();

        void StateTransition( NodeState next_state );

        void MigrateDatabase( std::function<void( outcome::result<void> )> callback );

        void ScheduleMigrationRetry();

        void ScheduleBlockchainRetry( std::chrono::seconds delay = std::chrono::seconds( 5 ) );

        std::filesystem::path ResolveBridgeChainsConfigPath() const;

        void InitializeAndStartBridge();

        void OnRpcEndpointsReady( std::vector<ChainContractPair> chains ) override;

        void PerformStartupCatchupScan();

        void ShutdownForDestruction();

        outcome::result<void> ShutdownAccountBoundServices( bool deconfigure_account );

        outcome::result<std::shared_ptr<TransactionManager>>      GetTransactionManager() const;
        outcome::result<std::shared_ptr<crdt::AtomicTransaction>> CreateEscrowInfoCRDTTransaction(
            std::string        path,
            sgns::base::Buffer value );

        void DHTInit();

        static boost::optional<libp2p::peer::PeerInfo> ParsePeerInfoFromString( const std::string &multiaddr_str );

        void InitBootstrapReconnect();

        void StartBootstrapHealthCheck();

        void ScheduleBootstrapReconnect( const libp2p::peer::PeerId &peer_id, unsigned attempt );

        void DoReconnectToBootstrapPeer( const libp2p::peer::PeerId &peer_id );

        void ScheduleNextHealthCheck();

        void PerformHealthCheck();

        struct PriceInfo
        {
            double                                             price;      
            std::chrono::time_point<std::chrono::system_clock> lastUpdate; 
        };

        std::map<std::string, PriceInfo>                   m_tokenPriceCache; 
        const std::chrono::minutes                         m_cacheValidityDuration{ 1 }; 
        std::chrono::time_point<std::chrono::system_clock> m_lastApiCall{}; 
        static constexpr std::chrono::seconds              MIN_API_CALL_INTERVAL{ 5 }; 

        static constexpr size_t                   DEFAULT_IO_THREADS = 4;                 
        size_t                                    io_thread_count_{ DEFAULT_IO_THREADS }; 
        std::vector<std::thread>                  io_threads_;                            
        std::thread                               upnp_thread;                      
        std::atomic<bool>                         stop_upnp{ false };               
        std::string                               base58key_;                       
        std::shared_ptr<libp2p::basic::Scheduler> scheduler_;                       
        std::shared_ptr<ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator_; 
        std::shared_ptr<ipfs_lite::ipfs::graphsync::Network>            graphsyncnetwork_; 

        std::unique_ptr<boost::asio::thread_pool> processing_callback_pool_; 

        std::atomic<NodeState> state_{ NodeState::CREATING }; 
        std::atomic_bool       shutdown_started_{ false };    

        // ── Bootstrap fullnode reconnection ──
        struct BootstrapReconnectConfig
        {
            std::chrono::seconds base_delay{ 5 };
            std::chrono::seconds max_delay{ 300 };
            std::chrono::seconds health_check_interval{ 60 };
            std::chrono::seconds health_check_disconnected_interval{ 15 };
            double               background_multiplier{ 3.0 };
        };

        BootstrapReconnectConfig                           reconnect_config_;
        std::optional<libp2p::event::Handle>               bootstrap_disconnect_subscription_;
        std::optional<libp2p::basic::Scheduler::Handle>    health_check_handle_;
        std::unordered_map<libp2p::peer::PeerId, unsigned> reconnect_attempts_;
        std::mutex                                         reconnect_mutex_;

        crdt::GlobalDB::BackupOptions crdt_backup_config_{ true, 15, 12, true };

        outcome::result<std::pair<std::string, uint64_t>> PayEscrow(
            const std::string                       &escrow_path,
            const SGProcessing::TaskResult          &taskresult,
            std::shared_ptr<crdt::AtomicTransaction> crdt_transaction,
            std::chrono::milliseconds                timeout = std::chrono::milliseconds( TIMEOUT_ESCROW_PAY ) );

        void ProcessingDone( const std::string &task_id, const SGProcessing::TaskResult &taskresult );

        void ProcessingError( const std::string &task_id );

        void RotateLogFiles( const std::string &base_path );

        outcome::result<uint64_t> ParseBlockSize( const std::string &json_data );

        void TransactionStateChanged( TransactionManager::State old_state, TransactionManager::State new_state );

        static constexpr std::string_view DB_PATH         = "bc-%d/"; 
        static constexpr std::uint16_t    MAIN_NET        = 369;      
        static constexpr std::uint16_t    TEST_NET        = 963;      
        static constexpr std::size_t      MAX_NODES_COUNT = 1;        

        static constexpr std::string_view PROCESSING_GRID_CHANNEL = "SGNUS.Jobs.Channel";  
        static constexpr std::string_view PROCESSING_CHANNEL = "SGNUS.Processing.Channel"; 
        static constexpr std::string_view GNUS_NETWORK_PATH  = "SuperGNUSNode.Node";       

        static std::string GetLoggingSystem( const std::string &base_path )
        {
            std::string config( R"(
# ----------------
sinks:
    - name: file
      type: file
      capacity: 1000
      path: [basepath]/sgnslog.log
groups:
    - name: SuperGeniusNode
      sink: file
      level: error
      children:
        - name: libp2p
        - name: Gossip
        - name: yx-stream
# ----------------
  )" );

            boost::replace_all( config, "[basepath]", base_path );
            return config;
        }

        std::string MyTasksFilePath() const;

        void LoadMyTaskIds();

        void PersistMyTaskIds();
    };
}

OUTCOME_HPP_DECLARE_ERROR_2( sgns, GeniusNode::Error );

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

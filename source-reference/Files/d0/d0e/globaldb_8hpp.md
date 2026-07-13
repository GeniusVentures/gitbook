---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/globaldb/globaldb.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/globaldb/globaldb.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/)**  |
| struct | **[sgns::crdt::GlobalDB::BackupOptions](/source-reference/Classes/d3/d2a/structsgns_1_1crdt_1_1_global_d_b_1_1_backup_options/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| | **[OUTCOME_HPP_DECLARE_ERROR_2](/source-reference/Files/d0/d0e/globaldb_8hpp/#function-outcome_hpp_declare_error_2)**([sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/) , GlobalDB::Error )<br/>Macro for declaring error handling in the GlobalDB class.  |


## Functions Documentation

### function OUTCOME_HPP_DECLARE_ERROR_2

```cpp
OUTCOME_HPP_DECLARE_ERROR_2(
    sgns::crdt ,
    GlobalDB::Error 
)
```

Macro for declaring error handling in the GlobalDB class. 



## Source code

```cpp
#ifndef SUPERGENIUS_CRDT_GLOBALDB_HPP
#define SUPERGENIUS_CRDT_GLOBALDB_HPP

#include <unordered_set>

#include <boost/asio/io_context.hpp>
#include <boost/filesystem/path.hpp>
#include <ipfs_lite/ipfs/graphsync/impl/graphsync_impl.hpp>
#include <ipfs_lite/ipfs/graphsync/impl/local_requests.hpp>
#include <ipfs_pubsub/gossip_pubsub_topic.hpp>
#include <libp2p/protocol/autonat/autonat.hpp>
#include <libp2p/protocol/holepunch/holepunch_client.hpp>
#include <libp2p/protocol/holepunch/holepunch_server.hpp>
#include <libp2p/protocol/identify/identify.hpp>

#include "crdt/atomic_transaction.hpp"
#include "crdt/crdt_datastore.hpp"
#include "crdt/crdt_options.hpp"
#include "outcome/outcome.hpp"
#include "pubsub_broadcaster_ext.hpp"

namespace sgns::crdt
{
    class GlobalDB : public std::enable_shared_from_this<GlobalDB>
    {
    public:
        struct BackupOptions
        {
            bool     enabled{ false };
            uint32_t interval_minutes{ 15 };
            uint32_t keep_count{ 12 };
            bool     auto_restore_on_repair_failure{ true };
        };

        using Buffer             = base::Buffer;
        using QueryResult        = CrdtDatastore::QueryResult;
        using RocksDB            = storage::rocksdb;
        using CRDTHeadListResult = CrdtHeads::CRDTListResult;

        static outcome::result<std::shared_ptr<GlobalDB>> New(
            std::shared_ptr<boost::asio::io_context>                              context,
            std::string                                                           databasePath,
            std::shared_ptr<sgns::ipfs_pubsub::GossipPubSub>                      pubsub,
            std::shared_ptr<CrdtOptions>                                          crdtOptions,
            std::shared_ptr<sgns::ipfs_lite::ipfs::graphsync::Network>            graphsyncnetwork,
            std::shared_ptr<libp2p::basic::Scheduler>                             scheduler,
            std::shared_ptr<sgns::ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator,
            std::shared_ptr<RocksDB>                                              datastore = nullptr,
            BackupOptions                                                         backup_options = BackupOptions{ false, 15, 12, true } );

        ~GlobalDB();

        using DataPair = std::pair<HierarchicalKey, Buffer>;
        using GlobalDBFilterCallback         = CrdtDatastore::CRDTElementFilterCallback;
        using GlobalDBNewElementCallback     = CrdtDatastore::CRDTNewElementCallback;
        using GlobalDBDeletedElementCallback = CrdtDatastore::CRDTDeletedElementCallback;

        enum class Error : uint8_t
        {
            ROCKSDB_IO = 0,                 
            IPFS_DB_NOT_CREATED,            
            DAG_SYNCHER_NOT_LISTENING,      
            CRDT_DATASTORE_NOT_CREATED,     
            PUBSUB_BROADCASTER_NOT_CREATED, 
            INVALID_PARAMETERS,             
            GLOBALDB_NOT_STARTED,           
        };

        outcome::result<CID> Put( const HierarchicalKey                 &key,
                                  const Buffer                          &value,
                                  const std::unordered_set<std::string> &topics );

        outcome::result<CID> Put( const std::vector<DataPair>           &data_vector,
                                  const std::unordered_set<std::string> &topics );

        outcome::result<Buffer> Get( const HierarchicalKey &key );

        outcome::result<CID> Remove( const HierarchicalKey &key, const std::unordered_set<std::string> &topics );

        outcome::result<QueryResult> QueryKeyValues( std::string_view keyPrefix );

        outcome::result<QueryResult> QueryKeyValues( const std::string &prefix_base,
                                                     const std::string &middle_part,
                                                     const std::string &remainder_prefix );

        outcome::result<std::string> KeyToString( const Buffer &key ) const;

        std::shared_ptr<AtomicTransaction> BeginTransaction();

        outcome::result<void> AddBroadcastTopic( const std::string &topicName );
        void                  AddTopicName( const std::string &topicName );
        void                  AddListenTopic( const std::string &topicName );

        void PrintDataStore();

        std::shared_ptr<RocksDB>                          GetDataStore();
        std::shared_ptr<sgns::crdt::PubSubBroadcasterExt> GetBroadcaster();
        std::shared_ptr<CRDTWorkJournal>                  GetWorkJournal() const;

        bool RegisterElementFilter( const std::string &pattern, GlobalDBFilterCallback filter );

        bool RegisterNewElementCallback( const std::string &pattern, GlobalDBNewElementCallback callback );

        bool RegisterDeletedElementCallback( const std::string &pattern, GlobalDBDeletedElementCallback callback );

        void UnregisterElementFilter( const std::string &pattern );

        
        void UnregisterNewElementCallback( const std::string &pattern );
        void UnregisterDeletedElementCallback( const std::string &pattern );

        void Start();

        void ShutdownNow();

        void StartCIDReceiving();

        void StartCICSync();

        void StartRebroadcastHeads();

        outcome::result<CRDTHeadListResult> GetCRDTHeadList();

        outcome::result<uint64_t> GetCRDTHeadHeight( const CID &aCid, const std::string &topic );
        outcome::result<void>     CRDTHeadRemove( const CID &aCid, const std::string &topic );
        outcome::result<void>     CRDTHeadAdd( const CID &aCid, const std::string &topic, uint64_t priority );
        outcome::result<crdt::CrdtDatastore::JobStatus> GetCIDJobStatus( const CID &cid ) const;

        outcome::result<void> RequestHeadBroadcast( const std::set<std::string> &topics );

        outcome::result<std::unordered_set<std::string>> GetMonitoredTopics() const;

        std::shared_ptr<crdt::CrdtDatastore> GetCRDTDataStore();

        outcome::result<std::vector<std::pair<std::string, base::Buffer>>> GetCIDContent(
            const std::string &cid_string );

    private:
        GlobalDB( std::shared_ptr<boost::asio::io_context>         context,
                  std::string                                      databasePath,
                  std::shared_ptr<sgns::ipfs_pubsub::GossipPubSub> pubsub );

        outcome::result<void> Init( std::shared_ptr<CrdtOptions>                               crdtOptions,
                                    std::shared_ptr<sgns::ipfs_lite::ipfs::graphsync::Network> graphsyncnetwork,
                                    std::shared_ptr<libp2p::basic::Scheduler>                  scheduler,
                                    std::shared_ptr<sgns::ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator,
                                    std::shared_ptr<RocksDB> datastore = nullptr );

        void scheduleBootstrap( std::shared_ptr<boost::asio::io_context> io_context,
                                std::shared_ptr<libp2p::Host>            host );

        std::shared_ptr<boost::asio::io_context> m_context;
        std::string                              m_databasePath;
        int                                      m_dagSyncPort;
        std::string                              m_graphSyncAddrs;

        std::shared_ptr<sgns::ipfs_pubsub::GossipPubSub>  m_pubsub;
        std::shared_ptr<sgns::crdt::PubSubBroadcasterExt> m_broadcaster;
        std::shared_ptr<RocksDB>                          m_datastore;
        std::atomic_bool                                  started_;
        bool                                              cid_sync_started_;
        bool                                              cid_receiving_started_;
        bool                                              head_broadcasting_started_;
        BackupOptions                                     backup_options_{};
        std::string                                       backup_directory_;
        std::atomic_bool                                  stop_backup_thread_{ false };
        std::atomic_bool                                  shutdown_started_{ false };
        std::thread                                       backup_thread_;
        std::mutex                                        backup_wait_mutex_;
        std::condition_variable                           backup_wait_cv_;

        //std::shared_ptr<sgns::ipfs_lite::ipfs::dht::IpfsDHT> dht_;
        //std::shared_ptr<libp2p::protocol::Identify> identify_;
        //std::shared_ptr<libp2p::protocol::IdentifyMessageProcessor> identifymsgproc_;
        //std::shared_ptr<libp2p::protocol::HolepunchClient> holepunch_;
        //std::shared_ptr<libp2p::protocol::HolepunchClientMsgProc> holepunchmsgproc_;

        int obsAddrRetries = 0;

        std::shared_ptr<CrdtDatastore> m_crdtDatastore;

        std::string ResolveBackupDirectory( const std::string &databasePathAbsolute ) const;
        void        CreateBackupNow();
        void        StartBackupLoop();
        void        StopBackupLoop();

        sgns::base::Logger m_logger = sgns::base::createLogger( "GlobalDB" );
    };
}

OUTCOME_HPP_DECLARE_ERROR_2( sgns::crdt, GlobalDB::Error );

#endif // SUPERGENIUS_CRDT_GLOBALDB_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

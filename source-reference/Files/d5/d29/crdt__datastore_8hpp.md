---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/crdt_datastore.hpp
summary: CRDT datastore class source file. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/crdt_datastore.hpp



CRDT datastore class source file.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::CrdtDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/)** <br/>Forward declaration of CRDT Set class.  |

## Functions

|                | Name           |
| -------------- | -------------- |
| | **[OUTCOME_HPP_DECLARE_ERROR_2](/source-reference/Files/d5/d29/crdt__datastore_8hpp/#function-outcome_hpp_declare_error_2)**([sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/) , CrdtDatastore::Error )<br/>Macro for declaring error handling in the CrdtDatastore class.  |

## Detailed Description

CRDT datastore class source file. 

**Date**: 2025-04-04 devcareer0 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 

## Functions Documentation

### function OUTCOME_HPP_DECLARE_ERROR_2

```cpp
OUTCOME_HPP_DECLARE_ERROR_2(
    sgns::crdt ,
    CrdtDatastore::Error 
)
```

Macro for declaring error handling in the CrdtDatastore class. 



## Source code

```cpp


#ifndef SUPERGENIUS_CRDT_DATASTORE_HPP
#define SUPERGENIUS_CRDT_DATASTORE_HPP

#include <shared_mutex>
#include <future>
#include <chrono>
#include <queue>
#include <unordered_set>
#include <map>
#include <condition_variable>
#include <optional>
#include <thread>

#include <boost/asio/steady_timer.hpp>
#include <ipfs_lite/ipld/ipld_node.hpp>
#include <primitives/cid/cid.hpp>

#include "base/logger.hpp"
#include "crdt/crdt_set.hpp"
#include "crdt/crdt_heads.hpp"
#include "crdt/broadcaster.hpp"
#include "crdt/dagsyncer.hpp"
#include "crdt/crdt_options.hpp"
#include "crdt/crdt_data_filter.hpp"
#include "crdt/crdt_callback_manager.hpp"
#include "crdt/globaldb/crdt_work_journal.hpp"
#include "storage/rocksdb/rocksdb.hpp"

namespace sgns
{
    class Blockchain;
    class ValidatorRegistry;
}

namespace sgns::crdt
{
    class CrdtSet; 

    class CrdtDatastore : public std::enable_shared_from_this<CrdtDatastore>
    {
    public:
        using Buffer      = base::Buffer;
        using Logger      = base::Logger;
        using RocksDB     = storage::rocksdb;
        using QueryResult = RocksDB::QueryResult;
        using Delta       = pb::Delta;
        using Element     = pb::Element;
        using IPLDNode    = ipfs_lite::ipld::IPLDNode;

        using CRDTElementFilterCallback  = CRDTDataFilter::ElementFilterCallback;
        using CRDTNewElementCallback     = CRDTCallbackManager::NewDataCallback;
        using CRDTDeletedElementCallback = CRDTCallbackManager::DeletedDataCallback;

        enum class JobStatus
        {
            PENDING,
            COMPLETED,
            FAILED
        };

        enum class Error
        {
            INVALID_PARAM = 0,
            FETCH_ROOT_NODE,
            NODE_DESERIALIZATION,
            FETCHING_GRAPH,
            NODE_CREATION,
            GET_NODE,
            INVALID_JOB,
        };

        static std::shared_ptr<CrdtDatastore> New( std::shared_ptr<RocksDB>     aDatastore,
                                                   const HierarchicalKey       &aKey,
                                                   std::shared_ptr<DAGSyncer>   aDagSyncer,
                                                   std::shared_ptr<Broadcaster> aBroadcaster,
                                                   std::shared_ptr<CrdtOptions> aOptions );

        void Start();
        void StartCIDProcessing();
        void StartRebroadcastHeads();
        virtual ~CrdtDatastore();

        static std::shared_ptr<Delta> DeltaMerge( const std::shared_ptr<Delta> &aDelta1,
                                                  const std::shared_ptr<Delta> &aDelta2 );

        outcome::result<Buffer> GetKey( const HierarchicalKey &aKey ) const;

        outcome::result<QueryResult> QueryKeyValues( std::string_view aPrefix ) const;

        outcome::result<QueryResult> QueryKeyValues( const std::string &prefix_base,
                                                     const std::string &middle_part,
                                                     const std::string &remainder_prefix ) const;

        std::string GetKeysPrefix() const;

        static std::string GetValueSuffix();

        outcome::result<CID> PutKey( const HierarchicalKey                 &aKey,
                                     const Buffer                          &aValue,
                                     const std::unordered_set<std::string> &topics );

        outcome::result<bool> HasKey( const HierarchicalKey &aKey ) const;

        outcome::result<CID> DeleteKey( const HierarchicalKey &aKey, const std::unordered_set<std::string> &topics );

        outcome::result<CID> Publish( const std::shared_ptr<Delta>          &aDelta,
                                      const std::unordered_set<std::string> &topics );

        outcome::result<void> PrintDAG();

        static outcome::result<std::vector<CID>> DecodeBroadcast( const Buffer &buff );

        static outcome::result<std::shared_ptr<Delta>> CreateDeltaToAdd( const std::string &key,
                                                                         const std::string &value );

        outcome::result<std::shared_ptr<Delta>> CreateDeltaToRemove( const std::string &key ) const;

        void PrintDataStore();

        void Close();

        void CancelAndCloseNow();

        bool RegisterElementFilter( const std::string &pattern, CRDTElementFilterCallback filter );
        bool RegisterNewElementCallback( const std::string &pattern, CRDTNewElementCallback callback );
        bool RegisterDeletedElementCallback( const std::string &pattern, CRDTDeletedElementCallback callback );
        void UnregisterElementFilter( const std::string &pattern );
        void UnregisterNewElementCallback( const std::string &pattern );
        void UnregisterDeletedElementCallback( const std::string &pattern );
        std::shared_ptr<CRDTWorkJournal> GetWorkJournal() const;

        void AddTopicName( const std::string &topic );

        outcome::result<CrdtHeads::CRDTListResult> GetHeadList();
        outcome::result<void>                      RemoveHead( const CID &aCid, const std::string &topic );
        outcome::result<uint64_t>                  GetHeadHeight( const CID &aCid, const std::string &topic );
        outcome::result<void>      AddHead( const CID &aCid, const std::string &topic, uint64_t priority );
        outcome::result<JobStatus> GetJobStatus( const CID &cid );

        outcome::result<void> BroadcastHeadsForTopics( const std::set<std::string> &topics );


        bool IsBroadcastEnabled() const;

        std::unordered_set<std::string> GetTopicNames() const;

        outcome::result<std::vector<std::pair<std::string, base::Buffer>>> GetILPDNodeContent(
            const std::string &cid_string );

    protected:
        friend class PubSubBroadcasterExt;
        friend class ::sgns::Blockchain;
        friend class ::sgns::ValidatorRegistry;

        struct RootCIDJob
        {
            std::shared_ptr<IPLDNode> node_;            
            std::shared_ptr<IPLDNode> root_node_;       
            bool                      created_by_self_; 
        };

        struct DagWorker
        {
            std::future<void> dagWorkerFuture_;                /*> Future for DAG worker thread */
            std::atomic<bool> dagWorkerThreadRunning_ = false; /*> Flag used for keep track of thread cycle */
            std::thread::id   threadId_;                       /*> Worker thread ID */
        };

        void HandleCIDBroadcast();
        outcome::result<void> HandleRootCIDBlock( const CID &aCid );
        outcome::result<RootCIDJob> CreateRootJob( const CID &aRootCID );
        outcome::result<std::set<CID>> GetLinksToFetch( const RootCIDJob &job );
        outcome::result<void> FetchNodes( const RootCIDJob &aRootJob, const std::set<CID> &aLinks );
        outcome::result<Delta> GetDeltaFromNode( const IPLDNode &aNode, bool created_by_self );
        outcome::result<void> MergeDataFromDelta( const CID &node_cid, const Delta &aDelta );
        outcome::result<void> ProcessJobIteration( const RootCIDJob &job_to_process );

        outcome::result<void> Sync( const HierarchicalKey &aKey );

        outcome::result<void> PrintDAGRec( const CID &aCID, uint64_t aDepth, std::vector<CID> &aSet );

        void RebroadcastHeads();

        outcome::result<void> Broadcast( const std::set<CID>                    &cids,
                                         const std::string                      &topic,
                                         boost::optional<libp2p::peer::PeerInfo> peerInfo = boost::none );

        outcome::result<Buffer> EncodeBroadcast( const std::set<CID> &heads );

        static outcome::result<Buffer> EncodeBroadcastStatic( const std::set<CID> &heads );

        outcome::result<std::shared_ptr<IPLDNode>> CreateIPLDNode(
            const std::vector<std::pair<CID, std::string>> &aHeads,
            const std::shared_ptr<Delta>                   &aDelta,
            const std::unordered_set<std::string>          &topics ) const;

        outcome::result<std::shared_ptr<IPLDNode>> CreateDAGNode( const std::shared_ptr<Delta>          &aDelta,
                                                                  const std::unordered_set<std::string> &topics );
        outcome::result<CID> AddDAGNode( const std::shared_ptr<CrdtDatastore::IPLDNode> &node );

        outcome::result<void> SyncDatastore( const std::vector<HierarchicalKey> &aKeyList );

        void PutElementsCallback( const std::string &key, const Buffer &value, const std::string &cid );
        void DeleteElementsCallback( const std::string &key, const std::string &cid );

        void UpdateCRDTHeads( const CID &rootCID, uint64_t rootPriority, bool add_topics_to_broadcast );
        bool EnqueueRootCID( const CID &cid );

        outcome::result<CID> WaitForJob( const CID &cid );

    private:
        CrdtDatastore() = delete;

        CrdtDatastore( std::shared_ptr<RocksDB>     aDatastore,
                       const HierarchicalKey       &aKey,
                       std::shared_ptr<DAGSyncer>   aDagSyncer,
                       std::shared_ptr<Broadcaster> aBroadcaster,
                       std::shared_ptr<CrdtOptions> aOptions );

        bool ShouldContinueWorkerThread( DagWorker &dagWorker );
        bool ProcessJobs( std::queue<RootCIDJob> &jobs );
        bool SeedNextExternalRoot();
        void StopWorkerLoops();
        bool IsCurrentThreadInternalWorker() const;
        void WaitForWorkersToExit();
        bool IsRootCIDPendingOrActive( const CID &cid );
        bool IsRootCIDPendingOrActiveLocked( const CID &cid ) const;
        void HandleJobProcessingFailure( const RootCIDJob &job );
        void HandleJobProcessingSuccess( const RootCIDJob &job );
        void CleanupFailedJob( const RootCIDJob &job );

        std::shared_ptr<RocksDB>     dataStore_ = nullptr;
        std::shared_ptr<CrdtOptions> options_   = nullptr;

        HierarchicalKey namespaceKey_;

        std::shared_ptr<CrdtSet>   set_   = nullptr;
        std::shared_ptr<CrdtHeads> heads_ = nullptr;

        std::shared_ptr<Broadcaster> broadcaster_ = nullptr;
        std::shared_ptr<DAGSyncer>   dagSyncer_   = nullptr;
        Logger                       logger_      = base::createLogger( "CrdtDatastore" );

        static constexpr std::chrono::milliseconds threadSleepTimeInMilliseconds_ = std::chrono::milliseconds( 500 );
        static constexpr std::string_view          headsNamespace_                = "h";
        static constexpr std::string_view          setsNamespace_                 = "s";
        int                                        numberOfDagWorkers             = 1;

        std::future<void> handleNextFuture_;
        std::atomic<bool> handleNextThreadRunning_ = false;

        std::future<void> rebroadcastFuture_;
        std::atomic<bool> rebroadcastThreadRunning_ = false;

        std::vector<std::unique_ptr<DagWorker>> dagWorkers_;
        mutable std::mutex                      workerThreadIdsMutex_;
        std::thread::id                         handleNextThreadId_;
        std::thread::id                         rebroadcastThreadId_;

        std::atomic<bool>       closeStarted_                  = false;
        std::atomic<bool>       dagWorkerJobListThreadRunning_ = false;
        std::mutex              dagWorkerMutex_;
        std::condition_variable dagWorkerCv_;

        std::queue<RootCIDJob>                               rootCIDJobList_;     // External jobs
        std::queue<RootCIDJob>                               selfCreatedJobList_; // Self-created jobs (high priority)
        std::map<CID, std::set<std::pair<CID, std::string>>> pendingHeadsByRootCID_;
        std::mutex                                           pendingHeadsMutex_;
        std::queue<CID>                                      pendingRootQueue_;
        std::optional<CID>                                   activeRootCID_;

        std::shared_ptr<CRDTWorkJournal> work_journal_;
        CRDTDataFilter                   crdt_filter_;
        bool                             started_               = false;
        bool                             broadcast_enabled_     = false;
        bool                             root_cid_sync_enabled_ = false;

        std::mutex                      rebroadcastMutex_;
        std::mutex                      dagWorkerCvMutex_;
        std::condition_variable         rebroadcastCv_;
        std::unordered_set<std::string> topicNames_;
        mutable std::mutex              topicNamesMutex_;
        std::unordered_set<std::string> pendingBroadcastTopics_;

        CRDTCallbackManager crdt_cb_manager_;

        std::map<CID, JobStatus> pending_jobs_;
        bool                     has_full_node_topic_;
        std::atomic_bool         shutdown_started_{ false };

        void MarkJobPending( const CID &cid );
        void MarkJobFailed( const CID &cid );

        // Cache for CID string representations to avoid repeated base58 encoding
        mutable std::map<CID, std::string> cid_string_cache_;
        mutable std::mutex                 cid_string_cache_mutex_;
    };

}

OUTCOME_HPP_DECLARE_ERROR_2( sgns::crdt, CrdtDatastore::Error );

#endif //SUPERGENIUS_CRDT_DATASTORE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

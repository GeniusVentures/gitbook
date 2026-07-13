---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_service.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_service.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::ProcessingServiceImpl](/source-reference/Classes/dd/d81/classsgns_1_1processing_1_1_processing_service_impl/)**  |
| struct | **[sgns::processing::ProcessingServiceImpl::ProcessingStatus](/source-reference/Classes/d7/d27/structsgns_1_1processing_1_1_processing_service_impl_1_1_processing_status/)**  |




## Source code

```cpp
#ifndef GRPC_FOR_SUPERGENIUS_PROCESSING_SERVICE
#define GRPC_FOR_SUPERGENIUS_PROCESSING_SERVICE

#include <unordered_map>

#include "processing/processing_node.hpp"
#include "processing/processing_subtask_enqueuer.hpp"

namespace sgns::processing
{
    class ProcessingServiceImpl : public std::enable_shared_from_this<ProcessingServiceImpl>
    {
    public:
        enum class Status : uint8_t {
            DISABLED,
            IDLE,
            PROCESSING,
        };

        struct ProcessingStatus {
            Status status;
            float percentage; // 0.0 to 100.0

            ProcessingStatus(Status s = Status::DISABLED, float p = 0.0f)
                : status(s), percentage(p) {}
        };

        ProcessingServiceImpl( std::shared_ptr<ipfs_pubsub::GossipPubSub>                        gossipPubSub,
                               size_t                                                            maximalNodesCount,
                               std::shared_ptr<SubTaskEnqueuer>                                  subTaskEnqueuer,
                               std::shared_ptr<SubTaskResultStorage>                             subTaskResultStorage,
                               std::shared_ptr<ProcessingCore>                                   processingCore,
                               std::function<void( const std::string              &subTaskQueueId,
                                                   const SGProcessing::TaskResult &taskresult )> userCallbackSuccess,
                               std::function<void( const std::string &subTaskQueueId )>          userCallbackError,
                               std::string                                                       node_address );

        ~ProcessingServiceImpl();

        void StartProcessing( const std::string &processingGridChannelId );

        void StopProcessing();

        size_t GetProcessingNodesCount() const;

        void SetChannelListRequestTimeout( boost::posix_time::time_duration channelListRequestTimeout );

        [[nodiscard]] ProcessingStatus GetProcessingStatus() const;

    private:
        void Listen( const std::string &processingGridChannelId );

        void SendChannelListRequest();

        void OnMessage( boost::optional<const sgns::ipfs_pubsub::GossipPubSub::Message &> message );
        void OnQueueProcessingCompleted( const std::string              &subTaskQueueId,
                                         const SGProcessing::TaskResult &taskResult );
        void OnProcessingError( const std::string &subTaskQueueId, const std::string &errorMessage );
        void OnProcessingDone( const std::string &taskId );

        void AcceptProcessingChannel( const std::string &channelId );

        void PublishLocalChannelList();

        void HandleRequestTimeout();

        void BroadcastNodeCreationIntent( const std::string &subTaskQueueId );
        void HandleNodeCreationTimeout();
        void OnNodeCreationIntent( const std::string &peerAddress, const std::string &subTaskQueueId );
        bool HasLowestAddress() const;
        bool IsPendingCreationStale() const;
        void CancelPendingCreation( const std::string &reason );

        std::shared_ptr<sgns::ipfs_pubsub::GossipPubSub>       m_gossipPubSub;
        std::shared_ptr<boost::asio::io_context>               m_context;
        std::unique_ptr<boost::asio::io_context::work>         m_context_work; // Keep context alive
        std::thread                                            io_thread;
        size_t                                                 m_maximalNodesCount;
        std::shared_ptr<SubTaskEnqueuer>                       m_subTaskEnqueuer;
        std::shared_ptr<SubTaskResultStorage>                  m_subTaskResultStorage;
        std::shared_ptr<ProcessingCore>                        m_processingCore;
        std::unique_ptr<sgns::ipfs_pubsub::GossipPubSubTopic>  m_gridChannel;
        std::unordered_map<std::string, std::shared_ptr<ProcessingNode>> m_processingNodes;
        boost::asio::deadline_timer                            m_timerChannelListRequestTimeout;
        boost::posix_time::time_duration                       m_channelListRequestTimeout;
        bool                                                   m_waitingChannelRequest = false;
        std::atomic<bool>                                      m_isStopped;
        mutable std::recursive_mutex                           m_mutexNodes;
        std::function<void( const std::string &subTaskQueueId, const SGProcessing::TaskResult &taskresult )>
                                                                 userCallbackSuccess_;
        std::function<void( const std::string &subTaskQueueId )> userCallbackError_;
        std::string                                              node_address_;

        std::set<std::string>                 m_competingPeers;
        std::chrono::steady_clock::time_point m_pendingCreationTimestamp;
        std::chrono::seconds                  m_pendingCreationTimeout{ 10 };

        boost::asio::deadline_timer         m_nodeCreationTimer;
        boost::posix_time::time_duration    m_nodeCreationTimeout;
        std::string                         m_pendingSubTaskQueueId;
        std::list<SGProcessing::SubTask>    m_pendingSubTasks;
        boost::optional<SGProcessing::Task> m_pendingTask;
        std::mutex                          m_mutexPendingCreation;

        // Blacklist for failed tasks/channels to prevent repeated processing attempts
        std::set<std::string> m_blacklistedChannels;
        std::mutex            m_mutexBlacklist;

        base::Logger m_logger = base::createLogger( "ProcessingService" );
    };
}

#endif // GRPC_FOR_SUPERGENIUS_PROCESSING_SERVICE
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_queue_manager.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_queue_manager.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::ProcessingSubTaskQueueManager](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/)** <br/>Distributed subtask queue manager.  |




## Source code

```cpp


#ifndef SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_MANAGER_HPP
#define SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_MANAGER_HPP

#include "processing/processing_subtask_queue.hpp"
#include "processing/processing_subtask_queue_channel.hpp"

#include "processing/proto/SGProcessing.pb.h"

#include <boost/asio.hpp>
#include <boost/optional.hpp>
#include <list>
#include <queue>

namespace sgns::processing
{
    class ProcessingSubTaskQueueManager : public std::enable_shared_from_this<ProcessingSubTaskQueueManager>
    {
    public:
        using SubTaskGrabbedCallback = std::function<void( boost::optional<const SGProcessing::SubTask &> )>;

        ProcessingSubTaskQueueManager( std::shared_ptr<ProcessingSubTaskQueueChannel> queueChannel,
                                       std::shared_ptr<boost::asio::io_context>       context,
                                       const std::string                             &localNodeId,
                                       std::function<void( const std::string & )>     processingErrorSink,
                                       uint64_t                                       delayBetweenProcessingMs = 20 );
        ~ProcessingSubTaskQueueManager();

        void SetProcessingTimeout( const std::chrono::system_clock::duration &processingTimeout );

        bool CreateQueue( std::list<SGProcessing::SubTask> &subTasks );

        void GrabSubTask( SubTaskGrabbedCallback onSubTaskGrabbedCallback );

        bool MoveOwnershipTo( const std::string &nodeId );

        bool HasOwnership() const;

        bool ProcessSubTaskQueueMessage( SGProcessing::SubTaskQueue *queue );

        bool ProcessSubTaskQueueRequestMessage( const SGProcessing::SubTaskQueueRequest &request );

        std::unique_ptr<SGProcessing::SubTaskQueue> GetQueueSnapshot() const;

        void ChangeSubTaskProcessingStates( const std::set<std::string> &subTaskIds, bool isProcessed );

        bool IsQueueInit()
        {
            return m_queue != nullptr;
        }

        bool IsProcessed() const;

        void SetSubTaskQueueAssignmentEventSink(
            std::function<void( const std::vector<std::string> & )> subTaskQueueAssignmentEventSink );
        uint64_t GetCurrentQueueTimestamp();

        void SetMaxSubtasksPerOwnership( size_t maxSubtasksPerOwnership )
        {
            m_defaultMaxSubtasksPerOwnership = maxSubtasksPerOwnership;
        }

    private:
        bool UpdateQueue( SGProcessing::SubTaskQueue *queue );

        void HandleQueueRequestTimeout( const boost::system::error_code &ec );
        void PublishSubTaskQueue();
        void ProcessPendingSubTaskGrabbing();
        void GrabSubTasks();
        void HandleGrabSubTaskTimeout( const boost::system::error_code &ec );
        void LogQueue() const;

        bool HasAvailableWork( bool checkOwnershipQuota = true ) const;
        void UpdateQueueTimestamp();

        void CheckActiveCount();

        uint64_t CalculateGrabSubTaskTimeout() const;

        std::vector<int> UpdateUnprocessedSubTaskIndices( const SGProcessing::SubTaskQueue *queue ) const;

        std::shared_ptr<ProcessingSubTaskQueueChannel> m_queueChannel;
        std::shared_ptr<boost::asio::io_context>       m_context;
        std::string                                    m_localNodeId;

        std::shared_ptr<SGProcessing::SubTaskQueue> m_queue;
        mutable std::recursive_mutex                m_queueMutex;
        std::list<SubTaskGrabbedCallback>           m_onSubTaskGrabbedCallbacks;

        std::function<void( const std::vector<std::string> & )> m_subTaskQueueAssignmentEventSink;
        std::set<std::string>                                   m_processedSubTaskIds;

        boost::asio::deadline_timer      m_dltQueueResponseTimeout;
        boost::posix_time::time_duration m_queueResponseTimeout;

        boost::asio::deadline_timer m_dltGrabSubTaskTimeout;

        ProcessingSubTaskQueue                     m_processingQueue;
        std::chrono::system_clock::duration        m_processingTimeout;
        std::function<void( const std::string & )> m_processingErrorSink;

        uint64_t m_queue_timestamp_           = 0; // Aggregate time counter for the queue
        uint64_t m_ownership_acquired_at_     = 0; // When this node acquired ownership (in ms)
        uint64_t m_ownership_last_delta_time_ = 0; // When this node last updated the queue timestamp

        // Add to private section of ProcessingSubTaskQueueManager
        struct OwnershipRequest
        {
            std::string node_id;
            uint64_t    timestamp; // Timestamp when request was received
        };

        std::queue<OwnershipRequest> m_ownershipRequestQueue;

        base::Logger                          m_logger = base::createLogger( "ProcessingSubTaskQueueManager" );
        std::chrono::steady_clock::time_point m_lastQueueUpdateTime = std::chrono::steady_clock::now();

        size_t         m_processedSubtasksInCurrentOwnership = 0;
        size_t         m_defaultMaxSubtasksPerOwnership      = 1;
        size_t         m_maxSubtasksPerOwnership;
        const uint64_t m_delayBetweenProcessingMs;

        std::chrono::steady_clock::time_point m_lastActiveCountCheck = std::chrono::steady_clock::now();
        std::chrono::steady_clock::duration   m_activeCountElapsed{}; 
        uint64_t                              m_waitTimeBeforeReset = 3000;  // Initial wait time of 3000ms
        bool                                  m_initialDelayPassed  = false; // Track if initial delay has passed
    };
}

#endif // SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_MANAGER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

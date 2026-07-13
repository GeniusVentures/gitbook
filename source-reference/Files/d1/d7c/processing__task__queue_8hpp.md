---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_task_queue.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_task_queue.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::ProcessingTaskQueue](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/)**  |




## Source code

```cpp


#ifndef GRPC_FOR_SUPERGENIUS_PROCESSING_TASK_QUEUE_HPP
#define GRPC_FOR_SUPERGENIUS_PROCESSING_TASK_QUEUE_HPP

#include "processing/proto/SGProcessing.pb.h"
#include "outcome/outcome.hpp"
#include "crdt/atomic_transaction.hpp"
#include <list>

namespace sgns::processing
{
    class ProcessingTaskQueue
    {
    public:
        virtual ~ProcessingTaskQueue() = default;

        outcome::result<void> EnqueueTask( const SGProcessing::Task               &task,
                                           const std::list<SGProcessing::SubTask> &subTasks )
        {
            return EnqueueTask( task, subTasks, nullptr );
        }

        virtual outcome::result<void> EnqueueTask( const SGProcessing::Task                &task,
                                                   const std::list<SGProcessing::SubTask>  &subTasks,
                                                   std::shared_ptr<crdt::AtomicTransaction> crdt_transaction ) = 0;

        virtual outcome::result<SGProcessing::Task> GetTask( const std::string &taskId ) = 0;

        virtual bool GetSubTasks( const std::string &taskId, std::list<SGProcessing::SubTask> &subTasks ) = 0;

        virtual outcome::result<std::pair<std::string, SGProcessing::Task>> GrabTask() = 0;
        
        virtual outcome::result<std::shared_ptr<crdt::AtomicTransaction>> CompleteTask(
            const std::string              &taskId,
            const SGProcessing::TaskResult &result ) = 0;

        virtual bool IsTaskCompleted( const std::string &taskId ) = 0;

        virtual void MarkTaskBad( const std::string &taskKey ) = 0;

        virtual std::vector<std::string> ListTaskKeys() = 0;

        virtual outcome::result<SGProcessing::TaskResult> GetTaskResult( const std::string &taskId ) = 0;
    };
}


#endif // GRPC_FOR_SUPERGENIUS_PROCESSING_TASK_QUEUE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/impl/TaskQueueImpl.hpp
summary: Header file for the implementation of the task queue using CRDT. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/impl/TaskQueueImpl.hpp



Header file for the implementation of the task queue using CRDT.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::TaskQueueImpl](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/)** <br/>Implements the task storage on CRDT.  |

## Detailed Description

Header file for the implementation of the task queue using CRDT. 

**Date**: 2026-05-18 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef TASK_QUEUE_IMPL_HPP
#define TASK_QUEUE_IMPL_HPP

#include <unordered_set>
#include <string>
#include <utility>
#include <memory>

#include "processing/processing_task_queue.hpp"
#include "crdt/globaldb/globaldb.hpp"
#include "crdt/atomic_transaction.hpp"
#include "processing/impl/TaskKeys.hpp"
#include "outcome/outcome.hpp"

namespace sgns::processing
{
    class TaskQueueImpl : public ProcessingTaskQueue
    {
    public:
        static std::shared_ptr<TaskQueueImpl> New( std::shared_ptr<sgns::crdt::GlobalDB> db,
                                                   std::string                           processing_topic );

        ~TaskQueueImpl() override = default;

        outcome::result<void> EnqueueTask(
            const SGProcessing::Task                &task,
            const std::list<SGProcessing::SubTask>  &subTasks,
            std::shared_ptr<crdt::AtomicTransaction> crdt_transaction = nullptr ) override;

        outcome::result<SGProcessing::Task> GetTask( const std::string &taskId ) override;
        bool GetSubTasks( const std::string &taskId, std::list<SGProcessing::SubTask> &subTasks ) override;

        outcome::result<std::pair<std::string, SGProcessing::Task>> GrabTask() override;

        outcome::result<std::shared_ptr<crdt::AtomicTransaction>> CompleteTask(
            const std::string              &taskKey,
            const SGProcessing::TaskResult &taskResult ) override;

        bool IsTaskCompleted( const std::string &taskId ) override;
        void MarkTaskBad( const std::string &taskKey ) override;

        std::vector<std::string> ListTaskKeys() override;
        outcome::result<SGProcessing::TaskResult> GetTaskResult( const std::string &taskId ) override;

    private:
        static constexpr auto LOCK_TIMEOUT = std::chrono::seconds( 10 );
        explicit TaskQueueImpl( std::shared_ptr<sgns::crdt::GlobalDB> db, std::string processing_topic );

        bool IsTaskLocked( const std::string &taskKey );

        bool LockTask( const std::string &taskKey );


        bool MoveExpiredTaskLock( const std::string &taskKey, SGProcessing::Task &task );
        std::shared_ptr<sgns::crdt::GlobalDB> db_;
        std::string processing_topic_;
        std::unordered_set<std::string> incompatible_jobs_;
    };
}
#endif // TASK_QUEUE_IMPL_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

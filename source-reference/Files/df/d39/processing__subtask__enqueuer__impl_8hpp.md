---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_enqueuer_impl.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_enqueuer_impl.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::SubTaskEnqueuerImpl](/source-reference/Classes/d1/d37/classsgns_1_1processing_1_1_sub_task_enqueuer_impl/)**  |




## Source code

```cpp
#ifndef SUPERGENIUS_PROCESSING_SUBTASK_ENQUEUER_IMPL_HPP
#define SUPERGENIUS_PROCESSING_SUBTASK_ENQUEUER_IMPL_HPP

#include <list>
#include <string>

#include "base/logger.hpp"
#include "processing/processing_subtask_enqueuer.hpp"
#include "processing/processing_task_queue.hpp"

namespace sgns::processing
{
    // Encapsulates subtask queue construction algorithm
    class SubTaskEnqueuerImpl : public SubTaskEnqueuer
    {
    public:
        SubTaskEnqueuerImpl( std::shared_ptr<ProcessingTaskQueue> taskQueue );

        outcome::result<SGProcessing::Task>  EnqueueSubTasks( std::string &subTaskQueueId, std::list<SGProcessing::SubTask> &subTasks ) override;
        void                                MarkTaskBad( const std::string &taskKey ) override;
    private:
        std::shared_ptr<ProcessingTaskQueue> m_taskQueue;
        sgns::base::Logger                   m_logger = sgns::base::createLogger( "SubTaskEnqueuerImpl" );
    };
}

#endif // SUPERGENIUS_PROCESSING_SUBTASK_ENQUEUER_IMPL_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

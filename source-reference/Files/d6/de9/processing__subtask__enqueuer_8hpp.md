---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_enqueuer.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_enqueuer.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::SubTaskEnqueuer](/source-reference/Classes/d2/d46/classsgns_1_1processing_1_1_sub_task_enqueuer/)**  |




## Source code

```cpp
#ifndef SUPERGENIUS_PROCESSING_SUBTASK_ENQUEUER_HPP
#define SUPERGENIUS_PROCESSING_SUBTASK_ENQUEUER_HPP

#include "processing/proto/SGProcessing.pb.h"
#include "outcome/outcome.hpp"
#include <list>
#include <string>

namespace sgns::processing
{
// Encapsulates subtask queue construction algorithm
class SubTaskEnqueuer
{
public:
    virtual ~SubTaskEnqueuer() = default;

    virtual outcome::result<SGProcessing::Task> EnqueueSubTasks(
        std::string& subTaskQueueId, 
        std::list<SGProcessing::SubTask>& subTasks) = 0;
    virtual void                                MarkTaskBad( const std::string &taskKey )                     = 0;
};    
}

#endif // SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_SELECTOR_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

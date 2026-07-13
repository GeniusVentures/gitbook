---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_queue_accessor.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_queue_accessor.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::SubTaskQueueAccessor](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/)**  |




## Source code

```cpp


#ifndef SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_ACCESSOR_HPP
#define SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_ACCESSOR_HPP

#include "processing/proto/SGProcessing.pb.h"
#include <boost/optional.hpp>
#include <list>

namespace sgns::processing
{
    class SubTaskQueueAccessor
    {
    public:
        using SubTaskGrabbedCallback = std::function<void( boost::optional<const SGProcessing::SubTask &> )>;

        virtual ~SubTaskQueueAccessor() = default;

        virtual bool ConnectToSubTaskQueue( std::function<void()> onSubTaskQueueConnectedEventSink ) = 0;

        virtual bool AssignSubTasks( std::list<SGProcessing::SubTask> &subTasks ) = 0;

        virtual void GrabSubTask( SubTaskGrabbedCallback onSubTaskGrabbedCallback ) = 0;

        virtual void CompleteSubTask( const std::string                 &subTaskId,
                                      const SGProcessing::SubTaskResult &subTaskResult ) = 0;

        virtual bool CreateResultsChannel( const std::string &task_id ) = 0;

        // @todo Add SetErrorsHandler method
    };
}

#endif // SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_ACCESSOR_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

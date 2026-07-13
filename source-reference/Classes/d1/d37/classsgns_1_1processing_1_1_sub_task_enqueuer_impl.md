---
title: sgns::processing::SubTaskEnqueuerImpl

---

# sgns::processing::SubTaskEnqueuerImpl






`#include <processing_subtask_enqueuer_impl.hpp>`

Inherits from [sgns::processing::SubTaskEnqueuer](/source-reference/Classes/d2/d46/classsgns_1_1processing_1_1_sub_task_enqueuer/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[SubTaskEnqueuerImpl](/source-reference/Classes/d1/d37/classsgns_1_1processing_1_1_sub_task_enqueuer_impl/#function-subtaskenqueuerimpl)**(std::shared_ptr< [ProcessingTaskQueue](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/) > taskQueue) |
| virtual outcome::result< SGProcessing::Task > | **[EnqueueSubTasks](/source-reference/Classes/d1/d37/classsgns_1_1processing_1_1_sub_task_enqueuer_impl/#function-enqueuesubtasks)**(std::string & subTaskQueueId, std::list< SGProcessing::SubTask > & subTasks) override |
| virtual void | **[MarkTaskBad](/source-reference/Classes/d1/d37/classsgns_1_1processing_1_1_sub_task_enqueuer_impl/#function-marktaskbad)**(const std::string & taskKey) override |

## Additional inherited members

**Public Functions inherited from [sgns::processing::SubTaskEnqueuer](/source-reference/Classes/d2/d46/classsgns_1_1processing_1_1_sub_task_enqueuer/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~SubTaskEnqueuer](/source-reference/Classes/d2/d46/classsgns_1_1processing_1_1_sub_task_enqueuer/#function-~subtaskenqueuer)**() =default |


## Public Functions Documentation

### function SubTaskEnqueuerImpl

```cpp
SubTaskEnqueuerImpl(
    std::shared_ptr< ProcessingTaskQueue > taskQueue
)
```


### function EnqueueSubTasks

```cpp
virtual outcome::result< SGProcessing::Task > EnqueueSubTasks(
    std::string & subTaskQueueId,
    std::list< SGProcessing::SubTask > & subTasks
) override
```


**Reimplements**: [sgns::processing::SubTaskEnqueuer::EnqueueSubTasks](/source-reference/Classes/d2/d46/classsgns_1_1processing_1_1_sub_task_enqueuer/#function-enqueuesubtasks)


### function MarkTaskBad

```cpp
virtual void MarkTaskBad(
    const std::string & taskKey
) override
```


**Reimplements**: [sgns::processing::SubTaskEnqueuer::MarkTaskBad](/source-reference/Classes/d2/d46/classsgns_1_1processing_1_1_sub_task_enqueuer/#function-marktaskbad)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
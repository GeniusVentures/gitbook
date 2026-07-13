---
title: sgns::processing::SubTaskEnqueuer

---

# sgns::processing::SubTaskEnqueuer






`#include <processing_subtask_enqueuer.hpp>`

Inherited by [sgns::processing::SubTaskEnqueuerImpl](/source-reference/Classes/d1/d37/classsgns_1_1processing_1_1_sub_task_enqueuer_impl/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~SubTaskEnqueuer](/source-reference/Classes/d2/d46/classsgns_1_1processing_1_1_sub_task_enqueuer/#function-~subtaskenqueuer)**() =default |
| virtual outcome::result< SGProcessing::Task > | **[EnqueueSubTasks](/source-reference/Classes/d2/d46/classsgns_1_1processing_1_1_sub_task_enqueuer/#function-enqueuesubtasks)**(std::string & subTaskQueueId, std::list< SGProcessing::SubTask > & subTasks) =0 |
| virtual void | **[MarkTaskBad](/source-reference/Classes/d2/d46/classsgns_1_1processing_1_1_sub_task_enqueuer/#function-marktaskbad)**(const std::string & taskKey) =0 |

## Public Functions Documentation

### function ~SubTaskEnqueuer

```cpp
virtual ~SubTaskEnqueuer() =default
```


### function EnqueueSubTasks

```cpp
virtual outcome::result< SGProcessing::Task > EnqueueSubTasks(
    std::string & subTaskQueueId,
    std::list< SGProcessing::SubTask > & subTasks
) =0
```


**Reimplemented by**: [sgns::processing::SubTaskEnqueuerImpl::EnqueueSubTasks](/source-reference/Classes/d1/d37/classsgns_1_1processing_1_1_sub_task_enqueuer_impl/#function-enqueuesubtasks)


### function MarkTaskBad

```cpp
virtual void MarkTaskBad(
    const std::string & taskKey
) =0
```


**Reimplemented by**: [sgns::processing::SubTaskEnqueuerImpl::MarkTaskBad](/source-reference/Classes/d1/d37/classsgns_1_1processing_1_1_sub_task_enqueuer_impl/#function-marktaskbad)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
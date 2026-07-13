---
title: sgns::processing::SubTaskQueueAccessor

---

# sgns::processing::SubTaskQueueAccessor



 [More...](#detailed-description)


`#include <processing_subtask_queue_accessor.hpp>`

Inherited by [sgns::processing::SubTaskQueueAccessorImpl](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/)

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::function< void(boost::optional< const SGProcessing::SubTask & >)> | **[SubTaskGrabbedCallback](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#using-subtaskgrabbedcallback)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~SubTaskQueueAccessor](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#function-~subtaskqueueaccessor)**() =default |
| virtual bool | **[ConnectToSubTaskQueue](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#function-connecttosubtaskqueue)**(std::function< void()> onSubTaskQueueConnectedEventSink) =0 |
| virtual bool | **[AssignSubTasks](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#function-assignsubtasks)**(std::list< SGProcessing::SubTask > & subTasks) =0 |
| virtual void | **[GrabSubTask](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#function-grabsubtask)**([SubTaskGrabbedCallback](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#using-subtaskgrabbedcallback) onSubTaskGrabbedCallback) =0 |
| virtual void | **[CompleteSubTask](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#function-completesubtask)**(const std::string & subTaskId, const SGProcessing::SubTaskResult & subTaskResult) =0 |
| virtual bool | **[CreateResultsChannel](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#function-createresultschannel)**(const std::string & task_id) =0 |

## Detailed Description

```cpp
class sgns::processing::SubTaskQueueAccessor;
```


Subtask queue accessor interface 

## Public Types Documentation

### using SubTaskGrabbedCallback

```cpp
using sgns::processing::SubTaskQueueAccessor::SubTaskGrabbedCallback = std::function<void( boost::optional<const SGProcessing::SubTask &> )>;
```


## Public Functions Documentation

### function ~SubTaskQueueAccessor

```cpp
virtual ~SubTaskQueueAccessor() =default
```


### function ConnectToSubTaskQueue

```cpp
virtual bool ConnectToSubTaskQueue(
    std::function< void()> onSubTaskQueueConnectedEventSink
) =0
```


**Parameters**: 

  * **onSubTaskQueueConnectedEventSink** hadnler which is called when subtask queue is connected 


**Reimplemented by**: [sgns::processing::SubTaskQueueAccessorImpl::ConnectToSubTaskQueue](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-connecttosubtaskqueue)


Starts a waiting for subtasks queue 


### function AssignSubTasks

```cpp
virtual bool AssignSubTasks(
    std::list< SGProcessing::SubTask > & subTasks
) =0
```


**Parameters**: 

  * **subTasks** - a list of enqueued subtasks 


**Reimplemented by**: [sgns::processing::SubTaskQueueAccessorImpl::AssignSubTasks](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-assignsubtasks)


Assigns a subtask list to processing queue 


### function GrabSubTask

```cpp
virtual void GrabSubTask(
    SubTaskGrabbedCallback onSubTaskGrabbedCallback
) =0
```


**Parameters**: 

  * **onSubTaskGrabbedCallback** a callback that is called when a subtask is grabbed by the local node 


**Reimplemented by**: [sgns::processing::SubTaskQueueAccessorImpl::GrabSubTask](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-grabsubtask)


Asynchronous getting of a subtask from the queue 


### function CompleteSubTask

```cpp
virtual void CompleteSubTask(
    const std::string & subTaskId,
    const SGProcessing::SubTaskResult & subTaskResult
) =0
```


**Parameters**: 

  * **subTaskId** - id of processed subtask 
  * **subTaskResult** - result of subtask processing 


**Reimplemented by**: [sgns::processing::SubTaskQueueAccessorImpl::CompleteSubTask](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-completesubtask)


Finalizes subtask execution 


### function CreateResultsChannel

```cpp
virtual bool CreateResultsChannel(
    const std::string & task_id
) =0
```


**Reimplemented by**: [sgns::processing::SubTaskQueueAccessorImpl::CreateResultsChannel](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-createresultschannel)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
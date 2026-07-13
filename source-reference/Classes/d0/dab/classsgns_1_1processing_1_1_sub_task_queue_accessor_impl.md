---
title: sgns::processing::SubTaskQueueAccessorImpl
summary: Subtask queue accessor implementation. 

---

# sgns::processing::SubTaskQueueAccessorImpl



Subtask queue accessor implementation. 


`#include <processing_subtask_queue_accessor_impl.hpp>`

Inherits from [sgns::processing::SubTaskQueueAccessor](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/), std::enable_shared_from_this< SubTaskQueueAccessorImpl >

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[FinalizationRetVal](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#enum-finalizationretval)** { NOT_FINALIZED = 0, FINALIZED = 1, FINALIZED_BUT_NOT_OWNER = 2} |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[SubTaskQueueAccessorImpl](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-subtaskqueueaccessorimpl)**(std::shared_ptr< ipfs_pubsub::GossipPubSub > gossipPubSub, std::shared_ptr< [ProcessingSubTaskQueueManager](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/) > subTaskQueueManager, std::shared_ptr< [SubTaskResultStorage](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/) > subTaskResultStorage, std::function< void(const SGProcessing::TaskResult &)> taskResultProcessingSink, std::function< void(const std::string &)> processingErrorSink) |
| | **[~SubTaskQueueAccessorImpl](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-~subtaskqueueaccessorimpl)**() override |
| virtual bool | **[ConnectToSubTaskQueue](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-connecttosubtaskqueue)**(std::function< void()> onSubTaskQueueConnectedEventSink) override |
| virtual bool | **[AssignSubTasks](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-assignsubtasks)**(std::list< SGProcessing::SubTask > & subTasks) override |
| virtual void | **[GrabSubTask](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-grabsubtask)**([SubTaskGrabbedCallback](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#using-subtaskgrabbedcallback) onSubTaskGrabbedCallback) override |
| virtual void | **[CompleteSubTask](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-completesubtask)**(const std::string & subTaskId, const SGProcessing::SubTaskResult & subTaskResult) override |
| virtual bool | **[CreateResultsChannel](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-createresultschannel)**(const std::string & task_id) override |
| std::vector< std::tuple< std::string, SGProcessing::SubTaskResult > > | **[GetResults](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/#function-getresults)**() const |

## Additional inherited members

**Public Types inherited from [sgns::processing::SubTaskQueueAccessor](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/)**

|                | Name           |
| -------------- | -------------- |
| using std::function< void(boost::optional< const SGProcessing::SubTask & >)> | **[SubTaskGrabbedCallback](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#using-subtaskgrabbedcallback)**  |

**Public Functions inherited from [sgns::processing::SubTaskQueueAccessor](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~SubTaskQueueAccessor](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#function-~subtaskqueueaccessor)**() =default |


## Public Types Documentation

### enum FinalizationRetVal

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| NOT_FINALIZED | 0|   |
| FINALIZED | 1|   |
| FINALIZED_BUT_NOT_OWNER | 2|   |




## Public Functions Documentation

### function SubTaskQueueAccessorImpl

```cpp
SubTaskQueueAccessorImpl(
    std::shared_ptr< ipfs_pubsub::GossipPubSub > gossipPubSub,
    std::shared_ptr< ProcessingSubTaskQueueManager > subTaskQueueManager,
    std::shared_ptr< SubTaskResultStorage > subTaskResultStorage,
    std::function< void(const SGProcessing::TaskResult &)> taskResultProcessingSink,
    std::function< void(const std::string &)> processingErrorSink
)
```


**Parameters**: 

  * **gossipPubSub** PubSub host used to subscribe to result channel. 
  * **subTaskQueueManager** In-memory queue manager. 
  * **subTaskResultStorage** Processing results storage. 
  * **taskResultProcessingSink** Callback invoked when task processing completes. 
  * **processingErrorSink** Callback invoked on processing errors. 


Creates subtask queue accessor implementation object. 


### function ~SubTaskQueueAccessorImpl

```cpp
~SubTaskQueueAccessorImpl() override
```


### function ConnectToSubTaskQueue

```cpp
virtual bool ConnectToSubTaskQueue(
    std::function< void()> onSubTaskQueueConnectedEventSink
) override
```


**Reimplements**: [sgns::processing::SubTaskQueueAccessor::ConnectToSubTaskQueue](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#function-connecttosubtaskqueue)


[SubTaskQueueAccessor](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/) overrides 


### function AssignSubTasks

```cpp
virtual bool AssignSubTasks(
    std::list< SGProcessing::SubTask > & subTasks
) override
```


**Parameters**: 

  * **subTasks** - a list of enqueued subtasks 


**Reimplements**: [sgns::processing::SubTaskQueueAccessor::AssignSubTasks](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#function-assignsubtasks)


Assigns a subtask list to processing queue 


### function GrabSubTask

```cpp
virtual void GrabSubTask(
    SubTaskGrabbedCallback onSubTaskGrabbedCallback
) override
```


**Parameters**: 

  * **onSubTaskGrabbedCallback** a callback that is called when a subtask is grabbed by the local node 


**Reimplements**: [sgns::processing::SubTaskQueueAccessor::GrabSubTask](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#function-grabsubtask)


Asynchronous getting of a subtask from the queue 


### function CompleteSubTask

```cpp
virtual void CompleteSubTask(
    const std::string & subTaskId,
    const SGProcessing::SubTaskResult & subTaskResult
) override
```


**Parameters**: 

  * **subTaskId** - id of processed subtask 
  * **subTaskResult** - result of subtask processing 


**Reimplements**: [sgns::processing::SubTaskQueueAccessor::CompleteSubTask](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#function-completesubtask)


Finalizes subtask execution 


### function CreateResultsChannel

```cpp
virtual bool CreateResultsChannel(
    const std::string & task_id
) override
```


**Reimplements**: [sgns::processing::SubTaskQueueAccessor::CreateResultsChannel](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/#function-createresultschannel)


### function GetResults

```cpp
std::vector< std::tuple< std::string, SGProcessing::SubTaskResult > > GetResults() const
```


**Return**: a vector of subtask id->results pairs 

Returns available results of subtask queue 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
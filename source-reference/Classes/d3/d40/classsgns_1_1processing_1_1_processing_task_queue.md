---
title: sgns::processing::ProcessingTaskQueue

---

# sgns::processing::ProcessingTaskQueue






`#include <processing_task_queue.hpp>`

Inherited by [sgns::processing::TaskQueueImpl](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~ProcessingTaskQueue](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-~processingtaskqueue)**() =default<br/>Distributed task queue interface.  |
| outcome::result< void > | **[EnqueueTask](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-enqueuetask)**(const SGProcessing::Task & task, const std::list< SGProcessing::SubTask > & subTasks)<br/>Stores a task with its subtasks.  |
| virtual outcome::result< void > | **[EnqueueTask](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-enqueuetask)**(const SGProcessing::Task & task, const std::list< SGProcessing::SubTask > & subTasks, std::shared_ptr< [crdt::AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/) > crdt_transaction) =0<br/>Stores a task with its subtasks within an atomic transaction.  |
| virtual outcome::result< SGProcessing::Task > | **[GetTask](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-gettask)**(const std::string & taskId) =0<br/>Returns a task by task id, returns failure if task not found or invalid.  |
| virtual bool | **[GetSubTasks](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-getsubtasks)**(const std::string & taskId, std::list< SGProcessing::SubTask > & subTasks) =0<br/>Retrieves the subtasks for a given task ID.  |
| virtual outcome::result< std::pair< std::string, SGProcessing::Task > > | **[GrabTask](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-grabtask)**() =0<br/>Grabs task from the storage, returning its ID and data.  |
| virtual outcome::result< std::shared_ptr< [crdt::AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/) > > | **[CompleteTask](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-completetask)**(const std::string & taskId, const SGProcessing::TaskResult & result) =0<br/>Completes a task with its result returning an atomic transaction to commit the completion.  |
| virtual bool | **[IsTaskCompleted](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-istaskcompleted)**(const std::string & taskId) =0<br/>Checks if the task is completed.  |
| virtual void | **[MarkTaskBad](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-marktaskbad)**(const std::string & taskKey) =0<br/>Mark a task key as bad to be skipped.  |
| virtual std::vector< std::string > | **[ListTaskKeys](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-listtaskkeys)**() =0<br/>Lists all known task IDs in the queue.  |
| virtual outcome::result< SGProcessing::TaskResult > | **[GetTaskResult](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-gettaskresult)**(const std::string & taskId) =0<br/>Retrieves the completed task result, if available.  |

## Public Functions Documentation

### function ~ProcessingTaskQueue

```cpp
virtual ~ProcessingTaskQueue() =default
```

Distributed task queue interface. 

Provides enqueue, retrieval, and completion tracking for tasks and their subtasks. 


### function EnqueueTask

```cpp
inline outcome::result< void > EnqueueTask(
    const SGProcessing::Task & task,
    const std::list< SGProcessing::SubTask > & subTasks
)
```

Stores a task with its subtasks. 

**Parameters**: 

  * **task** The task to store 
  * **subTasks** The subtasks to store 


**Return**: Success if the task and subtasks were stored successfully, failure otherwise 

### function EnqueueTask

```cpp
virtual outcome::result< void > EnqueueTask(
    const SGProcessing::Task & task,
    const std::list< SGProcessing::SubTask > & subTasks,
    std::shared_ptr< crdt::AtomicTransaction > crdt_transaction
) =0
```

Stores a task with its subtasks within an atomic transaction. 

**Parameters**: 

  * **task** The task to store 
  * **subTasks** The subtasks to store 
  * **crdt_transaction** The atomic transaction to use 


**Return**: Success if the task and subtasks were stored successfully, failure otherwise 

**Reimplemented by**: [sgns::processing::TaskQueueImpl::EnqueueTask](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-enqueuetask)


### function GetTask

```cpp
virtual outcome::result< SGProcessing::Task > GetTask(
    const std::string & taskId
) =0
```

Returns a task by task id, returns failure if task not found or invalid. 

**Parameters**: 

  * **taskId** the ID of the task 


**Return**: The task if found, failure otherwise 

**Reimplemented by**: [sgns::processing::TaskQueueImpl::GetTask](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-gettask)


### function GetSubTasks

```cpp
virtual bool GetSubTasks(
    const std::string & taskId,
    std::list< SGProcessing::SubTask > & subTasks
) =0
```

Retrieves the subtasks for a given task ID. 

**Parameters**: 

  * **taskId** The ID of the task for which to retrieve subtasks. 
  * **subTasks** A reference to a list where the retrieved subtasks will be stored. 


**Return**: true if the subtasks were retrieved successfully, false otherwise. 

**Reimplemented by**: [sgns::processing::TaskQueueImpl::GetSubTasks](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-getsubtasks)


### function GrabTask

```cpp
virtual outcome::result< std::pair< std::string, SGProcessing::Task > > GrabTask() =0
```

Grabs task from the storage, returning its ID and data. 

**Return**: A pair of task ID and task data if a task is found, failure otherwise. 

**Reimplemented by**: [sgns::processing::TaskQueueImpl::GrabTask](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-grabtask)


### function CompleteTask

```cpp
virtual outcome::result< std::shared_ptr< crdt::AtomicTransaction > > CompleteTask(
    const std::string & taskId,
    const SGProcessing::TaskResult & result
) =0
```

Completes a task with its result returning an atomic transaction to commit the completion. 

**Parameters**: 

  * **taskId** The ID of the task to complete 
  * **result** The result of the completed task 


**Return**: A CRDT atomic transaction if the task completion was successful, failure otherwise 

**Reimplemented by**: [sgns::processing::TaskQueueImpl::CompleteTask](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-completetask)


### function IsTaskCompleted

```cpp
virtual bool IsTaskCompleted(
    const std::string & taskId
) =0
```

Checks if the task is completed. 

**Parameters**: 

  * **taskId** Task id. 


**Return**: true if the task is completed, false otherwise. 

**Reimplemented by**: [sgns::processing::TaskQueueImpl::IsTaskCompleted](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-istaskcompleted)


### function MarkTaskBad

```cpp
virtual void MarkTaskBad(
    const std::string & taskKey
) =0
```

Mark a task key as bad to be skipped. 

**Parameters**: 

  * **taskKey** Task key to mark as bad. 


**Reimplemented by**: [sgns::processing::TaskQueueImpl::MarkTaskBad](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-marktaskbad)


### function ListTaskKeys

```cpp
virtual std::vector< std::string > ListTaskKeys() =0
```

Lists all known task IDs in the queue. 

**Return**: Vector of task IDs, or empty vector if none found. 

**Reimplemented by**: [sgns::processing::TaskQueueImpl::ListTaskKeys](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-listtaskkeys)


### function GetTaskResult

```cpp
virtual outcome::result< SGProcessing::TaskResult > GetTaskResult(
    const std::string & taskId
) =0
```

Retrieves the completed task result, if available. 

**Parameters**: 

  * **taskId** The ID of the task to retrieve the result for. 


**Return**: The TaskResult if the task is completed, or failure otherwise. 

**Reimplemented by**: [sgns::processing::TaskQueueImpl::GetTaskResult](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-gettaskresult)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: sgns::processing::TaskQueueImpl
summary: Implements the task storage on CRDT. 

---

# sgns::processing::TaskQueueImpl



Implements the task storage on CRDT. 


`#include <TaskQueueImpl.hpp>`

Inherits from [sgns::processing::ProcessingTaskQueue](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [TaskQueueImpl](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-taskqueueimpl) > | **[New](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-new)**(std::shared_ptr< [sgns::crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) > db, std::string processing_topic)<br/>Factory method to create a [TaskQueueImpl](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/) instance.  |
| | **[~TaskQueueImpl](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-~taskqueueimpl)**() override =default |
| virtual outcome::result< void > | **[EnqueueTask](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-enqueuetask)**(const SGProcessing::Task & task, const std::list< SGProcessing::SubTask > & subTasks, std::shared_ptr< [crdt::AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/) > crdt_transaction =nullptr) override<br/>Stores a task with its subtasks within an atomic transaction.  |
| virtual outcome::result< SGProcessing::Task > | **[GetTask](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-gettask)**(const std::string & taskId) override<br/>Returns a task by task id, returns failure if task not found or invalid.  |
| virtual bool | **[GetSubTasks](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-getsubtasks)**(const std::string & taskId, std::list< SGProcessing::SubTask > & subTasks) override<br/>Retrieves the subtasks for a given task ID.  |
| virtual outcome::result< std::pair< std::string, SGProcessing::Task > > | **[GrabTask](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-grabtask)**() override<br/>Grabs task from the storage, returning its ID and data.  |
| virtual outcome::result< std::shared_ptr< [crdt::AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/) > > | **[CompleteTask](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-completetask)**(const std::string & taskId, const SGProcessing::TaskResult & result) override<br/>Completes a task with its result returning an atomic transaction to commit the completion.  |
| virtual bool | **[IsTaskCompleted](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-istaskcompleted)**(const std::string & taskId) override<br/>Checks if the task is completed.  |
| virtual void | **[MarkTaskBad](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-marktaskbad)**(const std::string & taskKey) override<br/>Mark a task key as bad to be skipped.  |
| virtual std::vector< std::string > | **[ListTaskKeys](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-listtaskkeys)**() override<br/>Lists all known task IDs in the queue.  |
| virtual outcome::result< SGProcessing::TaskResult > | **[GetTaskResult](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/#function-gettaskresult)**(const std::string & taskId) override<br/>Retrieves the completed task result, if available.  |

## Additional inherited members

**Public Functions inherited from [sgns::processing::ProcessingTaskQueue](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~ProcessingTaskQueue](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-~processingtaskqueue)**() =default<br/>Distributed task queue interface.  |


## Public Functions Documentation

### function New

```cpp
static std::shared_ptr< TaskQueueImpl > New(
    std::shared_ptr< sgns::crdt::GlobalDB > db,
    std::string processing_topic
)
```

Factory method to create a [TaskQueueImpl](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/) instance. 

**Parameters**: 

  * **db** The database instance to use for storing tasks and subtasks 
  * **processing_topic** The topic for processing tasks 


**Return**: Instance of the [TaskQueueImpl](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/) initialized or nullptr if error occurs 

### function ~TaskQueueImpl

```cpp
~TaskQueueImpl() override =default
```


### function EnqueueTask

```cpp
virtual outcome::result< void > EnqueueTask(
    const SGProcessing::Task & task,
    const std::list< SGProcessing::SubTask > & subTasks,
    std::shared_ptr< crdt::AtomicTransaction > crdt_transaction =nullptr
) override
```

Stores a task with its subtasks within an atomic transaction. 

**Parameters**: 

  * **task** The task to store 
  * **subTasks** The subtasks to store 
  * **crdt_transaction** The atomic transaction to use 


**Return**: Success if the task and subtasks were stored successfully, failure otherwise 

**Reimplements**: [sgns::processing::ProcessingTaskQueue::EnqueueTask](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-enqueuetask)


### function GetTask

```cpp
virtual outcome::result< SGProcessing::Task > GetTask(
    const std::string & taskId
) override
```

Returns a task by task id, returns failure if task not found or invalid. 

**Parameters**: 

  * **taskId** the ID of the task 


**Return**: The task if found, failure otherwise 

**Reimplements**: [sgns::processing::ProcessingTaskQueue::GetTask](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-gettask)


### function GetSubTasks

```cpp
virtual bool GetSubTasks(
    const std::string & taskId,
    std::list< SGProcessing::SubTask > & subTasks
) override
```

Retrieves the subtasks for a given task ID. 

**Parameters**: 

  * **taskId** The ID of the task for which to retrieve subtasks. 
  * **subTasks** A reference to a list where the retrieved subtasks will be stored. 


**Return**: true if the subtasks were retrieved successfully, false otherwise. 

**Reimplements**: [sgns::processing::ProcessingTaskQueue::GetSubTasks](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-getsubtasks)


### function GrabTask

```cpp
virtual outcome::result< std::pair< std::string, SGProcessing::Task > > GrabTask() override
```

Grabs task from the storage, returning its ID and data. 

**Return**: A pair of task ID and task data if a task is found, failure otherwise. 

**Reimplements**: [sgns::processing::ProcessingTaskQueue::GrabTask](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-grabtask)


### function CompleteTask

```cpp
virtual outcome::result< std::shared_ptr< crdt::AtomicTransaction > > CompleteTask(
    const std::string & taskId,
    const SGProcessing::TaskResult & result
) override
```

Completes a task with its result returning an atomic transaction to commit the completion. 

**Parameters**: 

  * **taskId** The ID of the task to complete 
  * **result** The result of the completed task 


**Return**: A CRDT atomic transaction if the task completion was successful, failure otherwise 

**Reimplements**: [sgns::processing::ProcessingTaskQueue::CompleteTask](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-completetask)


### function IsTaskCompleted

```cpp
virtual bool IsTaskCompleted(
    const std::string & taskId
) override
```

Checks if the task is completed. 

**Parameters**: 

  * **taskId** Task id. 


**Return**: true if the task is completed, false otherwise. 

**Reimplements**: [sgns::processing::ProcessingTaskQueue::IsTaskCompleted](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-istaskcompleted)


### function MarkTaskBad

```cpp
virtual void MarkTaskBad(
    const std::string & taskKey
) override
```

Mark a task key as bad to be skipped. 

**Parameters**: 

  * **taskKey** Task key to mark as bad. 


**Reimplements**: [sgns::processing::ProcessingTaskQueue::MarkTaskBad](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-marktaskbad)


### function ListTaskKeys

```cpp
virtual std::vector< std::string > ListTaskKeys() override
```

Lists all known task IDs in the queue. 

**Return**: Vector of task IDs, or empty vector if none found. 

**Reimplements**: [sgns::processing::ProcessingTaskQueue::ListTaskKeys](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-listtaskkeys)


### function GetTaskResult

```cpp
virtual outcome::result< SGProcessing::TaskResult > GetTaskResult(
    const std::string & taskId
) override
```

Retrieves the completed task result, if available. 

**Parameters**: 

  * **taskId** The ID of the task to retrieve the result for. 


**Return**: The TaskResult if the task is completed, or failure otherwise. 

**Reimplements**: [sgns::processing::ProcessingTaskQueue::GetTaskResult](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/#function-gettaskresult)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
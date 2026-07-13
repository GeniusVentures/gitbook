---
title: sgns::processing::ProcessingSubTaskQueueManager
summary: Distributed subtask queue manager. 

---

# sgns::processing::ProcessingSubTaskQueueManager



Distributed subtask queue manager. 


`#include <processing_subtask_queue_manager.hpp>`

Inherits from std::enable_shared_from_this< ProcessingSubTaskQueueManager >

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::function< void(boost::optional< const SGProcessing::SubTask & >)> | **[SubTaskGrabbedCallback](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#using-subtaskgrabbedcallback)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[ProcessingSubTaskQueueManager](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-processingsubtaskqueuemanager)**(std::shared_ptr< [ProcessingSubTaskQueueChannel](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/) > queueChannel, std::shared_ptr< boost::asio::io_context > context, const std::string & localNodeId, std::function< void(const std::string &)> processingErrorSink, uint64_t delayBetweenProcessingMs =20) |
| | **[~ProcessingSubTaskQueueManager](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-~processingsubtaskqueuemanager)**() |
| void | **[SetProcessingTimeout](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-setprocessingtimeout)**(const std::chrono::system_clock::duration & processingTimeout) |
| bool | **[CreateQueue](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-createqueue)**(std::list< SGProcessing::SubTask > & subTasks) |
| void | **[GrabSubTask](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-grabsubtask)**([SubTaskGrabbedCallback](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#using-subtaskgrabbedcallback) onSubTaskGrabbedCallback) |
| bool | **[MoveOwnershipTo](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-moveownershipto)**(const std::string & nodeId) |
| bool | **[HasOwnership](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-hasownership)**() const |
| bool | **[ProcessSubTaskQueueMessage](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-processsubtaskqueuemessage)**(SGProcessing::SubTaskQueue * queue) |
| bool | **[ProcessSubTaskQueueRequestMessage](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-processsubtaskqueuerequestmessage)**(const SGProcessing::SubTaskQueueRequest & request) |
| std::unique_ptr< SGProcessing::SubTaskQueue > | **[GetQueueSnapshot](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-getqueuesnapshot)**() const |
| void | **[ChangeSubTaskProcessingStates](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-changesubtaskprocessingstates)**(const std::set< std::string > & subTaskIds, bool isProcessed) |
| bool | **[IsQueueInit](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-isqueueinit)**() |
| bool | **[IsProcessed](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-isprocessed)**() const |
| void | **[SetSubTaskQueueAssignmentEventSink](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-setsubtaskqueueassignmenteventsink)**(std::function< void(const std::vector< std::string > &)> subTaskQueueAssignmentEventSink) |
| uint64_t | **[GetCurrentQueueTimestamp](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-getcurrentqueuetimestamp)**() |
| void | **[SetMaxSubtasksPerOwnership](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/#function-setmaxsubtasksperownership)**(size_t maxSubtasksPerOwnership) |

## Public Types Documentation

### using SubTaskGrabbedCallback

```cpp
using sgns::processing::ProcessingSubTaskQueueManager::SubTaskGrabbedCallback = std::function<void( boost::optional<const SGProcessing::SubTask &> )>;
```


## Public Functions Documentation

### function ProcessingSubTaskQueueManager

```cpp
ProcessingSubTaskQueueManager(
    std::shared_ptr< ProcessingSubTaskQueueChannel > queueChannel,
    std::shared_ptr< boost::asio::io_context > context,
    const std::string & localNodeId,
    std::function< void(const std::string &)> processingErrorSink,
    uint64_t delayBetweenProcessingMs =20
)
```


**Parameters**: 

  * **queueChannel** - Task processing channel. 
  * **context** - IO context to handle timers. 
  * **localNodeId** - Local processing node ID. 
  * **processingErrorSink** - Callback for processing errors. 
  * **delayBetweenProcessingMs** - Delay between processing cycles (ms). 


Construct an empty queue manager. 


### function ~ProcessingSubTaskQueueManager

```cpp
~ProcessingSubTaskQueueManager()
```


### function SetProcessingTimeout

```cpp
void SetProcessingTimeout(
    const std::chrono::system_clock::duration & processingTimeout
)
```


**Parameters**: 

  * **processingTimeout** - subtask processing timeout Once the timeout is exceeded the subtask is marked as expired. 


Set a timeout for subtask processing 


### function CreateQueue

```cpp
bool CreateQueue(
    std::list< SGProcessing::SubTask > & subTasks
)
```


**Parameters**: 

  * **subTasks** - a list of subtasks that should be added to the queue in subtasks to allow a validation 


**Return**: false if not queue was created due to errors 

Create a subtask queue by splitting the task to subtasks using the processing code 


### function GrabSubTask

```cpp
void GrabSubTask(
    SubTaskGrabbedCallback onSubTaskGrabbedCallback
)
```


**Parameters**: 

  * **onSubTaskGrabbedCallback** a callback that is called when a grabbed iosubtask is locked by the local node 


Asynchronous getting of a subtask from the queue 


### function MoveOwnershipTo

```cpp
bool MoveOwnershipTo(
    const std::string & nodeId
)
```


**Parameters**: 

  * **nodeId** - processing node ID that the ownership should be transferred 


Transfer the queue ownership to another processing node 


### function HasOwnership

```cpp
bool HasOwnership() const
```


**Return**: true is the local node owns the queue 

Checks id the local processing node owns the queue 


### function ProcessSubTaskQueueMessage

```cpp
bool ProcessSubTaskQueueMessage(
    SGProcessing::SubTaskQueue * queue
)
```


**Parameters**: 

  * **queue** received queue snapshot 


Changes the local queue state with respect to passed queue snapshot The method should be called from a processing channel message handler 


### function ProcessSubTaskQueueRequestMessage

```cpp
bool ProcessSubTaskQueueRequestMessage(
    const SGProcessing::SubTaskQueueRequest & request
)
```


**Parameters**: 

  * **request** is a request for the queue ownership transferring 


Changes the local queue state with respect to passed queue request The method should be called from a processing channel message handler 


### function GetQueueSnapshot

```cpp
std::unique_ptr< SGProcessing::SubTaskQueue > GetQueueSnapshot() const
```


**Return**: the queue snapshot 

Returns the current local queue snapshot 


### function ChangeSubTaskProcessingStates

```cpp
void ChangeSubTaskProcessingStates(
    const std::set< std::string > & subTaskIds,
    bool isProcessed
)
```


**Parameters**: 

  * **subTaskIds** - a list of subtask which state should be changed 
  * **isProcessed** - new state 


Mark a subtask as processed/unprocessed 


### function IsQueueInit

```cpp
inline bool IsQueueInit()
```


Check whether queue has been initialized to prevent nullptr access to the queue. 


### function IsProcessed

```cpp
bool IsProcessed() const
```


**Return**: true if the queue is processed 

Checks if all subtask in the queue are processed 


### function SetSubTaskQueueAssignmentEventSink

```cpp
void SetSubTaskQueueAssignmentEventSink(
    std::function< void(const std::vector< std::string > &)> subTaskQueueAssignmentEventSink
)
```


**Parameters**: 

  * **subTaskQueueAssignmentEventSink** * lambda or function handling the event 


Sink that gets subtask assignment events 


### function GetCurrentQueueTimestamp

```cpp
uint64_t GetCurrentQueueTimestamp()
```


**Return**: The current queue timestamp as a 64-bit unsigned integer. 

Retrieves the current timestamp associated with the queue. 


### function SetMaxSubtasksPerOwnership

```cpp
inline void SetMaxSubtasksPerOwnership(
    size_t maxSubtasksPerOwnership
)
```


**Parameters**: 

  * **maxSubtasksPerOwnership** The maximum number of subtasks that can be assigned to a single ownership instance. 


Sets the maximum number of subtasks that can be owned at one time.


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
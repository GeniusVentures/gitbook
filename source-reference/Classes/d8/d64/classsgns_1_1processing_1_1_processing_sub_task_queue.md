---
title: sgns::processing::ProcessingSubTaskQueue
summary: Distributed subtask queue implementation. 

---

# sgns::processing::ProcessingSubTaskQueue



Distributed subtask queue implementation. 


`#include <processing_subtask_queue.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::function< uint64_t()> | **[TimestampProvider](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#using-timestampprovider)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[ProcessingSubTaskQueue](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#function-processingsubtaskqueue)**(std::string localNodeId, [TimestampProvider](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#using-timestampprovider) timestampProvider =nullptr) |
| void | **[CreateQueue](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#function-createqueue)**(SGProcessing::ProcessingQueue * queue, const std::vector< int > & enabledItemIndices) |
| bool | **[GrabItem](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#function-grabitem)**(size_t & grabbedItemIndex, uint64_t timestamp) |
| bool | **[MoveOwnershipTo](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#function-moveownershipto)**(const std::string & nodeId) |
| bool | **[RollbackOwnership](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#function-rollbackownership)**() |
| bool | **[HasOwnership](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#function-hasownership)**() const |
| bool | **[UpdateQueue](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#function-updatequeue)**(SGProcessing::ProcessingQueue * queue, const std::vector< int > & enabledItemIndices) |
| bool | **[UnlockExpiredItems](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#function-unlockexpireditems)**(uint64_t currentTime) |
| uint64_t | **[GetLastLockTimestamp](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#function-getlastlocktimestamp)**() const |
| bool | **[AddOwnershipRequest](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#function-addownershiprequest)**(const std::string & nodeId, uint64_t timestamp) |
| bool | **[ProcessNextOwnershipRequest](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/#function-processnextownershiprequest)**() |

## Public Types Documentation

### using TimestampProvider

```cpp
using sgns::processing::ProcessingSubTaskQueue::TimestampProvider = std::function<uint64_t()>;
```


## Public Functions Documentation

### function ProcessingSubTaskQueue

```cpp
ProcessingSubTaskQueue(
    std::string localNodeId,
    TimestampProvider timestampProvider =nullptr
)
```


**Parameters**: 

  * **localNodeId** local processing node ID 
  * **timestampProvider** get the current timestamp from the manager function 


Construct an empty queue 


### function CreateQueue

```cpp
void CreateQueue(
    SGProcessing::ProcessingQueue * queue,
    const std::vector< int > & enabledItemIndices
)
```


**Parameters**: 

  * **queue** - Queue snapshot to initialize. 
  * **enabledItemIndices** - Indexes of enabled items; disabled items are treated as deleted. 


Initialize a subtask queue snapshot. 


### function GrabItem

```cpp
bool GrabItem(
    size_t & grabbedItemIndex,
    uint64_t timestamp
)
```


**Parameters**: 

  * **grabbedItemIndex** - Index of the grabbed item if successful. 
  * **timestamp** - Current timestamp for the queue. 


**Return**: true if an item was grabbed, false otherwise. 

Attempts to grab a subtask from the queue. 


### function MoveOwnershipTo

```cpp
bool MoveOwnershipTo(
    const std::string & nodeId
)
```


**Parameters**: 

  * **nodeId** - processing node ID that the ownership should be transferred 


Transfer the queue ownership to another processing node 


### function RollbackOwnership

```cpp
bool RollbackOwnership()
```


**Return**: true if the ownership is successfully rolled back 

Rollbacks the queue ownership to the previous state 


### function HasOwnership

```cpp
bool HasOwnership() const
```


**Return**: true is the lolca node owns the queue 

Checks id the local processing node owns the queue 


### function UpdateQueue

```cpp
bool UpdateQueue(
    SGProcessing::ProcessingQueue * queue,
    const std::vector< int > & enabledItemIndices
)
```


**Parameters**: 

  * **queue** - the queue snapshot 
  * **enabledItemIndices** - indexes of enabled items. Disabled items are considered as deleted. 


Updates the local queue with a snapshot that have the most recent timestamp 


### function UnlockExpiredItems

```cpp
bool UnlockExpiredItems(
    uint64_t currentTime
)
```


**Parameters**: 

  * **currentTime** - the current queue time 


**Return**: true if at least one item was unlocked 

Unlocks expired queue items 


### function GetLastLockTimestamp

```cpp
uint64_t GetLastLockTimestamp() const
```


Returns the most recent item lock timestamp 


### function AddOwnershipRequest

```cpp
bool AddOwnershipRequest(
    const std::string & nodeId,
    uint64_t timestamp
)
```


**Parameters**: 

  * **nodeId** - ID of the node requesting ownership 
  * **timestamp** - timestamp when the request was created 


**Return**: true if the request was successfully added, false if it already exists 

Adds a new ownership request to the queue 


### function ProcessNextOwnershipRequest

```cpp
bool ProcessNextOwnershipRequest()
```


**Return**: true if an ownership request was processed, false if the queue is empty or the node doesn't have ownership 

Processes the next ownership request in the queue 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: sgns::processing::ProcessingNode
summary: Node for distributed computation. 

---

# sgns::processing::ProcessingNode



Node for distributed computation.  [More...](#detailed-description)


`#include <processing_node.hpp>`

Inherits from std::enable_shared_from_this< ProcessingNode >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [ProcessingNode](/source-reference/Classes/d2/d5b/classsgns_1_1processing_1_1_processing_node/#function-processingnode) > | **[New](/source-reference/Classes/d2/d5b/classsgns_1_1processing_1_1_processing_node/#function-new)**(std::shared_ptr< ipfs_pubsub::GossipPubSub > gossipPubSub, std::shared_ptr< [SubTaskResultStorage](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/) > subTaskResultStorage, std::shared_ptr< [ProcessingCore](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/) > processingCore, std::function< void(const SGProcessing::TaskResult &)> taskResultProcessingSink, std::function< void(const std::string &)> processingErrorSink, std::function< void(void)> processingDoneSink, std::string node_id, const std::string & processingQueueChannelId, std::list< SGProcessing::SubTask > subTasks ={}, std::chrono::milliseconds msSubscriptionWaitingDuration =std::chrono::milliseconds(2000), std::chrono::seconds ttl =std::chrono::minutes(2))<br/>Creates a processing node instance.  |
| | **[~ProcessingNode](/source-reference/Classes/d2/d5b/classsgns_1_1processing_1_1_processing_node/#function-~processingnode)**() |
| bool | **[HasQueueOwnership](/source-reference/Classes/d2/d5b/classsgns_1_1processing_1_1_processing_node/#function-hasqueueownership)**() const |
| float | **[GetProgress](/source-reference/Classes/d2/d5b/classsgns_1_1processing_1_1_processing_node/#function-getprogress)**() const |

## Detailed Description

```cpp
class sgns::processing::ProcessingNode;
```

Node for distributed computation. 

Coordinates subtask queue ownership, processing, and result publication. 

## Public Functions Documentation

### function New

```cpp
static std::shared_ptr< ProcessingNode > New(
    std::shared_ptr< ipfs_pubsub::GossipPubSub > gossipPubSub,
    std::shared_ptr< SubTaskResultStorage > subTaskResultStorage,
    std::shared_ptr< ProcessingCore > processingCore,
    std::function< void(const SGProcessing::TaskResult &)> taskResultProcessingSink,
    std::function< void(const std::string &)> processingErrorSink,
    std::function< void(void)> processingDoneSink,
    std::string node_id,
    const std::string & processingQueueChannelId,
    std::list< SGProcessing::SubTask > subTasks ={},
    std::chrono::milliseconds msSubscriptionWaitingDuration =std::chrono::milliseconds(2000),
    std::chrono::seconds ttl =std::chrono::minutes(2)
)
```

Creates a processing node instance. 

**Parameters**: 

  * **gossipPubSub** PubSub service for queue coordination. 
  * **subTaskResultStorage** Storage for subtask results. 
  * **processingCore** Processing core to execute subtasks. 
  * **taskResultProcessingSink** Callback for task result processing. 
  * **processingErrorSink** Callback for processing errors. 
  * **processingDoneSink** Callback when processing is done. 
  * **node_id** Identifier of the processing node. 
  * **processingQueueChannelId** Queue channel identifier. 
  * **subTasks** Optional initial subtask list. 
  * **msSubscriptionWaitingDuration** Wait duration for queue subscription. 
  * **ttl** Time-to-live for node ownership. 


### function ~ProcessingNode

```cpp
~ProcessingNode()
```


### function HasQueueOwnership

```cpp
bool HasQueueOwnership() const
```


### function GetProgress

```cpp
float GetProgress() const
```


**Return**: Progress percentage (0.0 to 100.0) 

Get current processing progress 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
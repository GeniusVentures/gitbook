---
title: sgns::processing::ProcessingSubTaskQueueChannel

---

# sgns::processing::ProcessingSubTaskQueueChannel



 [More...](#detailed-description)


`#include <processing_subtask_queue_channel.hpp>`

Inherited by [sgns::processing::ProcessingSubTaskQueueChannelPubSub](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~ProcessingSubTaskQueueChannel](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/#function-~processingsubtaskqueuechannel)**() =default |
| virtual void | **[RequestQueueOwnership](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/#function-requestqueueownership)**(const std::string & nodeId) =0 |
| virtual void | **[PublishQueue](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/#function-publishqueue)**(std::shared_ptr< SGProcessing::SubTaskQueue > queue) =0 |
| virtual size_t | **[GetActiveNodesCount](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/#function-getactivenodescount)**() const =0 |
| virtual std::vector< libp2p::peer::PeerId > | **[GetActiveNodes](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/#function-getactivenodes)**() const =0 |

## Detailed Description

```cpp
class sgns::processing::ProcessingSubTaskQueueChannel;
```


Subtask queue channel interface which is used for in-memory queue synchronization 

## Public Functions Documentation

### function ~ProcessingSubTaskQueueChannel

```cpp
virtual ~ProcessingSubTaskQueueChannel() =default
```


### function RequestQueueOwnership

```cpp
virtual void RequestQueueOwnership(
    const std::string & nodeId
) =0
```


**Reimplemented by**: [sgns::processing::ProcessingSubTaskQueueChannelPubSub::RequestQueueOwnership](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-requestqueueownership)


Sends a request for queue ownership nodeId - requestor node id 


### function PublishQueue

```cpp
virtual void PublishQueue(
    std::shared_ptr< SGProcessing::SubTaskQueue > queue
) =0
```


**Reimplemented by**: [sgns::processing::ProcessingSubTaskQueueChannelPubSub::PublishQueue](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-publishqueue)


Publishes queue to all queue consumers queue = subtask queue 


### function GetActiveNodesCount

```cpp
virtual size_t GetActiveNodesCount() const =0
```


**Return**: number of nodes in the channel 

**Reimplemented by**: [sgns::processing::ProcessingSubTaskQueueChannelPubSub::GetActiveNodesCount](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-getactivenodescount)


Returns the number of active nodes in the channel 


### function GetActiveNodes

```cpp
virtual std::vector< libp2p::peer::PeerId > GetActiveNodes() const =0
```


**Return**: vector of nodes in the channel 

**Reimplemented by**: [sgns::processing::ProcessingSubTaskQueueChannelPubSub::GetActiveNodes](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-getactivenodes)


Get the number of active nodes in the channel 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
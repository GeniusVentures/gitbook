---
title: sgns::processing::ProcessingSubTaskQueueChannelPubSub

---

# sgns::processing::ProcessingSubTaskQueueChannelPubSub



 [More...](#detailed-description)


`#include <processing_subtask_queue_channel_pubsub.hpp>`

Inherits from [sgns::processing::ProcessingSubTaskQueueChannel](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/), std::enable_shared_from_this< ProcessingSubTaskQueueChannelPubSub >

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::function< bool(const SGProcessing::SubTaskQueueRequest &)> | **[QueueRequestSink](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#using-queuerequestsink)**  |
| using std::function< bool(SGProcessing::SubTaskQueue *)> | **[QueueUpdateSink](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#using-queueupdatesink)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[ProcessingSubTaskQueueChannelPubSub](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-processingsubtaskqueuechannelpubsub)**(std::shared_ptr< sgns::ipfs_pubsub::GossipPubSub > gossipPubSub, const std::string & processingQueueChannelId) |
| | **[~ProcessingSubTaskQueueChannelPubSub](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-~processingsubtaskqueuechannelpubsub)**() override |
| virtual void | **[RequestQueueOwnership](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-requestqueueownership)**(const std::string & nodeId) override |
| virtual void | **[PublishQueue](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-publishqueue)**(std::shared_ptr< SGProcessing::SubTaskQueue > queue) override |
| void | **[SetQueueRequestSink](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-setqueuerequestsink)**([QueueRequestSink](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#using-queuerequestsink) queueRequestSink) |
| void | **[SetQueueUpdateSink](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-setqueueupdatesink)**([QueueUpdateSink](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#using-queueupdatesink) queueUpdateSink) |
| outcome::result< std::variant< std::chrono::milliseconds, std::shared_future< std::shared_ptr< GossipPubSubTopic::Subscription > > > > | **[Listen](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-listen)**(std::chrono::milliseconds msSubscriptionWaitingDuration =std::chrono::milliseconds(2000)) |
| virtual size_t | **[GetActiveNodesCount](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-getactivenodescount)**() const override |
| virtual std::vector< libp2p::peer::PeerId > | **[GetActiveNodes](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/#function-getactivenodes)**() const override |

## Additional inherited members

**Public Functions inherited from [sgns::processing::ProcessingSubTaskQueueChannel](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~ProcessingSubTaskQueueChannel](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/#function-~processingsubtaskqueuechannel)**() =default |


## Detailed Description

```cpp
class sgns::processing::ProcessingSubTaskQueueChannelPubSub;
```


Subtask queue channel implementation that uses pubsub as a data transport protocol 

## Public Types Documentation

### using QueueRequestSink

```cpp
using sgns::processing::ProcessingSubTaskQueueChannelPubSub::QueueRequestSink = std::function<bool( const SGProcessing::SubTaskQueueRequest & )>;
```


### using QueueUpdateSink

```cpp
using sgns::processing::ProcessingSubTaskQueueChannelPubSub::QueueUpdateSink = std::function<bool( SGProcessing::SubTaskQueue * )>;
```


## Public Functions Documentation

### function ProcessingSubTaskQueueChannelPubSub

```cpp
ProcessingSubTaskQueueChannelPubSub(
    std::shared_ptr< sgns::ipfs_pubsub::GossipPubSub > gossipPubSub,
    const std::string & processingQueueChannelId
)
```


**Parameters**: 

  * **gossipPubSub** - ipfs pubsub 
  * **processingQueueChannelId** - a unique id of queue data channel 


Constructs subtask queue channel object 


### function ~ProcessingSubTaskQueueChannelPubSub

```cpp
~ProcessingSubTaskQueueChannelPubSub() override
```


### function RequestQueueOwnership

```cpp
virtual void RequestQueueOwnership(
    const std::string & nodeId
) override
```


**Reimplements**: [sgns::processing::ProcessingSubTaskQueueChannel::RequestQueueOwnership](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/#function-requestqueueownership)


[ProcessingSubTaskQueueChannel](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/) overrides 


### function PublishQueue

```cpp
virtual void PublishQueue(
    std::shared_ptr< SGProcessing::SubTaskQueue > queue
) override
```


**Reimplements**: [sgns::processing::ProcessingSubTaskQueueChannel::PublishQueue](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/#function-publishqueue)


Publishes queue to all queue consumers queue = subtask queue 


### function SetQueueRequestSink

```cpp
void SetQueueRequestSink(
    QueueRequestSink queueRequestSink
)
```


**Parameters**: 

  * **queueRequestSink** - request handler 


Sets a handler for remote queue requests processing 


### function SetQueueUpdateSink

```cpp
void SetQueueUpdateSink(
    QueueUpdateSink queueUpdateSink
)
```


Sets a handler for remote queue updates processing 


### function Listen

```cpp
outcome::result< std::variant< std::chrono::milliseconds, std::shared_future< std::shared_ptr< GossipPubSubTopic::Subscription > > > > Listen(
    std::chrono::milliseconds msSubscriptionWaitingDuration =std::chrono::milliseconds(2000)
)
```


**Parameters**: 

  * **msSubscriptionWaitingDuration** - Duration to wait for subscription, 0 means no waiting 


**Return**: If msSubscriptionWaitingDuration > 0: outcome with success/failure and actual wait time If msSubscriptionWaitingDuration = 0: outcome with future that completes when subscription is established 

Starts a listening to pubsub channel 


### function GetActiveNodesCount

```cpp
virtual size_t GetActiveNodesCount() const override
```


**Return**: The number of active nodes currently participating in the channel. 

**Reimplements**: [sgns::processing::ProcessingSubTaskQueueChannel::GetActiveNodesCount](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/#function-getactivenodescount)


Retrieves the count of active nodes in the subtask queue channel. 


### function GetActiveNodes

```cpp
virtual std::vector< libp2p::peer::PeerId > GetActiveNodes() const override
```


**Return**: A vector of strings containing the IDs of active nodes in the channel. 

**Reimplements**: [sgns::processing::ProcessingSubTaskQueueChannel::GetActiveNodes](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/#function-getactivenodes)


Retrieves the list of active node IDs currently participating in the subtask queue channel. 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
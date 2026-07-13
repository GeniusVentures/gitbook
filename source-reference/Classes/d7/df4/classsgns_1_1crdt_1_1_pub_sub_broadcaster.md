---
title: sgns::crdt::PubSubBroadcaster

---

# sgns::crdt::PubSubBroadcaster






`#include <pubsub_broadcaster.hpp>`

Inherits from [sgns::crdt::Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/)

## Public Types

|                | Name           |
| -------------- | -------------- |
| using sgns::ipfs_pubsub::GossipPubSub | **[GossipPubSub](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/#using-gossippubsub)**  |
| using sgns::ipfs_pubsub::GossipPubSubTopic | **[GossipPubSubTopic](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/#using-gossippubsubtopic)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[PubSubBroadcaster](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/#function-pubsubbroadcaster)**(std::shared_ptr< [GossipPubSubTopic](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/#using-gossippubsubtopic) > pubSubTopic) |
| void | **[SetLogger](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/#function-setlogger)**([base::Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) logger) |
| virtual outcome::result< void > | **[Broadcast](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/#function-broadcast)**(const [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) & buff, std::string topic, boost::optional< libp2p::peer::PeerInfo > peerInfo =boost::none) override |
| virtual outcome::result< [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) > | **[Next](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/#function-next)**() override |
| virtual bool | **[HasTopic](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/#function-hastopic)**(const std::string & topic) override<br/>Checks whether the broadcaster is subscribed to the specified topic.  |

## Additional inherited members

**Public Types inherited from [sgns::crdt::Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/)**

|                | Name           |
| -------------- | -------------- |
| enum class| **[ErrorCode](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#enum-errorcode)** { Success, ErrNoMoreBroadcast} |

**Public Functions inherited from [sgns::crdt::Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-~broadcaster)**() =default |
| virtual std::shared_ptr< void > | **[GetDagSyncer](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-getdagsyncer)**() const<br/>Get the underlying DAG syncer (if available).  |


## Public Types Documentation

### using GossipPubSub

```cpp
using sgns::crdt::PubSubBroadcaster::GossipPubSub = sgns::ipfs_pubsub::GossipPubSub;
```


### using GossipPubSubTopic

```cpp
using sgns::crdt::PubSubBroadcaster::GossipPubSubTopic = sgns::ipfs_pubsub::GossipPubSubTopic;
```


## Public Functions Documentation

### function PubSubBroadcaster

```cpp
PubSubBroadcaster(
    std::shared_ptr< GossipPubSubTopic > pubSubTopic
)
```


### function SetLogger

```cpp
inline void SetLogger(
    base::Logger logger
)
```


### function Broadcast

```cpp
virtual outcome::result< void > Broadcast(
    const base::Buffer & buff,
    std::string topic,
    boost::optional< libp2p::peer::PeerInfo > peerInfo =boost::none
) override
```


**Parameters**: 

  * **buff** [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) containing the data to broadcast. 
  * **topic** Topic to broadcast to. 
  * **peerInfo** Optional peer info. 


**Return**: outcome::success on success or outcome::failure on error 

**Reimplements**: [sgns::crdt::Broadcaster::Broadcast](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-broadcast)


Send buffer payload to other replicas. 


### function Next

```cpp
virtual outcome::result< base::Buffer > Next() override
```


**Return**: buffer value or outcome::failure on error 

**Reimplements**: [sgns::crdt::Broadcaster::Next](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-next)


Obtain the next payload received from the network. 


### function HasTopic

```cpp
inline virtual bool HasTopic(
    const std::string & topic
) override
```

Checks whether the broadcaster is subscribed to the specified topic. 

**Parameters**: 

  * **topic** The topic string to check. 


**Return**: true if the broadcaster is subscribed to the topic, false otherwise. 

**Reimplements**: [sgns::crdt::Broadcaster::HasTopic](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-hastopic)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
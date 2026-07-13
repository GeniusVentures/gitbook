---
title: sgns::crdt::PubSubBroadcasterExt
summary: Extended PubSub broadcaster that integrates with a CRDT datastore and Graphsync DAG syncer. 

---

# sgns::crdt::PubSubBroadcasterExt



Extended PubSub broadcaster that integrates with a CRDT datastore and Graphsync DAG syncer.  [More...](#detailed-description)


`#include <pubsub_broadcaster_ext.hpp>`

Inherits from [sgns::crdt::Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/), std::enable_shared_from_this< PubSubBroadcasterExt >

## Public Types

|                | Name           |
| -------------- | -------------- |
| using sgns::ipfs_pubsub::GossipPubSub | **[GossipPubSub](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#using-gossippubsub)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[~PubSubBroadcasterExt](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-~pubsubbroadcasterext)**() |
| virtual outcome::result< void > | **[Broadcast](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-broadcast)**(const [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) & buff, std::string topic, boost::optional< libp2p::peer::PeerInfo > peerInfo =boost::none) override<br/>Sends the given buffer as a broadcast to peers.  |
| virtual outcome::result< [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) > | **[Next](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-next)**() override<br/>Retrieves the next incoming broadcast payload.  |
| void | **[Start](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-start)**()<br/>Subscribes to all configured topics and starts message processing. Must be called before using [Next()](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-next) to receive incoming messages.  |
| outcome::result< void > | **[AddBroadcastTopic](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-addbroadcasttopic)**(const std::string & topicName)<br/>Adds a new topic by name.  |
| void | **[AddListenTopic](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-addlistentopic)**(std::string topic)<br/>Subscribe to a given topic and store its future.  |
| virtual bool | **[HasTopic](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-hastopic)**(const std::string & topic) override<br/>Checks whether the given topic is already registered.  |
| virtual std::shared_ptr< void > | **[GetDagSyncer](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-getdagsyncer)**() const override<br/>Get the underlying [GraphsyncDAGSyncer](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/) instance.  |
| void | **[Stop](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-stop)**() |
| bool | **[AddSingleCIDInfo](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-addsinglecidinfo)**(const std::string & cid, const std::string peer_id, const std::string address) |
| std::shared_ptr< [PubSubBroadcasterExt](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-pubsubbroadcasterext) > | **[New](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-new)**(std::shared_ptr< [sgns::crdt::GraphsyncDAGSyncer](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/) > dagSyncer, std::shared_ptr< [GossipPubSub](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#using-gossippubsub) > pubSub)<br/>Factory method to create a broadcaster for multiple topics.  |

## Additional inherited members

**Public Types inherited from [sgns::crdt::Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/)**

|                | Name           |
| -------------- | -------------- |
| enum class| **[ErrorCode](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#enum-errorcode)** { Success, ErrNoMoreBroadcast} |

**Public Functions inherited from [sgns::crdt::Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-~broadcaster)**() =default |


## Detailed Description

```cpp
class sgns::crdt::PubSubBroadcasterExt;
```

Extended PubSub broadcaster that integrates with a CRDT datastore and Graphsync DAG syncer. 

Manages multiple gossip topics, broadcasting messages and processing incoming payloads. 

## Public Types Documentation

### using GossipPubSub

```cpp
using sgns::crdt::PubSubBroadcasterExt::GossipPubSub = sgns::ipfs_pubsub::GossipPubSub;
```


## Public Functions Documentation

### function ~PubSubBroadcasterExt

```cpp
~PubSubBroadcasterExt()
```


### function Broadcast

```cpp
virtual outcome::result< void > Broadcast(
    const base::Buffer & buff,
    std::string topic,
    boost::optional< libp2p::peer::PeerInfo > peerInfo =boost::none
) override
```

Sends the given buffer as a broadcast to peers. 

**Parameters**: 

  * **buff** [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) containing the data to broadcast. 
  * **topic** Topic to broadcast to. 
  * **peerInfo** Optional peer info to avoid repeated GetPeerInfo calls. 


**Return**: outcome::success on successful publish, or outcome::failure on error. 

**Reimplements**: [sgns::crdt::Broadcaster::Broadcast](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-broadcast)


### function Next

```cpp
virtual outcome::result< base::Buffer > Next() override
```

Retrieves the next incoming broadcast payload. 

**Return**: buffer value or outcome::failure on error 

**Reimplements**: [sgns::crdt::Broadcaster::Next](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-next)


### function Start

```cpp
void Start()
```

Subscribes to all configured topics and starts message processing. Must be called before using [Next()](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-next) to receive incoming messages. 

**Note**: Ensures message processing is ready before any CRDT operations run. 

### function AddBroadcastTopic

```cpp
outcome::result< void > AddBroadcastTopic(
    const std::string & topicName
)
```

Adds a new topic by name. 

**Parameters**: 

  * **topicName** Name of the topic to add. 


**Return**: outcome::success() on success (or if topic already existed), outcome::failure() on error. 

### function AddListenTopic

```cpp
void AddListenTopic(
    std::string topic
)
```

Subscribe to a given topic and store its future. 

**Parameters**: 

  * **topic** Name of the topic to listen to. 


### function HasTopic

```cpp
virtual bool HasTopic(
    const std::string & topic
) override
```

Checks whether the given topic is already registered. 

**Parameters**: 

  * **topic** Name of the topic to check. 


**Return**: True if the topic exists, false otherwise. 

**Reimplements**: [sgns::crdt::Broadcaster::HasTopic](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-hastopic)


### function GetDagSyncer

```cpp
inline virtual std::shared_ptr< void > GetDagSyncer() const override
```

Get the underlying [GraphsyncDAGSyncer](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/) instance. 

**Return**: Shared pointer to the [GraphsyncDAGSyncer](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/) (as void pointer). 

**Reimplements**: [sgns::crdt::Broadcaster::GetDagSyncer](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-getdagsyncer)


### function Stop

```cpp
void Stop()
```


### function AddSingleCIDInfo

```cpp
bool AddSingleCIDInfo(
    const std::string & cid,
    const std::string peer_id,
    const std::string address
)
```


### function New

```cpp
static std::shared_ptr< PubSubBroadcasterExt > New(
    std::shared_ptr< sgns::crdt::GraphsyncDAGSyncer > dagSyncer,
    std::shared_ptr< GossipPubSub > pubSub
)
```

Factory method to create a broadcaster for multiple topics. 

**Parameters**: 

  * **dagSyncer** Graphsync DAG syncer for block exchange. 
  * **pubSub** PubSub instance used to subscribe and publish. 


**Return**: Shared pointer to the new [PubSubBroadcasterExt](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/). 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
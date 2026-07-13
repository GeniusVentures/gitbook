---
title: sgns::crdt::Broadcaster
summary: A Broadcaster provides a way to send (notify) an opaque payload to all replicas and to retrieve payloads broadcasted. 

---

# sgns::crdt::Broadcaster



A [Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/) provides a way to send (notify) an opaque payload to all replicas and to retrieve payloads broadcasted. 


`#include <broadcaster.hpp>`

Inherited by [sgns::crdt::PubSubBroadcaster](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/), [sgns::crdt::PubSubBroadcasterExt](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/)

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[ErrorCode](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#enum-errorcode)** { Success = 0, ErrNoMoreBroadcast = 1} |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-~broadcaster)**() =default |
| virtual outcome::result< void > | **[Broadcast](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-broadcast)**(const [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) & buff, std::string topic, boost::optional< libp2p::peer::PeerInfo > peerInfo =boost::none) =0 |
| virtual outcome::result< [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) > | **[Next](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-next)**() =0 |
| virtual bool | **[HasTopic](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-hastopic)**(const std::string & topic) =0<br/>Checks whether the broadcaster is subscribed to the specified topic.  |
| virtual std::shared_ptr< void > | **[GetDagSyncer](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/#function-getdagsyncer)**() const<br/>Get the underlying DAG syncer (if available).  |

## Public Types Documentation

### enum ErrorCode

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| Success | 0|   |
| ErrNoMoreBroadcast | 1|   |




## Public Functions Documentation

### function ~Broadcaster

```cpp
virtual ~Broadcaster() =default
```


### function Broadcast

```cpp
virtual outcome::result< void > Broadcast(
    const base::Buffer & buff,
    std::string topic,
    boost::optional< libp2p::peer::PeerInfo > peerInfo =boost::none
) =0
```


**Parameters**: 

  * **buff** [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) containing the data to broadcast. 
  * **topic** Topic to broadcast to. 
  * **peerInfo** Optional peer info to avoid repeated GetPeerInfo calls. 


**Return**: outcome::success on success or outcome::failure on error. 

**Reimplemented by**: [sgns::crdt::PubSubBroadcaster::Broadcast](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/#function-broadcast), [sgns::crdt::PubSubBroadcasterExt::Broadcast](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-broadcast)


Send buffer payload to other replicas. 


### function Next

```cpp
virtual outcome::result< base::Buffer > Next() =0
```


**Return**: buffer value or outcome::failure on error 

**Reimplemented by**: [sgns::crdt::PubSubBroadcaster::Next](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/#function-next), [sgns::crdt::PubSubBroadcasterExt::Next](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-next)


Obtain the next payload and its topic received from the network. 


### function HasTopic

```cpp
virtual bool HasTopic(
    const std::string & topic
) =0
```

Checks whether the broadcaster is subscribed to the specified topic. 

**Parameters**: 

  * **topic** The topic string to check. 


**Return**: true if the broadcaster is subscribed to the topic, false otherwise. 

**Reimplemented by**: [sgns::crdt::PubSubBroadcaster::HasTopic](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/#function-hastopic), [sgns::crdt::PubSubBroadcasterExt::HasTopic](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-hastopic)


### function GetDagSyncer

```cpp
inline virtual std::shared_ptr< void > GetDagSyncer() const
```

Get the underlying DAG syncer (if available). 

**Return**: Shared pointer to the DAG syncer, or nullptr if not available. 

**Reimplemented by**: [sgns::crdt::PubSubBroadcasterExt::GetDagSyncer](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/#function-getdagsyncer)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: sgns::subscription::SubscriptionEngine

---

# sgns::subscription::SubscriptionEngine



 [More...](#detailed-description)


`#include <subscription_engine.hpp>`

Inherits from std::enable_shared_from_this< SubscriptionEngine< Key, Type, Arguments... > >

## Public Types

|                | Name           |
| -------------- | -------------- |
| using Key | **[KeyType](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-keytype)**  |
| using Type | **[ValueType](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-valuetype)**  |
| using [Subscriber](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#friend-subscriber)< [KeyType](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-keytype), [ValueType](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-valuetype), Arguments... > | **[SubscriberType](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-subscribertype)**  |
| using std::shared_ptr< [SubscriberType](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-subscribertype) > | **[SubscriberPtr](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-subscriberptr)**  |
| using std::weak_ptr< [SubscriberType](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-subscribertype) > | **[SubscriberWPtr](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-subscriberwptr)**  |
| using std::list< [SubscriberWPtr](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-subscriberwptr) > | **[SubscribersContainer](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-subscriberscontainer)**  |
| using typename SubscribersContainer::iterator | **[IteratorType](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-iteratortype)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[SubscriptionEngine](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#function-subscriptionengine)**() =default |
| | **[~SubscriptionEngine](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#function-~subscriptionengine)**() =default |
| | **[SubscriptionEngine](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#function-subscriptionengine)**(SubscriptionEngine && ) =default |
| [SubscriptionEngine](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#function-subscriptionengine) & | **[operator=](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#function-operator=)**([SubscriptionEngine](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#function-subscriptionengine) && ) =default |
| | **[SubscriptionEngine](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#function-subscriptionengine)**(const SubscriptionEngine & ) =delete |
| [SubscriptionEngine](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#function-subscriptionengine) & | **[operator=](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#function-operator=)**(const [SubscriptionEngine](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#function-subscriptionengine) & ) =delete |
| size_t | **[size](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#function-size)**(const [KeyType](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-keytype) & key) const |
| void | **[notify](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#function-notify)**(const [KeyType](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#using-keytype) & key, const Arguments &... args) |

## Friends

|                | Name           |
| -------------- | -------------- |
| class | **[Subscriber](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/#friend-subscriber)**  |

## Detailed Description

```cpp
template <typename Key ,
typename Type ,
typename... Arguments>
class sgns::subscription::SubscriptionEngine;
```

## Public Types Documentation

### using KeyType

```cpp
using sgns::subscription::SubscriptionEngine< Key, Type, Arguments >::KeyType = Key;
```


### using ValueType

```cpp
using sgns::subscription::SubscriptionEngine< Key, Type, Arguments >::ValueType = Type;
```


### using SubscriberType

```cpp
using sgns::subscription::SubscriptionEngine< Key, Type, Arguments >::SubscriberType = Subscriber<KeyType, ValueType, Arguments...>;
```


### using SubscriberPtr

```cpp
using sgns::subscription::SubscriptionEngine< Key, Type, Arguments >::SubscriberPtr = std::shared_ptr<SubscriberType>;
```


### using SubscriberWPtr

```cpp
using sgns::subscription::SubscriptionEngine< Key, Type, Arguments >::SubscriberWPtr = std::weak_ptr<SubscriberType>;
```


### using SubscribersContainer

```cpp
using sgns::subscription::SubscriptionEngine< Key, Type, Arguments >::SubscribersContainer = std::list<SubscriberWPtr>;
```


List is preferable here because this container iterators remain alive after removal from the middle of the container TODO(iceseer): PRE-476 remove processor cache penalty, while iterating, using custom allocator 


### using IteratorType

```cpp
using sgns::subscription::SubscriptionEngine< Key, Type, Arguments >::IteratorType = typename SubscribersContainer::iterator;
```


## Public Functions Documentation

### function SubscriptionEngine

```cpp
SubscriptionEngine() =default
```


### function ~SubscriptionEngine

```cpp
~SubscriptionEngine() =default
```


### function SubscriptionEngine

```cpp
SubscriptionEngine(
    SubscriptionEngine && 
) =default
```


### function operator=

```cpp
SubscriptionEngine & operator=(
    SubscriptionEngine && 
) =default
```


### function SubscriptionEngine

```cpp
SubscriptionEngine(
    const SubscriptionEngine & 
) =delete
```


### function operator=

```cpp
SubscriptionEngine & operator=(
    const SubscriptionEngine & 
) =delete
```


### function size

```cpp
inline size_t size(
    const KeyType & key
) const
```


### function notify

```cpp
inline void notify(
    const KeyType & key,
    const Arguments &... args
)
```


## Friends

### friend Subscriber

```cpp
friend class Subscriber(
    Subscriber 
);
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
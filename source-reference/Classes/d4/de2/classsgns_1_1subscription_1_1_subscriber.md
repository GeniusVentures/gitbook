---
title: sgns::subscription::Subscriber

---

# sgns::subscription::Subscriber



 [More...](#detailed-description)


`#include <subscriber.hpp>`

Inherits from std::enable_shared_from_this< Subscriber< Key, Type, Arguments... > >

## Public Types

|                | Name           |
| -------------- | -------------- |
| using Key | **[KeyType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-keytype)**  |
| using Type | **[ValueType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-valuetype)**  |
| using size_t | **[HashType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-hashtype)**  |
| using uint64_t | **[SubscriptionSetId](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-subscriptionsetid)**  |
| using [SubscriptionEngine](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/)< [KeyType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-keytype), [ValueType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-valuetype), Arguments... > | **[SubscriptionEngineType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-subscriptionenginetype)**  |
| using std::shared_ptr< [SubscriptionEngineType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-subscriptionenginetype) > | **[SubscriptionEnginePtr](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-subscriptionengineptr)**  |
| using std::function< void([ValueType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-valuetype) &, const [KeyType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-keytype) &, const Arguments &...)> | **[CallbackFnType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-callbackfntype)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| template <typename... Args\> <br/>| **[Subscriber](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-subscriber)**([SubscriptionEnginePtr](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-subscriptionengineptr) & ptr, Args &&... args) |
| | **[~Subscriber](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-~subscriber)**() |
| | **[Subscriber](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-subscriber)**(const Subscriber & ) =delete |
| [Subscriber](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-subscriber) & | **[operator=](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-operator=)**(const [Subscriber](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-subscriber) & ) =delete |
| | **[Subscriber](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-subscriber)**(Subscriber && ) =default |
| [Subscriber](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-subscriber) & | **[operator=](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-operator=)**([Subscriber](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-subscriber) && ) =default |
| void | **[setCallback](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-setcallback)**([CallbackFnType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-callbackfntype) && f) |
| [SubscriptionSetId](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-subscriptionsetid) | **[generateSubscriptionSetId](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-generatesubscriptionsetid)**() |
| void | **[subscribe](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-subscribe)**([SubscriptionSetId](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-subscriptionsetid) id, const [KeyType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-keytype) & key) |
| void | **[unsubscribe](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-unsubscribe)**([SubscriptionSetId](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-subscriptionsetid) id, const [KeyType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-keytype) & key) |
| void | **[unsubscribe](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-unsubscribe)**([SubscriptionSetId](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-subscriptionsetid) id) |
| void | **[unsubscribe](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-unsubscribe)**() |
| void | **[on_notify](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#function-on_notify)**(const [KeyType](/source-reference/Classes/d4/de2/classsgns_1_1subscription_1_1_subscriber/#using-keytype) & key, const Arguments &... args) |

## Detailed Description

```cpp
template <typename Key ,
typename Type ,
typename... Arguments>
class sgns::subscription::Subscriber;
```


**Template Parameters**: 

  * **Key** is a type of a subscription Key. 
  * **Type** is a type of an object to receive notifications in. 
  * **Arguments** is a set of types of objects needed to construct Type. 


Is a wrapper class, which provides subscription to events from [SubscriptionEngine](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/)

## Public Types Documentation

### using KeyType

```cpp
using sgns::subscription::Subscriber< Key, Type, Arguments >::KeyType = Key;
```


### using ValueType

```cpp
using sgns::subscription::Subscriber< Key, Type, Arguments >::ValueType = Type;
```


### using HashType

```cpp
using sgns::subscription::Subscriber< Key, Type, Arguments >::HashType = size_t;
```


### using SubscriptionSetId

```cpp
using sgns::subscription::Subscriber< Key, Type, Arguments >::SubscriptionSetId = uint64_t;
```


### using SubscriptionEngineType

```cpp
using sgns::subscription::Subscriber< Key, Type, Arguments >::SubscriptionEngineType = 
SubscriptionEngine<KeyType, ValueType, Arguments...>;
```


### using SubscriptionEnginePtr

```cpp
using sgns::subscription::Subscriber< Key, Type, Arguments >::SubscriptionEnginePtr = std::shared_ptr<SubscriptionEngineType>;
```


### using CallbackFnType

```cpp
using sgns::subscription::Subscriber< Key, Type, Arguments >::CallbackFnType = std::function<void(ValueType&, const KeyType &, const Arguments &...)>;
```


## Public Functions Documentation

### function Subscriber

```cpp
template <typename... Args>
inline explicit Subscriber(
    SubscriptionEnginePtr & ptr,
    Args &&... args
)
```


### function ~Subscriber

```cpp
inline ~Subscriber()
```


Unsubscribe all


### function Subscriber

```cpp
Subscriber(
    const Subscriber & 
) =delete
```


### function operator=

```cpp
Subscriber & operator=(
    const Subscriber & 
) =delete
```


### function Subscriber

```cpp
Subscriber(
    Subscriber && 
) =default
```


### function operator=

```cpp
Subscriber & operator=(
    Subscriber && 
) =default
```


### function setCallback

```cpp
inline void setCallback(
    CallbackFnType && f
)
```


### function generateSubscriptionSetId

```cpp
inline SubscriptionSetId generateSubscriptionSetId()
```


### function subscribe

```cpp
inline void subscribe(
    SubscriptionSetId id,
    const KeyType & key
)
```


Here we check first local subscriptions because of strong connection with [SubscriptionEngine](/source-reference/Classes/d7/d3a/classsgns_1_1subscription_1_1_subscription_engine/).


### function unsubscribe

```cpp
inline void unsubscribe(
    SubscriptionSetId id,
    const KeyType & key
)
```


### function unsubscribe

```cpp
inline void unsubscribe(
    SubscriptionSetId id
)
```


### function unsubscribe

```cpp
inline void unsubscribe()
```


### function on_notify

```cpp
inline void on_notify(
    const KeyType & key,
    const Arguments &... args
)
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
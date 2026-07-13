---
title: sgns::watcher::MessagingWatcher

---

# sgns::watcher::MessagingWatcher






`#include <messaging_watcher.hpp>`

Inherited by [sgns::evmwatcher::BridgeRpcWatcher](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/), [sgns::evmwatcher::EvmMessagingWatcher](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/)

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::function< void(const std::string &)> | **[MessageCallback](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#using-messagecallback)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-~messagingwatcher)**() =default |
| virtual void | **[startWatching](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-startwatching)**() |
| virtual void | **[stopWatching](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-stopwatching)**() |
| bool | **[isRunning](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-isrunning)**() const |
| void | **[addWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-addwatcher)**(const std::shared_ptr< [MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-messagingwatcher) > & newWatcher) |
| void | **[startAll](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-startall)**() |
| void | **[stopAll](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-stopall)**() |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| | **[MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-messagingwatcher)**([MessageCallback](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#using-messagecallback) callback) |
| virtual void | **[watch](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-watch)**() |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| [MessageCallback](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#using-messagecallback) | **[messageCallback](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#variable-messagecallback)**  |
| bool | **[running](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#variable-running)**  |
| std::mutex | **[running_mutex](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#variable-running_mutex)**  |
| boost::thread | **[watcherThread](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#variable-watcherthread)**  |

## Public Types Documentation

### using MessageCallback

```cpp
using sgns::watcher::MessagingWatcher::MessageCallback = std::function<void(const std::string &)>;
```


## Public Functions Documentation

### function ~MessagingWatcher

```cpp
virtual ~MessagingWatcher() =default
```


### function startWatching

```cpp
virtual void startWatching()
```


**Reimplemented by**: [sgns::evmwatcher::BridgeRpcWatcher::startWatching](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/#function-startwatching), [sgns::evmwatcher::EvmMessagingWatcher::startWatching](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#function-startwatching)


### function stopWatching

```cpp
virtual void stopWatching()
```


**Reimplemented by**: [sgns::evmwatcher::BridgeRpcWatcher::stopWatching](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/#function-stopwatching), [sgns::evmwatcher::EvmMessagingWatcher::stopWatching](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#function-stopwatching)


### function isRunning

```cpp
bool isRunning() const
```


### function addWatcher

```cpp
static void addWatcher(
    const std::shared_ptr< MessagingWatcher > & newWatcher
)
```


### function startAll

```cpp
static void startAll()
```


### function stopAll

```cpp
static void stopAll()
```


## Protected Functions Documentation

### function MessagingWatcher

```cpp
explicit MessagingWatcher(
    MessageCallback callback
)
```


### function watch

```cpp
virtual void watch()
```


**Reimplemented by**: [sgns::evmwatcher::BridgeRpcWatcher::watch](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/#function-watch)


## Protected Attributes Documentation

### variable messageCallback

```cpp
MessageCallback messageCallback;
```


### variable running

```cpp
bool running;
```


### variable running_mutex

```cpp
std::mutex running_mutex;
```


### variable watcherThread

```cpp
boost::thread watcherThread;
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
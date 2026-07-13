---
title: sgns::evmwatcher::BridgeRpcWatcher
summary: RPC-based bridge event watcher that polls eth_getLogs, verifies receipts, and produces normalized BridgeEventClaim objects. 

---

# sgns::evmwatcher::BridgeRpcWatcher



RPC-based bridge event watcher that polls eth_getLogs, verifies receipts, and produces normalized BridgeEventClaim objects.  [More...](#detailed-description)


`#include <bridge_rpc_watcher.hpp>`

Inherits from [sgns::watcher::MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/)

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[Config](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/)** <br/>Configuration structure for [BridgeRpcWatcher](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/).  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::function< void(const eth::BridgeEventClaim &)> | **[BridgeClaimCallback](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/#using-bridgeclaimcallback)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[BridgeRpcWatcher](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/#function-bridgerpcwatcher)**(const [Config](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/) & config, [MessageCallback](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#using-messagecallback) message_callback, [BridgeClaimCallback](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/#using-bridgeclaimcallback) claim_callback)<br/>Constructs a [BridgeRpcWatcher](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/) with the specified configuration and callbacks.  |
| virtual void | **[startWatching](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/#function-startwatching)**() override |
| virtual void | **[stopWatching](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/#function-stopwatching)**() override |
| const [Config](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/) & | **[GetConfig](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/#function-getconfig)**() const<br/>Returns the watcher's configuration.  |
| uint64_t | **[GetLastProcessedBlock](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/#function-getlastprocessedblock)**() const<br/>Returns the last processed block number.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual void | **[watch](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/#function-watch)**() override |

## Additional inherited members

**Public Types inherited from [sgns::watcher::MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/)**

|                | Name           |
| -------------- | -------------- |
| using std::function< void(const std::string &)> | **[MessageCallback](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#using-messagecallback)**  |

**Public Functions inherited from [sgns::watcher::MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-~messagingwatcher)**() =default |
| bool | **[isRunning](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-isrunning)**() const |
| void | **[addWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-addwatcher)**(const std::shared_ptr< [MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-messagingwatcher) > & newWatcher) |
| void | **[startAll](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-startall)**() |
| void | **[stopAll](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-stopall)**() |

**Protected Functions inherited from [sgns::watcher::MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/)**

|                | Name           |
| -------------- | -------------- |
| | **[MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-messagingwatcher)**([MessageCallback](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#using-messagecallback) callback) |

**Protected Attributes inherited from [sgns::watcher::MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/)**

|                | Name           |
| -------------- | -------------- |
| [MessageCallback](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#using-messagecallback) | **[messageCallback](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#variable-messagecallback)**  |
| bool | **[running](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#variable-running)**  |
| std::mutex | **[running_mutex](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#variable-running_mutex)**  |
| boost::thread | **[watcherThread](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#variable-watcherthread)**  |


## Detailed Description

```cpp
class sgns::evmwatcher::BridgeRpcWatcher;
```

RPC-based bridge event watcher that polls eth_getLogs, verifies receipts, and produces normalized BridgeEventClaim objects. 

Unlike [EvmMessagingWatcher](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/) (which uses WebSocket eth_subscribe), this watcher uses eth::rpc::RpcHttpTransport for JSON-RPC over HTTP. It polls at a configurable interval, fetches logs for the bridge contract, verifies each event through eth_getTransactionReceipt, and emits eth::BridgeEventClaim objects via a typed callback. 

## Public Types Documentation

### using BridgeClaimCallback

```cpp
using sgns::evmwatcher::BridgeRpcWatcher::BridgeClaimCallback = std::function<void( const eth::BridgeEventClaim & )>;
```


## Public Functions Documentation

### function BridgeRpcWatcher

```cpp
BridgeRpcWatcher(
    const Config & config,
    MessageCallback message_callback,
    BridgeClaimCallback claim_callback
)
```

Constructs a [BridgeRpcWatcher](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/) with the specified configuration and callbacks. 

**Parameters**: 

  * **config** Configuration parameters for the watcher. 
  * **message_callback** Callback for raw message handling (inherited from MessagingWatcher). 
  * **claim_callback** Typed callback invoked with parsed BridgeEventClaim objects when events are detected. 


### function startWatching

```cpp
virtual void startWatching() override
```


**Reimplements**: [sgns::watcher::MessagingWatcher::startWatching](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-startwatching)


### function stopWatching

```cpp
virtual void stopWatching() override
```


**Reimplements**: [sgns::watcher::MessagingWatcher::stopWatching](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-stopwatching)


### function GetConfig

```cpp
inline const Config & GetConfig() const
```

Returns the watcher's configuration. 

**Return**: Reference to the [Config](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/) struct used by this watcher. 

### function GetLastProcessedBlock

```cpp
inline uint64_t GetLastProcessedBlock() const
```

Returns the last processed block number. 

**Return**: Returns the last block number that was processed by the watcher. 

## Protected Functions Documentation

### function watch

```cpp
virtual void watch() override
```


**Reimplements**: [sgns::watcher::MessagingWatcher::watch](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-watch)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
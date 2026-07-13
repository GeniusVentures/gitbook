---
title: sgns::evmwatcher::EvmMessagingWatcher

---

# sgns::evmwatcher::EvmMessagingWatcher






`#include <evm_messaging_watcher.hpp>`

Inherits from [sgns::watcher::MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/)

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[ChainConfig](/source-reference/Classes/d7/d91/structsgns_1_1evmwatcher_1_1_evm_messaging_watcher_1_1_chain_config/)**  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| using [api::WsClientImpl::Context](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#using-context) | **[Context](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#using-context)**  |
| using struct { std::string topic_hash; } | **[TopicFilter](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#using-topicfilter)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[EvmMessagingWatcher](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#function-evmmessagingwatcher)**(const rapidjson::Document & config, [MessageCallback](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#using-messagecallback) callback, const std::string & contract_address, const std::vector< [TopicFilter](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#using-topicfilter) > & topic_filters) |
| std::string | **[getContractAddress](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#function-getcontractaddress)**() const |
| void | **[setContractAddress](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#function-setcontractaddress)**(const std::string & contract_address) |
| std::vector< [TopicFilter](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#using-topicfilter) > | **[getTopicFilters](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#function-gettopicfilters)**() const |
| void | **[setTopicFilters](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#function-settopicfilters)**(const std::vector< [TopicFilter](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#using-topicfilter) > & topic_filters) |
| void | **[setupWebSocketListener](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#function-setupwebsocketlistener)**(const [ChainConfig](/source-reference/Classes/d7/d91/structsgns_1_1evmwatcher_1_1_evm_messaging_watcher_1_1_chain_config/) & chainConfig) |
| [ChainConfig](/source-reference/Classes/d7/d91/structsgns_1_1evmwatcher_1_1_evm_messaging_watcher_1_1_chain_config/) | **[getChain](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#function-getchain)**() const |
| virtual void | **[startWatching](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#function-startwatching)**() override |
| virtual void | **[stopWatching](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/#function-stopwatching)**() override |

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
| virtual void | **[watch](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#function-watch)**() |

**Protected Attributes inherited from [sgns::watcher::MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/)**

|                | Name           |
| -------------- | -------------- |
| [MessageCallback](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#using-messagecallback) | **[messageCallback](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#variable-messagecallback)**  |
| bool | **[running](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#variable-running)**  |
| std::mutex | **[running_mutex](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#variable-running_mutex)**  |
| boost::thread | **[watcherThread](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/#variable-watcherthread)**  |


## Public Types Documentation

### using Context

```cpp
using sgns::evmwatcher::EvmMessagingWatcher::Context = api::WsClientImpl::Context;
```


### using TopicFilter

```cpp
using sgns::evmwatcher::EvmMessagingWatcher::TopicFilter = struct {
           std::string topic_hash;
       };
```


## Public Functions Documentation

### function EvmMessagingWatcher

```cpp
EvmMessagingWatcher(
    const rapidjson::Document & config,
    MessageCallback callback,
    const std::string & contract_address,
    const std::vector< TopicFilter > & topic_filters
)
```


### function getContractAddress

```cpp
std::string getContractAddress() const
```


### function setContractAddress

```cpp
void setContractAddress(
    const std::string & contract_address
)
```


### function getTopicFilters

```cpp
std::vector< TopicFilter > getTopicFilters() const
```


### function setTopicFilters

```cpp
void setTopicFilters(
    const std::vector< TopicFilter > & topic_filters
)
```


### function setupWebSocketListener

```cpp
void setupWebSocketListener(
    const ChainConfig & chainConfig
)
```


### function getChain

```cpp
ChainConfig getChain() const
```


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


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
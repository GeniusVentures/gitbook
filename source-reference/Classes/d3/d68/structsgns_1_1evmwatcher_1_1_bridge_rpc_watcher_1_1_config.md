---
title: sgns::evmwatcher::BridgeRpcWatcher::Config
summary: Configuration structure for BridgeRpcWatcher. 

---

# sgns::evmwatcher::BridgeRpcWatcher::Config



Configuration structure for [BridgeRpcWatcher](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/). 


`#include <bridge_rpc_watcher.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::string | **[rpc_url](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/#variable-rpc_url)** <br/>URL of the RPC.  |
| uint64_t | **[chain_id](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/#variable-chain_id)** <br/>The source chain ID.  |
| uint64_t | **[dest_chain_id](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/#variable-dest_chain_id)** <br/>The destination chain ID (Genius).  |
| std::string | **[contract_address](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/#variable-contract_address)** <br/>The address of the bridge contract.  |
| std::string | **[event_signature](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/#variable-event_signature)** <br/>The signature of the event to listen for.  |
| uint64_t | **[confirmation_depth](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/#variable-confirmation_depth)** <br/>The number of blocks to wait before considering an event confirmed.  |
| std::chrono::seconds | **[poll_interval](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/#variable-poll_interval)** <br/>The interval at which to poll for new events.  |
| uint64_t | **[max_log_range](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/#variable-max_log_range)** <br/>The maximum range of blocks to query for logs.  |

## Public Attributes Documentation

### variable rpc_url

```cpp
std::string rpc_url;
```

URL of the RPC. 

### variable chain_id

```cpp
uint64_t chain_id = 0;
```

The source chain ID. 

### variable dest_chain_id

```cpp
uint64_t dest_chain_id = 0;
```

The destination chain ID (Genius). 

### variable contract_address

```cpp
std::string contract_address;
```

The address of the bridge contract. 

### variable event_signature

```cpp
std::string event_signature;
```

The signature of the event to listen for. 

### variable confirmation_depth

```cpp
uint64_t confirmation_depth = 12;
```

The number of blocks to wait before considering an event confirmed. 

### variable poll_interval

```cpp
std::chrono::seconds poll_interval { 4 };
```

The interval at which to poll for new events. 

### variable max_log_range

```cpp
uint64_t max_log_range = 1000;
```

The maximum range of blocks to query for logs. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
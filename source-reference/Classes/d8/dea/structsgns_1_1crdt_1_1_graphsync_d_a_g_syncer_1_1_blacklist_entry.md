---
title: sgns::crdt::GraphsyncDAGSyncer::BlacklistEntry

---

# sgns::crdt::GraphsyncDAGSyncer::BlacklistEntry






`#include <graphsync_dagsyncer.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[BlacklistEntry](/source-reference/Classes/d8/dea/structsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_blacklist_entry/#function-blacklistentry)**(uint64_t time, uint64_t count, bool connected =false) |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| uint64_t | **[timestamp](/source-reference/Classes/d8/dea/structsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_blacklist_entry/#variable-timestamp)**  |
| uint64_t | **[failures](/source-reference/Classes/d8/dea/structsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_blacklist_entry/#variable-failures)**  |
| bool | **[ever_connected](/source-reference/Classes/d8/dea/structsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_blacklist_entry/#variable-ever_connected)**  |
| uint64_t | **[backoff_attempts](/source-reference/Classes/d8/dea/structsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_blacklist_entry/#variable-backoff_attempts)**  |

## Public Functions Documentation

### function BlacklistEntry

```cpp
inline BlacklistEntry(
    uint64_t time,
    uint64_t count,
    bool connected =false
)
```


## Public Attributes Documentation

### variable timestamp

```cpp
uint64_t timestamp;
```


### variable failures

```cpp
uint64_t failures;
```


### variable ever_connected

```cpp
bool ever_connected;
```


### variable backoff_attempts

```cpp
uint64_t backoff_attempts;
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
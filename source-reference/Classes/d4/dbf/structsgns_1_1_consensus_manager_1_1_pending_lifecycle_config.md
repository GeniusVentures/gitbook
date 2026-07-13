---
title: sgns::ConsensusManager::PendingLifecycleConfig
summary: Local pending proposal lifecycle limits. 

---

# sgns::ConsensusManager::PendingLifecycleConfig



Local pending proposal lifecycle limits. 


`#include <Consensus.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::size_t | **[max_pending_proposals](/source-reference/Classes/d4/dbf/structsgns_1_1_consensus_manager_1_1_pending_lifecycle_config/#variable-max_pending_proposals)**  |
| std::size_t | **[max_pending_per_proposer](/source-reference/Classes/d4/dbf/structsgns_1_1_consensus_manager_1_1_pending_lifecycle_config/#variable-max_pending_per_proposer)**  |
| std::size_t | **[max_retained_pending_bytes](/source-reference/Classes/d4/dbf/structsgns_1_1_consensus_manager_1_1_pending_lifecycle_config/#variable-max_retained_pending_bytes)**  |
| std::chrono::milliseconds | **[pending_ttl](/source-reference/Classes/d4/dbf/structsgns_1_1_consensus_manager_1_1_pending_lifecycle_config/#variable-pending_ttl)**  |
| std::chrono::milliseconds | **[min_dependency_retry_interval](/source-reference/Classes/d4/dbf/structsgns_1_1_consensus_manager_1_1_pending_lifecycle_config/#variable-min_dependency_retry_interval)**  |
| std::vector< std::chrono::milliseconds > | **[scheduled_retry_delays](/source-reference/Classes/d4/dbf/structsgns_1_1_consensus_manager_1_1_pending_lifecycle_config/#variable-scheduled_retry_delays)**  |

## Public Attributes Documentation

### variable max_pending_proposals

```cpp
std::size_t max_pending_proposals = 1024;
```


### variable max_pending_per_proposer

```cpp
std::size_t max_pending_per_proposer = 64;
```


### variable max_retained_pending_bytes

```cpp
std::size_t max_retained_pending_bytes = 64ULL * 1024ULL * 1024ULL;
```


### variable pending_ttl

```cpp
std::chrono::milliseconds pending_ttl = std::chrono::minutes( 3 );
```


### variable min_dependency_retry_interval

```cpp
std::chrono::milliseconds min_dependency_retry_interval = std::chrono::seconds( 1 );
```


### variable scheduled_retry_delays

```cpp
std::vector< std::chrono::milliseconds > scheduled_retry_delays = { std::chrono::seconds( 1 ),
                               std::chrono::seconds( 2 ),
                               std::chrono::seconds( 5 ),
                               std::chrono::seconds( 10 ) };
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
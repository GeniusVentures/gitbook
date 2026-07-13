---
title: sgns::ConsensusManager::ValidationResult
summary: Local structured validation result for subject handlers. 

---

# sgns::ConsensusManager::ValidationResult



Local structured validation result for subject handlers.  [More...](#detailed-description)


`#include <Consensus.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[ValidationResult](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#function-validationresult)**() =default |
| | **[ValidationResult](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#function-validationresult)**([Check](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#enum-check) result) |
| [ValidationResult](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#function-validationresult) | **[Approve](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#function-approve)**() |
| [ValidationResult](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#function-validationresult) | **[Reject](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#function-reject)**() |
| [ValidationResult](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#function-validationresult) | **[Stalled](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#function-stalled)**() |
| [ValidationResult](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#function-validationresult) | **[Pending](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#function-pending)**(std::vector< [PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/) > deps ={}, std::optional< std::chrono::milliseconds > retry =std::nullopt) |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [Check](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#enum-check) | **[check](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#variable-check)**  |
| std::vector< [PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/) > | **[dependencies](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#variable-dependencies)**  |
| std::optional< std::chrono::milliseconds > | **[retry_after](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/#variable-retry_after)**  |

## Detailed Description

```cpp
struct sgns::ConsensusManager::ValidationResult;
```

Local structured validation result for subject handlers. 

Pending metadata is local bookkeeping only. It is not serialized, broadcast, or counted toward quorum. 

## Public Functions Documentation

### function ValidationResult

```cpp
ValidationResult() =default
```


### function ValidationResult

```cpp
inline ValidationResult(
    Check result
)
```


### function Approve

```cpp
static inline ValidationResult Approve()
```


### function Reject

```cpp
static inline ValidationResult Reject()
```


### function Stalled

```cpp
static inline ValidationResult Stalled()
```


### function Pending

```cpp
static inline ValidationResult Pending(
    std::vector< PendingDependencyKey > deps ={},
    std::optional< std::chrono::milliseconds > retry =std::nullopt
)
```


## Public Attributes Documentation

### variable check

```cpp
Check check { Check::Reject };
```


### variable dependencies

```cpp
std::vector< PendingDependencyKey > dependencies;
```


### variable retry_after

```cpp
std::optional< std::chrono::milliseconds > retry_after;
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
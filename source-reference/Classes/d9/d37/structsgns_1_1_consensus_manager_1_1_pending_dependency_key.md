---
title: sgns::ConsensusManager::PendingDependencyKey
summary: Local-only dependency key for deferred subject validation. 

---

# sgns::ConsensusManager::PendingDependencyKey



Local-only dependency key for deferred subject validation. 


`#include <Consensus.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[Type](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/#enum-type)** { Certificate} |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[operator==](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/#function-operator==)**(const [PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/) & other) const |
| [PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/) | **[Certificate](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/#function-certificate)**(std::string subject_hash) |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [Type](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/#enum-type) | **[type](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/#variable-type)**  |
| std::string | **[value](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/#variable-value)**  |

## Public Types Documentation

### enum Type

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| Certificate | | Waiting for a certificate by subject/transaction hash.   |




## Public Functions Documentation

### function operator==

```cpp
inline bool operator==(
    const PendingDependencyKey & other
) const
```


### function Certificate

```cpp
static inline PendingDependencyKey Certificate(
    std::string subject_hash
)
```


## Public Attributes Documentation

### variable type

```cpp
Type type { Type::Certificate };
```


### variable value

```cpp
std::string value;
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
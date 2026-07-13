---
title: sgns::ConsensusManager::PendingDependencyKeyHash
summary: Hash functor for PendingDependencyKey unordered containers. 

---

# sgns::ConsensusManager::PendingDependencyKeyHash



Hash functor for [PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/) unordered containers. 


`#include <Consensus.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::size_t | **[operator()](/source-reference/Classes/d3/dbe/structsgns_1_1_consensus_manager_1_1_pending_dependency_key_hash/#function-operator())**(const [PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/) & key) const |

## Public Functions Documentation

### function operator()

```cpp
inline std::size_t operator()(
    const PendingDependencyKey & key
) const
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
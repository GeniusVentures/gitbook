---
title: sgns::ConsensusManager::QuorumTally
summary: Quorum tally structure. 

---

# sgns::ConsensusManager::QuorumTally



Quorum tally structure. 


`#include <Consensus.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| uint64_t | **[total_weight](/source-reference/Classes/d1/dce/structsgns_1_1_consensus_manager_1_1_quorum_tally/#variable-total_weight)** <br/>The total maximum weight of the quorum.  |
| uint64_t | **[approved_weight](/source-reference/Classes/d1/dce/structsgns_1_1_consensus_manager_1_1_quorum_tally/#variable-approved_weight)** <br/>The weight which was already approved.  |
| bool | **[has_quorum](/source-reference/Classes/d1/dce/structsgns_1_1_consensus_manager_1_1_quorum_tally/#variable-has_quorum)** <br/>Flag indicating if quorum was reached.  |
| uint64_t | **[qualified_sum](/source-reference/Classes/d1/dce/structsgns_1_1_consensus_manager_1_1_quorum_tally/#variable-qualified_sum)** <br/>Slot-weighted qualified contribution.  |
| uint64_t | **[slot_threshold](/source-reference/Classes/d1/dce/structsgns_1_1_consensus_manager_1_1_quorum_tally/#variable-slot_threshold)** <br/>total_voting_reputation * 0.75 (D-06).  |

## Public Attributes Documentation

### variable total_weight

```cpp
uint64_t total_weight = 0;
```

The total maximum weight of the quorum. 

### variable approved_weight

```cpp
uint64_t approved_weight = 0;
```

The weight which was already approved. 

### variable has_quorum

```cpp
bool has_quorum = false;
```

Flag indicating if quorum was reached. 

### variable qualified_sum

```cpp
uint64_t qualified_sum = 0;
```

Slot-weighted qualified contribution. 

### variable slot_threshold

```cpp
uint64_t slot_threshold = 0;
```

total_voting_reputation * 0.75 (D-06). 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
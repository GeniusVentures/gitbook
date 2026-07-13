---
title: sgns::ValidatorRegistry::SlotQuorumResult
summary: Result of the Phase 6 cumulative slot-quorum tally (D-06). 

---

# sgns::ValidatorRegistry::SlotQuorumResult



Result of the Phase 6 cumulative slot-quorum tally (D-06).  [More...](#detailed-description)


`#include <ValidatorRegistry.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| uint64_t | **[qualified_sum](/source-reference/Classes/dd/d8c/structsgns_1_1_validator_registry_1_1_slot_quorum_result/#variable-qualified_sum)** <br/>Sum of slot-weighted contributions (D-06).  |
| uint64_t | **[total_voting_reputation](/source-reference/Classes/dd/d8c/structsgns_1_1_validator_registry_1_1_slot_quorum_result/#variable-total_voting_reputation)** <br/>Sum of weight of ALL approve voters.  |
| uint64_t | **[threshold](/source-reference/Classes/dd/d8c/structsgns_1_1_validator_registry_1_1_slot_quorum_result/#variable-threshold)** <br/>ceil(total * slot_quorum_numerator_ / slot_quorum_denominator_).  |
| bool | **[has_quorum](/source-reference/Classes/dd/d8c/structsgns_1_1_validator_registry_1_1_slot_quorum_result/#variable-has_quorum)** <br/>qualified_sum > threshold (STRICT, D-06).  |

## Detailed Description

```cpp
struct sgns::ValidatorRegistry::SlotQuorumResult;
```

Result of the Phase 6 cumulative slot-quorum tally (D-06). 

Deterministic across peers: computed ONLY from the vote vector and a registry snapshot (REQ-DETERM-01). No clocks, no local config, no node state is consulted. 

## Public Attributes Documentation

### variable qualified_sum

```cpp
uint64_t qualified_sum = 0;
```

Sum of slot-weighted contributions (D-06). 

### variable total_voting_reputation

```cpp
uint64_t total_voting_reputation = 0;
```

Sum of weight of ALL approve voters. 

### variable threshold

```cpp
uint64_t threshold = 0;
```

ceil(total * slot_quorum_numerator_ / slot_quorum_denominator_). 

### variable has_quorum

```cpp
bool has_quorum = false;
```

qualified_sum > threshold (STRICT, D-06). 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
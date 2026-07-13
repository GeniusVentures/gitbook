---
title: sgns::ConsensusManager::SlotState
summary: Runtime slot arbitration state. 

---

# sgns::ConsensusManager::SlotState



Runtime slot arbitration state. 

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::string | **[best_proposal_id](/source-reference/Classes/df/d49/structsgns_1_1_consensus_manager_1_1_slot_state/#variable-best_proposal_id)** <br/>Current best proposal id in the slot.  |
| std::string | **[best_tx_hash](/source-reference/Classes/df/d49/structsgns_1_1_consensus_manager_1_1_slot_state/#variable-best_tx_hash)** <br/>Hash used for deterministic tie-breaking.  |
| bool | **[voted](/source-reference/Classes/df/d49/structsgns_1_1_consensus_manager_1_1_slot_state/#variable-voted)** <br/>Whether local vote has already been cast for the slot.  |

## Public Attributes Documentation

### variable best_proposal_id

```cpp
std::string best_proposal_id;
```

Current best proposal id in the slot. 

### variable best_tx_hash

```cpp
std::string best_tx_hash;
```

Hash used for deterministic tie-breaking. 

### variable voted

```cpp
bool voted = false;
```

Whether local vote has already been cast for the slot. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
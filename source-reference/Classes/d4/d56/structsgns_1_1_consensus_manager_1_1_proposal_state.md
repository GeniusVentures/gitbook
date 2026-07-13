---
title: sgns::ConsensusManager::ProposalState
summary: Runtime state tracked for one proposal. 

---

# sgns::ConsensusManager::ProposalState



Runtime state tracked for one proposal. 

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) | **[proposal](/source-reference/Classes/d4/d56/structsgns_1_1_consensus_manager_1_1_proposal_state/#variable-proposal)** <br/>[Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) currently tracked.  |
| std::vector< [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) > | **[votes](/source-reference/Classes/d4/d56/structsgns_1_1_consensus_manager_1_1_proposal_state/#variable-votes)** <br/>Votes accepted for the proposal.  |
| std::string | **[slot_key](/source-reference/Classes/d4/d56/structsgns_1_1_consensus_manager_1_1_proposal_state/#variable-slot_key)** <br/>Slot key grouping competing proposals.  |
| uint64_t | **[total_weight](/source-reference/Classes/d4/d56/structsgns_1_1_consensus_manager_1_1_proposal_state/#variable-total_weight)** <br/>Total eligible weight for tally.  |
| uint64_t | **[approved_weight](/source-reference/Classes/d4/d56/structsgns_1_1_consensus_manager_1_1_proposal_state/#variable-approved_weight)** <br/>Approved weight accumulated so far.  |
| std::unordered_set< std::string > | **[seen_voters](/source-reference/Classes/d4/d56/structsgns_1_1_consensus_manager_1_1_proposal_state/#variable-seen_voters)** <br/>Voter ids already counted.  |
| bool | **[quorum_reached](/source-reference/Classes/d4/d56/structsgns_1_1_consensus_manager_1_1_proposal_state/#variable-quorum_reached)** <br/>Whether quorum has been reached.  |
| uint64_t | **[quorum_reached_ts_ms](/source-reference/Classes/d4/d56/structsgns_1_1_consensus_manager_1_1_proposal_state/#variable-quorum_reached_ts_ms)** <br/>Timestamp when quorum was reached.  |
| uint64_t | **[last_attempt_round](/source-reference/Classes/d4/d56/structsgns_1_1_consensus_manager_1_1_proposal_state/#variable-last_attempt_round)** <br/>Last certificate-attempt round.  |

## Public Attributes Documentation

### variable proposal

```cpp
Proposal proposal;
```

[Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) currently tracked. 

### variable votes

```cpp
std::vector< Vote > votes;
```

Votes accepted for the proposal. 

### variable slot_key

```cpp
std::string slot_key;
```

Slot key grouping competing proposals. 

### variable total_weight

```cpp
uint64_t total_weight = 0;
```

Total eligible weight for tally. 

### variable approved_weight

```cpp
uint64_t approved_weight = 0;
```

Approved weight accumulated so far. 

### variable seen_voters

```cpp
std::unordered_set< std::string > seen_voters;
```

Voter ids already counted. 

### variable quorum_reached

```cpp
bool quorum_reached = false;
```

Whether quorum has been reached. 

### variable quorum_reached_ts_ms

```cpp
uint64_t quorum_reached_ts_ms = 0;
```

Timestamp when quorum was reached. 

### variable last_attempt_round

```cpp
uint64_t last_attempt_round = NO_ROUND;
```

Last certificate-attempt round. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
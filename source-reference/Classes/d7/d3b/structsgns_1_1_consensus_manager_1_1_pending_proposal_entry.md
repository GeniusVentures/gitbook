---
title: sgns::ConsensusManager::PendingProposalEntry
summary: Canonical local pending proposal entry. 

---

# sgns::ConsensusManager::PendingProposalEntry



Canonical local pending proposal entry. 

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) | **[proposal](/source-reference/Classes/d7/d3b/structsgns_1_1_consensus_manager_1_1_pending_proposal_entry/#variable-proposal)**  |
| std::vector< [PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/) > | **[dependencies](/source-reference/Classes/d7/d3b/structsgns_1_1_consensus_manager_1_1_pending_proposal_entry/#variable-dependencies)**  |
| std::chrono::steady_clock::time_point | **[admitted_at](/source-reference/Classes/d7/d3b/structsgns_1_1_consensus_manager_1_1_pending_proposal_entry/#variable-admitted_at)**  |
| std::chrono::steady_clock::time_point | **[expires_at](/source-reference/Classes/d7/d3b/structsgns_1_1_consensus_manager_1_1_pending_proposal_entry/#variable-expires_at)**  |
| std::chrono::steady_clock::time_point | **[next_retry_at](/source-reference/Classes/d7/d3b/structsgns_1_1_consensus_manager_1_1_pending_proposal_entry/#variable-next_retry_at)**  |
| std::chrono::steady_clock::time_point | **[last_retry_at](/source-reference/Classes/d7/d3b/structsgns_1_1_consensus_manager_1_1_pending_proposal_entry/#variable-last_retry_at)**  |
| std::optional< std::chrono::milliseconds > | **[retry_after](/source-reference/Classes/d7/d3b/structsgns_1_1_consensus_manager_1_1_pending_proposal_entry/#variable-retry_after)**  |
| std::size_t | **[retained_bytes](/source-reference/Classes/d7/d3b/structsgns_1_1_consensus_manager_1_1_pending_proposal_entry/#variable-retained_bytes)**  |
| std::string | **[proposer_id](/source-reference/Classes/d7/d3b/structsgns_1_1_consensus_manager_1_1_pending_proposal_entry/#variable-proposer_id)**  |
| std::size_t | **[scheduled_retry_count](/source-reference/Classes/d7/d3b/structsgns_1_1_consensus_manager_1_1_pending_proposal_entry/#variable-scheduled_retry_count)**  |

## Public Attributes Documentation

### variable proposal

```cpp
Proposal proposal;
```


### variable dependencies

```cpp
std::vector< PendingDependencyKey > dependencies;
```


### variable admitted_at

```cpp
std::chrono::steady_clock::time_point admitted_at;
```


### variable expires_at

```cpp
std::chrono::steady_clock::time_point expires_at;
```


### variable next_retry_at

```cpp
std::chrono::steady_clock::time_point next_retry_at;
```


### variable last_retry_at

```cpp
std::chrono::steady_clock::time_point last_retry_at;
```


### variable retry_after

```cpp
std::optional< std::chrono::milliseconds > retry_after;
```


### variable retained_bytes

```cpp
std::size_t retained_bytes = 0;
```


### variable proposer_id

```cpp
std::string proposer_id;
```


### variable scheduled_retry_count

```cpp
std::size_t scheduled_retry_count = 0;
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
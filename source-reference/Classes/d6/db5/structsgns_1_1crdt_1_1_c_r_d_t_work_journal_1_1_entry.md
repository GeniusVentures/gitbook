---
title: sgns::crdt::CRDTWorkJournal::Entry
summary: Serialized work-journal entry for a key. 

---

# sgns::crdt::CRDTWorkJournal::Entry



Serialized work-journal entry for a key. 


`#include <crdt_work_journal.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::string | **[key](/source-reference/Classes/d6/db5/structsgns_1_1crdt_1_1_c_r_d_t_work_journal_1_1_entry/#variable-key)** <br/>Logical key being tracked.  |
| [State](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/#enum-state) | **[state](/source-reference/Classes/d6/db5/structsgns_1_1crdt_1_1_c_r_d_t_work_journal_1_1_entry/#variable-state)** <br/>Current processing state.  |
| uint64_t | **[attempt_count](/source-reference/Classes/d6/db5/structsgns_1_1crdt_1_1_c_r_d_t_work_journal_1_1_entry/#variable-attempt_count)** <br/>Number of processing/stall transitions.  |
| uint64_t | **[updated_at_ms](/source-reference/Classes/d6/db5/structsgns_1_1crdt_1_1_c_r_d_t_work_journal_1_1_entry/#variable-updated_at_ms)** <br/>Last update time in Unix milliseconds.  |
| uint64_t | **[lease_until_ms](/source-reference/Classes/d6/db5/structsgns_1_1crdt_1_1_c_r_d_t_work_journal_1_1_entry/#variable-lease_until_ms)** <br/>Processing lease deadline in Unix milliseconds.  |

## Public Attributes Documentation

### variable key

```cpp
std::string key;
```

Logical key being tracked. 

### variable state

```cpp
State state = State::Seen;
```

Current processing state. 

### variable attempt_count

```cpp
uint64_t attempt_count = 0;
```

Number of processing/stall transitions. 

### variable updated_at_ms

```cpp
uint64_t updated_at_ms = 0;
```

Last update time in Unix milliseconds. 

### variable lease_until_ms

```cpp
uint64_t lease_until_ms = 0;
```

Processing lease deadline in Unix milliseconds. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
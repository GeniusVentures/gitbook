---
title: sgns::crdt::CRDTWorkJournal
summary: Tracks key processing lifecycle persisted in RocksDB. 

---

# sgns::crdt::CRDTWorkJournal



Tracks key processing lifecycle persisted in RocksDB.  [More...](#detailed-description)


`#include <crdt_work_journal.hpp>`

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[Entry](/source-reference/Classes/d6/db5/structsgns_1_1crdt_1_1_c_r_d_t_work_journal_1_1_entry/)** <br/>Serialized work-journal entry for a key.  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class uint8_t | **[State](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/#enum-state)** { Seen = 0, Processing = 1, Stalled = 2}<br/>Processing state for a tracked key.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [CRDTWorkJournal](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/#function-crdtworkjournal) > | **[New](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/#function-new)**(std::shared_ptr< [storage::rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/) > datastore)<br/>Creates a work journal backed by RocksDB.  |
| void | **[MarkSeen](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/#function-markseen)**(const std::string & key)<br/>Marks a key as seen and pending processing.  |
| void | **[MarkProcessing](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/#function-markprocessing)**(const std::string & key, std::chrono::milliseconds lease =std::chrono::minutes(3))<br/>Marks an existing key as processing with a lease.  |
| void | **[MarkStalled](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/#function-markstalled)**(const std::string & key, std::chrono::milliseconds lease =std::chrono::minutes(3))<br/>Marks an existing key as stalled with a lease.  |
| bool | **[MarkDone](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/#function-markdone)**(const std::string & key)<br/>Removes a key from the journal.  |
| std::optional< [Entry](/source-reference/Classes/d6/db5/structsgns_1_1crdt_1_1_c_r_d_t_work_journal_1_1_entry/) > | **[GetEntry](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/#function-getentry)**(const std::string & key) const<br/>Retrieves one entry by logical key.  |
| std::vector< [Entry](/source-reference/Classes/d6/db5/structsgns_1_1crdt_1_1_c_r_d_t_work_journal_1_1_entry/) > | **[ListUnfinished](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/#function-listunfinished)**(std::string_view key_pattern ={}) const<br/>Lists all unfinished entries, optionally filtered by key regex.  |
| size_t | **[RecoverStaleProcessing](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/#function-recoverstaleprocessing)**(std::string_view key_pattern, std::chrono::milliseconds stale =std::chrono::milliseconds(0))<br/>Converts stale processing entries to stalled.  |

## Detailed Description

```cpp
class sgns::crdt::CRDTWorkJournal;
```

Tracks key processing lifecycle persisted in RocksDB. 

Entries are stored under the internal work namespace and can be recovered across process restarts. 

## Public Types Documentation

### enum State

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| Seen | 0| Key was discovered and is pending work.   |
| Processing | 1| Key is currently being processed.   |
| Stalled | 2| Key processing stalled and requires retry.   |



Processing state for a tracked key. 

## Public Functions Documentation

### function New

```cpp
static std::shared_ptr< CRDTWorkJournal > New(
    std::shared_ptr< storage::rocksdb > datastore
)
```

Creates a work journal backed by RocksDB. 

**Parameters**: 

  * **datastore** RocksDB instance used to persist entries. 


**Return**: Shared pointer to a new journal, or `nullptr` when datastore is null. 

### function MarkSeen

```cpp
void MarkSeen(
    const std::string & key
)
```

Marks a key as seen and pending processing. 

**Parameters**: 

  * **key** Logical key to track. 


### function MarkProcessing

```cpp
void MarkProcessing(
    const std::string & key,
    std::chrono::milliseconds lease =std::chrono::minutes(3)
)
```

Marks an existing key as processing with a lease. 

**Parameters**: 

  * **key** Logical key to update. 
  * **lease** Processing lease duration. Negative values are treated as zero. 


### function MarkStalled

```cpp
void MarkStalled(
    const std::string & key,
    std::chrono::milliseconds lease =std::chrono::minutes(3)
)
```

Marks an existing key as stalled with a lease. 

**Parameters**: 

  * **key** Logical key to update. 
  * **lease** Stall lease duration. Negative values are treated as zero. 


### function MarkDone

```cpp
bool MarkDone(
    const std::string & key
)
```

Removes a key from the journal. 

**Parameters**: 

  * **key** Logical key to remove. 


**Return**: `true` when deletion succeeds, otherwise `false`. 

### function GetEntry

```cpp
std::optional< Entry > GetEntry(
    const std::string & key
) const
```

Retrieves one entry by logical key. 

**Parameters**: 

  * **key** Logical key to fetch. 


**Return**: Journal entry when present and parseable, otherwise `std::nullopt`. 

### function ListUnfinished

```cpp
std::vector< Entry > ListUnfinished(
    std::string_view key_pattern ={}
) const
```

Lists all unfinished entries, optionally filtered by key regex. 

**Parameters**: 

  * **key_pattern** Optional regex applied to logical keys. 


**Return**: Vector with all matching unfinished entries. 

### function RecoverStaleProcessing

```cpp
size_t RecoverStaleProcessing(
    std::string_view key_pattern,
    std::chrono::milliseconds stale =std::chrono::milliseconds(0)
)
```

Converts stale processing entries to stalled. 

**Parameters**: 

  * **key_pattern** Regex to limit keys considered for recovery. 
  * **stale** Extra grace period in milliseconds before recovery. 


**Return**: Number of recovered entries. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: sgns::crdt::GlobalDB::BackupOptions

---

# sgns::crdt::GlobalDB::BackupOptions






`#include <globaldb.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| bool | **[enabled](/source-reference/Classes/d3/d2a/structsgns_1_1crdt_1_1_global_d_b_1_1_backup_options/#variable-enabled)**  |
| uint32_t | **[interval_minutes](/source-reference/Classes/d3/d2a/structsgns_1_1crdt_1_1_global_d_b_1_1_backup_options/#variable-interval_minutes)**  |
| uint32_t | **[keep_count](/source-reference/Classes/d3/d2a/structsgns_1_1crdt_1_1_global_d_b_1_1_backup_options/#variable-keep_count)**  |
| bool | **[auto_restore_on_repair_failure](/source-reference/Classes/d3/d2a/structsgns_1_1crdt_1_1_global_d_b_1_1_backup_options/#variable-auto_restore_on_repair_failure)**  |

## Public Attributes Documentation

### variable enabled

```cpp
bool enabled { false };
```


### variable interval_minutes

```cpp
uint32_t interval_minutes { 15 };
```


### variable keep_count

```cpp
uint32_t keep_count { 12 };
```


### variable auto_restore_on_repair_failure

```cpp
bool auto_restore_on_repair_failure { true };
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
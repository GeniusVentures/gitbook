---
title: sgns::storage::face::WriteBatch
summary: An abstraction over a storage, which can be used for batch writes. 

---

# sgns::storage::face::WriteBatch



An abstraction over a storage, which can be used for batch writes.  [More...](#detailed-description)


`#include <write_batch.hpp>`

Inherits from [sgns::storage::face::Writeable< K, V >](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual outcome::result< void > | **[commit](/source-reference/Classes/d9/d69/structsgns_1_1storage_1_1face_1_1_write_batch/#function-commit)**() =0<br/>Writes batch.  |
| virtual void | **[clear](/source-reference/Classes/d9/d69/structsgns_1_1storage_1_1face_1_1_write_batch/#function-clear)**() =0<br/>Clear batch.  |

## Additional inherited members

**Public Functions inherited from [sgns::storage::face::Writeable< K, V >](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Writeable](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-~writeable)**() =default |
| virtual outcome::result< void > | **[put](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-put)**(const K & key, const V & value) =0<br/>Store value by key.  |
| virtual outcome::result< void > | **[put](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-put)**(const K & key, V && value) =0 |
| virtual outcome::result< void > | **[remove](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-remove)**(const K & key) =0<br/>Remove value by key.  |


## Detailed Description

```cpp
template <typename K ,
typename V >
struct sgns::storage::face::WriteBatch;
```

An abstraction over a storage, which can be used for batch writes. 

**Template Parameters**: 

  * **K** key type 
  * **V** value type 

## Public Functions Documentation

### function commit

```cpp
virtual outcome::result< void > commit() =0
```

Writes batch. 

**Return**: error code in case of error. 

**Reimplemented by**: [sgns::storage::rocksdb::Batch::commit](/source-reference/Classes/d8/d2c/classsgns_1_1storage_1_1rocksdb_1_1_batch/#function-commit)


### function clear

```cpp
virtual void clear() =0
```

Clear batch. 

**Reimplemented by**: [sgns::storage::rocksdb::Batch::clear](/source-reference/Classes/d8/d2c/classsgns_1_1storage_1_1rocksdb_1_1_batch/#function-clear)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
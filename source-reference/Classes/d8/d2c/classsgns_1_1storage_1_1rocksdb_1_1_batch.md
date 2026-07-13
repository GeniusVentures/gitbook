---
title: sgns::storage::rocksdb::Batch
summary: Class that is used to implement efficient bulk (batch) modifications of the Map. 

---

# sgns::storage::rocksdb::Batch



Class that is used to implement efficient bulk (batch) modifications of the Map. 


`#include <rocksdb_batch.hpp>`

Inherits from [sgns::storage::face::WriteBatch< Buffer, Buffer >](/source-reference/Classes/d9/d69/structsgns_1_1storage_1_1face_1_1_write_batch/), [sgns::storage::face::Writeable< K, V >](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[Batch](/source-reference/Classes/d8/d2c/classsgns_1_1storage_1_1rocksdb_1_1_batch/#function-batch)**([rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/) & db) |
| outcome::result< void > | **[put](/source-reference/Classes/d8/d2c/classsgns_1_1storage_1_1rocksdb_1_1_batch/#function-put)**(const [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) & key, const [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) & value) override |
| outcome::result< void > | **[put](/source-reference/Classes/d8/d2c/classsgns_1_1storage_1_1rocksdb_1_1_batch/#function-put)**(const [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) & key, [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) && value) override |
| outcome::result< void > | **[remove](/source-reference/Classes/d8/d2c/classsgns_1_1storage_1_1rocksdb_1_1_batch/#function-remove)**(const [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) & key) override |
| virtual outcome::result< void > | **[commit](/source-reference/Classes/d8/d2c/classsgns_1_1storage_1_1rocksdb_1_1_batch/#function-commit)**() override<br/>Writes batch.  |
| virtual void | **[clear](/source-reference/Classes/d8/d2c/classsgns_1_1storage_1_1rocksdb_1_1_batch/#function-clear)**() override<br/>Clear batch.  |

## Additional inherited members

**Public Functions inherited from [sgns::storage::face::Writeable< K, V >](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Writeable](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-~writeable)**() =default |


## Public Functions Documentation

### function Batch

```cpp
explicit Batch(
    rocksdb & db
)
```


### function put

```cpp
outcome::result< void > put(
    const Buffer & key,
    const Buffer & value
) override
```


### function put

```cpp
outcome::result< void > put(
    const Buffer & key,
    Buffer && value
) override
```


### function remove

```cpp
outcome::result< void > remove(
    const Buffer & key
) override
```


### function commit

```cpp
virtual outcome::result< void > commit() override
```

Writes batch. 

**Return**: error code in case of error. 

**Reimplements**: [sgns::storage::face::WriteBatch::commit](/source-reference/Classes/d9/d69/structsgns_1_1storage_1_1face_1_1_write_batch/#function-commit)


### function clear

```cpp
virtual void clear() override
```

Clear batch. 

**Reimplements**: [sgns::storage::face::WriteBatch::clear](/source-reference/Classes/d9/d69/structsgns_1_1storage_1_1face_1_1_write_batch/#function-clear)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
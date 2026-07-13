---
title: sgns::storage::face::Batchable
summary: A mixin for a map that supports batching for efficiency of modifications. 

---

# sgns::storage::face::Batchable



A mixin for a map that supports batching for efficiency of modifications.  [More...](#detailed-description)


`#include <batchable.hpp>`

Inherited by [sgns::storage::face::BatchWriteMap< Buffer, Buffer >](/source-reference/Classes/d3/df4/structsgns_1_1storage_1_1face_1_1_batch_write_map/), [sgns::storage::face::BatchWriteMap< K, V >](/source-reference/Classes/d3/df4/structsgns_1_1storage_1_1face_1_1_batch_write_map/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Batchable](/source-reference/Classes/de/d2d/structsgns_1_1storage_1_1face_1_1_batchable/#function-~batchable)**() =default |
| virtual std::unique_ptr< [WriteBatch](/source-reference/Classes/d9/d69/structsgns_1_1storage_1_1face_1_1_write_batch/)< K, V > > | **[batch](/source-reference/Classes/de/d2d/structsgns_1_1storage_1_1face_1_1_batchable/#function-batch)**() =0<br/>Creates new Write Batch - an object, which can be used to efficiently write bulk data.  |

## Detailed Description

```cpp
template <typename K ,
typename V >
struct sgns::storage::face::Batchable;
```

A mixin for a map that supports batching for efficiency of modifications. 

**Template Parameters**: 

  * **K** key type 
  * **V** value type 

## Public Functions Documentation

### function ~Batchable

```cpp
virtual ~Batchable() =default
```


### function batch

```cpp
virtual std::unique_ptr< WriteBatch< K, V > > batch() =0
```

Creates new Write Batch - an object, which can be used to efficiently write bulk data. 

**Reimplemented by**: [sgns::storage::rocksdb::batch](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-batch)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
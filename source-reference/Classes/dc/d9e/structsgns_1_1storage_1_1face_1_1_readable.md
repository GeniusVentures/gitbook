---
title: sgns::storage::face::Readable
summary: A mixin for read-only map. 

---

# sgns::storage::face::Readable



A mixin for read-only map.  [More...](#detailed-description)


`#include <readable.hpp>`

Inherited by [sgns::storage::face::ReadOnlyMap< Buffer, Buffer >](/source-reference/Classes/d6/d8f/structsgns_1_1storage_1_1face_1_1_read_only_map/), [sgns::storage::face::ReadOnlyMap< K, V >](/source-reference/Classes/d6/d8f/structsgns_1_1storage_1_1face_1_1_read_only_map/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Readable](/source-reference/Classes/dc/d9e/structsgns_1_1storage_1_1face_1_1_readable/#function-~readable)**() =default |
| virtual outcome::result< V > | **[get](/source-reference/Classes/dc/d9e/structsgns_1_1storage_1_1face_1_1_readable/#function-get)**(const K & key) const =0<br/>Get value by key.  |
| virtual bool | **[contains](/source-reference/Classes/dc/d9e/structsgns_1_1storage_1_1face_1_1_readable/#function-contains)**(const K & key) const =0<br/>Returns true if given key-value binding exists in the storage.  |
| virtual bool | **[empty](/source-reference/Classes/dc/d9e/structsgns_1_1storage_1_1face_1_1_readable/#function-empty)**() const =0<br/>Returns true if the storage is empty.  |

## Detailed Description

```cpp
template <typename K ,
typename V >
struct sgns::storage::face::Readable;
```

A mixin for read-only map. 

**Template Parameters**: 

  * **K** key type 
  * **V** value type 

## Public Functions Documentation

### function ~Readable

```cpp
virtual ~Readable() =default
```


### function get

```cpp
virtual outcome::result< V > get(
    const K & key
) const =0
```

Get value by key. 

**Parameters**: 

  * **key** K 


**Return**: V 

### function contains

```cpp
virtual bool contains(
    const K & key
) const =0
```

Returns true if given key-value binding exists in the storage. 

**Parameters**: 

  * **key** K 


**Return**: true if key has value, false otherwise. 

### function empty

```cpp
virtual bool empty() const =0
```

Returns true if the storage is empty. 

**Reimplemented by**: [sgns::storage::rocksdb::empty](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-empty)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
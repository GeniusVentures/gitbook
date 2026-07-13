---
title: sgns::storage::face::Iterable
summary: A mixin for an iterable map. 

---

# sgns::storage::face::Iterable



A mixin for an iterable map.  [More...](#detailed-description)


`#include <iterable.hpp>`

Inherited by [sgns::storage::face::ReadOnlyMap< Buffer, Buffer >](/source-reference/Classes/d6/d8f/structsgns_1_1storage_1_1face_1_1_read_only_map/), [sgns::storage::face::ReadOnlyMap< K, V >](/source-reference/Classes/d6/d8f/structsgns_1_1storage_1_1face_1_1_read_only_map/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Iterable](/source-reference/Classes/d4/d27/structsgns_1_1storage_1_1face_1_1_iterable/#function-~iterable)**() =default |
| virtual std::unique_ptr< [MapCursor](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/)< K, V > > | **[cursor](/source-reference/Classes/d4/d27/structsgns_1_1storage_1_1face_1_1_iterable/#function-cursor)**() =0<br/>Returns new key-value iterator.  |

## Detailed Description

```cpp
template <typename K ,
typename V >
struct sgns::storage::face::Iterable;
```

A mixin for an iterable map. 

**Template Parameters**: 

  * **K** key type 
  * **V** value type 

## Public Functions Documentation

### function ~Iterable

```cpp
virtual ~Iterable() =default
```


### function cursor

```cpp
virtual std::unique_ptr< MapCursor< K, V > > cursor() =0
```

Returns new key-value iterator. 

**Return**: kv iterator 

**Reimplemented by**: [sgns::storage::rocksdb::cursor](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-cursor)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: sgns::storage::face::GenericMap
summary: An abstraction over a readable, writeable, iterable key-value map. 

---

# sgns::storage::face::GenericMap



An abstraction over a readable, writeable, iterable key-value map.  [More...](#detailed-description)


`#include <generic_maps.hpp>`

Inherits from [sgns::storage::face::ReadOnlyMap< K, V >](/source-reference/Classes/d6/d8f/structsgns_1_1storage_1_1face_1_1_read_only_map/), [sgns::storage::face::Writeable< K, V >](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/), [sgns::storage::face::Iterable< K, V >](/source-reference/Classes/d4/d27/structsgns_1_1storage_1_1face_1_1_iterable/), [sgns::storage::face::Readable< K, V >](/source-reference/Classes/dc/d9e/structsgns_1_1storage_1_1face_1_1_readable/)

## Additional inherited members

**Public Functions inherited from [sgns::storage::face::Writeable< K, V >](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Writeable](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-~writeable)**() =default |
| virtual outcome::result< void > | **[put](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-put)**(const K & key, const V & value) =0<br/>Store value by key.  |
| virtual outcome::result< void > | **[put](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-put)**(const K & key, V && value) =0 |
| virtual outcome::result< void > | **[remove](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-remove)**(const K & key) =0<br/>Remove value by key.  |

**Public Functions inherited from [sgns::storage::face::Iterable< K, V >](/source-reference/Classes/d4/d27/structsgns_1_1storage_1_1face_1_1_iterable/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Iterable](/source-reference/Classes/d4/d27/structsgns_1_1storage_1_1face_1_1_iterable/#function-~iterable)**() =default |
| virtual std::unique_ptr< [MapCursor](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/)< K, V > > | **[cursor](/source-reference/Classes/d4/d27/structsgns_1_1storage_1_1face_1_1_iterable/#function-cursor)**() =0<br/>Returns new key-value iterator.  |

**Public Functions inherited from [sgns::storage::face::Readable< K, V >](/source-reference/Classes/dc/d9e/structsgns_1_1storage_1_1face_1_1_readable/)**

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
struct sgns::storage::face::GenericMap;
```

An abstraction over a readable, writeable, iterable key-value map. 

**Template Parameters**: 

  * **K** key type 
  * **V** value type 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
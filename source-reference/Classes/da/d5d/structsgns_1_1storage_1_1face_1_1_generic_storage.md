---
title: sgns::storage::face::GenericStorage
summary: An abstraction over readable, writeable, iterable key-value storage that supports write batches. 

---

# sgns::storage::face::GenericStorage



An abstraction over readable, writeable, iterable key-value storage that supports write batches.  [More...](#detailed-description)


`#include <generic_storage.hpp>`

Inherits from [sgns::storage::face::ReadOnlyMap< K, V >](/source-reference/Classes/d6/d8f/structsgns_1_1storage_1_1face_1_1_read_only_map/), [sgns::storage::face::BatchWriteMap< K, V >](/source-reference/Classes/d3/df4/structsgns_1_1storage_1_1face_1_1_batch_write_map/), [IComponent](/source-reference/Classes/d1/dbf/class_i_component/), [sgns::storage::face::Iterable< K, V >](/source-reference/Classes/d4/d27/structsgns_1_1storage_1_1face_1_1_iterable/), [sgns::storage::face::Readable< K, V >](/source-reference/Classes/dc/d9e/structsgns_1_1storage_1_1face_1_1_readable/), [sgns::storage::face::Writeable< K, V >](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/), [sgns::storage::face::Batchable< K, V >](/source-reference/Classes/de/d2d/structsgns_1_1storage_1_1face_1_1_batchable/)

## Additional inherited members

**Public Functions inherited from [IComponent](/source-reference/Classes/d1/dbf/class_i_component/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IComponent](/source-reference/Classes/d1/dbf/class_i_component/#function-~icomponent)**() =default |
| virtual std::string | **[GetName](/source-reference/Classes/d1/dbf/class_i_component/#function-getname)**() =0 |

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

**Public Functions inherited from [sgns::storage::face::Writeable< K, V >](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Writeable](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-~writeable)**() =default |
| virtual outcome::result< void > | **[put](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-put)**(const K & key, const V & value) =0<br/>Store value by key.  |
| virtual outcome::result< void > | **[put](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-put)**(const K & key, V && value) =0 |
| virtual outcome::result< void > | **[remove](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-remove)**(const K & key) =0<br/>Remove value by key.  |

**Public Functions inherited from [sgns::storage::face::Batchable< K, V >](/source-reference/Classes/de/d2d/structsgns_1_1storage_1_1face_1_1_batchable/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Batchable](/source-reference/Classes/de/d2d/structsgns_1_1storage_1_1face_1_1_batchable/#function-~batchable)**() =default |
| virtual std::unique_ptr< [WriteBatch](/source-reference/Classes/d9/d69/structsgns_1_1storage_1_1face_1_1_write_batch/)< K, V > > | **[batch](/source-reference/Classes/de/d2d/structsgns_1_1storage_1_1face_1_1_batchable/#function-batch)**() =0<br/>Creates new Write Batch - an object, which can be used to efficiently write bulk data.  |


## Detailed Description

```cpp
template <typename K ,
typename V >
struct sgns::storage::face::GenericStorage;
```

An abstraction over readable, writeable, iterable key-value storage that supports write batches. 

**Template Parameters**: 

  * **K** key type 
  * **V** value type 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
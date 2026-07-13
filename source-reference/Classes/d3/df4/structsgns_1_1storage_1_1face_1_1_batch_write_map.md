---
title: sgns::storage::face::BatchWriteMap
summary: An abstraction over a writeable key-value map with batching support. 

---

# sgns::storage::face::BatchWriteMap



An abstraction over a writeable key-value map with batching support.  [More...](#detailed-description)


`#include <generic_maps.hpp>`

Inherits from [sgns::storage::face::Writeable< K, V >](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/), [sgns::storage::face::Batchable< K, V >](/source-reference/Classes/de/d2d/structsgns_1_1storage_1_1face_1_1_batchable/)

Inherited by [sgns::storage::face::GenericStorage< K, V >](/source-reference/Classes/da/d5d/structsgns_1_1storage_1_1face_1_1_generic_storage/)

## Additional inherited members

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
struct sgns::storage::face::BatchWriteMap;
```

An abstraction over a writeable key-value map with batching support. 

**Template Parameters**: 

  * **K** key type 
  * **V** value type 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
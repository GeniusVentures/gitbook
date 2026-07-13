---
title: sgns::storage::face::Writeable
summary: An mixin for modifiable map. 

---

# sgns::storage::face::Writeable



An mixin for modifiable map.  [More...](#detailed-description)


`#include <writeable.hpp>`

Inherited by [sgns::storage::face::BatchWriteMap< Buffer, Buffer >](/source-reference/Classes/d3/df4/structsgns_1_1storage_1_1face_1_1_batch_write_map/), [sgns::storage::face::GenericMap< Buffer, Buffer >](/source-reference/Classes/d4/d01/structsgns_1_1storage_1_1face_1_1_generic_map/), [sgns::storage::face::WriteBatch< Buffer, Buffer >](/source-reference/Classes/d9/d69/structsgns_1_1storage_1_1face_1_1_write_batch/), [sgns::storage::face::BatchWriteMap< K, V >](/source-reference/Classes/d3/df4/structsgns_1_1storage_1_1face_1_1_batch_write_map/), [sgns::storage::face::GenericMap< K, V >](/source-reference/Classes/d4/d01/structsgns_1_1storage_1_1face_1_1_generic_map/), [sgns::storage::face::WriteBatch< K, V >](/source-reference/Classes/d9/d69/structsgns_1_1storage_1_1face_1_1_write_batch/)

## Public Functions

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
struct sgns::storage::face::Writeable;
```

An mixin for modifiable map. 

**Template Parameters**: 

  * **K** key type 
  * **V** value type 

## Public Functions Documentation

### function ~Writeable

```cpp
virtual ~Writeable() =default
```


### function put

```cpp
virtual outcome::result< void > put(
    const K & key,
    const V & value
) =0
```

Store value by key. 

**Parameters**: 

  * **key** key 
  * **value** value 


**Return**: result containing void if put successful, error otherwise 

### function put

```cpp
virtual outcome::result< void > put(
    const K & key,
    V && value
) =0
```


### function remove

```cpp
virtual outcome::result< void > remove(
    const K & key
) =0
```

Remove value by key. 

**Parameters**: 

  * **key** K 


**Return**: error code if error happened 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
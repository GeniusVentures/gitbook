---
title: sgns::OutPointHash
summary: Hash functor for using OutPoint keys in unordered containers. 

---

# sgns::OutPointHash



Hash functor for using [OutPoint](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/) keys in unordered containers. 


`#include <UTXOManager.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| size_t | **[operator()](/source-reference/Classes/d5/d40/structsgns_1_1_out_point_hash/#function-operator())**(const [OutPoint](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/) & outpoint) const<br/>Computes a combined hash for a transaction id and output index pair.  |

## Public Functions Documentation

### function operator()

```cpp
inline size_t operator()(
    const OutPoint & outpoint
) const
```

Computes a combined hash for a transaction id and output index pair. 

**Parameters**: 

  * **outpoint** The [OutPoint](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/) to hash, containing a transaction id and output index. 


**Return**: Size of the combined hash 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/generic_storage.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/generic_storage.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |
| **[sgns::storage::face](/source-reference/Namespaces/df/d29/namespacesgns_1_1storage_1_1face/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::storage::face::GenericStorage](/source-reference/Classes/da/d5d/structsgns_1_1storage_1_1face_1_1_generic_storage/)** <br/>An abstraction over readable, writeable, iterable key-value storage that supports write batches.  |




## Source code

```cpp
#ifndef SUPERGENIUS_GENERIC_STORAGE_HPP
#define SUPERGENIUS_GENERIC_STORAGE_HPP

#include "storage/face/generic_maps.hpp"
#include "singleton/IComponent.hpp"

namespace sgns::storage::face {

  template <typename K, typename V>
  struct GenericStorage : public ReadOnlyMap<K, V>,
                          public BatchWriteMap<K, V>,
                          public IComponent {};  

}  // namespace sgns::storage::face

#endif  // SUPERGENIUS_GENERIC_STORAGE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

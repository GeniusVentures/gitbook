---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/generic_maps.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/generic_maps.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |
| **[sgns::storage::face](/source-reference/Namespaces/df/d29/namespacesgns_1_1storage_1_1face/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::storage::face::ReadOnlyMap](/source-reference/Classes/d6/d8f/structsgns_1_1storage_1_1face_1_1_read_only_map/)** <br/>An abstraction over a readable and iterable key-value map.  |
| struct | **[sgns::storage::face::GenericMap](/source-reference/Classes/d4/d01/structsgns_1_1storage_1_1face_1_1_generic_map/)** <br/>An abstraction over a readable, writeable, iterable key-value map.  |
| struct | **[sgns::storage::face::BatchWriteMap](/source-reference/Classes/d3/df4/structsgns_1_1storage_1_1face_1_1_batch_write_map/)** <br/>An abstraction over a writeable key-value map with batching support.  |




## Source code

```cpp
#ifndef SUPERGENIUS_GENERIC_MAPS_HPP
#define SUPERGENIUS_GENERIC_MAPS_HPP

#include "storage/face/batchable.hpp"
#include "storage/face/iterable.hpp"
#include "storage/face/readable.hpp"
#include "storage/face/writeable.hpp"

namespace sgns::storage::face {

  template <typename K, typename V>
  struct ReadOnlyMap : public Iterable<K, V>, public Readable<K, V> {};

  template <typename K, typename V>
  struct GenericMap : public ReadOnlyMap<K, V>, public Writeable<K, V> {};

  template <typename K, typename V>
  struct BatchWriteMap : public Writeable<K, V>, public Batchable<K, V> {};
}  // namespace sgns::storage::face

#endif  // SUPERGENIUS_GENERIC_MAPS_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/iterable.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/iterable.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |
| **[sgns::storage::face](/source-reference/Namespaces/df/d29/namespacesgns_1_1storage_1_1face/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::storage::face::Iterable](/source-reference/Classes/d4/d27/structsgns_1_1storage_1_1face_1_1_iterable/)** <br/>A mixin for an iterable map.  |




## Source code

```cpp
#ifndef SUPERGENIUS_ITERABLE_HPP
#define SUPERGENIUS_ITERABLE_HPP

#include <memory>

#include "storage/face/map_cursor.hpp"

namespace sgns::storage::face {

  template <typename K, typename V>
  struct Iterable {
    virtual ~Iterable() = default;

    virtual std::unique_ptr<MapCursor<K, V>> cursor() = 0;
  };

}  // namespace sgns::storage::face

#endif  // SUPERGENIUS_ITERABLE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

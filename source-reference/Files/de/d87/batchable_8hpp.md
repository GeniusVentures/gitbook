---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/batchable.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/batchable.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |
| **[sgns::storage::face](/source-reference/Namespaces/df/d29/namespacesgns_1_1storage_1_1face/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::storage::face::Batchable](/source-reference/Classes/de/d2d/structsgns_1_1storage_1_1face_1_1_batchable/)** <br/>A mixin for a map that supports batching for efficiency of modifications.  |




## Source code

```cpp
#ifndef SUPERGENIUS_BATCHABLE_HPP
#define SUPERGENIUS_BATCHABLE_HPP

#include <memory>

#include "storage/face/write_batch.hpp"

namespace sgns::storage::face {

  template <typename K, typename V>
  struct Batchable {
    virtual ~Batchable() = default;

    virtual std::unique_ptr<WriteBatch<K, V>> batch() = 0;
  };

}  // namespace sgns::storage::face

#endif  // SUPERGENIUS_BATCHABLE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

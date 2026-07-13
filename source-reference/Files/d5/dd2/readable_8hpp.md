---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/readable.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/readable.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |
| **[sgns::storage::face](/source-reference/Namespaces/df/d29/namespacesgns_1_1storage_1_1face/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::storage::face::Readable](/source-reference/Classes/dc/d9e/structsgns_1_1storage_1_1face_1_1_readable/)** <br/>A mixin for read-only map.  |




## Source code

```cpp
#ifndef SUPERGENIUS_READABLE_HPP
#define SUPERGENIUS_READABLE_HPP

#include "outcome/outcome.hpp"

namespace sgns::storage::face {

  template <typename K, typename V>
  struct Readable {
    virtual ~Readable() = default;

    virtual outcome::result<V> get(const K &key) const = 0;

    virtual bool contains(const K &key) const = 0;

    virtual bool empty() const = 0;
  };

}  // namespace sgns::storage::face

#endif  // SUPERGENIUS_WRITEABLE_KEY_VALUE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

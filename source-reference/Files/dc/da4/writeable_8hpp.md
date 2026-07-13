---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/writeable.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/writeable.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |
| **[sgns::storage::face](/source-reference/Namespaces/df/d29/namespacesgns_1_1storage_1_1face/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::storage::face::Writeable](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/)** <br/>An mixin for modifiable map.  |




## Source code

```cpp
#ifndef SUPERGENIUS_WRITEABLE_HPP
#define SUPERGENIUS_WRITEABLE_HPP

#include "outcome/outcome.hpp"

namespace sgns::storage::face {

  template <typename K, typename V>
  struct Writeable {
    virtual ~Writeable() = default;

    virtual outcome::result<void> put(const K &key, const V &value) = 0;
    virtual outcome::result<void> put(const K &key, V&& value) = 0;

    virtual outcome::result<void> remove(const K &key) = 0;
  };

}  // namespace sgns::storage::face

#endif  // SUPERGENIUS_WRITEABLE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/map_cursor.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/map_cursor.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |
| **[sgns::storage::face](/source-reference/Namespaces/df/d29/namespacesgns_1_1storage_1_1face/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::storage::face::MapCursor](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/)** <br/>An abstraction over generic map cursor.  |




## Source code

```cpp
#ifndef SUPERGENIUS_MAP_CURSOR_HPP
#define SUPERGENIUS_MAP_CURSOR_HPP

#include "outcome/outcome.hpp"

namespace sgns::storage::face {

  template <typename K, typename V>
  struct MapCursor {
    virtual ~MapCursor() = default;

    virtual outcome::result<void> seekToFirst() = 0;

    virtual outcome::result<void> seek(const K &key) = 0;

    virtual outcome::result<void> seekToLast() = 0;

    virtual bool isValid() const = 0;

    virtual outcome::result<void> next() = 0;

    virtual outcome::result<void> prev() = 0;

    virtual outcome::result<K> key() const = 0;

    virtual outcome::result<V> value() const = 0;
  };

}  // namespace sgns::storage::face

#endif  //SUPERGENIUS_MAP_CURSOR_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

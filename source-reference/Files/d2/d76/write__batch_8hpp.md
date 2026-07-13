---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/write_batch.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/write_batch.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |
| **[sgns::storage::face](/source-reference/Namespaces/df/d29/namespacesgns_1_1storage_1_1face/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::storage::face::WriteBatch](/source-reference/Classes/d9/d69/structsgns_1_1storage_1_1face_1_1_write_batch/)** <br/>An abstraction over a storage, which can be used for batch writes.  |




## Source code

```cpp
#ifndef SUPERGENIUS_WRITE_BATCH_HPP
#define SUPERGENIUS_WRITE_BATCH_HPP

#include "storage/face/writeable.hpp"

namespace sgns::storage::face {

  template <typename K, typename V>
  struct WriteBatch : public Writeable<K, V> {
    virtual outcome::result<void> commit() = 0;

    virtual void clear() = 0;
  };

}  // namespace sgns::storage::face

#endif  // SUPERGENIUS_WRITE_BATCH_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

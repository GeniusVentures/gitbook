---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/rocksdb/rocksdb_cursor.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/rocksdb/rocksdb_cursor.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::storage::rocksdb::Cursor](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/)** <br/>Instance of cursor can be used as bidirectional iterator over key-value bindings of the Map.  |




## Source code

```cpp
#ifndef SUPERGENIUS_rocksdb_CURSOR_HPP
#define SUPERGENIUS_rocksdb_CURSOR_HPP

#include <rocksdb/iterator.h>
#include "storage/rocksdb/rocksdb.hpp"

namespace sgns::storage 
{

  class rocksdb::Cursor : public BufferMapCursor {
   public:
    ~Cursor() override = default;

    explicit Cursor(std::shared_ptr<Iterator> it);

    outcome::result<void> seekToFirst() override;

    outcome::result<void> seek(const Buffer &key) override;

    outcome::result<void> seekToLast() override;

    bool isValid() const override;

    outcome::result<void> next() override;

    outcome::result<void> prev() override;

    outcome::result<Buffer> key() const override;

    outcome::result<Buffer> value() const override;

   private:
    std::shared_ptr<Iterator> i_;
  };

}  // namespace sgns::storage

#endif  // SUPERGENIUS_rocksdb_CURSOR_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

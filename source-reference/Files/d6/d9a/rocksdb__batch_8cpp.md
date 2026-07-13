---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/rocksdb/rocksdb_batch.cpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/rocksdb/rocksdb_batch.cpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |




## Source code

```cpp
#include "storage/rocksdb/rocksdb_batch.hpp"

#include "storage/rocksdb/rocksdb_util.hpp"

namespace sgns::storage 
{

  rocksdb::Batch::Batch(rocksdb &db) : db_(db) {}

  outcome::result<void> rocksdb::Batch::put(const Buffer &key,
                                            const Buffer &value) 
  {
    batch_.Put(make_slice(key), make_slice(value));
    return outcome::success();
  }

  outcome::result<void> rocksdb::Batch::put(const Buffer &key,
                                            Buffer &&value) 
  {
    return put(key, static_cast<const Buffer&>(value));
  }

  outcome::result<void> rocksdb::Batch::remove(const Buffer &key) 
  {
    batch_.Delete(make_slice(key));
    return outcome::success();
  }

  outcome::result<void> rocksdb::Batch::commit() 
  {
    auto status = db_.db_->Write(db_.wo_, &batch_);
    if (status.ok()) 
    {
      return outcome::success();
    }

    return error_as_result<void>(status, db_.logger_);
  }

  void rocksdb::Batch::clear() 
  {
    batch_.Clear();
  }

}  // namespace sgns::storage
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

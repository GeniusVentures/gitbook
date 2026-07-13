---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/rocksdb/rocksdb_batch.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/rocksdb/rocksdb_batch.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::storage::rocksdb::Batch](/source-reference/Classes/d8/d2c/classsgns_1_1storage_1_1rocksdb_1_1_batch/)** <br/>Class that is used to implement efficient bulk (batch) modifications of the Map.  |




## Source code

```cpp
#ifndef SUPERGENIUS_rocksdb_BATCH_HPP
#define SUPERGENIUS_rocksdb_BATCH_HPP

#include <rocksdb/write_batch.h>
#include <storage/rocksdb/rocksdb.hpp>

namespace sgns::storage 
{
  class rocksdb::Batch : public BufferBatch 
  {
   public:
    explicit Batch(rocksdb &db);

    outcome::result<void> put(const Buffer &key, const Buffer &value) override;
    outcome::result<void> put(const Buffer &key, Buffer &&value) override;

    outcome::result<void> remove(const Buffer &key) override;

    outcome::result<void> commit() override;

    void clear() override;

   private:
    rocksdb &db_;
    ::ROCKSDB_NAMESPACE::WriteBatch batch_;
  };

}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

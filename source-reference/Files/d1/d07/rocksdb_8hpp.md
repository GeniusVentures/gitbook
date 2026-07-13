---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/rocksdb/rocksdb.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/rocksdb/rocksdb.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::storage::rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/)** <br/>An implementation of PersistentBufferMap interface, which uses rocksdb as underlying storage.  |




## Source code

```cpp
#ifndef SUPERGENIUS_rocksdb_HPP
#define SUPERGENIUS_rocksdb_HPP

#include <rocksdb/rocksdb_namespace.h>
#include <rocksdb/db.h>
#include <rocksdb/slice.h>
#include <rocksdb/options.h>
#include <rocksdb/write_batch.h>

#include "base/logger.hpp"
#include "storage/buffer_map_types.hpp"

namespace sgns::storage
{

    class rocksdb : public BufferStorage
    {
    public:
        class Batch;
        class Cursor;

        using Iterator     = ::ROCKSDB_NAMESPACE::Iterator;
        using Options      = ::ROCKSDB_NAMESPACE::Options;
        using ReadOptions  = ::ROCKSDB_NAMESPACE::ReadOptions;
        using WriteOptions = ::ROCKSDB_NAMESPACE::WriteOptions;
        using DB           = ::ROCKSDB_NAMESPACE::DB;
        using Status       = ::ROCKSDB_NAMESPACE::Status;
        using Slice        = ::ROCKSDB_NAMESPACE::Slice;
        using QueryResult  = std::map<Buffer, Buffer>;
        using KeyValuePair = std::pair<Buffer, Buffer>;

        ~rocksdb() override;

        static outcome::result<std::shared_ptr<rocksdb>> create( std::string_view path,
                                                                 const Options   &options = Options() );

        static outcome::result<std::shared_ptr<rocksdb>> create( const std::shared_ptr<DB> &db );

        void setReadOptions( ReadOptions ro );

        void setWriteOptions( WriteOptions wo );

        std::unique_ptr<BufferMapCursor> cursor() override;

        std::unique_ptr<BufferBatch> batch() override;

        outcome::result<Buffer> get( const Buffer &key ) const override;

        outcome::result<QueryResult> query( const Buffer &keyPrefix ) const;

        outcome::result<QueryResult> query( const std::string &prefix_base,
                                            const std::string &middle_part,
                                            const std::string &remainder_prefix ) const;

        [[nodiscard]] bool contains( const Buffer &key ) const override;

        bool empty() const override;

        outcome::result<void> put( const Buffer &key, const Buffer &value ) override;

        // value will be copied, not moved, due to internal structure of rocksdb
        outcome::result<void> put( const Buffer &key, Buffer &&value ) override;

        outcome::result<void> remove( const Buffer &key ) override;

        std::string GetName() override
        {
            return "rocksdb";
        }

        [[nodiscard]] std::shared_ptr<DB> getDB() const
        {
            return db_;
        }

        std::vector<KeyValuePair> GetAll() const;

    private:
        std::shared_ptr<DB>      db_;
        ReadOptions              ro_;
        WriteOptions             wo_;
        base::Logger             logger_;
        std::shared_ptr<Options> options_;
        std::string              path_;
    };

} // namespace sgns::storage

#endif // SUPERGENIUS_rocksdb_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

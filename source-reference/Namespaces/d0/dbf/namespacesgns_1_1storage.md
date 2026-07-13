---
title: sgns::storage

---

# sgns::storage



 [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns::storage::face](/source-reference/Namespaces/df/d29/namespacesgns_1_1storage_1_1face/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::storage::rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/)** <br/>An implementation of PersistentBufferMap interface, which uses rocksdb as underlying storage.  |

## Types

|                | Name           |
| -------------- | -------------- |
| enum class uint8_t | **[DatabaseError](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#enum-databaseerror)** { OK, NOT_FOUND, CORRUPTION, NOT_SUPPORTED, INVALID_ARGUMENT, IO_ERROR, MERGE_IN_PROGRESS, INCOMPLETE, SHUTDOWN_IN_PROGRESS, TIMED_OUT, ABORTED, BUSY, EXPIRED, TRY_AGAIN_, COMPACTION_TOO_LARGE, COLUMN_FAMILY_DROPPED, UNITIALIZED, UNKNOWN}<br/>universal database interface error  |
| using [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) | **[Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer)**  |
| using [face::GenericMap](/source-reference/Classes/d4/d01/structsgns_1_1storage_1_1face_1_1_generic_map/)< [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer), [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) > | **[BufferMap](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffermap)**  |
| using [face::WriteBatch](/source-reference/Classes/d9/d69/structsgns_1_1storage_1_1face_1_1_write_batch/)< [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer), [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) > | **[BufferBatch](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-bufferbatch)**  |
| using [face::ReadOnlyMap](/source-reference/Classes/d6/d8f/structsgns_1_1storage_1_1face_1_1_read_only_map/)< [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer), [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) > | **[ReadOnlyBufferMap](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-readonlybuffermap)**  |
| using [face::BatchWriteMap](/source-reference/Classes/d3/df4/structsgns_1_1storage_1_1face_1_1_batch_write_map/)< [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer), [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) > | **[BatchWriteBufferMap](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-batchwritebuffermap)**  |
| using [face::GenericStorage](/source-reference/Classes/da/d5d/structsgns_1_1storage_1_1face_1_1_generic_storage/)< [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer), [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) > | **[BufferStorage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-bufferstorage)**  |
| using [face::MapCursor](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/)< [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer), [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) > | **[BufferMapCursor](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffermapcursor)**  |
| using ::ROCKSDB_NAMESPACE::BlockBasedTableOptions | **[BlockBasedTableOptions](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-blockbasedtableoptions)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| [DatabaseError](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#enum-databaseerror) | **[error_from_rocksdb](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#function-error_from_rocksdb)**(rocksdb::Status::Code code) |
| const std::string & | **[GetAuthoritySetKey](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#function-getauthoritysetkey)**() |
| const std::string & | **[GetSetStateKey](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#function-getsetstatekey)**() |
| const std::string & | **[GetGenesisBlockHashLookupKey](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#function-getgenesisblockhashlookupkey)**() |
| const std::string & | **[GetLastFinalizedBlockHashLookupKey](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#function-getlastfinalizedblockhashlookupkey)**() |
| template <typename T \> <br/>outcome::result< T > | **[error_as_result](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#function-error_as_result)**(const [rocksdb::Status](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-status) & s) |
| template <typename T \> <br/>outcome::result< T > | **[error_as_result](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#function-error_as_result)**(const [rocksdb::Status](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-status) & s, const [base::Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) & logger) |
| [rocksdb::Slice](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-slice) | **[make_slice](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#function-make_slice)**(const [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) & buf) |
| gsl::span< const uint8_t > | **[make_span](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#function-make_span)**(const [rocksdb::Slice](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-slice) & s) |
| [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) | **[make_buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#function-make_buffer)**(const [rocksdb::Slice](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-slice) & s) |

## Detailed Description


This file contains convenience typedefs for interfaces from face/, as they are mostly used with [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) key and value types 

## Types Documentation

### enum DatabaseError

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| OK | |   |
| NOT_FOUND | |   |
| CORRUPTION | |   |
| NOT_SUPPORTED | |   |
| INVALID_ARGUMENT | |   |
| IO_ERROR | |   |
| MERGE_IN_PROGRESS | |   |
| INCOMPLETE | |   |
| SHUTDOWN_IN_PROGRESS | |   |
| TIMED_OUT | |   |
| ABORTED | |   |
| BUSY | |   |
| EXPIRED | |   |
| TRY_AGAIN_ | |   |
| COMPACTION_TOO_LARGE | |   |
| COLUMN_FAMILY_DROPPED | |   |
| UNITIALIZED | |   |
| UNKNOWN | |   |



universal database interface error 

### using Buffer

```cpp
using sgns::storage::Buffer = base::Buffer;
```


### using BufferMap

```cpp
using sgns::storage::BufferMap = face::GenericMap<Buffer, Buffer>;
```


### using BufferBatch

```cpp
using sgns::storage::BufferBatch = face::WriteBatch<Buffer, Buffer>;
```


### using ReadOnlyBufferMap

```cpp
using sgns::storage::ReadOnlyBufferMap = face::ReadOnlyMap<Buffer, Buffer>;
```


### using BatchWriteBufferMap

```cpp
using sgns::storage::BatchWriteBufferMap = face::BatchWriteMap<Buffer, Buffer>;
```


### using BufferStorage

```cpp
using sgns::storage::BufferStorage = face::GenericStorage<Buffer, Buffer>;
```


### using BufferMapCursor

```cpp
using sgns::storage::BufferMapCursor = face::MapCursor<Buffer, Buffer>;
```


### using BlockBasedTableOptions

```cpp
using sgns::storage::BlockBasedTableOptions = ::ROCKSDB_NAMESPACE::BlockBasedTableOptions;
```



## Functions Documentation

### function error_from_rocksdb

```cpp
DatabaseError error_from_rocksdb(
    rocksdb::Status::Code code
)
```


### function GetAuthoritySetKey

```cpp
const std::string & GetAuthoritySetKey()
```


### function GetSetStateKey

```cpp
const std::string & GetSetStateKey()
```


### function GetGenesisBlockHashLookupKey

```cpp
const std::string & GetGenesisBlockHashLookupKey()
```


### function GetLastFinalizedBlockHashLookupKey

```cpp
const std::string & GetLastFinalizedBlockHashLookupKey()
```


### function error_as_result

```cpp
template <typename T >
inline outcome::result< T > error_as_result(
    const rocksdb::Status & s
)
```


### function error_as_result

```cpp
template <typename T >
inline outcome::result< T > error_as_result(
    const rocksdb::Status & s,
    const base::Logger & logger
)
```


### function make_slice

```cpp
inline rocksdb::Slice make_slice(
    const base::Buffer & buf
)
```


### function make_span

```cpp
inline gsl::span< const uint8_t > make_span(
    const rocksdb::Slice & s
)
```


### function make_buffer

```cpp
inline base::Buffer make_buffer(
    const rocksdb::Slice & s
)
```






-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
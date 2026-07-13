---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/buffer_map_types.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/buffer_map_types.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |

## Types

|                | Name           |
| -------------- | -------------- |
| using base::Buffer | **[Buffer](/source-reference/Files/d8/dcc/buffer__map__types_8hpp/#using-buffer)**  |
| using face::GenericMap< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/), [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > | **[BufferMap](/source-reference/Files/d8/dcc/buffer__map__types_8hpp/#using-buffermap)**  |
| using face::WriteBatch< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/), [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > | **[BufferBatch](/source-reference/Files/d8/dcc/buffer__map__types_8hpp/#using-bufferbatch)**  |
| using face::ReadOnlyMap< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/), [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > | **[ReadOnlyBufferMap](/source-reference/Files/d8/dcc/buffer__map__types_8hpp/#using-readonlybuffermap)**  |
| using face::BatchWriteMap< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/), [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > | **[BatchWriteBufferMap](/source-reference/Files/d8/dcc/buffer__map__types_8hpp/#using-batchwritebuffermap)**  |
| using face::GenericStorage< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/), [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > | **[BufferStorage](/source-reference/Files/d8/dcc/buffer__map__types_8hpp/#using-bufferstorage)**  |
| using face::MapCursor< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/), [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > | **[BufferMapCursor](/source-reference/Files/d8/dcc/buffer__map__types_8hpp/#using-buffermapcursor)**  |

## Types Documentation

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





## Source code

```cpp
#ifndef SUPERGENIUS_BUFFER_MAP_TYPES_HPP
#define SUPERGENIUS_BUFFER_MAP_TYPES_HPP


#include <gsl/span>

#include "base/buffer.hpp"
#include "storage/face/generic_storage.hpp"
#include "storage/face/write_batch.hpp"

namespace sgns::storage {

  using Buffer = base::Buffer;

  using BufferMap = face::GenericMap<Buffer, Buffer>;

  using BufferBatch = face::WriteBatch<Buffer, Buffer>;

  using ReadOnlyBufferMap = face::ReadOnlyMap<Buffer, Buffer>;
  using BatchWriteBufferMap = face::BatchWriteMap<Buffer, Buffer>;

  using BufferStorage = face::GenericStorage<Buffer, Buffer>;

  using BufferMapCursor = face::MapCursor<Buffer, Buffer>;

}  // namespace sgns::storage

#endif  // SUPERGENIUS_BUFFER_MAP_TYPES_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

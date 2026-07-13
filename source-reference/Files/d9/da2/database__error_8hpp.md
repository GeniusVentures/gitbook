---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/database_error.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/database_error.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |

## Types

|                | Name           |
| -------------- | -------------- |
| enum class uint8_t | **[DatabaseError](/source-reference/Files/d9/da2/database__error_8hpp/#enum-databaseerror)** { OK, NOT_FOUND, CORRUPTION, NOT_SUPPORTED, INVALID_ARGUMENT, IO_ERROR, MERGE_IN_PROGRESS, INCOMPLETE, SHUTDOWN_IN_PROGRESS, TIMED_OUT, ABORTED, BUSY, EXPIRED, TRY_AGAIN_, COMPACTION_TOO_LARGE, COLUMN_FAMILY_DROPPED, UNITIALIZED, UNKNOWN}<br/>universal database interface error  |

## Functions

|                | Name           |
| -------------- | -------------- |
| DatabaseError | **[error_from_rocksdb](/source-reference/Files/d9/da2/database__error_8hpp/#function-error_from_rocksdb)**(rocksdb::Status::Code code) |
| | **[OUTCOME_HPP_DECLARE_ERROR_2](/source-reference/Files/d9/da2/database__error_8hpp/#function-outcome_hpp_declare_error_2)**([sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/) , DatabaseError ) |

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


## Functions Documentation

### function error_from_rocksdb

```cpp
DatabaseError error_from_rocksdb(
    rocksdb::Status::Code code
)
```


### function OUTCOME_HPP_DECLARE_ERROR_2

```cpp
OUTCOME_HPP_DECLARE_ERROR_2(
    sgns::storage ,
    DatabaseError 
)
```




## Source code

```cpp
#ifndef STORAGE_DATABASE_ERROR_HPP
#define STORAGE_DATABASE_ERROR_HPP

#include "outcome/outcome.hpp"

#include <rocksdb/status.h>

namespace sgns::storage
{
    enum class DatabaseError : uint8_t
    {
        OK,
        NOT_FOUND,
        CORRUPTION,
        NOT_SUPPORTED,
        INVALID_ARGUMENT,
        IO_ERROR,
        MERGE_IN_PROGRESS,
        INCOMPLETE,
        SHUTDOWN_IN_PROGRESS,
        TIMED_OUT,
        ABORTED,
        BUSY,
        EXPIRED,
        TRY_AGAIN_,
        COMPACTION_TOO_LARGE,
        COLUMN_FAMILY_DROPPED,
        UNITIALIZED,
        UNKNOWN,
    };

    DatabaseError error_from_rocksdb( rocksdb::Status::Code code );
}

OUTCOME_HPP_DECLARE_ERROR_2( sgns::storage, DatabaseError );

#endif // STORAGE_DATABASE_ERROR_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

---
title: sgns::storage::rocksdb
summary: An implementation of PersistentBufferMap interface, which uses rocksdb as underlying storage. 

---

# sgns::storage::rocksdb



An implementation of PersistentBufferMap interface, which uses rocksdb as underlying storage. 


`#include <rocksdb.hpp>`

Inherits from [sgns::storage::face::GenericStorage< Buffer, Buffer >](/source-reference/Classes/da/d5d/structsgns_1_1storage_1_1face_1_1_generic_storage/), [sgns::storage::face::ReadOnlyMap< K, V >](/source-reference/Classes/d6/d8f/structsgns_1_1storage_1_1face_1_1_read_only_map/), [sgns::storage::face::BatchWriteMap< K, V >](/source-reference/Classes/d3/df4/structsgns_1_1storage_1_1face_1_1_batch_write_map/), [IComponent](/source-reference/Classes/d1/dbf/class_i_component/), [sgns::storage::face::Iterable< K, V >](/source-reference/Classes/d4/d27/structsgns_1_1storage_1_1face_1_1_iterable/), [sgns::storage::face::Readable< K, V >](/source-reference/Classes/dc/d9e/structsgns_1_1storage_1_1face_1_1_readable/), [sgns::storage::face::Writeable< K, V >](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/), [sgns::storage::face::Batchable< K, V >](/source-reference/Classes/de/d2d/structsgns_1_1storage_1_1face_1_1_batchable/)

## Public Classes

|                | Name           |
| -------------- | -------------- |
| class | **[Batch](/source-reference/Classes/d8/d2c/classsgns_1_1storage_1_1rocksdb_1_1_batch/)** <br/>Class that is used to implement efficient bulk (batch) modifications of the Map.  |
| class | **[Cursor](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/)** <br/>Instance of cursor can be used as bidirectional iterator over key-value bindings of the Map.  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| using ::ROCKSDB_NAMESPACE::Iterator | **[Iterator](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-iterator)**  |
| using ::ROCKSDB_NAMESPACE::Options | **[Options](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-options)**  |
| using ::ROCKSDB_NAMESPACE::ReadOptions | **[ReadOptions](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-readoptions)**  |
| using ::ROCKSDB_NAMESPACE::WriteOptions | **[WriteOptions](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-writeoptions)**  |
| using ::ROCKSDB_NAMESPACE::DB | **[DB](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-db)**  |
| using ::ROCKSDB_NAMESPACE::Status | **[Status](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-status)**  |
| using ::ROCKSDB_NAMESPACE::Slice | **[Slice](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-slice)**  |
| using std::map< [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer), [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) > | **[QueryResult](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-queryresult)**  |
| using std::pair< [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer), [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) > | **[KeyValuePair](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-keyvaluepair)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[~rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-~rocksdb)**() override |
| void | **[setReadOptions](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-setreadoptions)**([ReadOptions](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-readoptions) ro)<br/>Set read options, which are used in.  |
| void | **[setWriteOptions](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-setwriteoptions)**([WriteOptions](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-writeoptions) wo)<br/>Set write options, which are used in.  |
| virtual std::unique_ptr< [BufferMapCursor](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffermapcursor) > | **[cursor](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-cursor)**() override<br/>Returns new key-value iterator.  |
| virtual std::unique_ptr< [BufferBatch](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-bufferbatch) > | **[batch](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-batch)**() override<br/>Creates new Write [Batch](/source-reference/Classes/d8/d2c/classsgns_1_1storage_1_1rocksdb_1_1_batch/) - an object, which can be used to efficiently write bulk data.  |
| outcome::result< [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) > | **[get](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-get)**(const [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) & key) const override |
| outcome::result< [QueryResult](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-queryresult) > | **[query](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-query)**(const [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) & keyPrefix) const |
| outcome::result< [QueryResult](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-queryresult) > | **[query](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-query)**(const std::string & prefix_base, const std::string & middle_part, const std::string & remainder_prefix) const<br/>Queries with a middle part that can be a wildcard, negated string or normal string.  |
| bool | **[contains](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-contains)**(const [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) & key) const override |
| virtual bool | **[empty](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-empty)**() const override<br/>Returns true if the storage is empty.  |
| outcome::result< void > | **[put](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-put)**(const [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) & key, const [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) & value) override |
| outcome::result< void > | **[put](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-put)**(const [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) & key, [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) && value) override |
| outcome::result< void > | **[remove](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-remove)**(const [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) & key) override |
| virtual std::string | **[GetName](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-getname)**() override |
| std::shared_ptr< [DB](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-db) > | **[getDB](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-getdb)**() const |
| std::vector< [KeyValuePair](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-keyvaluepair) > | **[GetAll](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-getall)**() const<br/>Gets all key value pairs on rocksdb.  |
| outcome::result< std::shared_ptr< [rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/) > > | **[create](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-create)**(std::string_view path, const [Options](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-options) & options =[Options](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-options)())<br/>Factory method to create an instance of rocksdb class.  |
| outcome::result< std::shared_ptr< [rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/) > > | **[create](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-create)**(const std::shared_ptr< [DB](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-db) > & db)<br/>Factory method to create an instance of rocksdb class.  |

## Additional inherited members

**Public Functions inherited from [IComponent](/source-reference/Classes/d1/dbf/class_i_component/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IComponent](/source-reference/Classes/d1/dbf/class_i_component/#function-~icomponent)**() =default |

**Public Functions inherited from [sgns::storage::face::Iterable< K, V >](/source-reference/Classes/d4/d27/structsgns_1_1storage_1_1face_1_1_iterable/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Iterable](/source-reference/Classes/d4/d27/structsgns_1_1storage_1_1face_1_1_iterable/#function-~iterable)**() =default |

**Public Functions inherited from [sgns::storage::face::Readable< K, V >](/source-reference/Classes/dc/d9e/structsgns_1_1storage_1_1face_1_1_readable/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Readable](/source-reference/Classes/dc/d9e/structsgns_1_1storage_1_1face_1_1_readable/#function-~readable)**() =default |

**Public Functions inherited from [sgns::storage::face::Writeable< K, V >](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Writeable](/source-reference/Classes/d7/dc2/structsgns_1_1storage_1_1face_1_1_writeable/#function-~writeable)**() =default |

**Public Functions inherited from [sgns::storage::face::Batchable< K, V >](/source-reference/Classes/de/d2d/structsgns_1_1storage_1_1face_1_1_batchable/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~Batchable](/source-reference/Classes/de/d2d/structsgns_1_1storage_1_1face_1_1_batchable/#function-~batchable)**() =default |


## Public Types Documentation

### using Iterator

```cpp
using sgns::storage::rocksdb::Iterator = ::ROCKSDB_NAMESPACE::Iterator;
```


### using Options

```cpp
using sgns::storage::rocksdb::Options = ::ROCKSDB_NAMESPACE::Options;
```


### using ReadOptions

```cpp
using sgns::storage::rocksdb::ReadOptions = ::ROCKSDB_NAMESPACE::ReadOptions;
```


### using WriteOptions

```cpp
using sgns::storage::rocksdb::WriteOptions = ::ROCKSDB_NAMESPACE::WriteOptions;
```


### using DB

```cpp
using sgns::storage::rocksdb::DB = ::ROCKSDB_NAMESPACE::DB;
```


### using Status

```cpp
using sgns::storage::rocksdb::Status = ::ROCKSDB_NAMESPACE::Status;
```


### using Slice

```cpp
using sgns::storage::rocksdb::Slice = ::ROCKSDB_NAMESPACE::Slice;
```


### using QueryResult

```cpp
using sgns::storage::rocksdb::QueryResult = std::map<Buffer, Buffer>;
```


### using KeyValuePair

```cpp
using sgns::storage::rocksdb::KeyValuePair = std::pair<Buffer, Buffer>;
```


## Public Functions Documentation

### function ~rocksdb

```cpp
~rocksdb() override
```


### function setReadOptions

```cpp
void setReadOptions(
    ReadOptions ro
)
```

Set read options, which are used in. 

**Parameters**: 

  * **ro** options 


**See**: [rocksdb::get](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-get)

### function setWriteOptions

```cpp
void setWriteOptions(
    WriteOptions wo
)
```

Set write options, which are used in. 

**Parameters**: 

  * **wo** options 


**See**: [rocksdb::put](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-put)

### function cursor

```cpp
virtual std::unique_ptr< BufferMapCursor > cursor() override
```

Returns new key-value iterator. 

**Return**: kv iterator 

**Reimplements**: [sgns::storage::face::Iterable::cursor](/source-reference/Classes/d4/d27/structsgns_1_1storage_1_1face_1_1_iterable/#function-cursor)


### function batch

```cpp
virtual std::unique_ptr< BufferBatch > batch() override
```

Creates new Write [Batch](/source-reference/Classes/d8/d2c/classsgns_1_1storage_1_1rocksdb_1_1_batch/) - an object, which can be used to efficiently write bulk data. 

**Reimplements**: [sgns::storage::face::Batchable::batch](/source-reference/Classes/de/d2d/structsgns_1_1storage_1_1face_1_1_batchable/#function-batch)


### function get

```cpp
outcome::result< Buffer > get(
    const Buffer & key
) const override
```


### function query

```cpp
outcome::result< QueryResult > query(
    const Buffer & keyPrefix
) const
```


### function query

```cpp
outcome::result< QueryResult > query(
    const std::string & prefix_base,
    const std::string & middle_part,
    const std::string & remainder_prefix
) const
```

Queries with a middle part that can be a wildcard, negated string or normal string. 

**Parameters**: 

  * **prefix_base** The base prefix to query 
  * **middle_part** Either a string (normal query), '*' or !string 
  * **remainder_prefix** The remainder part of the query prefix 


**Return**: List of query results 

### function contains

```cpp
bool contains(
    const Buffer & key
) const override
```


### function empty

```cpp
virtual bool empty() const override
```

Returns true if the storage is empty. 

**Reimplements**: [sgns::storage::face::Readable::empty](/source-reference/Classes/dc/d9e/structsgns_1_1storage_1_1face_1_1_readable/#function-empty)


### function put

```cpp
outcome::result< void > put(
    const Buffer & key,
    const Buffer & value
) override
```


### function put

```cpp
outcome::result< void > put(
    const Buffer & key,
    Buffer && value
) override
```


### function remove

```cpp
outcome::result< void > remove(
    const Buffer & key
) override
```


### function GetName

```cpp
inline virtual std::string GetName() override
```


**Reimplements**: [IComponent::GetName](/source-reference/Classes/d1/dbf/class_i_component/#function-getname)


### function getDB

```cpp
inline std::shared_ptr< DB > getDB() const
```


### function GetAll

```cpp
std::vector< KeyValuePair > GetAll() const
```

Gets all key value pairs on rocksdb. 

### function create

```cpp
static outcome::result< std::shared_ptr< rocksdb > > create(
    std::string_view path,
    const Options & options =Options()
)
```

Factory method to create an instance of rocksdb class. 

**Parameters**: 

  * **path** filesystem path where database is going to be 
  * **options** rocksdb options, such as caching, logging, etc. 


**Return**: instance of rocksdb 

### function create

```cpp
static outcome::result< std::shared_ptr< rocksdb > > create(
    const std::shared_ptr< DB > & db
)
```

Factory method to create an instance of rocksdb class. 

**Parameters**: 

  * **db** pointer to rocksdb database instance 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
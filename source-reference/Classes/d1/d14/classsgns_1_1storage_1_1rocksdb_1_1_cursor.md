---
title: sgns::storage::rocksdb::Cursor
summary: Instance of cursor can be used as bidirectional iterator over key-value bindings of the Map. 

---

# sgns::storage::rocksdb::Cursor



Instance of cursor can be used as bidirectional iterator over key-value bindings of the Map. 


`#include <rocksdb_cursor.hpp>`

Inherits from [sgns::storage::face::MapCursor< Buffer, Buffer >](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[~Cursor](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-~cursor)**() override =default |
| | **[Cursor](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-cursor)**(std::shared_ptr< [Iterator](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-iterator) > it) |
| virtual outcome::result< void > | **[seekToFirst](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-seektofirst)**() override<br/>Same as std::begin(...);.  |
| virtual outcome::result< void > | **[seek](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-seek)**(const [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) & key) override<br/>Find given key and seek iterator to this key.  |
| virtual outcome::result< void > | **[seekToLast](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-seektolast)**() override<br/>Same as std::rbegin(...);, e.g. points to the last valid element.  |
| virtual bool | **[isValid](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-isvalid)**() const override<br/>Is iterator valid?  |
| virtual outcome::result< void > | **[next](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-next)**() override<br/>Make step forward.  |
| virtual outcome::result< void > | **[prev](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-prev)**() override<br/>Make step backwards.  |
| virtual outcome::result< [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) > | **[key](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-key)**() const override<br/>Getter for key.  |
| virtual outcome::result< [Buffer](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-buffer) > | **[value](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-value)**() const override<br/>Getter for value.  |

## Additional inherited members

**Public Functions inherited from [sgns::storage::face::MapCursor< Buffer, Buffer >](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~MapCursor](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-~mapcursor)**() =default |


## Public Functions Documentation

### function ~Cursor

```cpp
~Cursor() override =default
```


### function Cursor

```cpp
explicit Cursor(
    std::shared_ptr< Iterator > it
)
```


### function seekToFirst

```cpp
virtual outcome::result< void > seekToFirst() override
```

Same as std::begin(...);. 

**Reimplements**: [sgns::storage::face::MapCursor::seekToFirst](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-seektofirst)


### function seek

```cpp
virtual outcome::result< void > seek(
    const Buffer & key
) override
```

Find given key and seek iterator to this key. 

**Reimplements**: [sgns::storage::face::MapCursor::seek](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-seek)


### function seekToLast

```cpp
virtual outcome::result< void > seekToLast() override
```

Same as std::rbegin(...);, e.g. points to the last valid element. 

**Reimplements**: [sgns::storage::face::MapCursor::seekToLast](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-seektolast)


### function isValid

```cpp
virtual bool isValid() const override
```

Is iterator valid? 

**Return**: true if iterator points to the element of map, false otherwise 

**Reimplements**: [sgns::storage::face::MapCursor::isValid](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-isvalid)


### function next

```cpp
virtual outcome::result< void > next() override
```

Make step forward. 

**Reimplements**: [sgns::storage::face::MapCursor::next](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-next)


### function prev

```cpp
virtual outcome::result< void > prev() override
```

Make step backwards. 

**Reimplements**: [sgns::storage::face::MapCursor::prev](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-prev)


### function key

```cpp
virtual outcome::result< Buffer > key() const override
```

Getter for key. 

**Return**: key 

**Reimplements**: [sgns::storage::face::MapCursor::key](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-key)


### function value

```cpp
virtual outcome::result< Buffer > value() const override
```

Getter for value. 

**Return**: value 

**Reimplements**: [sgns::storage::face::MapCursor::value](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-value)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
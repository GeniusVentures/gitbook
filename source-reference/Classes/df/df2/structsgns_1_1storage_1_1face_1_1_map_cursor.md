---
title: sgns::storage::face::MapCursor
summary: An abstraction over generic map cursor. 

---

# sgns::storage::face::MapCursor



An abstraction over generic map cursor.  [More...](#detailed-description)


`#include <map_cursor.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~MapCursor](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-~mapcursor)**() =default |
| virtual outcome::result< void > | **[seekToFirst](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-seektofirst)**() =0<br/>Same as std::begin(...);.  |
| virtual outcome::result< void > | **[seek](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-seek)**(const K & key) =0<br/>Find given key and seek iterator to this key.  |
| virtual outcome::result< void > | **[seekToLast](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-seektolast)**() =0<br/>Same as std::rbegin(...);, e.g. points to the last valid element.  |
| virtual bool | **[isValid](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-isvalid)**() const =0<br/>Is iterator valid?  |
| virtual outcome::result< void > | **[next](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-next)**() =0<br/>Make step forward.  |
| virtual outcome::result< void > | **[prev](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-prev)**() =0<br/>Make step backwards.  |
| virtual outcome::result< K > | **[key](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-key)**() const =0<br/>Getter for key.  |
| virtual outcome::result< V > | **[value](/source-reference/Classes/df/df2/structsgns_1_1storage_1_1face_1_1_map_cursor/#function-value)**() const =0<br/>Getter for value.  |

## Detailed Description

```cpp
template <typename K ,
typename V >
struct sgns::storage::face::MapCursor;
```

An abstraction over generic map cursor. 

**Template Parameters**: 

  * **K** key type 
  * **V** value type 

## Public Functions Documentation

### function ~MapCursor

```cpp
virtual ~MapCursor() =default
```


### function seekToFirst

```cpp
virtual outcome::result< void > seekToFirst() =0
```

Same as std::begin(...);. 

**Reimplemented by**: [sgns::storage::rocksdb::Cursor::seekToFirst](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-seektofirst)


### function seek

```cpp
virtual outcome::result< void > seek(
    const K & key
) =0
```

Find given key and seek iterator to this key. 

**Reimplemented by**: [sgns::storage::rocksdb::Cursor::seek](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-seek)


### function seekToLast

```cpp
virtual outcome::result< void > seekToLast() =0
```

Same as std::rbegin(...);, e.g. points to the last valid element. 

**Reimplemented by**: [sgns::storage::rocksdb::Cursor::seekToLast](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-seektolast)


### function isValid

```cpp
virtual bool isValid() const =0
```

Is iterator valid? 

**Return**: true if iterator points to the element of map, false otherwise 

**Reimplemented by**: [sgns::storage::rocksdb::Cursor::isValid](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-isvalid)


### function next

```cpp
virtual outcome::result< void > next() =0
```

Make step forward. 

**Reimplemented by**: [sgns::storage::rocksdb::Cursor::next](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-next)


### function prev

```cpp
virtual outcome::result< void > prev() =0
```

Make step backwards. 

**Reimplemented by**: [sgns::storage::rocksdb::Cursor::prev](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-prev)


### function key

```cpp
virtual outcome::result< K > key() const =0
```

Getter for key. 

**Return**: key 

**Reimplemented by**: [sgns::storage::rocksdb::Cursor::key](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-key)


### function value

```cpp
virtual outcome::result< V > value() const =0
```

Getter for value. 

**Return**: value 

**Reimplemented by**: [sgns::storage::rocksdb::Cursor::value](/source-reference/Classes/d1/d14/classsgns_1_1storage_1_1rocksdb_1_1_cursor/#function-value)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
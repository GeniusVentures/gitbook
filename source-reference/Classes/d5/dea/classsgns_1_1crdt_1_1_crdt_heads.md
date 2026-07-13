---
title: sgns::crdt::CrdtHeads
summary: CrdtHeads manages the current Merkle-CRDT heads. 

---

# sgns::crdt::CrdtHeads



[CrdtHeads](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/) manages the current Merkle-CRDT heads. 


`#include <crdt_heads.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| using [storage::rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/) | **[DataStore](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#using-datastore)**  |
| using [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) | **[Buffer](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#using-buffer)**  |
| using std::unordered_map< std::string, std::set< CID > > | **[CRDTHeadList](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#using-crdtheadlist)**  |
| using std::pair< [CRDTHeadList](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#using-crdtheadlist), uint64_t > | **[CRDTListResult](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#using-crdtlistresult)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CrdtHeads](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-crdtheads)**(std::shared_ptr< [DataStore](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#using-datastore) > aDatastore, const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & aNamespace) |
| | **[CrdtHeads](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-crdtheads)**(const CrdtHeads & aHeads) |
| virtual | **[~CrdtHeads](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-~crdtheads)**() =default<br/>Destroy the Crdt Heads object.  |
| bool | **[operator==](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-operator==)**(const [CrdtHeads](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-crdtheads) & aHeads) const |
| bool | **[operator!=](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-operator!=)**(const [CrdtHeads](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-crdtheads) & aHeads) const |
| [CrdtHeads](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-crdtheads) & | **[operator=](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-operator=)**(const [CrdtHeads](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-crdtheads) & aHeads) |
| [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) | **[GetNamespaceKey](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-getnamespacekey)**() const |
| outcome::result< [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) > | **[GetKey](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-getkey)**(const std::string & topic, const CID & aCid) const |
| bool | **[IsHead](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-ishead)**(const CID & aCid, const std::string & topic) const |
| outcome::result< uint64_t > | **[GetHeadHeight](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-getheadheight)**(const CID & aCid, const std::string & topic) const |
| outcome::result< size_t > | **[GetLength](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-getlength)**(const std::string & topic ="") const |
| outcome::result< void > | **[Add](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-add)**(const CID & aCid, uint64_t aHeight, const std::string & topic) |
| outcome::result< void > | **[Remove](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-remove)**(const CID & aCid, const std::string & topic) |
| outcome::result< void > | **[Replace](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-replace)**(const CID & aCidHead, const CID & aNewHeadCid, uint64_t aHeight, const std::string & topic) |
| outcome::result< [CRDTListResult](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#using-crdtlistresult) > | **[GetList](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-getlist)**(const std::unordered_set< std::string > & topics ={}) const |
| outcome::result< void > | **[PrimeCache](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-primecache)**() |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| outcome::result< void > | **[Write](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-write)**([storage::BufferBatch](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-bufferbatch) & aDataStore, const CID & aCid, uint64_t aHeight, const std::string & topic) const |
| outcome::result< void > | **[Delete](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#function-delete)**(const std::unique_ptr< [storage::BufferBatch](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-bufferbatch) > & aDataStore, const CID & aCid, const std::string & topic) const |

## Public Types Documentation

### using DataStore

```cpp
using sgns::crdt::CrdtHeads::DataStore = storage::rocksdb;
```


### using Buffer

```cpp
using sgns::crdt::CrdtHeads::Buffer = base::Buffer;
```


### using CRDTHeadList

```cpp
using sgns::crdt::CrdtHeads::CRDTHeadList = std::unordered_map<std::string, std::set<CID>>;
```


### using CRDTListResult

```cpp
using sgns::crdt::CrdtHeads::CRDTListResult = std::pair<CRDTHeadList, uint64_t>;
```


## Public Functions Documentation

### function CrdtHeads

```cpp
CrdtHeads(
    std::shared_ptr< DataStore > aDatastore,
    const HierarchicalKey & aNamespace
)
```


**Parameters**: 

  * **aDatastore** Pointer to datastore 
  * **aNamespace** Namespace key (e.g "/namespace") 


Constructor 


### function CrdtHeads

```cpp
CrdtHeads(
    const CrdtHeads & aHeads
)
```


Copy constructor 


### function ~CrdtHeads

```cpp
virtual ~CrdtHeads() =default
```

Destroy the Crdt Heads object. 

### function operator==

```cpp
bool operator==(
    const CrdtHeads & aHeads
) const
```


**Return**: true if equal otherwise, it returns false. 

Equality operator 


### function operator!=

```cpp
bool operator!=(
    const CrdtHeads & aHeads
) const
```


**Return**: true if NOT equal otherwise, it returns false. 

Equality operator 


### function operator=

```cpp
CrdtHeads & operator=(
    const CrdtHeads & aHeads
)
```


Assignment operator 


### function GetNamespaceKey

```cpp
HierarchicalKey GetNamespaceKey() const
```


Get namespace hierarchical key 


### function GetKey

```cpp
outcome::result< HierarchicalKey > GetKey(
    const std::string & topic,
    const CID & aCid
) const
```


**Parameters**: 

  * **topic** Topic namespace. 
  * **aCid** Content identifier. 


**Return**: full path to CID key as [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) or outcome::failure on error 

Get full path to CID key. Path format: /namespace/topic/cid 


### function IsHead

```cpp
bool IsHead(
    const CID & aCid,
    const std::string & topic
) const
```


**Parameters**: 

  * **aCid** Content identifier 
  * **topic** Topic namespace 


**Return**: true is CID is head, false otherwise 

Check if CID is among the current heads. 


### function GetHeadHeight

```cpp
outcome::result< uint64_t > GetHeadHeight(
    const CID & aCid,
    const std::string & topic
) const
```


**Parameters**: 

  * **aCid** Content identifier 
  * **topic** Topic namespace 


**Return**: Height of head or outcome::failure on error 

Check if CID is head and return it height if it is 


### function GetLength

```cpp
outcome::result< size_t > GetLength(
    const std::string & topic =""
) const
```


**Return**: length, current number of heads or outcome::failure on error 

Get current number of heads 


### function Add

```cpp
outcome::result< void > Add(
    const CID & aCid,
    uint64_t aHeight,
    const std::string & topic
)
```


**Parameters**: 

  * **aCid** Content identifier 
  * **aHeight** height of head 
  * **topic** Topic namespace 


**Return**: outcome::failure on error 

Add head CID to datastore with full namespace 


### function Remove

```cpp
outcome::result< void > Remove(
    const CID & aCid,
    const std::string & topic
)
```


### function Replace

```cpp
outcome::result< void > Replace(
    const CID & aCidHead,
    const CID & aNewHeadCid,
    uint64_t aHeight,
    const std::string & topic
)
```


**Parameters**: 

  * **aCidHead** Content identifier of head to replace 
  * **aNewHeadCid** Content identifier of new head 
  * **aHeight** height of head 
  * **topic** Topic namespace 


**Return**: outcome::failure on error 

Replace a head with a new cid. 


### function GetList

```cpp
outcome::result< CRDTListResult > GetList(
    const std::unordered_set< std::string > & topics ={}
) const
```


**Parameters**: 

  * **topics** Topic to get list from 


**Return**: outcome::failure on error 

Returns the list of current heads plus the max height. 


### function PrimeCache

```cpp
outcome::result< void > PrimeCache()
```


**Return**: outcome::failure on error 

primeCache builds the heads cache based on what's in storage; since it is called from the constructor only we don't bother locking. 


## Protected Functions Documentation

### function Write

```cpp
outcome::result< void > Write(
    storage::BufferBatch & aDataStore,
    const CID & aCid,
    uint64_t aHeight,
    const std::string & topic
) const
```


**Parameters**: 

  * **aDataStore** Pointer to datastore batch 
  * **aCid** Content identifier to add 
  * **aHeight** height of CID head 
  * **topic** Topic namespace 


**Return**: outcome::failure on error 

Write data to datastore in batch mode 


### function Delete

```cpp
outcome::result< void > Delete(
    const std::unique_ptr< storage::BufferBatch > & aDataStore,
    const CID & aCid,
    const std::string & topic
) const
```


**Parameters**: 

  * **aDataStore** Pointer to datastore batch 
  * **aCid** Content identifier to remove 
  * **topic** Topic namespace 


Delete data from datastore in batch mode 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
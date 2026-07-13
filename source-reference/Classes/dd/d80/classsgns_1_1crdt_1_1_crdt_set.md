---
title: sgns::crdt::CrdtSet
summary: CrdtSet implements an Add-Wins Observed-Remove Set using delta-CRDTs (https://arxiv.org/abs/1410.2803) and backing all the data in a datastore. It is fully agnostic to MerkleCRDTs or the delta distribution layer. It chooses the Value with most priority for a Key as the current Value. When two values have the same priority, it chooses by alphabetically sorting their unique IDs alphabetically. 

---

# sgns::crdt::CrdtSet



[CrdtSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/) implements an Add-Wins Observed-Remove Set using delta-CRDTs ([https://arxiv.org/abs/1410.2803](https://arxiv.org/abs/1410.2803)) and backing all the data in a datastore. It is fully agnostic to MerkleCRDTs or the delta distribution layer. It chooses the Value with most priority for a Key as the current Value. When two values have the same priority, it chooses by alphabetically sorting their unique IDs alphabetically. 


`#include <crdt_set.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[QuerySuffix](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#enum-querysuffix)** { QUERY_ALL, QUERY_VALUESUFFIX, QUERY_PRIORITYSUFFIX} |
| using pb::Delta | **[Delta](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-delta)**  |
| using pb::Element | **[Element](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-element)**  |
| using [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) | **[Buffer](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-buffer)**  |
| using [storage::rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/) | **[DataStore](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-datastore)**  |
| using [DataStore::QueryResult](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-queryresult) | **[QueryResult](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-queryresult)**  |
| using std::function< void(const std::string &k, const [Buffer](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-buffer) &v, const std::string &cid)> | **[PutHookPtr](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-puthookptr)**  |
| using std::function< void(const std::string &k, const std::string &cid)> | **[DeleteHookPtr](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-deletehookptr)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CrdtSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-crdtset)**(std::shared_ptr< [DataStore](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-datastore) > aDatastore, const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & aNamespace, [PutHookPtr](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-puthookptr) aPutHookPtr =nullptr, [DeleteHookPtr](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-deletehookptr) aDeleteHookPtr =nullptr) |
| | **[CrdtSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-crdtset)**(const CrdtSet & aSet) |
| virtual | **[~CrdtSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-~crdtset)**() =default |
| bool | **[operator==](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-operator==)**(const [CrdtSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-crdtset) & aSet) const |
| bool | **[operator!=](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-operator!=)**(const [CrdtSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-crdtset) & aSet) const |
| [CrdtSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-crdtset) & | **[operator=](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-operator=)**(const [CrdtSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-crdtset) & aSet) |
| outcome::result< std::string > | **[GetValueFromDatastore](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-getvaluefromdatastore)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & aKey) const |
| outcome::result< std::shared_ptr< [Delta](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-delta) > > | **[CreateDeltaToRemove](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-createdeltatoremove)**(const std::string & aKey) const |
| outcome::result< [Buffer](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-buffer) > | **[GetElement](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-getelement)**(const std::string & aKey) const |
| outcome::result< [QueryResult](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-queryresult) > | **[QueryElements](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-queryelements)**(std::string_view aPrefix, const [QuerySuffix](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#enum-querysuffix) & aSuffix =[QuerySuffix::QUERY_ALL](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#enumvalue-query_all)) const |
| outcome::result< [QueryResult](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-queryresult) > | **[QueryElements](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-queryelements)**(const std::string & prefix_base, const std::string & middle_part, const std::string & remainder_prefix, const [QuerySuffix](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#enum-querysuffix) & aSuffix =[QuerySuffix::QUERY_ALL](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#enumvalue-query_all)) const<br/>Queries with a middle part that can be a wildcard, negated string or normal string.  |
| outcome::result< bool > | **[IsValueInSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-isvalueinset)**(const std::string & aKey) const |
| outcome::result< bool > | **[InElemsNotTombstoned](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-inelemsnottombstoned)**(const std::string & aKey) const |
| [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) | **[KeyPrefix](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-keyprefix)**(const std::string & aKey) const |
| [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) | **[ElemsPrefix](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-elemsprefix)**(const std::string & aKey) const |
| [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) | **[TombsPrefix](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-tombsprefix)**(const std::string & aKey) const |
| [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) | **[KeysKey](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-keyskey)**(std::string_view aKey) const |
| [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) | **[ValueKey](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-valuekey)**(const std::string & aKey) const |
| [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) | **[PriorityKey](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-prioritykey)**(const std::string & aKey) const |
| outcome::result< uint64_t > | **[GetPriority](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-getpriority)**(const std::string & aKey) const |
| outcome::result< void > | **[SetPriority](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-setpriority)**(const std::string & aKey, uint64_t aPriority) |
| outcome::result< void > | **[SetValue](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-setvalue)**(const std::string & aKey, const std::string & aID, const [Buffer](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-buffer) & aValue, uint64_t aPriority) |
| outcome::result< void > | **[SetValue](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-setvalue)**(const std::unique_ptr< [storage::BufferBatch](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/#using-bufferbatch) > & aDataStore, const std::string & aKey, const std::string & aID, const [Buffer](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-buffer) & aValue, uint64_t aPriority) |
| outcome::result< void > | **[PutElems](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-putelems)**(std::vector< [Element](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-element) > & aElems, const std::string & aID, uint64_t aPriority) |
| outcome::result< void > | **[PutTombs](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-puttombs)**(const std::vector< [Element](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-element) > & aTombs, const std::string & aID) const |
| outcome::result< void > | **[Merge](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-merge)**(const [Delta](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-delta) & aDelta, const std::string & aID) |
| outcome::result< bool > | **[InTombsKeyID](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-intombskeyid)**(const std::string & aKey, const std::string & aID) const |
| void | **[SetPutHook](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-setputhook)**(const [PutHookPtr](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-puthookptr) & putHookPtr) |
| void | **[SetDeleteHook](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-setdeletehook)**(const [DeleteHookPtr](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-deletehookptr) & deleteHookPtr) |
| outcome::result< void > | **[DataStoreSync](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-datastoresync)**(const std::vector< [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) > & aKeyList) |
| void | **[PrintDataStore](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-printdatastore)**() const |
| std::string | **[GetPrioritySuffix](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-getprioritysuffix)**() |
| std::string | **[GetValueSuffix](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-getvaluesuffix)**() |
| outcome::result< std::shared_ptr< [Delta](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#using-delta) > > | **[CreateDeltaToAdd](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#function-createdeltatoadd)**(const std::string & aKey, const std::string & aValue) |

## Public Types Documentation

### enum QuerySuffix

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| QUERY_ALL | |   |
| QUERY_VALUESUFFIX | |   |
| QUERY_PRIORITYSUFFIX | |   |




### using Delta

```cpp
using sgns::crdt::CrdtSet::Delta = pb::Delta;
```


### using Element

```cpp
using sgns::crdt::CrdtSet::Element = pb::Element;
```


### using Buffer

```cpp
using sgns::crdt::CrdtSet::Buffer = base::Buffer;
```


### using DataStore

```cpp
using sgns::crdt::CrdtSet::DataStore = storage::rocksdb;
```


### using QueryResult

```cpp
using sgns::crdt::CrdtSet::QueryResult = DataStore::QueryResult;
```


### using PutHookPtr

```cpp
using sgns::crdt::CrdtSet::PutHookPtr = std::function<void( const std::string &k, const Buffer &v, const std::string &cid )>;
```


**Parameters**: 

  * **k** key name 
  * **v** buffer value 


Function pointer to notify caller if key added to datastore 


### using DeleteHookPtr

```cpp
using sgns::crdt::CrdtSet::DeleteHookPtr = std::function<void( const std::string &k, const std::string &cid )>;
```


**Parameters**: 

  * **k** key name 


Function pointer to notify caller when key deleted from datastore 


## Public Functions Documentation

### function CrdtSet

```cpp
CrdtSet(
    std::shared_ptr< DataStore > aDatastore,
    const HierarchicalKey & aNamespace,
    PutHookPtr aPutHookPtr =nullptr,
    DeleteHookPtr aDeleteHookPtr =nullptr
)
```


**Parameters**: 

  * **aDatastore** Pointer to datastore 
  * **aNamespace** Namespce key (e.g "/namespace") 
  * **aPutHookPtr** Function pointer to nofify when key added to datastore, default nullptr 
  * **aDeleteHookPtr** Function pointer to nofify when key deleted from datastore, default nullptr 


Constructor 


### function CrdtSet

```cpp
CrdtSet(
    const CrdtSet & aSet
)
```


Copy constructor 


### function ~CrdtSet

```cpp
virtual ~CrdtSet() =default
```


Destructor 


### function operator==

```cpp
bool operator==(
    const CrdtSet & aSet
) const
```


**Return**: true if equal otherwise, it returns false. 

Equality operator 


### function operator!=

```cpp
bool operator!=(
    const CrdtSet & aSet
) const
```


**Return**: true if NOT equal otherwise, it returns false. 

Equality operator 


### function operator=

```cpp
CrdtSet & operator=(
    const CrdtSet & aSet
)
```


Assignment operator 


### function GetValueFromDatastore

```cpp
outcome::result< std::string > GetValueFromDatastore(
    const HierarchicalKey & aKey
) const
```


**Parameters**: 

  * **aKey** [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) to get value from datastore 


**Return**: buffer value as string or outcome::failure on error 

Get value from datastore for [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) defined 


### function CreateDeltaToRemove

```cpp
outcome::result< std::shared_ptr< Delta > > CreateDeltaToRemove(
    const std::string & aKey
) const
```


**Parameters**: 

  * **aKey** delta key to remove from datastore 


**Return**: pointer to delta or outcome::failure on error 

Returns a new delta-set removing the given keys with prefix /namespace/s/key 


### function GetElement

```cpp
outcome::result< Buffer > GetElement(
    const std::string & aKey
) const
```


**Parameters**: 

  * **aKey** Key name 


**Return**: buffer value or outcome::failure on error 

Get the value of an element from the CRDT set /namespace/k/key/v 


### function QueryElements

```cpp
outcome::result< QueryResult > QueryElements(
    std::string_view aPrefix,
    const QuerySuffix & aSuffix =QuerySuffix::QUERY_ALL
) const
```


**Parameters**: 

  * **aPrefix** prefix to search, if empty string, return all 
  * **aSuffix** suffix to search 


**See**: [QuerySuffix](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/#enum-querysuffix)

**Return**: list of key-value pairs matches prefix and suffix 

Query datastore key-value pairs by prefix, if prefix empty return all elements /namespace/k/prefix 


### function QueryElements

```cpp
outcome::result< QueryResult > QueryElements(
    const std::string & prefix_base,
    const std::string & middle_part,
    const std::string & remainder_prefix,
    const QuerySuffix & aSuffix =QuerySuffix::QUERY_ALL
) const
```

Queries with a middle part that can be a wildcard, negated string or normal string. 

**Parameters**: 

  * **prefix_base** The base prefix to query 
  * **middle_part** Either a string (normal query), '*' or !string 
  * **remainder_prefix** The remainder part of the query prefix 
  * **aSuffix** The suffix to search 


**Return**: List of query results 

### function IsValueInSet

```cpp
outcome::result< bool > IsValueInSet(
    const std::string & aKey
) const
```


**Parameters**: 

  * **aKey** key name 


**Return**: true if the key belongs to one of the elements and is not tombstoned or outcome::failure on error 

Returns true if the key belongs to one of the elements in the /namespace/k/key/v set, and this element is not tombstoned. 


### function InElemsNotTombstoned

```cpp
outcome::result< bool > InElemsNotTombstoned(
    const std::string & aKey
) const
```


**Parameters**: 

  * **aKey** key name 


**Return**: true if the key has not been tombstoned, false otherwise or outcome::failure on error 

Returns in we have a key/block combinations in the elements set that has not been tombstoned. 


### function KeyPrefix

```cpp
HierarchicalKey KeyPrefix(
    const std::string & aKey
) const
```


**Parameters**: 

  * **aKey** key string 


**Return**: [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) with key prefix 

Get full path prefix in namespace for a key /namespace/key 


### function ElemsPrefix

```cpp
HierarchicalKey ElemsPrefix(
    const std::string & aKey
) const
```


**Parameters**: 

  * **aKey** key string 


**Return**: [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) with elems prefix 

Get elems full path prefix in namespace for a key /namespace/s/key 


### function TombsPrefix

```cpp
HierarchicalKey TombsPrefix(
    const std::string & aKey
) const
```


**Parameters**: 

  * **aKey** key string 


**Return**: [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) with tombs prefix 

Get tombs full path prefix in namespace for a key /namespace/t/key 


### function KeysKey

```cpp
HierarchicalKey KeysKey(
    std::string_view aKey
) const
```


**Parameters**: 

  * **aKey** key string 


**Return**: [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) with key prefix 

Get keys full path prefix in namespace for a key /namespace/k/key 


### function ValueKey

```cpp
HierarchicalKey ValueKey(
    const std::string & aKey
) const
```


**Parameters**: 

  * **aKey** key string 


**Return**: [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) with value prefix 

Get value full path prefix in namespace for a key /namespace/k/key/v 


### function PriorityKey

```cpp
HierarchicalKey PriorityKey(
    const std::string & aKey
) const
```


**Parameters**: 

  * **aKey** key string 


**Return**: [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) with priority prefix 

Get priority full path prefix in namespace for a key /namespace/k/key/p 


### function GetPriority

```cpp
outcome::result< uint64_t > GetPriority(
    const std::string & aKey
) const
```


**Parameters**: 

  * **aKey** key string 


**Return**: priority of the key or outcome::failure on error 

Get priority for a key from datastore 


### function SetPriority

```cpp
outcome::result< void > SetPriority(
    const std::string & aKey,
    uint64_t aPriority
)
```


**Parameters**: 

  * **aKey** key string 
  * **aPriority** priority to save 


**Return**: priority of the key or outcome::failure on error 

Set priority for a key and put into datastore 


### function SetValue

```cpp
outcome::result< void > SetValue(
    const std::string & aKey,
    const std::string & aID,
    const Buffer & aValue,
    uint64_t aPriority
)
```


**Parameters**: 

  * **aKey** key string 
  * **aID** tomb key ID 
  * **aValue** buffer value to set 
  * **aPriority** priority to save 


**Return**: priority of the key or outcome::failure on error 

Sets a value to datastore if priority is higher. When equal, it sets if the value is lexicographically higher than the current value. 


### function SetValue

```cpp
outcome::result< void > SetValue(
    const std::unique_ptr< storage::BufferBatch > & aDataStore,
    const std::string & aKey,
    const std::string & aID,
    const Buffer & aValue,
    uint64_t aPriority
)
```


**Parameters**: 

  * **aDataStore** datastore batch 
  * **aKey** key string 
  * **aID** tomb key ID 
  * **aValue** buffer value to set 
  * **aPriority** priority to save 


**Return**: priority of the key or outcome::failure on error 

Sets a value to datastore in batch mode if priority is higher. When equal, it sets if the value is lexicographically higher than the current value. 


### function PutElems

```cpp
outcome::result< void > PutElems(
    std::vector< Element > & aElems,
    const std::string & aID,
    uint64_t aPriority
)
```


**Parameters**: 

  * **aElems** list of elems to to into datastore 
  * **aID** tomb key ID 
  * **aPriority** priority to save 


**Return**: outcome::success on success or outcome::failure otherwise 

putElems adds items to the "elems" set. It will also set current values and priorities for each element. This needs to run in a lock, as otherwise races may occur when reading/writing the priorities, resulting in bad behaviours.

Technically the lock should only affect the keys that are being written, but with the batching optimization the locks would need to be hold until the batch is written), and one lock per key might be way worse than a single global lock in the end. 


### function PutTombs

```cpp
outcome::result< void > PutTombs(
    const std::vector< Element > & aTombs,
    const std::string & aID
) const
```


**Parameters**: 

  * **aTombs** list of tomb elements to put into datastore 
  * **aID** tomb key ID 


**Return**: outcome::success on success or outcome::failure otherwise 

PutTombs adds items to the "tombs" set (marked as deleted) 


### function Merge

```cpp
outcome::result< void > Merge(
    const Delta & aDelta,
    const std::string & aID
)
```


**Parameters**: 

  * **aDelta** delta with elems and tombs to save into datastore 
  * **aID** tomb key ID 


**Return**: outcome::success on success or outcome::failure otherwise 

Merge elems and tombs from delta into datastore 


### function InTombsKeyID

```cpp
outcome::result< bool > InTombsKeyID(
    const std::string & aKey,
    const std::string & aID
) const
```


**Parameters**: 

  * **aKey** key string 
  * **aID** tomb key ID 


**Return**: true if key with ID is tombstoned, false otherwise or outcome::failure on error 

Check if key is tombstoned with tomb ID and found in datastore 


### function SetPutHook

```cpp
void SetPutHook(
    const PutHookPtr & putHookPtr
)
```


**Parameters**: 

  * **putHookPtr** Function pointer to callback function 


The PutHook function is triggered whenever an element is successfully added to the datastore (either by a local or remote update), and only when that addition is considered the prevalent value. 


### function SetDeleteHook

```cpp
void SetDeleteHook(
    const DeleteHookPtr & deleteHookPtr
)
```


**Parameters**: 

  * **deleteHookPtr** Function pointer to callback function 


The DeleteHook function is triggered whenever a version of an element is successfully removed from the datastore (either by a local or remote update). Unordered and concurrent updates may result in the DeleteHook being triggered even though the element is still present in the datastore because it was re-added. If that is relevant, use Has() to check if the removed element is still part of the datastore. 


### function DataStoreSync

```cpp
outcome::result< void > DataStoreSync(
    const std::vector< HierarchicalKey > & aKeyList
)
```


**Parameters**: 

  * **aKeyList** all heads and the set entries related to the given prefix 


**Return**: outcome::success on success or outcome::failure otherwise 

Perform a Sync against all the paths associated with a key prefix 


### function PrintDataStore

```cpp
void PrintDataStore() const
```


### function GetPrioritySuffix

```cpp
static inline std::string GetPrioritySuffix()
```


Get priority suffix 


### function GetValueSuffix

```cpp
static inline std::string GetValueSuffix()
```


Get value suffix 


### function CreateDeltaToAdd

```cpp
static outcome::result< std::shared_ptr< Delta > > CreateDeltaToAdd(
    const std::string & aKey,
    const std::string & aValue
)
```


**Parameters**: 

  * **aKey** delta key to add to datastore 
  * **aValue** delta value to add to datastore 


**Return**: pointer to new delta or outcome::failure on error 

Returns a new delta-set adding the given key/value. 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
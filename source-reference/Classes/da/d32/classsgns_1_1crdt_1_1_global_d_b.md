---
title: sgns::crdt::GlobalDB

---

# sgns::crdt::GlobalDB






`#include <globaldb.hpp>`

Inherits from std::enable_shared_from_this< GlobalDB >

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[BackupOptions](/source-reference/Classes/d3/d2a/structsgns_1_1crdt_1_1_global_d_b_1_1_backup_options/)**  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class uint8_t | **[Error](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#enum-error)** { ROCKSDB_IO = 0, IPFS_DB_NOT_CREATED, DAG_SYNCHER_NOT_LISTENING, CRDT_DATASTORE_NOT_CREATED, PUBSUB_BROADCASTER_NOT_CREATED, INVALID_PARAMETERS, GLOBALDB_NOT_STARTED}<br/>Enumeration of error codes used in the proof classes.  |
| using [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) | **[Buffer](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-buffer)**  |
| using [CrdtDatastore::QueryResult](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-queryresult) | **[QueryResult](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-queryresult)**  |
| using [storage::rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/) | **[RocksDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-rocksdb)**  |
| using [CrdtHeads::CRDTListResult](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#using-crdtlistresult) | **[CRDTHeadListResult](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-crdtheadlistresult)**  |
| using std::pair< [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/), [Buffer](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-buffer) > | **[DataPair](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-datapair)** <br/>Pair of key and value to be stored in CRDT.  |
| using [CrdtDatastore::CRDTElementFilterCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-crdtelementfiltercallback) | **[GlobalDBFilterCallback](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-globaldbfiltercallback)** <br/>CRDT Filter callback type.  |
| using [CrdtDatastore::CRDTNewElementCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-crdtnewelementcallback) | **[GlobalDBNewElementCallback](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-globaldbnewelementcallback)**  |
| using [CrdtDatastore::CRDTDeletedElementCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-crdtdeletedelementcallback) | **[GlobalDBDeletedElementCallback](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-globaldbdeletedelementcallback)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| outcome::result< std::shared_ptr< [GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-globaldb) > > | **[New](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-new)**(std::shared_ptr< boost::asio::io_context > context, std::string databasePath, std::shared_ptr< sgns::ipfs_pubsub::GossipPubSub > pubsub, std::shared_ptr< [CrdtOptions](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/) > crdtOptions, std::shared_ptr< sgns::ipfs_lite::ipfs::graphsync::Network > graphsyncnetwork, std::shared_ptr< libp2p::basic::Scheduler > scheduler, std::shared_ptr< sgns::ipfs_lite::ipfs::graphsync::RequestIdGenerator > generator, std::shared_ptr< [RocksDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-rocksdb) > datastore =nullptr, [BackupOptions](/source-reference/Classes/d3/d2a/structsgns_1_1crdt_1_1_global_d_b_1_1_backup_options/) backup_options =[BackupOptions](/source-reference/Classes/d3/d2a/structsgns_1_1crdt_1_1_global_d_b_1_1_backup_options/){ false, 15, 12, true })<br/>Factory method to create a [GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) instance.  |
| | **[~GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-~globaldb)**()<br/>Destructor or [GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/).  |
| outcome::result< CID > | **[Put](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-put)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & key, const [Buffer](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-buffer) & value, const std::unordered_set< std::string > & topics)<br/>Puts key-value pair to the CRDT store, optionally specifying a broadcast topic.  |
| outcome::result< CID > | **[Put](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-put)**(const std::vector< [DataPair](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-datapair) > & data_vector, const std::unordered_set< std::string > & topics)<br/>Writes a batch of CRDT data all at once.  |
| outcome::result< [Buffer](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-buffer) > | **[Get](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-get)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & key) |
| outcome::result< CID > | **[Remove](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-remove)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & key, const std::unordered_set< std::string > & topics) |
| outcome::result< [QueryResult](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-queryresult) > | **[QueryKeyValues](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-querykeyvalues)**(std::string_view keyPrefix) |
| outcome::result< [QueryResult](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-queryresult) > | **[QueryKeyValues](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-querykeyvalues)**(const std::string & prefix_base, const std::string & middle_part, const std::string & remainder_prefix)<br/>Queries with a middle part that can be a wildcard, negated string or normal string.  |
| outcome::result< std::string > | **[KeyToString](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-keytostring)**(const [Buffer](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-buffer) & key) const |
| std::shared_ptr< [AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/) > | **[BeginTransaction](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-begintransaction)**() |
| outcome::result< void > | **[AddBroadcastTopic](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-addbroadcasttopic)**(const std::string & topicName) |
| void | **[AddTopicName](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-addtopicname)**(const std::string & topicName) |
| void | **[AddListenTopic](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-addlistentopic)**(const std::string & topicName) |
| void | **[PrintDataStore](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-printdatastore)**() |
| std::shared_ptr< [RocksDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-rocksdb) > | **[GetDataStore](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-getdatastore)**() |
| std::shared_ptr< [sgns::crdt::PubSubBroadcasterExt](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/) > | **[GetBroadcaster](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-getbroadcaster)**() |
| std::shared_ptr< [CRDTWorkJournal](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/) > | **[GetWorkJournal](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-getworkjournal)**() const |
| bool | **[RegisterElementFilter](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-registerelementfilter)**(const std::string & pattern, [GlobalDBFilterCallback](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-globaldbfiltercallback) filter) |
| bool | **[RegisterNewElementCallback](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-registernewelementcallback)**(const std::string & pattern, [GlobalDBNewElementCallback](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-globaldbnewelementcallback) callback) |
| bool | **[RegisterDeletedElementCallback](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-registerdeletedelementcallback)**(const std::string & pattern, [GlobalDBDeletedElementCallback](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-globaldbdeletedelementcallback) callback) |
| void | **[UnregisterElementFilter](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-unregisterelementfilter)**(const std::string & pattern) |
| void | **[UnregisterNewElementCallback](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-unregisternewelementcallback)**(const std::string & pattern)<br/>Unregisters the new element callback for a pattern.  |
| void | **[UnregisterDeletedElementCallback](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-unregisterdeletedelementcallback)**(const std::string & pattern)<br/>Unregisters the deleted element callback for a pattern.  |
| void | **[Start](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-start)**()<br/>Starts the [GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) instance.  |
| void | **[ShutdownNow](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-shutdownnow)**()<br/>Immediately quiesce and shut down CRDT intake and workers. Safe to call multiple times.  |
| void | **[StartCIDReceiving](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-startcidreceiving)**()<br/>Starts receiving CIDs.  |
| void | **[StartCICSync](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-startcicsync)**()<br/>Starts CIC synchronization.  |
| void | **[StartRebroadcastHeads](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-startrebroadcastheads)**()<br/>Starts rebroadcasting heads.  |
| outcome::result< [CRDTHeadListResult](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-crdtheadlistresult) > | **[GetCRDTHeadList](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-getcrdtheadlist)**() |
| outcome::result< uint64_t > | **[GetCRDTHeadHeight](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-getcrdtheadheight)**(const CID & aCid, const std::string & topic) |
| outcome::result< void > | **[CRDTHeadRemove](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-crdtheadremove)**(const CID & aCid, const std::string & topic) |
| outcome::result< void > | **[CRDTHeadAdd](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-crdtheadadd)**(const CID & aCid, const std::string & topic, uint64_t priority) |
| outcome::result< [crdt::CrdtDatastore::JobStatus](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#enum-jobstatus) > | **[GetCIDJobStatus](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-getcidjobstatus)**(const CID & cid) const |
| outcome::result< void > | **[RequestHeadBroadcast](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-requestheadbroadcast)**(const std::set< std::string > & topics)<br/>Request head broadcast for specified topics.  |
| outcome::result< std::unordered_set< std::string > > | **[GetMonitoredTopics](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-getmonitoredtopics)**() const<br/>Get the topics that are being listened to.  |
| std::shared_ptr< [crdt::CrdtDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/) > | **[GetCRDTDataStore](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-getcrdtdatastore)**() |
| outcome::result< std::vector< std::pair< std::string, [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) > > > | **[GetCIDContent](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#function-getcidcontent)**(const std::string & cid_string) |

## Public Types Documentation

### enum Error

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| ROCKSDB_IO | 0| [RocksDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#using-rocksdb) wasn't opened.   |
| IPFS_DB_NOT_CREATED | | IPFS datastore not created.   |
| DAG_SYNCHER_NOT_LISTENING | | DAG Syncher listen error.   |
| CRDT_DATASTORE_NOT_CREATED | | CRDT DataStore not created.   |
| PUBSUB_BROADCASTER_NOT_CREATED | | CRDT DataStore not created.   |
| INVALID_PARAMETERS | | Invalid parameters.   |
| GLOBALDB_NOT_STARTED | | Start wasn't called.   |



Enumeration of error codes used in the proof classes. 

### using Buffer

```cpp
using sgns::crdt::GlobalDB::Buffer = base::Buffer;
```


### using QueryResult

```cpp
using sgns::crdt::GlobalDB::QueryResult = CrdtDatastore::QueryResult;
```


### using RocksDB

```cpp
using sgns::crdt::GlobalDB::RocksDB = storage::rocksdb;
```


### using CRDTHeadListResult

```cpp
using sgns::crdt::GlobalDB::CRDTHeadListResult = CrdtHeads::CRDTListResult;
```


### using DataPair

```cpp
using sgns::crdt::GlobalDB::DataPair = std::pair<HierarchicalKey, Buffer>;
```

Pair of key and value to be stored in CRDT. 

### using GlobalDBFilterCallback

```cpp
using sgns::crdt::GlobalDB::GlobalDBFilterCallback = CrdtDatastore::CRDTElementFilterCallback;
```

CRDT Filter callback type. 

### using GlobalDBNewElementCallback

```cpp
using sgns::crdt::GlobalDB::GlobalDBNewElementCallback = CrdtDatastore::CRDTNewElementCallback;
```


### using GlobalDBDeletedElementCallback

```cpp
using sgns::crdt::GlobalDB::GlobalDBDeletedElementCallback = CrdtDatastore::CRDTDeletedElementCallback;
```


## Public Functions Documentation

### function New

```cpp
static outcome::result< std::shared_ptr< GlobalDB > > New(
    std::shared_ptr< boost::asio::io_context > context,
    std::string databasePath,
    std::shared_ptr< sgns::ipfs_pubsub::GossipPubSub > pubsub,
    std::shared_ptr< CrdtOptions > crdtOptions,
    std::shared_ptr< sgns::ipfs_lite::ipfs::graphsync::Network > graphsyncnetwork,
    std::shared_ptr< libp2p::basic::Scheduler > scheduler,
    std::shared_ptr< sgns::ipfs_lite::ipfs::graphsync::RequestIdGenerator > generator,
    std::shared_ptr< RocksDB > datastore =nullptr,
    BackupOptions backup_options =BackupOptions{ false, 15, 12, true }
)
```

Factory method to create a [GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) instance. 

**Parameters**: 

  * **context** The io context used to run its inner methods 
  * **databasePath** Local system's path where data will be stored, not used if datastore is not nullptr 
  * **pubsub** The pubsub instance used to communicate 
  * **crdtOptions** CRDT options 
  * **graphsyncnetwork** The graphsync networks used 
  * **scheduler** libp2p scheduler 
  * **generator** The request ID generator from graphsync 
  * **datastore** datastore to be used. If not defined, created using databasePath 
  * **backup_options** configuration for automatic backups of the CRDT data 


**Return**: Instance of the [GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) initialized or [Error](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/#enum-error)

### function ~GlobalDB

```cpp
~GlobalDB()
```

Destructor or [GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/). 

### function Put

```cpp
outcome::result< CID > Put(
    const HierarchicalKey & key,
    const Buffer & value,
    const std::unordered_set< std::string > & topics
)
```

Puts key-value pair to the CRDT store, optionally specifying a broadcast topic. 

**Parameters**: 

  * **key** The hierarchical key where the value should be stored. 
  * **value** The value to store. 
  * **topics** Topics to publish to. 


**Return**: outcome::success on success, or outcome::failure otherwise. 

### function Put

```cpp
outcome::result< CID > Put(
    const std::vector< DataPair > & data_vector,
    const std::unordered_set< std::string > & topics
)
```

Writes a batch of CRDT data all at once. 

**Parameters**: 

  * **data_vector** A set of crdt to be written in a single transaction 
  * **topics** Topics to publish to. 


**Return**: outcome::failure on error or success otherwise 

### function Get

```cpp
outcome::result< Buffer > Get(
    const HierarchicalKey & key
)
```


**Parameters**: 

  * **key** - value key 


**Return**: value as a [Buffer](/source-reference/Classes/d5/d2a/class_buffer/)

Gets a value that corresponds to specified key. 


### function Remove

```cpp
outcome::result< CID > Remove(
    const HierarchicalKey & key,
    const std::unordered_set< std::string > & topics
)
```


**Parameters**: 

  * **key** to remove from storage 
  * **topics** Topics to publish to 


**Return**: outcome::failure on error or success otherwise 

Removes value for a given key. 


### function QueryKeyValues

```cpp
outcome::result< QueryResult > QueryKeyValues(
    std::string_view keyPrefix
)
```


**Parameters**: 

  * **keyPrefix** - keys prefix to match. An empty prefix matches any key. 


**Return**: list of key-value pairs matches prefix 

Queries CRDT key-value pairs by prefix. If the prefix is empty returns all elements that were not tombstoned 


### function QueryKeyValues

```cpp
outcome::result< QueryResult > QueryKeyValues(
    const std::string & prefix_base,
    const std::string & middle_part,
    const std::string & remainder_prefix
)
```

Queries with a middle part that can be a wildcard, negated string or normal string. 

**Parameters**: 

  * **prefix_base** The base prefix to query 
  * **middle_part** Either a string (normal query), '*' or !string 
  * **remainder_prefix** The remainder part of the query prefix 


**Return**: A list of key value pairs 

### function KeyToString

```cpp
outcome::result< std::string > KeyToString(
    const Buffer & key
) const
```


**Parameters**: 

  * **key** - binary key to convert 


**Return**: string represenation of a unique key part 

Converts a unique key part to a string representation 


### function BeginTransaction

```cpp
std::shared_ptr< AtomicTransaction > BeginTransaction()
```


**Return**: new transaction 

Create a transaction object 


### function AddBroadcastTopic

```cpp
outcome::result< void > AddBroadcastTopic(
    const std::string & topicName
)
```


### function AddTopicName

```cpp
void AddTopicName(
    const std::string & topicName
)
```


### function AddListenTopic

```cpp
void AddListenTopic(
    const std::string & topicName
)
```


### function PrintDataStore

```cpp
void PrintDataStore()
```


### function GetDataStore

```cpp
std::shared_ptr< RocksDB > GetDataStore()
```


### function GetBroadcaster

```cpp
std::shared_ptr< sgns::crdt::PubSubBroadcasterExt > GetBroadcaster()
```


### function GetWorkJournal

```cpp
std::shared_ptr< CRDTWorkJournal > GetWorkJournal() const
```


### function RegisterElementFilter

```cpp
bool RegisterElementFilter(
    const std::string & pattern,
    GlobalDBFilterCallback filter
)
```


**Parameters**: 

  * **pattern** The pattern to match elements against. 
  * **filter** The callback to invoke for matching elements. 


**Return**: true if the filter was successfully registered, false otherwise. 

Registers a filter callback for elements matching a pattern. 


### function RegisterNewElementCallback

```cpp
bool RegisterNewElementCallback(
    const std::string & pattern,
    GlobalDBNewElementCallback callback
)
```


**Parameters**: 

  * **pattern** The pattern to match new elements against. 
  * **callback** The callback to invoke for matching new elements. 


**Return**: true if the callback was successfully registered, false otherwise. 

Registers a callback for new elements matching a pattern. 


### function RegisterDeletedElementCallback

```cpp
bool RegisterDeletedElementCallback(
    const std::string & pattern,
    GlobalDBDeletedElementCallback callback
)
```


**Parameters**: 

  * **pattern** The pattern to match deleted elements against. 
  * **callback** The callback to invoke for matching deleted elements. 


**Return**: true if the callback was successfully registered, false otherwise. 

Registers a callback for deleted elements matching a pattern. 


### function UnregisterElementFilter

```cpp
void UnregisterElementFilter(
    const std::string & pattern
)
```


**Parameters**: 

  * **pattern** The pattern to unregister the filter for. 


Unregisters the filter callback for a pattern. 


### function UnregisterNewElementCallback

```cpp
void UnregisterNewElementCallback(
    const std::string & pattern
)
```

Unregisters the new element callback for a pattern. 

**Parameters**: 

  * **pattern** The pattern to unregister the new element callback for. 


### function UnregisterDeletedElementCallback

```cpp
void UnregisterDeletedElementCallback(
    const std::string & pattern
)
```

Unregisters the deleted element callback for a pattern. 

**Parameters**: 

  * **pattern** The pattern to unregister the deleted element callback for. 


### function Start

```cpp
void Start()
```

Starts the [GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) instance. 

### function ShutdownNow

```cpp
void ShutdownNow()
```

Immediately quiesce and shut down CRDT intake and workers. Safe to call multiple times. 

### function StartCIDReceiving

```cpp
void StartCIDReceiving()
```

Starts receiving CIDs. 

### function StartCICSync

```cpp
void StartCICSync()
```

Starts CIC synchronization. 

### function StartRebroadcastHeads

```cpp
void StartRebroadcastHeads()
```

Starts rebroadcasting heads. 

### function GetCRDTHeadList

```cpp
outcome::result< CRDTHeadListResult > GetCRDTHeadList()
```


### function GetCRDTHeadHeight

```cpp
outcome::result< uint64_t > GetCRDTHeadHeight(
    const CID & aCid,
    const std::string & topic
)
```


### function CRDTHeadRemove

```cpp
outcome::result< void > CRDTHeadRemove(
    const CID & aCid,
    const std::string & topic
)
```


### function CRDTHeadAdd

```cpp
outcome::result< void > CRDTHeadAdd(
    const CID & aCid,
    const std::string & topic,
    uint64_t priority
)
```


### function GetCIDJobStatus

```cpp
outcome::result< crdt::CrdtDatastore::JobStatus > GetCIDJobStatus(
    const CID & cid
) const
```


### function RequestHeadBroadcast

```cpp
outcome::result< void > RequestHeadBroadcast(
    const std::set< std::string > & topics
)
```

Request head broadcast for specified topics. 

**Parameters**: 

  * **topics** Vector of topic names to broadcast heads for 


**Return**: outcome::success on success, or outcome::failure on error 

### function GetMonitoredTopics

```cpp
outcome::result< std::unordered_set< std::string > > GetMonitoredTopics() const
```

Get the topics that are being listened to. 

**Return**: A set of the monitored topic names 

### function GetCRDTDataStore

```cpp
std::shared_ptr< crdt::CrdtDatastore > GetCRDTDataStore()
```


### function GetCIDContent

```cpp
outcome::result< std::vector< std::pair< std::string, base::Buffer > > > GetCIDContent(
    const std::string & cid_string
)
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
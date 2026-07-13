---
title: sgns::crdt::CRDTCallbackManager

---

# sgns::crdt::CRDTCallbackManager






`#include <crdt_callback_manager.hpp>`

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[NewDataCallbackEntry](/source-reference/Classes/d3/d91/structsgns_1_1crdt_1_1_c_r_d_t_callback_manager_1_1_new_data_callback_entry/)**  |
| struct | **[DeletedDataCallbackEntry](/source-reference/Classes/de/d54/structsgns_1_1crdt_1_1_c_r_d_t_callback_manager_1_1_deleted_data_callback_entry/)**  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::pair< std::string, [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) > | **[NewDataPair](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#using-newdatapair)**  |
| using std::function< void([NewDataPair](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#using-newdatapair) new_data, std::string cid)> | **[NewDataCallback](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#using-newdatacallback)**  |
| using std::vector< std::shared_ptr< const [NewDataCallbackEntry](/source-reference/Classes/d3/d91/structsgns_1_1crdt_1_1_c_r_d_t_callback_manager_1_1_new_data_callback_entry/) > > | **[NewDataCallbackRegistry](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#using-newdatacallbackregistry)**  |
| using std::function< void(std::string deleted_key, std::string cid)> | **[DeletedDataCallback](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#using-deleteddatacallback)**  |
| using std::vector< std::shared_ptr< const [DeletedDataCallbackEntry](/source-reference/Classes/de/d54/structsgns_1_1crdt_1_1_c_r_d_t_callback_manager_1_1_deleted_data_callback_entry/) > > | **[DeletedDataCallbackRegistry](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#using-deleteddatacallbackregistry)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CRDTCallbackManager](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#function-crdtcallbackmanager)**(std::shared_ptr< [CRDTWorkJournal](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/) > work_journal)<br/>Construct a new [CRDTCallbackManager](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/) object.  |
| | **[~CRDTCallbackManager](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#function-~crdtcallbackmanager)**()<br/>Destroy the [CRDTCallbackManager](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/) object.  |
| bool | **[RegisterNewDataCallback](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#function-registernewdatacallback)**(const std::string & pattern, [NewDataCallback](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#using-newdatacallback) callback)<br/>Registers a callback for when new data gets recorded to a specific pattern.  |
| bool | **[RegisterDeletedDataCallback](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#function-registerdeleteddatacallback)**(const std::string & pattern, [DeletedDataCallback](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#using-deleteddatacallback) callback)<br/>Registers a callback for when data gets deleted to a specific pattern.  |
| void | **[UnregisterNewDataCallback](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#function-unregisternewdatacallback)**(const std::string & pattern)<br/>Removes a previously registered new data callback.  |
| void | **[UnregisterDeletedDataCallback](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#function-unregisterdeleteddatacallback)**(const std::string & pattern)<br/>Removes a previously registered deleted data callback.  |
| void | **[PutDataCallback](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#function-putdatacallback)**(const std::string & key, const [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) & value, const std::string & cid)<br/>Executes a registered new data callback that matches the key.  |
| void | **[DeleteDataCallback](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#function-deletedatacallback)**(const std::string & deleted_key, const std::string & cid)<br/>Executes a registered deleted data callback that matches the key.  |

## Public Types Documentation

### using NewDataPair

```cpp
using sgns::crdt::CRDTCallbackManager::NewDataPair = std::pair<std::string, base::Buffer>;
```


### using NewDataCallback

```cpp
using sgns::crdt::CRDTCallbackManager::NewDataCallback = std::function<void( NewDataPair new_data, std::string cid )>;
```


### using NewDataCallbackRegistry

```cpp
using sgns::crdt::CRDTCallbackManager::NewDataCallbackRegistry = std::vector<std::shared_ptr<const NewDataCallbackEntry>>;
```


### using DeletedDataCallback

```cpp
using sgns::crdt::CRDTCallbackManager::DeletedDataCallback = std::function<void( std::string deleted_key, std::string cid )>;
```


### using DeletedDataCallbackRegistry

```cpp
using sgns::crdt::CRDTCallbackManager::DeletedDataCallbackRegistry = std::vector<std::shared_ptr<const DeletedDataCallbackEntry>>;
```


## Public Functions Documentation

### function CRDTCallbackManager

```cpp
explicit CRDTCallbackManager(
    std::shared_ptr< CRDTWorkJournal > work_journal
)
```

Construct a new [CRDTCallbackManager](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/) object. 

### function ~CRDTCallbackManager

```cpp
~CRDTCallbackManager()
```

Destroy the [CRDTCallbackManager](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/) object. 

### function RegisterNewDataCallback

```cpp
bool RegisterNewDataCallback(
    const std::string & pattern,
    NewDataCallback callback
)
```

Registers a callback for when new data gets recorded to a specific pattern. 

**Parameters**: 

  * **pattern** Regex pattern that the key should match to call the callback 
  * **callback** The callback itself 


**Return**: true if registered, false otherwise 

### function RegisterDeletedDataCallback

```cpp
bool RegisterDeletedDataCallback(
    const std::string & pattern,
    DeletedDataCallback callback
)
```

Registers a callback for when data gets deleted to a specific pattern. 

**Parameters**: 

  * **pattern** Regex pattern that the key should match to call the callback 
  * **callback** The callback itself 


**Return**: true if registered, false otherwise 

### function UnregisterNewDataCallback

```cpp
void UnregisterNewDataCallback(
    const std::string & pattern
)
```

Removes a previously registered new data callback. 

**Parameters**: 

  * **pattern** The pattern of the callback to be deleted 


### function UnregisterDeletedDataCallback

```cpp
void UnregisterDeletedDataCallback(
    const std::string & pattern
)
```

Removes a previously registered deleted data callback. 

**Parameters**: 

  * **pattern** The pattern of the callback to be deleted 


### function PutDataCallback

```cpp
void PutDataCallback(
    const std::string & key,
    const base::Buffer & value,
    const std::string & cid
)
```

Executes a registered new data callback that matches the key. 

**Parameters**: 

  * **key** key of the CRDT 
  * **value** value contained on the key 
  * **cid** content identifier associated with the value 


### function DeleteDataCallback

```cpp
void DeleteDataCallback(
    const std::string & deleted_key,
    const std::string & cid
)
```

Executes a registered deleted data callback that matches the key. 

**Parameters**: 

  * **deleted_key** key of the CRDT that was deleted 
  * **cid** content identifier associated with the deletion 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
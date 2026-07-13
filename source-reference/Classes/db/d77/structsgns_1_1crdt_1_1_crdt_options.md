---
title: sgns::crdt::CrdtOptions
summary: Options holds configurable values for CrdtDatastore. 

---

# sgns::crdt::CrdtOptions



Options holds configurable values for [CrdtDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/). 


`#include <crdt_options.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[VerifyErrorCode](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#enum-verifyerrorcode)** { Success = 0, InvalidRebroadcastInterval, LoggerUndefinied, BadNumberOfNumWorkers, InvalidDAGSyncerTimeout} |
| using [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) | **[Buffer](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#using-buffer)**  |
| using [base::Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) | **[Logger](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#using-logger)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [CrdtOptions](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/) > | **[DefaultOptions](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#function-defaultoptions)**() |
| outcome::result< [VerifyErrorCode](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#enum-verifyerrorcode) > | **[Verify](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#function-verify)**() const |
| bool | **[operator==](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#function-operator==)**(const [CrdtOptions](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/) & rhs) const |
| bool | **[operator!=](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#function-operator!=)**(const [CrdtOptions](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/) & rhs) const |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [Logger](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#using-logger) | **[logger](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#variable-logger)**  |
| long long | **[rebroadcastIntervalMilliseconds](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#variable-rebroadcastintervalmilliseconds)**  |
| long long | **[dagSyncerTimeoutSec](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#variable-dagsyncertimeoutsec)**  |
| int | **[numWorkers](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/#variable-numworkers)**  |

## Public Types Documentation

### enum VerifyErrorCode

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| Success | 0|   |
| InvalidRebroadcastInterval | |   |
| LoggerUndefinied | |   |
| BadNumberOfNumWorkers | |   |
| InvalidDAGSyncerTimeout | |   |




### using Buffer

```cpp
using sgns::crdt::CrdtOptions::Buffer = base::Buffer;
```


### using Logger

```cpp
using sgns::crdt::CrdtOptions::Logger = base::Logger;
```


## Public Functions Documentation

### function DefaultOptions

```cpp
static inline std::shared_ptr< CrdtOptions > DefaultOptions()
```


### function Verify

```cpp
inline outcome::result< VerifyErrorCode > Verify() const
```


Verifies [CrdtOptions](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/)


### function operator==

```cpp
inline bool operator==(
    const CrdtOptions & rhs
) const
```


### function operator!=

```cpp
inline bool operator!=(
    const CrdtOptions & rhs
) const
```


## Public Attributes Documentation

### variable logger

```cpp
Logger logger = nullptr;
```


### variable rebroadcastIntervalMilliseconds

```cpp
long long rebroadcastIntervalMilliseconds = 0;
```


RebroadcastInterval specifies interval to rebroadcast data 


### variable dagSyncerTimeoutSec

```cpp
long long dagSyncerTimeoutSec = 0;
```


DAGSyncerTimeout specifies how long to wait for a [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/). Set to 0 to disable. 


### variable numWorkers

```cpp
int numWorkers = 0;
```


NumWorkers specifies the number of workers ready to walk DAGs 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: sgns::crdt::CrdtDatastore::DagWorker

---

# sgns::crdt::CrdtDatastore::DagWorker



 [More...](#detailed-description)


`#include <crdt_datastore.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::future< void > | **[dagWorkerFuture_](/source-reference/Classes/db/d23/structsgns_1_1crdt_1_1_crdt_datastore_1_1_dag_worker/#variable-dagworkerfuture_)**  |
| std::atomic< bool > | **[dagWorkerThreadRunning_](/source-reference/Classes/db/d23/structsgns_1_1crdt_1_1_crdt_datastore_1_1_dag_worker/#variable-dagworkerthreadrunning_)**  |
| std::thread::id | **[threadId_](/source-reference/Classes/db/d23/structsgns_1_1crdt_1_1_crdt_datastore_1_1_dag_worker/#variable-threadid_)**  |

## Detailed Description

```cpp
struct sgns::crdt::CrdtDatastore::DagWorker;
```


DAG worker structure to keep track of worker threads 

## Public Attributes Documentation

### variable dagWorkerFuture_

```cpp
std::future< void > dagWorkerFuture_;
```


### variable dagWorkerThreadRunning_

```cpp
std::atomic< bool > dagWorkerThreadRunning_ = false;
```


### variable threadId_

```cpp
std::thread::id threadId_;
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
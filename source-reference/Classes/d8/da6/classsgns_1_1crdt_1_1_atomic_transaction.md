---
title: sgns::crdt::AtomicTransaction
summary: AtomicTransaction provides atomic multi-key operations for CRDT datastore All operations within a transaction are combined into a single delta and published atomically to ensure consistency. 

---

# sgns::crdt::AtomicTransaction



[AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/) provides atomic multi-key operations for CRDT datastore All operations within a transaction are combined into a single delta and published atomically to ensure consistency. 


`#include <atomic_transaction.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| using [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) | **[Buffer](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#using-buffer)**  |
| using pb::Delta | **[Delta](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#using-delta)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#function-atomictransaction)**(std::shared_ptr< [CrdtDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/) > datastore)<br/>Constructor for [AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/).  |
| | **[~AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#function-~atomictransaction)**()<br/>Destructor ensures rollback if not committed.  |
| outcome::result< void > | **[Put](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#function-put)**([HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) key, [Buffer](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#using-buffer) value)<br/>Add a key-value pair to the transaction.  |
| outcome::result< void > | **[Remove](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#function-remove)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & key)<br/>Delete a key in the transaction.  |
| outcome::result< [Buffer](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#using-buffer) > | **[Get](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#function-get)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & key) const<br/>Get a value for a key.  |
| outcome::result< void > | **[Erase](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#function-erase)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & key)<br/>Erase a key from the transaction (alias for Remove).  |
| bool | **[HasKey](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#function-haskey)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & key) const<br/>Check if a key has been modified in this transaction.  |
| outcome::result< void > | **[AddTopic](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#function-addtopic)**(const std::string & topic)<br/>Add a single topic to this transaction's internal topic set.  |
| outcome::result< void > | **[AddTopics](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#function-addtopics)**(const std::unordered_set< std::string > & topics)<br/>Add multiple topics to this transaction's internal topic set.  |
| outcome::result< CID > | **[Commit](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#function-commit)**(const std::unordered_set< std::string > & topics)<br/>Commits all pending operations atomically. Combines all pending operations into a single [Delta](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#using-delta) and publishes it.  |

## Public Types Documentation

### using Buffer

```cpp
using sgns::crdt::AtomicTransaction::Buffer = base::Buffer;
```


### using Delta

```cpp
using sgns::crdt::AtomicTransaction::Delta = pb::Delta;
```


## Public Functions Documentation

### function AtomicTransaction

```cpp
explicit AtomicTransaction(
    std::shared_ptr< CrdtDatastore > datastore
)
```

Constructor for [AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/). 

**Parameters**: 

  * **datastore** pointer to CRDT datastore 


### function ~AtomicTransaction

```cpp
~AtomicTransaction()
```

Destructor ensures rollback if not committed. 

### function Put

```cpp
outcome::result< void > Put(
    HierarchicalKey key,
    Buffer value
)
```

Add a key-value pair to the transaction. 

**Parameters**: 

  * **key** hierarchical key to add 
  * **value** buffer value to store 


**Return**: outcome::success or failure if already committed 

### function Remove

```cpp
outcome::result< void > Remove(
    const HierarchicalKey & key
)
```

Delete a key in the transaction. 

**Parameters**: 

  * **key** hierarchical key to remove 


**Return**: outcome::success or failure if already committed 

### function Get

```cpp
outcome::result< Buffer > Get(
    const HierarchicalKey & key
) const
```

Get a value for a key. 

**Parameters**: 

  * **key** hierarchical key to retrieve 


**Return**: [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) containing the value if found, or error if not found/committed 

**Note**: This method checks pending operations first, then falls back to datastore 

### function Erase

```cpp
outcome::result< void > Erase(
    const HierarchicalKey & key
)
```

Erase a key from the transaction (alias for Remove). 

**Parameters**: 

  * **key** hierarchical key to erase 


**Return**: outcome::success or failure if already committed 

### function HasKey

```cpp
bool HasKey(
    const HierarchicalKey & key
) const
```

Check if a key has been modified in this transaction. 

**Parameters**: 

  * **key** hierarchical key to check 


**Return**: true if key has pending operations in this transaction 

### function AddTopic

```cpp
outcome::result< void > AddTopic(
    const std::string & topic
)
```

Add a single topic to this transaction's internal topic set. 

**Parameters**: 

  * **topic** topic name to add 


**Return**: outcome::success or failure if already committed 

### function AddTopics

```cpp
outcome::result< void > AddTopics(
    const std::unordered_set< std::string > & topics
)
```

Add multiple topics to this transaction's internal topic set. 

**Parameters**: 

  * **topics** topic names to add 


**Return**: outcome::success or failure if already committed 

### function Commit

```cpp
outcome::result< CID > Commit(
    const std::unordered_set< std::string > & topics
)
```

Commits all pending operations atomically. Combines all pending operations into a single [Delta](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/#using-delta) and publishes it. 

**Parameters**: 

  * **topics** Optional topic name for targeted publishing. If not provided, the default broadcast behavior is used. 


**Return**: outcome::success on successful commit, or outcome::failure if an error occurs. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
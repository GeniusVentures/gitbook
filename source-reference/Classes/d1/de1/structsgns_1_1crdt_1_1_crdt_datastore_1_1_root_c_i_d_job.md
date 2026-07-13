---
title: sgns::crdt::CrdtDatastore::RootCIDJob

---

# sgns::crdt::CrdtDatastore::RootCIDJob






`#include <crdt_datastore.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [IPLDNode](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-ipldnode) > | **[node_](/source-reference/Classes/d1/de1/structsgns_1_1crdt_1_1_crdt_datastore_1_1_root_c_i_d_job/#variable-node_)** <br/>Current node to process.  |
| std::shared_ptr< [IPLDNode](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-ipldnode) > | **[root_node_](/source-reference/Classes/d1/de1/structsgns_1_1crdt_1_1_crdt_datastore_1_1_root_c_i_d_job/#variable-root_node_)** <br/>Root node of the Job.  |
| bool | **[created_by_self_](/source-reference/Classes/d1/de1/structsgns_1_1crdt_1_1_crdt_datastore_1_1_root_c_i_d_job/#variable-created_by_self_)** <br/>True if the root node was created by self.  |

## Public Attributes Documentation

### variable node_

```cpp
std::shared_ptr< IPLDNode > node_;
```

Current node to process. 

### variable root_node_

```cpp
std::shared_ptr< IPLDNode > root_node_;
```

Root node of the Job. 

### variable created_by_self_

```cpp
bool created_by_self_;
```

True if the root node was created by self. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
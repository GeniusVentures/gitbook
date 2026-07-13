---
title: sgns::crdt::GraphsyncDAGSyncer::LRUCIDCache

---

# sgns::crdt::GraphsyncDAGSyncer::LRUCIDCache





## Public Functions

|                | Name           |
| -------------- | -------------- |
| void | **[init](/source-reference/Classes/d9/d91/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_l_r_u_c_i_d_cache/#function-init)**(const CID & cid) |
| bool | **[add](/source-reference/Classes/d9/d91/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_l_r_u_c_i_d_cache/#function-add)**(const CID & cid, std::shared_ptr< ipfs_lite::ipld::IPLDNode > node) |
| std::shared_ptr< ipfs_lite::ipld::IPLDNode > | **[get](/source-reference/Classes/d9/d91/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_l_r_u_c_i_d_cache/#function-get)**(const CID & cid) |
| bool | **[remove](/source-reference/Classes/d9/d91/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_l_r_u_c_i_d_cache/#function-remove)**(const CID & cid) |
| bool | **[contains](/source-reference/Classes/d9/d91/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_l_r_u_c_i_d_cache/#function-contains)**(const CID & cid) const |
| bool | **[hasContent](/source-reference/Classes/d9/d91/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_l_r_u_c_i_d_cache/#function-hascontent)**(const CID & cid) const |
| size_t | **[size](/source-reference/Classes/d9/d91/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_l_r_u_c_i_d_cache/#function-size)**() const |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| size_t | **[MAX_CACHE_SIZE](/source-reference/Classes/d9/d91/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_l_r_u_c_i_d_cache/#variable-max_cache_size)**  |
| std::map< CID, std::pair< std::shared_ptr< ipfs_lite::ipld::IPLDNode >, std::list< CID >::iterator > > | **[cache_map_](/source-reference/Classes/d9/d91/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_l_r_u_c_i_d_cache/#variable-cache_map_)**  |
| std::list< CID > | **[lru_list_](/source-reference/Classes/d9/d91/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_l_r_u_c_i_d_cache/#variable-lru_list_)**  |
| std::mutex | **[mutex_](/source-reference/Classes/d9/d91/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_l_r_u_c_i_d_cache/#variable-mutex_)**  |

## Public Functions Documentation

### function init

```cpp
void init(
    const CID & cid
)
```


### function add

```cpp
bool add(
    const CID & cid,
    std::shared_ptr< ipfs_lite::ipld::IPLDNode > node
)
```


### function get

```cpp
std::shared_ptr< ipfs_lite::ipld::IPLDNode > get(
    const CID & cid
)
```


### function remove

```cpp
bool remove(
    const CID & cid
)
```


### function contains

```cpp
bool contains(
    const CID & cid
) const
```


### function hasContent

```cpp
bool hasContent(
    const CID & cid
) const
```


### function size

```cpp
inline size_t size() const
```


## Public Attributes Documentation

### variable MAX_CACHE_SIZE

```cpp
static size_t MAX_CACHE_SIZE = 250;
```


### variable cache_map_

```cpp
std::map< CID, std::pair< std::shared_ptr< ipfs_lite::ipld::IPLDNode >, std::list< CID >::iterator > > cache_map_;
```


### variable lru_list_

```cpp
std::list< CID > lru_list_;
```


### variable mutex_

```cpp
std::mutex mutex_;
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
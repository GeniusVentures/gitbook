---
title: sgns::crdt::DAGSyncer
summary: A DAGSyncer is an abstraction to an IPLD-based p2p storage layer. A DAGSyncer is a DAGService with the ability to publish new ipld nodes to the network, and retrieving others from it. 

---

# sgns::crdt::DAGSyncer



A [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/) is an abstraction to an IPLD-based p2p storage layer. A [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/) is a DAGService with the ability to publish new ipld nodes to the network, and retrieving others from it. 


`#include <dagsyncer.hpp>`

Inherits from ipfs_lite::ipfs::merkledag::MerkleDagService

Inherited by [sgns::crdt::GraphsyncDAGSyncer](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/)

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::pair< CID, std::string > | **[LinkInfoPair](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#using-linkinfopair)**  |
| using std::set< [LinkInfoPair](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#using-linkinfopair) > | **[LinkInfoSet](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#using-linkinfoset)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual outcome::result< bool > | **[HasBlock](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-hasblock)**(const CID & cid) const =0 |
| virtual outcome::result< std::shared_ptr< ipfs_lite::ipld::IPLDNode > > | **[GetNodeWithoutRequest](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-getnodewithoutrequest)**(const CID & cid) const =0 |
| virtual std::pair< [LinkInfoSet](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#using-linkinfoset), [LinkInfoSet](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#using-linkinfoset) > | **[TraverseCIDsLinks](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-traversecidslinks)**(ipfs_lite::ipld::IPLDNode & node, std::string link_name, [LinkInfoSet](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#using-linkinfoset) visited_links) const =0 |
| virtual void | **[InitCIDBlock](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-initcidblock)**(const CID & cid) =0 |
| virtual bool | **[IsCIDInCache](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-iscidincache)**(const CID & cid) const =0 |
| virtual outcome::result< void > | **[DeleteCIDBlock](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-deletecidblock)**(const CID & cid) =0 |
| virtual void | **[Stop](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-stop)**() =0 |
| virtual IPFS::outcome::result< void > | **[markResolved](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-markresolved)**(const CID & cid) =0 |
| virtual IPFS::outcome::result< bool > | **[isResolved](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-isresolved)**(const CID & cid) const =0 |

## Public Types Documentation

### using LinkInfoPair

```cpp
using sgns::crdt::DAGSyncer::LinkInfoPair = std::pair<CID, std::string>;
```


### using LinkInfoSet

```cpp
using sgns::crdt::DAGSyncer::LinkInfoSet = std::set<LinkInfoPair>;
```


## Public Functions Documentation

### function HasBlock

```cpp
virtual outcome::result< bool > HasBlock(
    const CID & cid
) const =0
```


**Parameters**: 

  * **cid** Content identifier of the node 


**Return**: true if the block is locally available or outcome::failure on error 

**Reimplemented by**: [sgns::crdt::GraphsyncDAGSyncer::HasBlock](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-hasblock)


Check if the block with cid is locally available (therefore, it is considered processed). 


### function GetNodeWithoutRequest

```cpp
virtual outcome::result< std::shared_ptr< ipfs_lite::ipld::IPLDNode > > GetNodeWithoutRequest(
    const CID & cid
) const =0
```


**Reimplemented by**: [sgns::crdt::GraphsyncDAGSyncer::GetNodeWithoutRequest](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-getnodewithoutrequest)


### function TraverseCIDsLinks

```cpp
virtual std::pair< LinkInfoSet, LinkInfoSet > TraverseCIDsLinks(
    ipfs_lite::ipld::IPLDNode & node,
    std::string link_name,
    LinkInfoSet visited_links
) const =0
```


**Reimplemented by**: [sgns::crdt::GraphsyncDAGSyncer::TraverseCIDsLinks](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-traversecidslinks)


### function InitCIDBlock

```cpp
virtual void InitCIDBlock(
    const CID & cid
) =0
```


**Reimplemented by**: [sgns::crdt::GraphsyncDAGSyncer::InitCIDBlock](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-initcidblock)


### function IsCIDInCache

```cpp
virtual bool IsCIDInCache(
    const CID & cid
) const =0
```


**Reimplemented by**: [sgns::crdt::GraphsyncDAGSyncer::IsCIDInCache](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-iscidincache)


### function DeleteCIDBlock

```cpp
virtual outcome::result< void > DeleteCIDBlock(
    const CID & cid
) =0
```


**Reimplemented by**: [sgns::crdt::GraphsyncDAGSyncer::DeleteCIDBlock](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-deletecidblock)


### function Stop

```cpp
virtual void Stop() =0
```


**Reimplemented by**: [sgns::crdt::GraphsyncDAGSyncer::Stop](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-stop)


### function markResolved

```cpp
virtual IPFS::outcome::result< void > markResolved(
    const CID & cid
) =0
```


**Reimplemented by**: [sgns::crdt::GraphsyncDAGSyncer::markResolved](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-markresolved)


### function isResolved

```cpp
virtual IPFS::outcome::result< bool > isResolved(
    const CID & cid
) const =0
```


**Reimplemented by**: [sgns::crdt::GraphsyncDAGSyncer::isResolved](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-isresolved)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
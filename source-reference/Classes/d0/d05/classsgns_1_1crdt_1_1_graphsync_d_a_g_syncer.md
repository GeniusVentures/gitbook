---
title: sgns::crdt::GraphsyncDAGSyncer
summary: A DAGSyncer is an abstraction to an IPLD-based p2p storage layer. A DAGSyncer is a DAGService with the ability to publish new ipld nodes to the network, and retrieving others from it. 

---

# sgns::crdt::GraphsyncDAGSyncer



A [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/) is an abstraction to an IPLD-based p2p storage layer. A [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/) is a DAGService with the ability to publish new ipld nodes to the network, and retrieving others from it. 


`#include <graphsync_dagsyncer.hpp>`

Inherits from [sgns::crdt::DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/), std::enable_shared_from_this< GraphsyncDAGSyncer >

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[BlacklistEntry](/source-reference/Classes/d8/dea/structsgns_1_1crdt_1_1_graphsync_d_a_g_syncer_1_1_blacklist_entry/)**  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class uint8_t | **[Error](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#enum-error)** { CID_NOT_FOUND = 0, ROUTE_NOT_FOUND, PEER_BLACKLISTED, TIMED_OUT, DAGSYNCER_NOT_STARTED, GRAPHSYNC_IS_NULL, HOST_IS_NULL} |
| using ipfs_lite::ipfs::IpfsDatastore | **[IpfsDatastore](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-ipfsdatastore)**  |
| using ipfs_lite::ipfs::graphsync::Graphsync | **[Graphsync](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-graphsync)**  |
| using ipfs_lite::ipfs::graphsync::ResponseMetadata | **[ResponseMetadata](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-responsemetadata)**  |
| using ipfs_lite::ipfs::graphsync::Extension | **[Extension](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-extension)**  |
| using ipfs_lite::ipfs::graphsync::ResponseStatusCode | **[ResponseStatusCode](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-responsestatuscode)**  |
| using libp2p::multi::Multiaddress | **[Multiaddress](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-multiaddress)**  |
| using libp2p::multi::Multihash | **[Multihash](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-multihash)**  |
| using libp2p::peer::PeerId | **[PeerId](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-peerid)**  |
| using libp2p::protocol::Subscription | **[Subscription](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-subscription)**  |
| using [base::Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) | **[Logger](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-logger)**  |
| using Graphsync::BlockCallback | **[BlockCallback](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-blockcallback)**  |
| using size_t | **[PeerKey](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-peerkey)**  |
| using std::pair< [PeerId](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-peerid), std::vector< [Multiaddress](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-multiaddress) > > | **[PeerEntry](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-peerentry)**  |
| using std::map< CID, std::vector< [PeerKey](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-peerkey) > > | **[RouteMapType](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-routemaptype)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[GraphsyncDAGSyncer](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-graphsyncdagsyncer)**(std::shared_ptr< [IpfsDatastore](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-ipfsdatastore) > service, std::shared_ptr< [Graphsync](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-graphsync) > graphsync, std::shared_ptr< libp2p::Host > host) |
| | **[~GraphsyncDAGSyncer](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-~graphsyncdagsyncer)**() override |
| outcome::result< void > | **[Listen](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-listen)**(const [Multiaddress](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-multiaddress) & listen_to) |
| outcome::result< void > | **[StartSync](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-startsync)**() |
| void | **[AddRoute](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-addroute)**(const CID & cid, const [PeerId](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-peerid) & peer, std::vector< [Multiaddress](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-multiaddress) > address) |
| outcome::result< void > | **[addNode](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-addnode)**(std::shared_ptr< const ipfs_lite::ipld::IPLDNode > node) override |
| outcome::result< std::shared_ptr< ipfs_lite::ipld::IPLDNode > > | **[getNode](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-getnode)**(const CID & cid) const override |
| outcome::result< void > | **[removeNode](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-removenode)**(const CID & cid) override |
| outcome::result< size_t > | **[select](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-select)**(gsl::span< const uint8_t > root_cid, gsl::span< const uint8_t > selector, std::function< bool(std::shared_ptr< const ipfs_lite::ipld::IPLDNode > node)> handler) const override |
| outcome::result< std::shared_ptr< ipfs_lite::ipfs::merkledag::Leaf > > | **[fetchGraph](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-fetchgraph)**(const CID & cid) const override |
| outcome::result< std::shared_ptr< ipfs_lite::ipfs::merkledag::Leaf > > | **[fetchGraphOnDepth](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-fetchgraphondepth)**(const CID & cid, uint64_t depth) const override |
| virtual outcome::result< bool > | **[HasBlock](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-hasblock)**(const CID & cid) const override |
| virtual outcome::result< std::shared_ptr< ipfs_lite::ipld::IPLDNode > > | **[GetNodeWithoutRequest](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-getnodewithoutrequest)**(const CID & cid) const override |
| outcome::result< std::shared_ptr< ipfs_lite::ipld::IPLDNode > > | **[GetNodeFromMerkleDAG](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-getnodefrommerkledag)**(const CID & cid) const |
| virtual std::pair< [LinkInfoSet](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#using-linkinfoset), [LinkInfoSet](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#using-linkinfoset) > | **[TraverseCIDsLinks](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-traversecidslinks)**(ipfs_lite::ipld::IPLDNode & node, std::string link_name ="", [LinkInfoSet](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#using-linkinfoset) visited ={}) const override |
| virtual outcome::result< void > | **[markResolved](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-markresolved)**(const CID & cid) override |
| virtual outcome::result< bool > | **[isResolved](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-isresolved)**(const CID & cid) const override |
| outcome::result< [PeerId](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-peerid) > | **[GetId](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-getid)**() const |
| outcome::result< libp2p::peer::PeerInfo > | **[GetPeerInfo](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-getpeerinfo)**() const |
| void | **[AddToBlackList](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-addtoblacklist)**(const [PeerId](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-peerid) & peer) const |
| bool | **[IsOnBlackList](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-isonblacklist)**(const [PeerId](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-peerid) & peer) const |
| virtual void | **[InitCIDBlock](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-initcidblock)**(const CID & cid) override |
| virtual bool | **[IsCIDInCache](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-iscidincache)**(const CID & cid) const override |
| virtual outcome::result< void > | **[DeleteCIDBlock](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-deletecidblock)**(const CID & cid) override |
| virtual void | **[Stop](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#function-stop)**() override |

## Additional inherited members

**Public Types inherited from [sgns::crdt::DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/)**

|                | Name           |
| -------------- | -------------- |
| using std::pair< CID, std::string > | **[LinkInfoPair](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#using-linkinfopair)**  |
| using std::set< [LinkInfoPair](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#using-linkinfopair) > | **[LinkInfoSet](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#using-linkinfoset)**  |


## Public Types Documentation

### enum Error

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| CID_NOT_FOUND | 0| The requested CID wasn't found.   |
| ROUTE_NOT_FOUND | | Route for the CID wasn't found.   |
| PEER_BLACKLISTED | | The peer that has the CID is blacklisted.   |
| TIMED_OUT | | The request has timed out.   |
| DAGSYNCER_NOT_STARTED | | Start wasn't called, or StopSync was called.   |
| GRAPHSYNC_IS_NULL | | [Graphsync](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-graphsync) member is nullptr.   |
| HOST_IS_NULL | | [Graphsync](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/#using-graphsync) member is nullptr.   |




### using IpfsDatastore

```cpp
using sgns::crdt::GraphsyncDAGSyncer::IpfsDatastore = ipfs_lite::ipfs::IpfsDatastore;
```


### using Graphsync

```cpp
using sgns::crdt::GraphsyncDAGSyncer::Graphsync = ipfs_lite::ipfs::graphsync::Graphsync;
```


### using ResponseMetadata

```cpp
using sgns::crdt::GraphsyncDAGSyncer::ResponseMetadata = ipfs_lite::ipfs::graphsync::ResponseMetadata;
```


### using Extension

```cpp
using sgns::crdt::GraphsyncDAGSyncer::Extension = ipfs_lite::ipfs::graphsync::Extension;
```


### using ResponseStatusCode

```cpp
using sgns::crdt::GraphsyncDAGSyncer::ResponseStatusCode = ipfs_lite::ipfs::graphsync::ResponseStatusCode;
```


### using Multiaddress

```cpp
using sgns::crdt::GraphsyncDAGSyncer::Multiaddress = libp2p::multi::Multiaddress;
```


### using Multihash

```cpp
using sgns::crdt::GraphsyncDAGSyncer::Multihash = libp2p::multi::Multihash;
```


### using PeerId

```cpp
using sgns::crdt::GraphsyncDAGSyncer::PeerId = libp2p::peer::PeerId;
```


### using Subscription

```cpp
using sgns::crdt::GraphsyncDAGSyncer::Subscription = libp2p::protocol::Subscription;
```


### using Logger

```cpp
using sgns::crdt::GraphsyncDAGSyncer::Logger = base::Logger;
```


### using BlockCallback

```cpp
using sgns::crdt::GraphsyncDAGSyncer::BlockCallback = Graphsync::BlockCallback;
```


### using PeerKey

```cpp
using sgns::crdt::GraphsyncDAGSyncer::PeerKey = size_t;
```


### using PeerEntry

```cpp
using sgns::crdt::GraphsyncDAGSyncer::PeerEntry = std::pair<PeerId, std::vector<Multiaddress>>;
```


### using RouteMapType

```cpp
using sgns::crdt::GraphsyncDAGSyncer::RouteMapType = std::map<CID, std::vector<PeerKey>>;
```


## Public Functions Documentation

### function GraphsyncDAGSyncer

```cpp
GraphsyncDAGSyncer(
    std::shared_ptr< IpfsDatastore > service,
    std::shared_ptr< Graphsync > graphsync,
    std::shared_ptr< libp2p::Host > host
)
```


### function ~GraphsyncDAGSyncer

```cpp
inline ~GraphsyncDAGSyncer() override
```


### function Listen

```cpp
outcome::result< void > Listen(
    const Multiaddress & listen_to
)
```


### function StartSync

```cpp
outcome::result< void > StartSync()
```


Starts instance and subscribes to blocks 


### function AddRoute

```cpp
void AddRoute(
    const CID & cid,
    const PeerId & peer,
    std::vector< Multiaddress > address
)
```


### function addNode

```cpp
outcome::result< void > addNode(
    std::shared_ptr< const ipfs_lite::ipld::IPLDNode > node
) override
```


### function getNode

```cpp
outcome::result< std::shared_ptr< ipfs_lite::ipld::IPLDNode > > getNode(
    const CID & cid
) const override
```


### function removeNode

```cpp
outcome::result< void > removeNode(
    const CID & cid
) override
```


### function select

```cpp
outcome::result< size_t > select(
    gsl::span< const uint8_t > root_cid,
    gsl::span< const uint8_t > selector,
    std::function< bool(std::shared_ptr< const ipfs_lite::ipld::IPLDNode > node)> handler
) const override
```


### function fetchGraph

```cpp
outcome::result< std::shared_ptr< ipfs_lite::ipfs::merkledag::Leaf > > fetchGraph(
    const CID & cid
) const override
```


### function fetchGraphOnDepth

```cpp
outcome::result< std::shared_ptr< ipfs_lite::ipfs::merkledag::Leaf > > fetchGraphOnDepth(
    const CID & cid,
    uint64_t depth
) const override
```


### function HasBlock

```cpp
virtual outcome::result< bool > HasBlock(
    const CID & cid
) const override
```


**Parameters**: 

  * **cid** Content identifier of the node 


**Return**: true if the block is locally available or outcome::failure on error 

**Reimplements**: [sgns::crdt::DAGSyncer::HasBlock](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-hasblock)


Check if the block with cid is locally available (therefore, it is considered processed). 


### function GetNodeWithoutRequest

```cpp
virtual outcome::result< std::shared_ptr< ipfs_lite::ipld::IPLDNode > > GetNodeWithoutRequest(
    const CID & cid
) const override
```


**Reimplements**: [sgns::crdt::DAGSyncer::GetNodeWithoutRequest](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-getnodewithoutrequest)


### function GetNodeFromMerkleDAG

```cpp
outcome::result< std::shared_ptr< ipfs_lite::ipld::IPLDNode > > GetNodeFromMerkleDAG(
    const CID & cid
) const
```


### function TraverseCIDsLinks

```cpp
virtual std::pair< LinkInfoSet, LinkInfoSet > TraverseCIDsLinks(
    ipfs_lite::ipld::IPLDNode & node,
    std::string link_name ="",
    LinkInfoSet visited ={}
) const override
```


**Reimplements**: [sgns::crdt::DAGSyncer::TraverseCIDsLinks](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-traversecidslinks)


### function markResolved

```cpp
virtual outcome::result< void > markResolved(
    const CID & cid
) override
```


**Reimplements**: [sgns::crdt::DAGSyncer::markResolved](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-markresolved)


### function isResolved

```cpp
virtual outcome::result< bool > isResolved(
    const CID & cid
) const override
```


**Reimplements**: [sgns::crdt::DAGSyncer::isResolved](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-isresolved)


### function GetId

```cpp
outcome::result< PeerId > GetId() const
```


### function GetPeerInfo

```cpp
outcome::result< libp2p::peer::PeerInfo > GetPeerInfo() const
```


### function AddToBlackList

```cpp
void AddToBlackList(
    const PeerId & peer
) const
```


### function IsOnBlackList

```cpp
bool IsOnBlackList(
    const PeerId & peer
) const
```


### function InitCIDBlock

```cpp
virtual void InitCIDBlock(
    const CID & cid
) override
```


**Reimplements**: [sgns::crdt::DAGSyncer::InitCIDBlock](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-initcidblock)


### function IsCIDInCache

```cpp
virtual bool IsCIDInCache(
    const CID & cid
) const override
```


**Reimplements**: [sgns::crdt::DAGSyncer::IsCIDInCache](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-iscidincache)


### function DeleteCIDBlock

```cpp
virtual outcome::result< void > DeleteCIDBlock(
    const CID & cid
) override
```


**Reimplements**: [sgns::crdt::DAGSyncer::DeleteCIDBlock](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-deletecidblock)


### function Stop

```cpp
virtual void Stop() override
```


**Reimplements**: [sgns::crdt::DAGSyncer::Stop](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/#function-stop)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
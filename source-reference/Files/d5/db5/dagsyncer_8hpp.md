---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/dagsyncer.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/dagsyncer.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/)** <br/>A [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/) is an abstraction to an IPLD-based p2p storage layer. A [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/) is a DAGService with the ability to publish new ipld nodes to the network, and retrieving others from it.  |




## Source code

```cpp
#ifndef SUPERGENIUS_DAGSYNCER_HPP
#define SUPERGENIUS_DAGSYNCER_HPP

#include <primitives/cid/cid.hpp>
#include <ipfs_lite/ipfs/merkledag/merkledag_service.hpp>
#include "outcome/outcome.hpp"
#include <set>

namespace sgns::crdt
{
    class DAGSyncer : public ipfs_lite::ipfs::merkledag::MerkleDagService
    {
    public:
        using LinkInfoPair = std::pair<CID, std::string>;
        using LinkInfoSet  = std::set<LinkInfoPair>;
        virtual outcome::result<bool> HasBlock( const CID &cid ) const = 0;

        virtual outcome::result<std::shared_ptr<ipfs_lite::ipld::IPLDNode>> GetNodeWithoutRequest(
            const CID &cid ) const                                                                       = 0;
        virtual std::pair<LinkInfoSet, LinkInfoSet> TraverseCIDsLinks( ipfs_lite::ipld::IPLDNode &node,
                                                                       std::string                link_name,
                                                                       LinkInfoSet visited_links ) const = 0;

        virtual void                        InitCIDBlock( const CID &cid )       = 0;
        virtual bool                        IsCIDInCache( const CID &cid ) const = 0;
        virtual outcome::result<void>       DeleteCIDBlock( const CID &cid )     = 0;
        virtual void                        Stop()                               = 0;
        virtual IPFS::outcome::result<void> markResolved( const CID &cid )       = 0;
        virtual IPFS::outcome::result<bool> isResolved( const CID &cid ) const   = 0;
    };
} // namespace sgns::crdt

#endif // SUPERGENIUS_DAGSYNCER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

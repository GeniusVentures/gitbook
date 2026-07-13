---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/globaldb/pubsub_broadcaster.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/globaldb/pubsub_broadcaster.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::PubSubBroadcaster](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/)**  |




## Source code

```cpp
#ifndef SUPERGENIUS_CRDT_PUBSUB_BROADCASTER_HPP
#define SUPERGENIUS_CRDT_PUBSUB_BROADCASTER_HPP

#include "crdt/broadcaster.hpp"
#include "base/logger.hpp"
#include <ipfs_pubsub/gossip_pubsub_topic.hpp>
#include <queue>

namespace sgns::crdt
{
class PubSubBroadcaster : public Broadcaster
{
public:
    using GossipPubSub = sgns::ipfs_pubsub::GossipPubSub;
    using GossipPubSubTopic = sgns::ipfs_pubsub::GossipPubSubTopic;

    PubSubBroadcaster( std::shared_ptr<GossipPubSubTopic> pubSubTopic );

    void SetLogger(base::Logger logger)
    {
        logger_ = std::move(logger);
    }

        outcome::result<void> Broadcast(const base::Buffer &buff, std::string topic, boost::optional<libp2p::peer::PeerInfo> peerInfo = boost::none) override;
        outcome::result<base::Buffer> Next() override;

        bool HasTopic(const std::string &topic) override { return true; }
private:
    std::shared_ptr<GossipPubSubTopic> gossipPubSubTopic_;
    std::queue<std::tuple<libp2p::peer::PeerId, std::string>> listOfMessages_;
    base::Logger logger_ = nullptr;
    std::mutex mutex_;
};
}


#endif // SUPERGENIUS_CRDT_PUBSUB_BROADCASTER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/globaldb/pubsub_broadcaster_ext.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/globaldb/pubsub_broadcaster_ext.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::PubSubBroadcasterExt](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/)** <br/>Extended PubSub broadcaster that integrates with a CRDT datastore and Graphsync DAG syncer.  |




## Source code

```cpp
#ifndef SUPERGENIUS_CRDT_PUBSUB_BROADCASTER_EXT_HPP
#define SUPERGENIUS_CRDT_PUBSUB_BROADCASTER_EXT_HPP

#include "crdt/broadcaster.hpp"
#include "crdt/graphsync_dagsyncer.hpp"
#include "crdt/crdt_datastore.hpp"
#include "base/logger.hpp"
#include <ipfs_pubsub/gossip_pubsub_topic.hpp>
#include <queue>
#include <tuple>
#include <vector>
#include <future>
#include <unordered_map>
#include <string>
#include <optional>
#include <mutex>

namespace sgns::crdt
{

    class PubSubBroadcasterExt : public Broadcaster, public std::enable_shared_from_this<PubSubBroadcasterExt>
    {
    public:
        using GossipPubSub = sgns::ipfs_pubsub::GossipPubSub;
        ~PubSubBroadcasterExt();

        static std::shared_ptr<PubSubBroadcasterExt> New( std::shared_ptr<sgns::crdt::GraphsyncDAGSyncer> dagSyncer,
                                                          std::shared_ptr<GossipPubSub>                   pubSub );

        outcome::result<void> Broadcast( const base::Buffer &buff, std::string topic, boost::optional<libp2p::peer::PeerInfo> peerInfo = boost::none ) override;

        outcome::result<base::Buffer> Next() override;

        void Start();

        outcome::result<void> AddBroadcastTopic( const std::string &topicName );

        void AddListenTopic( std::string topic );

        bool HasTopic( const std::string &topic ) override;

        std::shared_ptr<void> GetDagSyncer() const override { return dagSyncer_; }

        void Stop();

        bool AddSingleCIDInfo( const std::string &cid, const std::string peer_id, const std::string address );

    private:
        PubSubBroadcasterExt( std::shared_ptr<sgns::crdt::GraphsyncDAGSyncer> dagSyncer,
                              std::shared_ptr<GossipPubSub>                   pubSub );

        void OnMessage( boost::optional<const GossipPubSub::Message &> message, const std::string &incomingTopic );

        std::set<std::string>                                     topicsToListen_;
        std::set<std::string>                                     topicsToBroadcast_;
        std::shared_ptr<sgns::crdt::GraphsyncDAGSyncer>           dagSyncer_;
        std::queue<std::tuple<libp2p::peer::PeerId, std::string>> messageQueue_;

        std::shared_ptr<GossipPubSub> pubSub_; 

        std::mutex       queueMutex_;           
        std::mutex       listenTopicsMutex_;    
        std::mutex       broadcastTopicsMutex_; 
        std::mutex       subscriptionMutex_;    
        std::atomic_bool started_;

        sgns::base::Logger m_logger = sgns::base::createLogger( "PubSubBroadcasterExt" );
        std::vector<std::shared_future<std::shared_ptr<ipfs_pubsub::GossipPubSub::Subscription>>> subscriptionFutures_;

        bool AddMultiCIDInfo( const std::vector<CID>                         &cids,
                              const libp2p::peer::PeerId                     &peer_id,
                              const std::vector<libp2p::multi::Multiaddress> &addr_vector );
    };
}

#endif // SUPERGENIUS_CRDT_PUBSUB_BROADCASTER_EXT_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

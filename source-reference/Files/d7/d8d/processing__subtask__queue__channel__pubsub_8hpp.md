---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_queue_channel_pubsub.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_queue_channel_pubsub.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |
| **[sgns::ipfs_pubsub](/source-reference/Namespaces/d4/d75/namespacesgns_1_1ipfs__pubsub/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::ProcessingSubTaskQueueChannelPubSub](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/)**  |




## Source code

```cpp


#ifndef SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_CHANNEL_PUBSUB_HPP
#define SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_CHANNEL_PUBSUB_HPP

#include <future>
#include "outcome/outcome.hpp"

#include "processing/processing_subtask_queue_channel.hpp"

#include <ipfs_pubsub/gossip_pubsub_topic.hpp>
#include "base/logger.hpp"

using namespace sgns::ipfs_pubsub;

namespace sgns::processing
{
    class ProcessingSubTaskQueueChannelPubSub : public ProcessingSubTaskQueueChannel,
                                                public std::enable_shared_from_this<ProcessingSubTaskQueueChannelPubSub>
    {
    public:
        using QueueRequestSink = std::function<bool( const SGProcessing::SubTaskQueueRequest & )>;
        using QueueUpdateSink  = std::function<bool( SGProcessing::SubTaskQueue * )>;

        ProcessingSubTaskQueueChannelPubSub( std::shared_ptr<sgns::ipfs_pubsub::GossipPubSub> gossipPubSub,
                                             const std::string &processingQueueChannelId );

        ~ProcessingSubTaskQueueChannelPubSub() override;

        void RequestQueueOwnership( const std::string &nodeId ) override;
        void PublishQueue( std::shared_ptr<SGProcessing::SubTaskQueue> queue ) override;

        void SetQueueRequestSink( QueueRequestSink queueRequestSink );

        void SetQueueUpdateSink( QueueUpdateSink queueUpdateSink );

        outcome::result<std::variant<std::chrono::milliseconds, std::shared_future<std::shared_ptr<GossipPubSubTopic::Subscription>>>> Listen(
            std::chrono::milliseconds msSubscriptionWaitingDuration = std::chrono::milliseconds(2000));

        size_t GetActiveNodesCount() const override;

        std::vector<libp2p::peer::PeerId> GetActiveNodes() const override;


    private:
        std::shared_ptr<sgns::ipfs_pubsub::GossipPubSubTopic> m_processingQueueChannel;

        void OnProcessingChannelMessage( boost::optional<const sgns::ipfs_pubsub::GossipPubSub::Message &> message );

        void HandleSubTaskQueueRequest( SGProcessing::ProcessingChannelMessage &channelMesssage );
        void HandleSubTaskQueue( SGProcessing::ProcessingChannelMessage &channelMesssage );

        std::shared_ptr<sgns::ipfs_pubsub::GossipPubSub> m_gossipPubSub;
        std::shared_ptr<boost::asio::io_context>         m_context;

        std::function<bool( const SGProcessing::SubTaskQueueRequest & )> m_queueRequestSink;
        std::function<bool( SGProcessing::SubTaskQueue * )>              m_queueUpdateSink;

        base::Logger m_logger = base::createLogger( "ProcessingSubTaskQueueChannelPubSub" );


    };
}
#endif // SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_CHANNEL_PUBSUB_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

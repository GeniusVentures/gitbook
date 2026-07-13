---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_queue_channel.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_queue_channel.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::ProcessingSubTaskQueueChannel](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/)**  |




## Source code

```cpp


#ifndef SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_CHANNEL_HPP
#define SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_CHANNEL_HPP

#include "processing/proto/SGProcessing.pb.h"

#include <string>
#include <memory>

#include <ipfs_pubsub/gossip_pubsub_topic.hpp>

namespace sgns::processing
{
class ProcessingSubTaskQueueChannel
{
public:
    virtual ~ProcessingSubTaskQueueChannel() = default;

    virtual void RequestQueueOwnership(const std::string& nodeId) = 0;

    virtual void PublishQueue(std::shared_ptr<SGProcessing::SubTaskQueue> queue) = 0;

    virtual size_t GetActiveNodesCount() const = 0;

    virtual std::vector<libp2p::peer::PeerId> GetActiveNodes() const = 0;
};
}
#endif // SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_CHANNEL_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

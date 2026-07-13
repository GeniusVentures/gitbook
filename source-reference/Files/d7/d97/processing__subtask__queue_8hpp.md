---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_queue.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_queue.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::ProcessingSubTaskQueue](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/)** <br/>Distributed subtask queue implementation.  |




## Source code

```cpp


#ifndef SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_HPP
#define SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_HPP

#include "processing/proto/SGProcessing.pb.h"
#include "base/logger.hpp"

namespace sgns::processing
{
class ProcessingSubTaskQueue
{
public:

    using TimestampProvider = std::function<uint64_t()>;

    ProcessingSubTaskQueue(std::string localNodeId, TimestampProvider timestampProvider = nullptr);

    void CreateQueue(SGProcessing::ProcessingQueue* queue, const std::vector<int>& enabledItemIndices);

    bool GrabItem(size_t& grabbedItemIndex, uint64_t timestamp);

    bool MoveOwnershipTo(const std::string& nodeId);

    bool RollbackOwnership();

    bool HasOwnership() const;

    bool UpdateQueue(SGProcessing::ProcessingQueue* queue, const std::vector<int>& enabledItemIndices);

    bool UnlockExpiredItems(uint64_t currentTime);

    [[nodiscard]] uint64_t GetLastLockTimestamp() const;

    bool AddOwnershipRequest(const std::string& nodeId, uint64_t timestamp);

    bool ProcessNextOwnershipRequest();

private:

    void ChangeOwnershipTo(const std::string& nodeId);

    bool LockItem(size_t& lockedItemIndex, uint64_t timestamp);

    void LogQueue() const;

    std::string m_localNodeId;
    SGProcessing::ProcessingQueue* m_queue;

    std::vector<int> m_enabledItemIndices;

    base::Logger m_logger = base::createLogger("ProcessingSubTaskQueue");

    TimestampProvider m_timestampProvider;
};
}

#endif // SUPERGENIUS_PROCESSING_SUBTASK_QUEUE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

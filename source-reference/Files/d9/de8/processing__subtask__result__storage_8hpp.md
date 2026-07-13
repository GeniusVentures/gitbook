---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_result_storage.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_subtask_result_storage.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::SubTaskResultStorage](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/)**  |




## Source code

```cpp
#ifndef GRPC_FOR_SUPERGENIUS_PROCESSING_SUTASK_RESULT_STORAGE_HPP
#define GRPC_FOR_SUPERGENIUS_PROCESSING_SUTASK_RESULT_STORAGE_HPP

#include "processing/proto/SGProcessing.pb.h"

namespace sgns::processing
{
    class SubTaskResultStorage
    {
    public:
        virtual ~SubTaskResultStorage() = default;

        virtual void AddSubTaskResult( const SGProcessing::SubTaskResult &subTaskResult ) = 0;

        virtual void RemoveSubTaskResult( const std::string &subTaskId ) = 0;

        virtual std::vector<SGProcessing::SubTaskResult> GetSubTaskResults(
            const std::set<std::string> &subTaskIds ) = 0;
    };
}

#endif // GRPC_FOR_SUPERGENIUS_PROCESSING_SUTASK_RESULT_STORAGE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

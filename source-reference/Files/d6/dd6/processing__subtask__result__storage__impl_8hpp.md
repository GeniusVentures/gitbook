---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/impl/processing_subtask_result_storage_impl.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/impl/processing_subtask_result_storage_impl.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::SubTaskResultStorageImpl](/source-reference/Classes/d3/df7/classsgns_1_1processing_1_1_sub_task_result_storage_impl/)** <br/>Handles subtask result storage.  |




## Source code

```cpp
#ifndef GRPC_FOR_SUPERGENIUS_PROCESSING_SUBTASK_RESULT_STORAGE_IMPL_HPP
#define GRPC_FOR_SUPERGENIUS_PROCESSING_SUBTASK_RESULT_STORAGE_IMPL_HPP

#include "processing/processing_subtask_result_storage.hpp"
#include "crdt/globaldb/globaldb.hpp"

namespace sgns::processing
{
    class SubTaskResultStorageImpl : public SubTaskResultStorage
    {
    public:
        SubTaskResultStorageImpl( std::shared_ptr<crdt::GlobalDB> db, std::string topic );

        ~SubTaskResultStorageImpl() override;

        void AddSubTaskResult( const SGProcessing::SubTaskResult &result ) override;

        void RemoveSubTaskResult( const std::string &subTaskId ) override;

        std::vector<SGProcessing::SubTaskResult> GetSubTaskResults( const std::set<std::string> &subTaskIds ) override;

    private:
        std::shared_ptr<sgns::crdt::GlobalDB> m_db;
        std::string                           m_processing_topic;
    };
}

#endif // GRPC_FOR_SUPERGENIUS_PROCESSING_SUBTASK_RESULT_STORAGE_IMPL_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

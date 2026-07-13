---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/impl/processing_core_impl.hpp
summary: Header file of the Processing Core implementation that uses the ProcessingManager to execute subtasks. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/impl/processing_core_impl.hpp



Header file of the Processing Core implementation that uses the ProcessingManager to execute subtasks.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::sgprocessing](/source-reference/Namespaces/d1/dc7/namespacesgns_1_1sgprocessing/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::ProcessingCoreImpl](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/)** <br/>Default implementation of [ProcessingCore](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/) backed by GlobalDB.  |

## Functions

|                | Name           |
| -------------- | -------------- |
| | **[OUTCOME_HPP_DECLARE_ERROR_2](/source-reference/Files/dd/da6/processing__core__impl_8hpp/#function-outcome_hpp_declare_error_2)**([sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/) , ProcessingCoreImpl::Error ) |

## Detailed Description

Header file of the Processing Core implementation that uses the ProcessingManager to execute subtasks. 

**Date**: 2024-03-28 Justin Church ([jchurch@gnus.ai](mailto:jchurch@gnus.ai)) Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 

## Functions Documentation

### function OUTCOME_HPP_DECLARE_ERROR_2

```cpp
OUTCOME_HPP_DECLARE_ERROR_2(
    sgns::processing ,
    ProcessingCoreImpl::Error 
)
```




## Source code

```cpp


#ifndef PROCESSING_CORE_IMPL_HPP
#define PROCESSING_CORE_IMPL_HPP

#include <cmath>
#include <memory>
#include <iostream>
#include <utility>
#include <cstdint>

#include <libp2p/log/configurator.hpp>
#include <libp2p/log/logger.hpp>
#include <libp2p/multi/multibase_codec/multibase_codec_impl.hpp>
#include <libp2p/multi/content_identifier_codec.hpp>
#include <libp2p/injector/host_injector.hpp>
#include <libp2p/injector/kademlia_injector.hpp>

#include "processing/processing_core.hpp"
#include "processing/processing_task_queue.hpp"
#include "crdt/globaldb/globaldb.hpp"
#include "account/TokenID.hpp"

// Forward declaration
namespace sgns::sgprocessing
{
    class ProcessingManager;
}

namespace sgns::processing
{
    class ProcessingCoreImpl : public ProcessingCore
    {
    public:
        enum class Error
        {
            MAX_NUMBER_SUBTASKS = 1,    
            GLOBALDB_READ_ERROR,        
            NO_BUFFER_FROM_JOB_DATA,    
            TASK_DESERIALIZATION_ERROR, 
            JOB_INCOMPATIBILITY_ERROR,  
            INVALID_MODEL_ERROR         
        };

        static std::shared_ptr<ProcessingCoreImpl> New( std::shared_ptr<ProcessingTaskQueue> task_queue,
                                                        uint32_t maximalProcessingSubTaskCount,
                                                        TokenID  tokenId );

        ~ProcessingCoreImpl() = default;

        outcome::result<SGProcessing::SubTaskResult> ProcessSubTask( const SGProcessing::SubTask &subTask,
                                                                     uint32_t initialHashCode ) override;

        float GetProgress() const override;

    private:
        explicit ProcessingCoreImpl( std::shared_ptr<ProcessingTaskQueue> task_queue,
                                     uint32_t                             maximalProcessingSubTaskCount,
                                     TokenID                              tokenId );

        outcome::result<void> IncProcessingSubTaskCount();

        void DecProcessingSubTaskCount();

        std::shared_ptr<ProcessingTaskQueue> task_queue_;
        TokenID token_ID_;
        uint32_t max_processing_subtask_count_;

        std::mutex subtask_count_mutex_;
        uint32_t processing_subtask_count_{ 0 };
        mutable std::shared_ptr<sgprocessing::ProcessingManager> processing_manager_;
    };
}

OUTCOME_HPP_DECLARE_ERROR_2( sgns::processing, ProcessingCoreImpl::Error );

#endif // PROCESSING_CORE_IMPL_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

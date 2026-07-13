---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_validation_core.hpp
summary: Header file of core implementation of processing task results validation. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_validation_core.hpp



Header file of core implementation of processing task results validation.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::ProcessingValidationCore](/source-reference/Classes/d0/d2c/classsgns_1_1processing_1_1_processing_validation_core/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| | **[OUTCOME_HPP_DECLARE_ERROR_2](/source-reference/Files/d1/dd9/processing__validation__core_8hpp/#function-outcome_hpp_declare_error_2)**([sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/) , ProcessingValidationCore::Error )<br/>Macro for declaring error handling in the IBasicProof class.  |

## Detailed Description

Header file of core implementation of processing task results validation. 

**Date**: 2022-05-08 creativeid00 

**Note**: This was mostly rewritten by Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) and Justin Church ([jchurch@gnus.ai](mailto:jchurch@gnus.ai)) 

## Functions Documentation

### function OUTCOME_HPP_DECLARE_ERROR_2

```cpp
OUTCOME_HPP_DECLARE_ERROR_2(
    sgns::processing ,
    ProcessingValidationCore::Error 
)
```

Macro for declaring error handling in the IBasicProof class. 



## Source code

```cpp


#ifndef SUPERGENIUS_PROCESSING_VALIDATION_CORE_HPP
#define SUPERGENIUS_PROCESSING_VALIDATION_CORE_HPP

#include <map>
#include <string>
#include <set>
#include <vector>
#include <cstdint>

#include "outcome/outcome.hpp"
#include "base/logger.hpp"
#include "processing/proto/SGProcessing.pb.h"

namespace sgns::processing
{
    class ProcessingValidationCore
    {
    public:
        enum class Error
        {
            NO_RESULTS_FOR_SUBTASK = 0,  
            WRONG_RESULT_HASHES_LENGTH,  
            DUPLICATE_CHUNK_RESULT_HASH, 
            EMPTY_CHUNK_RESULT_HASH,     
            MISSING_CHUNK_RESULT,        
            INVALID_CHUNK_RESULT_HASH,   
            SUBTASK_ID_MISMATCH,         
            INVALID_RESULTS_BATCH        
        };
        ProcessingValidationCore();

        outcome::result<void> ValidateResults( const SGProcessing::SubTaskCollection                    &subTasks,
                                               const std::map<std::string, SGProcessing::SubTaskResult> &results,
                                               std::set<std::string> &invalidSubTaskIds );

        outcome::result<void> ValidateIndividualResult( const SGProcessing::SubTask       &subTask,
                                                        const SGProcessing::SubTaskResult &result ) const;

    private:
        outcome::result<void> CheckSubTaskResultHashes(
            const SGProcessing::SubTask                       &subTask,
            const std::map<std::string, std::vector<uint8_t>> &chunks ) const;

        base::Logger m_logger = base::createLogger( "ProcessingValidationCore" );
    };
}

OUTCOME_HPP_DECLARE_ERROR_2( sgns::processing, ProcessingValidationCore::Error );

#endif // SUPERGENIUS_PROCESSING_VALIDATION_CORE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

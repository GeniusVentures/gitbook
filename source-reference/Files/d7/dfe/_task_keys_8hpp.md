---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/impl/TaskKeys.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/impl/TaskKeys.hpp



 [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::TaskKeys](/source-reference/Classes/d9/df3/classsgns_1_1processing_1_1_task_keys/)**  |

## Detailed Description


**Date**: 2026-05-19 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp


#ifndef TASK_KEYS_HPP
#define TASK_KEYS_HPP

#include <string>
#include <string_view>

#include "base/sgns_version.hpp"

namespace sgns::processing
{
    class TaskKeys
    {
    public:
        static std::string ProcessingPrefix()
        {
            return std::string( PROCESSING_PREFIX_BASE ) + std::to_string( sgns::version::ProcessingVersion() );
        }

        static std::string TaskListKey()
        {
            return ProcessingPrefix() + std::string( TASK_LIST_SUFFIX );
        }

        static std::string SubTaskListKey()
        {
            return ProcessingPrefix() + std::string( SUBTASK_LIST_SUFFIX );
        }

        static std::string SubTaskListKey( std::string_view taskId )
        {
            return SubTaskListKey() + "/" + std::string( taskId );
        }

        static std::string TaskKey( std::string_view taskId )
        {
            return TaskListKey() + "/" + std::string( taskId );
        }

        static std::string SubTaskKey( std::string_view taskId, std::string_view subTaskId )
        {
            return SubTaskListKey( taskId ) + "/" + std::string( subTaskId );
        }

        static std::string ClaimableListKey()
        {
            return ProcessingPrefix() + std::string( CLAIMABLE_LIST_SUFFIX );
        }

        static std::string ClaimableTaskKey( std::string_view taskId )
        {
            return ClaimableListKey() + "/" + std::string( taskId );
        }

        static std::string ResultTaskKey( std::string_view taskId )
        {
            return ProcessingPrefix() + std::string( RESULTS_SUFFIX ) + std::string( TASK_LIST_SUFFIX ) +
                   std::string( taskId );
        }

        static std::string LockKey( std::string_view taskKey )
        {
            return std::string( LOCK_KEY_PREFIX ) + std::string( taskKey );
        }

    private:
        static constexpr std::string_view PROCESSING_PREFIX_BASE = "/processing_";
        static constexpr std::string_view TASK_LIST_SUFFIX       = "/tasks";
        static constexpr std::string_view SUBTASK_LIST_SUFFIX    = "/subtasks";
        static constexpr std::string_view CLAIMABLE_LIST_SUFFIX  = "/claimable";
        static constexpr std::string_view RESULTS_SUFFIX         = "/task_results";
        static constexpr std::string_view LOCK_KEY_PREFIX        = "/lock_";
    };
}

#endif // TASK_KEYS_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

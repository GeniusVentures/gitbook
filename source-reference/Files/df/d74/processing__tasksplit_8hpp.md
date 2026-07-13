---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_tasksplit.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_tasksplit.hpp



 [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::ProcessTaskSplitter](/source-reference/Classes/d7/de8/classsgns_1_1processing_1_1_process_task_splitter/)**  |

## Detailed Description


**Date**: 2024-04-23 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef _PROCESSING_TASKSPLIT_HPP_
#define _PROCESSING_TASKSPLIT_HPP_
#include <cstdlib>
#include <list>

#include <boost/format.hpp>

#include "processing/proto/SGProcessing.pb.h"

namespace sgns
{
    namespace processing
    {
        class ProcessTaskSplitter
        {
        public:
            ProcessTaskSplitter();

            void SplitTask( const SGProcessing::Task         &task,
                            std::list<SGProcessing::SubTask> &subTasks,
                            std::string                       json_data,
                            uint32_t                          numchunks,
                            bool                              addvalidationsubtask,
                            std::string                       ipfsid );
        };
    }
}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_core.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_core.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::ProcessingCore](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/)** <br/>Processing core interface.  |




## Source code

```cpp

#ifndef GRPC_FOR_SUPERGENIUS_PROCESSING_CORE_HPP
#define GRPC_FOR_SUPERGENIUS_PROCESSING_CORE_HPP

#include "processing/proto/SGProcessing.pb.h"
#include "outcome/outcome.hpp"
#include <boost/asio/io_context.hpp>

namespace sgns::processing
{
class ProcessingCore
{
public:
    virtual ~ProcessingCore() = default;

    virtual outcome::result<SGProcessing::SubTaskResult> ProcessSubTask(
        const SGProcessing::SubTask& subTask, uint32_t initialHashCode) = 0;


    virtual float GetProgress() const { return 0.0f; }
};

} // namespace sgns::processing

#endif // GRPC_FOR_SUPERGENIUS_PROCESSING_CORE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

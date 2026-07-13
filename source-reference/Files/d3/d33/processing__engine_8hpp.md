---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_engine.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/processing/processing_engine.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::processing](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::ProcessingEngine](/source-reference/Classes/dc/d00/classsgns_1_1processing_1_1_processing_engine/)** <br/>Handles subtask processing and result aggregation.  |




## Source code

```cpp


#ifndef GRPC_FOR_SUPERGENIUS_PROCESSING_ENGINE_HPP
#define GRPC_FOR_SUPERGENIUS_PROCESSING_ENGINE_HPP

#include "processing_core.hpp"
#include "processing_subtask_queue_accessor.hpp"
#include "base/logger.hpp"

namespace sgns::processing
{
    class ProcessingEngine : public std::enable_shared_from_this<ProcessingEngine>
    {
    public:
        ProcessingEngine( std::string                                nodeId,
                          std::shared_ptr<ProcessingCore>            processingCore,
                          std::function<void( const std::string & )> processingErrorSink,
                          std::function<void( void )>                processingDoneSink );
        ~ProcessingEngine();

        void StartQueueProcessing( std::shared_ptr<SubTaskQueueAccessor> subTaskQueueAccessor );

        void StopQueueProcessing();
        bool IsQueueProcessingStarted() const;

        float GetProgress() const;

    private:
        void OnSubTaskGrabbed( boost::optional<const SGProcessing::SubTask &> subTask );

        void ProcessSubTask( SGProcessing::SubTask subTask );

        std::string                                m_nodeId;
        std::shared_ptr<ProcessingCore>            m_processingCore;
        std::function<void( const std::string & )> m_processingErrorSink;
        std::function<void( void )>                m_processingDoneSink;

        std::shared_ptr<SubTaskQueueAccessor> m_subTaskQueueAccessor;

        mutable std::mutex m_mutexSubTaskQueue;

        base::Logger m_logger = base::createLogger( "ProcessingEngine" );
    };
}

#endif // GRPC_FOR_SUPERGENIUS_PROCESSING_ENGINE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

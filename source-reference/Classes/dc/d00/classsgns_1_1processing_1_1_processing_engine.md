---
title: sgns::processing::ProcessingEngine
summary: Handles subtask processing and result aggregation. 

---

# sgns::processing::ProcessingEngine



Handles subtask processing and result aggregation. 


`#include <processing_engine.hpp>`

Inherits from std::enable_shared_from_this< ProcessingEngine >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[ProcessingEngine](/source-reference/Classes/dc/d00/classsgns_1_1processing_1_1_processing_engine/#function-processingengine)**(std::string nodeId, std::shared_ptr< [ProcessingCore](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/) > processingCore, std::function< void(const std::string &)> processingErrorSink, std::function< void(void)> processingDoneSink) |
| | **[~ProcessingEngine](/source-reference/Classes/dc/d00/classsgns_1_1processing_1_1_processing_engine/#function-~processingengine)**() |
| void | **[StartQueueProcessing](/source-reference/Classes/dc/d00/classsgns_1_1processing_1_1_processing_engine/#function-startqueueprocessing)**(std::shared_ptr< [SubTaskQueueAccessor](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/) > subTaskQueueAccessor) |
| void | **[StopQueueProcessing](/source-reference/Classes/dc/d00/classsgns_1_1processing_1_1_processing_engine/#function-stopqueueprocessing)**() |
| bool | **[IsQueueProcessingStarted](/source-reference/Classes/dc/d00/classsgns_1_1processing_1_1_processing_engine/#function-isqueueprocessingstarted)**() const |
| float | **[GetProgress](/source-reference/Classes/dc/d00/classsgns_1_1processing_1_1_processing_engine/#function-getprogress)**() const |

## Public Functions Documentation

### function ProcessingEngine

```cpp
ProcessingEngine(
    std::string nodeId,
    std::shared_ptr< ProcessingCore > processingCore,
    std::function< void(const std::string &)> processingErrorSink,
    std::function< void(void)> processingDoneSink
)
```


**Parameters**: 

  * **nodeId** - Current processing node ID. 
  * **processingCore** - Processing core used to execute subtasks. 
  * **processingErrorSink** - Callback for processing errors. 
  * **processingDoneSink** - Callback when processing finishes. 


Create a processing engine object. 


### function ~ProcessingEngine

```cpp
~ProcessingEngine()
```


### function StartQueueProcessing

```cpp
void StartQueueProcessing(
    std::shared_ptr< SubTaskQueueAccessor > subTaskQueueAccessor
)
```


### function StopQueueProcessing

```cpp
void StopQueueProcessing()
```


### function IsQueueProcessingStarted

```cpp
bool IsQueueProcessingStarted() const
```


### function GetProgress

```cpp
float GetProgress() const
```


**Return**: Progress percentage (0.0 to 100.0) 

Get current processing progress 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
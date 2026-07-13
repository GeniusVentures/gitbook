---
title: sgns::processing::ProcessingCore
summary: Processing core interface. 

---

# sgns::processing::ProcessingCore



Processing core interface.  [More...](#detailed-description)


`#include <processing_core.hpp>`

Inherited by [sgns::processing::ProcessingCoreImpl](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~ProcessingCore](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/#function-~processingcore)**() =default |
| virtual outcome::result< SGProcessing::SubTaskResult > | **[ProcessSubTask](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/#function-processsubtask)**(const SGProcessing::SubTask & subTask, uint32_t initialHashCode) =0<br/>Processes a subtask and returns the result.  |
| virtual float | **[GetProgress](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/#function-getprogress)**() const<br/>Returns the progress of the processing core as a float between 0.0 and 100.0.  |

## Detailed Description

```cpp
class sgns::processing::ProcessingCore;
```

Processing core interface. 

Implementations encapsulate specific processing algorithms for subtasks. 

## Public Functions Documentation

### function ~ProcessingCore

```cpp
virtual ~ProcessingCore() =default
```


### function ProcessSubTask

```cpp
virtual outcome::result< SGProcessing::SubTaskResult > ProcessSubTask(
    const SGProcessing::SubTask & subTask,
    uint32_t initialHashCode
) =0
```

Processes a subtask and returns the result. 

**Parameters**: 

  * **subTask** The subtask to process 
  * **initialHashCode** An initial hash code that can be used for processing 


**Return**: The result of processing the subtask, or failure if processing failed 

**Reimplemented by**: [sgns::processing::ProcessingCoreImpl::ProcessSubTask](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/#function-processsubtask)


### function GetProgress

```cpp
inline virtual float GetProgress() const
```

Returns the progress of the processing core as a float between 0.0 and 100.0. 

**Return**: The percentage of the processing of the subtask 

**Reimplemented by**: [sgns::processing::ProcessingCoreImpl::GetProgress](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/#function-getprogress)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
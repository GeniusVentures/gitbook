---
title: sgns::processing::ProcessingCoreImpl
summary: Default implementation of ProcessingCore backed by GlobalDB. 

---

# sgns::processing::ProcessingCoreImpl



Default implementation of [ProcessingCore](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/) backed by GlobalDB. 


`#include <processing_core_impl.hpp>`

Inherits from [sgns::processing::ProcessingCore](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/)

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[Error](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/#enum-error)** { MAX_NUMBER_SUBTASKS = 1, GLOBALDB_READ_ERROR, NO_BUFFER_FROM_JOB_DATA, TASK_DESERIALIZATION_ERROR, JOB_INCOMPATIBILITY_ERROR, INVALID_MODEL_ERROR}<br/>[Error](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/#enum-error) codes for [ProcessingCoreImpl](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/) operations.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [ProcessingCoreImpl](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/#function-processingcoreimpl) > | **[New](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/#function-new)**(std::shared_ptr< [ProcessingTaskQueue](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/) > task_queue, uint32_t maximalProcessingSubTaskCount, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) tokenId)<br/>Factory method to create a new instance of [ProcessingCoreImpl](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/).  |
| | **[~ProcessingCoreImpl](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/#function-~processingcoreimpl)**() =default |
| virtual outcome::result< SGProcessing::SubTaskResult > | **[ProcessSubTask](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/#function-processsubtask)**(const SGProcessing::SubTask & subTask, uint32_t initialHashCode) override<br/>Processes a subtask and returns the result.  |
| virtual float | **[GetProgress](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/#function-getprogress)**() const override<br/>Returns the progress of the processing core as a float between 0.0 and 100.0.  |

## Additional inherited members

**Public Functions inherited from [sgns::processing::ProcessingCore](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~ProcessingCore](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/#function-~processingcore)**() =default |


## Public Types Documentation

### enum Error

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| MAX_NUMBER_SUBTASKS | 1| Number of subtasks exceeds the configured maximum.   |
| GLOBALDB_READ_ERROR | | Database read error.   |
| NO_BUFFER_FROM_JOB_DATA | | No buffer available from job data.   |
| TASK_DESERIALIZATION_ERROR | | [Error](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/#enum-error) occurred while deserializing the task.   |
| JOB_INCOMPATIBILITY_ERROR | | Job is incompatible with the processing core.   |
| INVALID_MODEL_ERROR | | The model is invalid.   |



[Error](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/#enum-error) codes for [ProcessingCoreImpl](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/) operations. 

## Public Functions Documentation

### function New

```cpp
static std::shared_ptr< ProcessingCoreImpl > New(
    std::shared_ptr< ProcessingTaskQueue > task_queue,
    uint32_t maximalProcessingSubTaskCount,
    TokenID tokenId
)
```

Factory method to create a new instance of [ProcessingCoreImpl](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/). 

**Parameters**: 

  * **task_queue** A shared pointer to the task queue used for retrieving tasks 
  * **maximalProcessingSubTaskCount** The maximum number of subtasks that can be processed concurrently 
  * **tokenId** The Token ID used on the results 


**Return**: A shared pointer to the created [ProcessingCoreImpl](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/) instance or nullptr if creation failed 

### function ~ProcessingCoreImpl

```cpp
~ProcessingCoreImpl() =default
```


### function ProcessSubTask

```cpp
virtual outcome::result< SGProcessing::SubTaskResult > ProcessSubTask(
    const SGProcessing::SubTask & subTask,
    uint32_t initialHashCode
) override
```

Processes a subtask and returns the result. 

**Parameters**: 

  * **subTask** The subtask to process 
  * **initialHashCode** An initial hash code that can be used for processing 


**Return**: The result of processing the subtask, or failure if processing failed 

**Reimplements**: [sgns::processing::ProcessingCore::ProcessSubTask](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/#function-processsubtask)


### function GetProgress

```cpp
virtual float GetProgress() const override
```

Returns the progress of the processing core as a float between 0.0 and 100.0. 

**Return**: The percentage of the processing of the subtask 

**Reimplements**: [sgns::processing::ProcessingCore::GetProgress](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/#function-getprogress)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
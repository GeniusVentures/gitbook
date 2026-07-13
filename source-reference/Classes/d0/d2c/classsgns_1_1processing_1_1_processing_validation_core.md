---
title: sgns::processing::ProcessingValidationCore

---

# sgns::processing::ProcessingValidationCore






`#include <processing_validation_core.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[Error](/source-reference/Classes/d0/d2c/classsgns_1_1processing_1_1_processing_validation_core/#enum-error)** { NO_RESULTS_FOR_SUBTASK = 0, WRONG_RESULT_HASHES_LENGTH, DUPLICATE_CHUNK_RESULT_HASH, EMPTY_CHUNK_RESULT_HASH, MISSING_CHUNK_RESULT, INVALID_CHUNK_RESULT_HASH, SUBTASK_ID_MISMATCH, INVALID_RESULTS_BATCH}<br/>Enumeration of error codes used in the processing validation class.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[ProcessingValidationCore](/source-reference/Classes/d0/d2c/classsgns_1_1processing_1_1_processing_validation_core/#function-processingvalidationcore)**() |
| outcome::result< void > | **[ValidateResults](/source-reference/Classes/d0/d2c/classsgns_1_1processing_1_1_processing_validation_core/#function-validateresults)**(const SGProcessing::SubTaskCollection & subTasks, const std::map< std::string, SGProcessing::SubTaskResult > & results, std::set< std::string > & invalidSubTaskIds) |
| outcome::result< void > | **[ValidateIndividualResult](/source-reference/Classes/d0/d2c/classsgns_1_1processing_1_1_processing_validation_core/#function-validateindividualresult)**(const SGProcessing::SubTask & subTask, const SGProcessing::SubTaskResult & result) const |

## Public Types Documentation

### enum Error

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| NO_RESULTS_FOR_SUBTASK | 0| a subtask had no result entry   |
| WRONG_RESULT_HASHES_LENGTH | | number of hashes != number of chunks   |
| DUPLICATE_CHUNK_RESULT_HASH | | duplicate hash inside a result   |
| EMPTY_CHUNK_RESULT_HASH | | empty hash seen   |
| MISSING_CHUNK_RESULT | | a chunk from subtask is missing from results map   |
| INVALID_CHUNK_RESULT_HASH | | conflicting/invalid chunk result hash observed   |
| SUBTASK_ID_MISMATCH | | subtask id != result id (individual check)   |
| INVALID_RESULTS_BATCH | | aggregated invalidities across subtasks   |



Enumeration of error codes used in the processing validation class. 

## Public Functions Documentation

### function ProcessingValidationCore

```cpp
ProcessingValidationCore()
```


### function ValidateResults

```cpp
outcome::result< void > ValidateResults(
    const SGProcessing::SubTaskCollection & subTasks,
    const std::map< std::string, SGProcessing::SubTaskResult > & results,
    std::set< std::string > & invalidSubTaskIds
)
```


**Return**: true if all chunk results are valid 

Checks if check result hashes are valid. If invalid chunk hashes found corresponding subtasks are invalidated and returned to processing queue 


### function ValidateIndividualResult

```cpp
outcome::result< void > ValidateIndividualResult(
    const SGProcessing::SubTask & subTask,
    const SGProcessing::SubTaskResult & result
) const
```


**Parameters**: 

  * **subTask** The subtask definition 
  * **result** The result to validate 


**Return**: true if the result is valid for the given subtask 

Validates a single subtask result against its corresponding subtask 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
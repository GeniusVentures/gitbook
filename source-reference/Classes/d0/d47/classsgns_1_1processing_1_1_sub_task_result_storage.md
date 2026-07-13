---
title: sgns::processing::SubTaskResultStorage

---

# sgns::processing::SubTaskResultStorage



 [More...](#detailed-description)


`#include <processing_subtask_result_storage.hpp>`

Inherited by [sgns::processing::SubTaskResultStorageImpl](/source-reference/Classes/d3/df7/classsgns_1_1processing_1_1_sub_task_result_storage_impl/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~SubTaskResultStorage](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/#function-~subtaskresultstorage)**() =default |
| virtual void | **[AddSubTaskResult](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/#function-addsubtaskresult)**(const SGProcessing::SubTaskResult & subTaskResult) =0 |
| virtual void | **[RemoveSubTaskResult](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/#function-removesubtaskresult)**(const std::string & subTaskId) =0 |
| virtual std::vector< SGProcessing::SubTaskResult > | **[GetSubTaskResults](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/#function-getsubtaskresults)**(const std::set< std::string > & subTaskIds) =0 |

## Detailed Description

```cpp
class sgns::processing::SubTaskResultStorage;
```


Handles subtask results storage 

## Public Functions Documentation

### function ~SubTaskResultStorage

```cpp
virtual ~SubTaskResultStorage() =default
```


### function AddSubTaskResult

```cpp
virtual void AddSubTaskResult(
    const SGProcessing::SubTaskResult & subTaskResult
) =0
```


**Parameters**: 

  * **subTaskResult** - processing result 


**Reimplemented by**: [sgns::processing::SubTaskResultStorageImpl::AddSubTaskResult](/source-reference/Classes/d3/df7/classsgns_1_1processing_1_1_sub_task_result_storage_impl/#function-addsubtaskresult)


Adds a result to the storage 


### function RemoveSubTaskResult

```cpp
virtual void RemoveSubTaskResult(
    const std::string & subTaskId
) =0
```


**Parameters**: 

  * **subTaskId** subtask id that the result was generated for 


**Reimplemented by**: [sgns::processing::SubTaskResultStorageImpl::RemoveSubTaskResult](/source-reference/Classes/d3/df7/classsgns_1_1processing_1_1_sub_task_result_storage_impl/#function-removesubtaskresult)


Removes result from the storage 


### function GetSubTaskResults

```cpp
virtual std::vector< SGProcessing::SubTaskResult > GetSubTaskResults(
    const std::set< std::string > & subTaskIds
) =0
```


**Parameters**: 

  * **subTaskIds** - list of subtask ids 


**Return**: results 

**Reimplemented by**: [sgns::processing::SubTaskResultStorageImpl::GetSubTaskResults](/source-reference/Classes/d3/df7/classsgns_1_1processing_1_1_sub_task_result_storage_impl/#function-getsubtaskresults)


Returns results for specified subtask ids 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
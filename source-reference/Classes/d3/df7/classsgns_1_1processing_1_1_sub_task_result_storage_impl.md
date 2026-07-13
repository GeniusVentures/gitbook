---
title: sgns::processing::SubTaskResultStorageImpl
summary: Handles subtask result storage. 

---

# sgns::processing::SubTaskResultStorageImpl



Handles subtask result storage. 


`#include <processing_subtask_result_storage_impl.hpp>`

Inherits from [sgns::processing::SubTaskResultStorage](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[SubTaskResultStorageImpl](/source-reference/Classes/d3/df7/classsgns_1_1processing_1_1_sub_task_result_storage_impl/#function-subtaskresultstorageimpl)**(std::shared_ptr< [crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) > db, std::string topic) |
| | **[~SubTaskResultStorageImpl](/source-reference/Classes/d3/df7/classsgns_1_1processing_1_1_sub_task_result_storage_impl/#function-~subtaskresultstorageimpl)**() override |
| virtual void | **[AddSubTaskResult](/source-reference/Classes/d3/df7/classsgns_1_1processing_1_1_sub_task_result_storage_impl/#function-addsubtaskresult)**(const SGProcessing::SubTaskResult & result) override |
| virtual void | **[RemoveSubTaskResult](/source-reference/Classes/d3/df7/classsgns_1_1processing_1_1_sub_task_result_storage_impl/#function-removesubtaskresult)**(const std::string & subTaskId) override |
| virtual std::vector< SGProcessing::SubTaskResult > | **[GetSubTaskResults](/source-reference/Classes/d3/df7/classsgns_1_1processing_1_1_sub_task_result_storage_impl/#function-getsubtaskresults)**(const std::set< std::string > & subTaskIds) override |

## Additional inherited members

**Public Functions inherited from [sgns::processing::SubTaskResultStorage](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~SubTaskResultStorage](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/#function-~subtaskresultstorage)**() =default |


## Public Functions Documentation

### function SubTaskResultStorageImpl

```cpp
SubTaskResultStorageImpl(
    std::shared_ptr< crdt::GlobalDB > db,
    std::string topic
)
```


**Parameters**: 

  * **db** - CRDT GlobalDB to use. 
  * **topic** - Topic prefix for result keys. 


Create a subtask storage. 


### function ~SubTaskResultStorageImpl

```cpp
~SubTaskResultStorageImpl() override
```


### function AddSubTaskResult

```cpp
virtual void AddSubTaskResult(
    const SGProcessing::SubTaskResult & result
) override
```


**Parameters**: 

  * **result** - Result to add 


**Reimplements**: [sgns::processing::SubTaskResultStorage::AddSubTaskResult](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/#function-addsubtaskresult)


Add a subtask result 


### function RemoveSubTaskResult

```cpp
virtual void RemoveSubTaskResult(
    const std::string & subTaskId
) override
```


**Parameters**: 

  * **subTaskId** - Result ID to remove 


**Reimplements**: [sgns::processing::SubTaskResultStorage::RemoveSubTaskResult](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/#function-removesubtaskresult)


Remove a subtask result 


### function GetSubTaskResults

```cpp
virtual std::vector< SGProcessing::SubTaskResult > GetSubTaskResults(
    const std::set< std::string > & subTaskIds
) override
```


**Parameters**: 

  * **subTaskIds** - List of subtask IDs to get results for. 


**Reimplements**: [sgns::processing::SubTaskResultStorage::GetSubTaskResults](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/#function-getsubtaskresults)


Get results for subtasks. 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
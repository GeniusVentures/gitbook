---
title: sgns::processing

---

# sgns::processing



 [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::processing::ProcessingCoreImpl](/source-reference/Classes/d0/d7f/classsgns_1_1processing_1_1_processing_core_impl/)** <br/>Default implementation of [ProcessingCore](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/) backed by GlobalDB.  |
| class | **[sgns::processing::SubTaskResultStorageImpl](/source-reference/Classes/d3/df7/classsgns_1_1processing_1_1_sub_task_result_storage_impl/)** <br/>Handles subtask result storage.  |
| class | **[sgns::processing::TaskKeys](/source-reference/Classes/d9/df3/classsgns_1_1processing_1_1_task_keys/)**  |
| class | **[sgns::processing::TaskQueueImpl](/source-reference/Classes/dd/ddf/classsgns_1_1processing_1_1_task_queue_impl/)** <br/>Implements the task storage on CRDT.  |
| class | **[sgns::processing::ProcessingCore](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/)** <br/>Processing core interface.  |
| class | **[sgns::processing::ProcessingEngine](/source-reference/Classes/dc/d00/classsgns_1_1processing_1_1_processing_engine/)** <br/>Handles subtask processing and result aggregation.  |
| class | **[sgns::processing::ProcessingNode](/source-reference/Classes/d2/d5b/classsgns_1_1processing_1_1_processing_node/)** <br/>Node for distributed computation.  |
| class | **[sgns::processing::ProcessingServiceImpl](/source-reference/Classes/dd/d81/classsgns_1_1processing_1_1_processing_service_impl/)**  |
| class | **[sgns::processing::SubTaskEnqueuer](/source-reference/Classes/d2/d46/classsgns_1_1processing_1_1_sub_task_enqueuer/)**  |
| class | **[sgns::processing::SubTaskEnqueuerImpl](/source-reference/Classes/d1/d37/classsgns_1_1processing_1_1_sub_task_enqueuer_impl/)**  |
| class | **[sgns::processing::ProcessingSubTaskQueue](/source-reference/Classes/d8/d64/classsgns_1_1processing_1_1_processing_sub_task_queue/)** <br/>Distributed subtask queue implementation.  |
| class | **[sgns::processing::SubTaskQueueAccessor](/source-reference/Classes/dd/d1c/classsgns_1_1processing_1_1_sub_task_queue_accessor/)**  |
| class | **[sgns::processing::SubTaskQueueAccessorImpl](/source-reference/Classes/d0/dab/classsgns_1_1processing_1_1_sub_task_queue_accessor_impl/)** <br/>Subtask queue accessor implementation.  |
| class | **[sgns::processing::ProcessingSubTaskQueueChannel](/source-reference/Classes/d7/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_channel/)**  |
| class | **[sgns::processing::ProcessingSubTaskQueueChannelPubSub](/source-reference/Classes/dd/d85/classsgns_1_1processing_1_1_processing_sub_task_queue_channel_pub_sub/)**  |
| class | **[sgns::processing::ProcessingSubTaskQueueManager](/source-reference/Classes/d4/d2b/classsgns_1_1processing_1_1_processing_sub_task_queue_manager/)** <br/>Distributed subtask queue manager.  |
| class | **[sgns::processing::SubTaskResultStorage](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/)**  |
| class | **[sgns::processing::ProcessingTaskQueue](/source-reference/Classes/d3/d40/classsgns_1_1processing_1_1_processing_task_queue/)**  |
| class | **[sgns::processing::ProcessTaskSplitter](/source-reference/Classes/d7/de8/classsgns_1_1processing_1_1_process_task_splitter/)**  |
| class | **[sgns::processing::ProcessingValidationCore](/source-reference/Classes/d0/d2c/classsgns_1_1processing_1_1_processing_validation_core/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| [base::Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) | **[TaskQueueImplLogger](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/#function-taskqueueimpllogger)**() |
| std::string | **[generate_uuid_with_ipfs_id](/source-reference/Namespaces/df/d6a/namespacesgns_1_1processing/#function-generate_uuid_with_ipfs_id)**(const std::string & ipfs_id) |

## Detailed Description


Header file for the distrubuted processing Room creativeid00

Header file for the distributed processing Room creativeid00

Header file for the distrubuted processing node creativeid00

Header file for the distributed subtasks queue creativeid00

Header file for subtask queue accessor interface creativeid00

Header file for subtask queue accessor implementation creativeid00

Header file for subtask queue channel interface creativeid00

Header file for the distributed subtasks queue SuperGenius/Creative00

Header file for the distrubuted task queue creativeid00 


## Functions Documentation

### function TaskQueueImplLogger

```cpp
base::Logger TaskQueueImplLogger()
```


### function generate_uuid_with_ipfs_id

```cpp
std::string generate_uuid_with_ipfs_id(
    const std::string & ipfs_id
)
```






-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
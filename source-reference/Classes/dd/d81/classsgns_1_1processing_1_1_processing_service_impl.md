---
title: sgns::processing::ProcessingServiceImpl

---

# sgns::processing::ProcessingServiceImpl






`#include <processing_service.hpp>`

Inherits from std::enable_shared_from_this< ProcessingServiceImpl >

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[ProcessingStatus](/source-reference/Classes/d7/d27/structsgns_1_1processing_1_1_processing_service_impl_1_1_processing_status/)**  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class uint8_t | **[Status](/source-reference/Classes/dd/d81/classsgns_1_1processing_1_1_processing_service_impl/#enum-status)** { DISABLED, IDLE, PROCESSING} |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[ProcessingServiceImpl](/source-reference/Classes/dd/d81/classsgns_1_1processing_1_1_processing_service_impl/#function-processingserviceimpl)**(std::shared_ptr< ipfs_pubsub::GossipPubSub > gossipPubSub, size_t maximalNodesCount, std::shared_ptr< [SubTaskEnqueuer](/source-reference/Classes/d2/d46/classsgns_1_1processing_1_1_sub_task_enqueuer/) > subTaskEnqueuer, std::shared_ptr< [SubTaskResultStorage](/source-reference/Classes/d0/d47/classsgns_1_1processing_1_1_sub_task_result_storage/) > subTaskResultStorage, std::shared_ptr< [ProcessingCore](/source-reference/Classes/d6/da7/classsgns_1_1processing_1_1_processing_core/) > processingCore, std::function< void(const std::string &subTaskQueueId, const SGProcessing::TaskResult &taskresult)> userCallbackSuccess, std::function< void(const std::string &subTaskQueueId)> userCallbackError, std::string node_address)<br/>Constructs a processing service with user callbacks.  |
| | **[~ProcessingServiceImpl](/source-reference/Classes/dd/d81/classsgns_1_1processing_1_1_processing_service_impl/#function-~processingserviceimpl)**() |
| void | **[StartProcessing](/source-reference/Classes/dd/d81/classsgns_1_1processing_1_1_processing_service_impl/#function-startprocessing)**(const std::string & processingGridChannelId) |
| void | **[StopProcessing](/source-reference/Classes/dd/d81/classsgns_1_1processing_1_1_processing_service_impl/#function-stopprocessing)**() |
| size_t | **[GetProcessingNodesCount](/source-reference/Classes/dd/d81/classsgns_1_1processing_1_1_processing_service_impl/#function-getprocessingnodescount)**() const |
| void | **[SetChannelListRequestTimeout](/source-reference/Classes/dd/d81/classsgns_1_1processing_1_1_processing_service_impl/#function-setchannellistrequesttimeout)**(boost::posix_time::time_duration channelListRequestTimeout) |
| [ProcessingStatus](/source-reference/Classes/d7/d27/structsgns_1_1processing_1_1_processing_service_impl_1_1_processing_status/) | **[GetProcessingStatus](/source-reference/Classes/dd/d81/classsgns_1_1processing_1_1_processing_service_impl/#function-getprocessingstatus)**() const |

## Public Types Documentation

### enum Status

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| DISABLED | |   |
| IDLE | |   |
| PROCESSING | |   |




## Public Functions Documentation

### function ProcessingServiceImpl

```cpp
ProcessingServiceImpl(
    std::shared_ptr< ipfs_pubsub::GossipPubSub > gossipPubSub,
    size_t maximalNodesCount,
    std::shared_ptr< SubTaskEnqueuer > subTaskEnqueuer,
    std::shared_ptr< SubTaskResultStorage > subTaskResultStorage,
    std::shared_ptr< ProcessingCore > processingCore,
    std::function< void(const std::string &subTaskQueueId, const SGProcessing::TaskResult &taskresult)> userCallbackSuccess,
    std::function< void(const std::string &subTaskQueueId)> userCallbackError,
    std::string node_address
)
```

Constructs a processing service with user callbacks. 

**Parameters**: 

  * **gossipPubSub** PubSub service. 
  * **maximalNodesCount** Max number of processing nodes handled by the service. 
  * **subTaskEnqueuer** Subtask enqueuer used to dispatch tasks. 
  * **subTaskResultStorage** Storage for subtask results. 
  * **processingCore** Processing core used to execute subtasks. 
  * **userCallbackSuccess** Callback invoked on successful task completion. 
  * **userCallbackError** Callback invoked on task error. 
  * **node_address** Local node address used in coordination. 


### function ~ProcessingServiceImpl

```cpp
~ProcessingServiceImpl()
```


### function StartProcessing

```cpp
void StartProcessing(
    const std::string & processingGridChannelId
)
```


### function StopProcessing

```cpp
void StopProcessing()
```


### function GetProcessingNodesCount

```cpp
size_t GetProcessingNodesCount() const
```


### function SetChannelListRequestTimeout

```cpp
void SetChannelListRequestTimeout(
    boost::posix_time::time_duration channelListRequestTimeout
)
```


### function GetProcessingStatus

```cpp
ProcessingStatus GetProcessingStatus() const
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
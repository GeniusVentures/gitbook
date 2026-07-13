---
title: sgns::processing::TaskKeys

---

# sgns::processing::TaskKeys






`#include <TaskKeys.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::string | **[ProcessingPrefix](/source-reference/Classes/d9/df3/classsgns_1_1processing_1_1_task_keys/#function-processingprefix)**()<br/>Returns the processing base prefix for the task queue.  |
| std::string | **[TaskListKey](/source-reference/Classes/d9/df3/classsgns_1_1processing_1_1_task_keys/#function-tasklistkey)**() |
| std::string | **[SubTaskListKey](/source-reference/Classes/d9/df3/classsgns_1_1processing_1_1_task_keys/#function-subtasklistkey)**() |
| std::string | **[SubTaskListKey](/source-reference/Classes/d9/df3/classsgns_1_1processing_1_1_task_keys/#function-subtasklistkey)**(std::string_view taskId) |
| std::string | **[TaskKey](/source-reference/Classes/d9/df3/classsgns_1_1processing_1_1_task_keys/#function-taskkey)**(std::string_view taskId) |
| std::string | **[SubTaskKey](/source-reference/Classes/d9/df3/classsgns_1_1processing_1_1_task_keys/#function-subtaskkey)**(std::string_view taskId, std::string_view subTaskId) |
| std::string | **[ClaimableListKey](/source-reference/Classes/d9/df3/classsgns_1_1processing_1_1_task_keys/#function-claimablelistkey)**() |
| std::string | **[ClaimableTaskKey](/source-reference/Classes/d9/df3/classsgns_1_1processing_1_1_task_keys/#function-claimabletaskkey)**(std::string_view taskId) |
| std::string | **[ResultTaskKey](/source-reference/Classes/d9/df3/classsgns_1_1processing_1_1_task_keys/#function-resulttaskkey)**(std::string_view taskId) |
| std::string | **[LockKey](/source-reference/Classes/d9/df3/classsgns_1_1processing_1_1_task_keys/#function-lockkey)**(std::string_view taskKey) |

## Public Functions Documentation

### function ProcessingPrefix

```cpp
static inline std::string ProcessingPrefix()
```

Returns the processing base prefix for the task queue. 

**Return**: "/<prefix_base 

### function TaskListKey

```cpp
static inline std::string TaskListKey()
```


### function SubTaskListKey

```cpp
static inline std::string SubTaskListKey()
```


### function SubTaskListKey

```cpp
static inline std::string SubTaskListKey(
    std::string_view taskId
)
```


### function TaskKey

```cpp
static inline std::string TaskKey(
    std::string_view taskId
)
```


### function SubTaskKey

```cpp
static inline std::string SubTaskKey(
    std::string_view taskId,
    std::string_view subTaskId
)
```


### function ClaimableListKey

```cpp
static inline std::string ClaimableListKey()
```


### function ClaimableTaskKey

```cpp
static inline std::string ClaimableTaskKey(
    std::string_view taskId
)
```


### function ResultTaskKey

```cpp
static inline std::string ResultTaskKey(
    std::string_view taskId
)
```


### function LockKey

```cpp
static inline std::string LockKey(
    std::string_view taskKey
)
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
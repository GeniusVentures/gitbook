---
title: sgns::processing::ProcessTaskSplitter

---

# sgns::processing::ProcessTaskSplitter






`#include <processing_tasksplit.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[ProcessTaskSplitter](/source-reference/Classes/d7/de8/classsgns_1_1processing_1_1_process_task_splitter/#function-processtasksplitter)**() |
| void | **[SplitTask](/source-reference/Classes/d7/de8/classsgns_1_1processing_1_1_process_task_splitter/#function-splittask)**(const SGProcessing::Task & task, std::list< SGProcessing::SubTask > & subTasks, std::string json_data, uint32_t numchunks, bool addvalidationsubtask, std::string ipfsid) |

## Public Functions Documentation

### function ProcessTaskSplitter

```cpp
ProcessTaskSplitter()
```


### function SplitTask

```cpp
void SplitTask(
    const SGProcessing::Task & task,
    std::list< SGProcessing::SubTask > & subTasks,
    std::string json_data,
    uint32_t numchunks,
    bool addvalidationsubtask,
    std::string ipfsid
)
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
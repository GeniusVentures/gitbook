---
title: sgns::GeniusAssigner::AssignerOutput

---

# sgns::GeniusAssigner::AssignerOutput






`#include <GeniusAssigner.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[AssignerOutput](/source-reference/Classes/d2/deb/structsgns_1_1_genius_assigner_1_1_assigner_output/#function-assigneroutput)**([PlonkConstraintSystemType](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-plonkconstraintsystemtype) new_constrains, [PlonkAssignTableType](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-plonkassigntabletype) new_table) |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [PlonkConstraintSystemType](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-plonkconstraintsystemtype) | **[constrains](/source-reference/Classes/d2/deb/structsgns_1_1_genius_assigner_1_1_assigner_output/#variable-constrains)**  |
| [PlonkAssignTableType](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-plonkassigntabletype) | **[table](/source-reference/Classes/d2/deb/structsgns_1_1_genius_assigner_1_1_assigner_output/#variable-table)**  |

## Public Functions Documentation

### function AssignerOutput

```cpp
inline explicit AssignerOutput(
    PlonkConstraintSystemType new_constrains,
    PlonkAssignTableType new_table
)
```


## Public Attributes Documentation

### variable constrains

```cpp
PlonkConstraintSystemType constrains;
```


### variable table

```cpp
PlonkAssignTableType table;
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
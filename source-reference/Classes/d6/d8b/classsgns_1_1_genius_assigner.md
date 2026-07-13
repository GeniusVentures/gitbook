---
title: sgns::GeniusAssigner

---

# sgns::GeniusAssigner






`#include <GeniusAssigner.hpp>`

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[AssignerOutput](/source-reference/Classes/d2/deb/structsgns_1_1_genius_assigner_1_1_assigner_output/)**  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[AssignerError](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#enum-assignererror)** { EMPTY_BYTECODE = 0, BYTECODE_MISMATCH, HAS_SIZE_ESTIMATION, TABLE_PATH_ERROR, CIRCUIT_PATH_ERROR, SELECTOR_COLUMNS_INVALID, WRONG_TARGET_PROVER, UNSATISFIED_CIRCUIT, TABLE_CIRCUIT_NUM_MISMATCH, CIRCUIT_NOT_FOUND} |
| using crypto3::zk::snark::plonk_table_description< [BlueprintFieldType](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-blueprintfieldtype) > | **[TableDescriptionType](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-tabledescriptiontype)**  |
| using crypto3::marshalling::types::plonk_constraint_system< nil::marshalling::field_type< [AssignerEndianess](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-assignerendianess) >, [ConstraintSystemType](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-constraintsystemtype) > | **[PlonkConstraintSystemType](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-plonkconstraintsystemtype)**  |
| using crypto3::marshalling::types::plonk_assignment_table< nil::marshalling::field_type< [AssignerEndianess](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-assignerendianess) >, [AssignmentTableType](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-assignmenttabletype) > | **[PlonkAssignTableType](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-plonkassigntabletype)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[GeniusAssigner](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#function-geniusassigner)**() |
| | **[~GeniusAssigner](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#function-~geniusassigner)**() =default |
| outcome::result< std::vector< [AssignerOutput](/source-reference/Classes/d2/deb/structsgns_1_1_genius_assigner_1_1_assigner_output/) > > | **[GenerateCircuitAndTable](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#function-generatecircuitandtable)**(const boost::json::array & public_inputs_json, const boost::json::array & private_inputs_json, const std::string & bytecode_file_payload) |
| outcome::result< std::vector< [AssignerOutput](/source-reference/Classes/d2/deb/structsgns_1_1_genius_assigner_1_1_assigner_output/) > > | **[GenerateCircuitAndTable](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#function-generatecircuitandtable)**(const std::vector< int > & public_inputs, const std::vector< int > & private_inputs, const std::string & bytecode_file_payload) |
| outcome::result< void > | **[PrintCircuitAndTable](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#function-printcircuitandtable)**(const std::vector< [AssignerOutput](/source-reference/Classes/d2/deb/structsgns_1_1_genius_assigner_1_1_assigner_output/) > & public_inputs, const std::string & table_path, const std::string & circuit_path) |
| const [TableDescriptionType](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#using-tabledescriptiontype) & | **[GetPlonkTableDescription](/source-reference/Classes/d6/d8b/classsgns_1_1_genius_assigner/#function-getplonktabledescription)**() |

## Public Types Documentation

### enum AssignerError

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| EMPTY_BYTECODE | 0|   |
| BYTECODE_MISMATCH | |   |
| HAS_SIZE_ESTIMATION | |   |
| TABLE_PATH_ERROR | |   |
| CIRCUIT_PATH_ERROR | |   |
| SELECTOR_COLUMNS_INVALID | |   |
| WRONG_TARGET_PROVER | |   |
| UNSATISFIED_CIRCUIT | |   |
| TABLE_CIRCUIT_NUM_MISMATCH | |   |
| CIRCUIT_NOT_FOUND | |   |




### using TableDescriptionType

```cpp
using sgns::GeniusAssigner::TableDescriptionType = crypto3::zk::snark::plonk_table_description<BlueprintFieldType>;
```


### using PlonkConstraintSystemType

```cpp
using sgns::GeniusAssigner::PlonkConstraintSystemType = 
crypto3::marshalling::types::plonk_constraint_system<nil::marshalling::field_type<AssignerEndianess>,
                                                     ConstraintSystemType>;
```


### using PlonkAssignTableType

```cpp
using sgns::GeniusAssigner::PlonkAssignTableType = 
crypto3::marshalling::types::plonk_assignment_table<nil::marshalling::field_type<AssignerEndianess>,
                                                    AssignmentTableType>;
```


## Public Functions Documentation

### function GeniusAssigner

```cpp
inline GeniusAssigner()
```


### function ~GeniusAssigner

```cpp
~GeniusAssigner() =default
```


### function GenerateCircuitAndTable

```cpp
outcome::result< std::vector< AssignerOutput > > GenerateCircuitAndTable(
    const boost::json::array & public_inputs_json,
    const boost::json::array & private_inputs_json,
    const std::string & bytecode_file_payload
)
```


### function GenerateCircuitAndTable

```cpp
outcome::result< std::vector< AssignerOutput > > GenerateCircuitAndTable(
    const std::vector< int > & public_inputs,
    const std::vector< int > & private_inputs,
    const std::string & bytecode_file_payload
)
```


### function PrintCircuitAndTable

```cpp
outcome::result< void > PrintCircuitAndTable(
    const std::vector< AssignerOutput > & public_inputs,
    const std::string & table_path,
    const std::string & circuit_path
)
```


### function GetPlonkTableDescription

```cpp
static inline const TableDescriptionType & GetPlonkTableDescription()
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
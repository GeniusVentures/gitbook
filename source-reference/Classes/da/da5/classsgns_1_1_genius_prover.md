---
title: sgns::GeniusProver
summary: Prover class of SuperGenius. 

---

# sgns::GeniusProver



Prover class of SuperGenius. 


`#include <GeniusProver.hpp>`

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[GeniusProof](/source-reference/Classes/d0/d7f/structsgns_1_1_genius_prover_1_1_genius_proof/)**  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[ProverError](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#enum-provererror)** { INVALID_PROOF_GENERATED = 0, TABLE_PATH_ERROR, CIRCUIT_PATH_ERROR, PROOF_PATH_ERROR, EMPTY_PROOF} |
| using crypto3::zk::snark::placeholder_proof< [BlueprintFieldType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-blueprintfieldtype), [PlaceholderParams](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-placeholderparams) > | **[ProofSnarkType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-proofsnarktype)**  |
| using crypto3::marshalling::types::placeholder_proof< nil::marshalling::field_type< [ProverEndianess](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-proverendianess) >, [ProofSnarkType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-proofsnarktype) > | **[ProofType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-prooftype)**  |
| using crypto3::marshalling::types::plonk_constraint_system< nil::marshalling::field_type< [ProverEndianess](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-proverendianess) >, [ConstraintSystemType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-constraintsystemtype) > | **[ConstraintMarshallingType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-constraintmarshallingtype)**  |
| using crypto3::marshalling::types::plonk_assignment_table< nil::marshalling::field_type< [ProverEndianess](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-proverendianess) >, [AssignmentTableType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-assignmenttabletype) > | **[PlonkMarshalledTableType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-plonkmarshalledtabletype)**  |
| using std::vector< BlueprintFieldType::value_type > | **[ParameterType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-parametertype)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[GeniusProver](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#function-geniusprover)**()<br/>Constructs a [GeniusProver](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/) with default settings.  |
| outcome::result< [GeniusProof](/source-reference/Classes/d0/d7f/structsgns_1_1_genius_prover_1_1_genius_proof/) > | **[CreateProof](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#function-createproof)**(const [GeniusAssigner::AssignerOutput](/source-reference/Classes/d2/deb/structsgns_1_1_genius_assigner_1_1_assigner_output/) & assigner_outputs) const |
| outcome::result< [GeniusProof](/source-reference/Classes/d0/d7f/structsgns_1_1_genius_prover_1_1_genius_proof/) > | **[CreateProof](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#function-createproof)**(const std::string & circuit_file, const std::string & assignment_table_file) const |
| bool | **[WriteProofToFile](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#function-writeprooftofile)**(const [ProofType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-prooftype) & proof, const std::string & path) const |
| std::vector< uint8_t > | **[WriteProofToVector](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#function-writeprooftovector)**(const [ProofType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-prooftype) & proof) const |
| bool | **[VerifyProof](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#function-verifyproof)**(const [GeniusProof](/source-reference/Classes/d0/d7f/structsgns_1_1_genius_prover_1_1_genius_proof/) & proof) |
| bool | **[VerifyProof](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#function-verifyproof)**(const [ProofType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-prooftype) & proof, const [GeniusAssigner::AssignerOutput](/source-reference/Classes/d2/deb/structsgns_1_1_genius_assigner_1_1_assigner_output/) & assigner_outputs) |
| bool | **[VerifyProof](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#function-verifyproof)**(const [ProofSnarkType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-proofsnarktype) & proof, const [PublicPreprocessedData](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-publicpreprocesseddata) & public_data, const [TableDescriptionType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-tabledescriptiontype) & desc, const [ConstraintSystemType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-constraintsystemtype) & constrains_sys, const [LpcScheme](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-lpcscheme) & scheme, std::vector< [ParameterType](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/#using-parametertype) > pub_parameters) |

## Public Types Documentation

### enum ProverError

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| INVALID_PROOF_GENERATED | 0|   |
| TABLE_PATH_ERROR | |   |
| CIRCUIT_PATH_ERROR | |   |
| PROOF_PATH_ERROR | |   |
| EMPTY_PROOF | |   |




### using ProofSnarkType

```cpp
using sgns::GeniusProver::ProofSnarkType = crypto3::zk::snark::placeholder_proof<BlueprintFieldType, PlaceholderParams>;
```


### using ProofType

```cpp
using sgns::GeniusProver::ProofType = crypto3::marshalling::types::placeholder_proof<nil::marshalling::field_type<ProverEndianess>,
                                                                        ProofSnarkType>;
```


### using ConstraintMarshallingType

```cpp
using sgns::GeniusProver::ConstraintMarshallingType = 
crypto3::marshalling::types::plonk_constraint_system<nil::marshalling::field_type<ProverEndianess>,
                                                     ConstraintSystemType>;
```


### using PlonkMarshalledTableType

```cpp
using sgns::GeniusProver::PlonkMarshalledTableType = 
crypto3::marshalling::types::plonk_assignment_table<nil::marshalling::field_type<ProverEndianess>,
                                                    AssignmentTableType>;
```


### using ParameterType

```cpp
using sgns::GeniusProver::ParameterType = std::vector<BlueprintFieldType::value_type>;
```


## Public Functions Documentation

### function GeniusProver

```cpp
inline GeniusProver()
```

Constructs a [GeniusProver](/source-reference/Classes/da/da5/classsgns_1_1_genius_prover/) with default settings. 

### function CreateProof

```cpp
outcome::result< GeniusProof > CreateProof(
    const GeniusAssigner::AssignerOutput & assigner_outputs
) const
```


### function CreateProof

```cpp
outcome::result< GeniusProof > CreateProof(
    const std::string & circuit_file,
    const std::string & assignment_table_file
) const
```


### function WriteProofToFile

```cpp
bool WriteProofToFile(
    const ProofType & proof,
    const std::string & path
) const
```


### function WriteProofToVector

```cpp
std::vector< uint8_t > WriteProofToVector(
    const ProofType & proof
) const
```


### function VerifyProof

```cpp
static bool VerifyProof(
    const GeniusProof & proof
)
```


### function VerifyProof

```cpp
static bool VerifyProof(
    const ProofType & proof,
    const GeniusAssigner::AssignerOutput & assigner_outputs
)
```


### function VerifyProof

```cpp
static bool VerifyProof(
    const ProofSnarkType & proof,
    const PublicPreprocessedData & public_data,
    const TableDescriptionType & desc,
    const ConstraintSystemType & constrains_sys,
    const LpcScheme & scheme,
    std::vector< ParameterType > pub_parameters
)
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
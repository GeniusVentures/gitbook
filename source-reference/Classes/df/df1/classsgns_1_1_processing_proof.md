---
title: sgns::ProcessingProof
summary: A class for generating and verifying processing proofs. 

---

# sgns::ProcessingProof



A class for generating and verifying processing proofs.  [More...](#detailed-description)


`#include <ProcessingProof.hpp>`

Inherits from [sgns::IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[ProcessingProof](/source-reference/Classes/df/df1/classsgns_1_1_processing_proof/#function-processingproof)**(std::string subtask_id)<br/>Constructor for the [ProcessingProof](/source-reference/Classes/df/df1/classsgns_1_1_processing_proof/) class.  |
| | **[~ProcessingProof](/source-reference/Classes/df/df1/classsgns_1_1_processing_proof/#function-~processingproof)**() =default<br/>Destructor for the [ProcessingProof](/source-reference/Classes/df/df1/classsgns_1_1_processing_proof/) class.  |
| virtual std::string | **[GetProofType](/source-reference/Classes/df/df1/classsgns_1_1_processing_proof/#function-getprooftype)**() const override<br/>Retrieves the type of proof for processings.  |

## Additional inherited members

**Public Types inherited from [sgns::IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/)**

|                | Name           |
| -------------- | -------------- |
| enum class| **[Error](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#enum-error)** { INSUFFICIENT_FUNDS, INVALID_PROOF, BYTECODE_NOT_FOUND, INVALID_CIRCUIT, INVALID_PROTO_PROOF, INVALID_PROOF_TYPE, UNEXPECTED_PROOF_TYPE, INVALID_PUBLIC_PARAMETERS}<br/>Enumeration of error codes used in the proof classes.  |
| using std::function< outcome::result< std::pair< boost::json::array, boost::json::array > >(const std::vector< uint8_t > &)> | **[PublicParamDeserializeFn](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#using-publicparamdeserializefn)** <br/>Alias for the de-serializer method type to be implemented in derived classes.  |

**Public Functions inherited from [sgns::IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/)**

|                | Name           |
| -------------- | -------------- |
| | **[IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-ibasicproof)**(std::string bytecode_payload)<br/>Constructs a proof and informs the bytecode that will be used.  |
| virtual | **[~IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-~ibasicproof)**() =default<br/>Virtual destructor for [IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/).  |
| outcome::result< std::vector< uint8_t > > | **[GenerateFullProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-generatefullproof)**()<br/>Generates a full proof using the internal class values.  |
| outcome::result< bool > | **[VerifyFullProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-verifyfullproof)**(const std::vector< uint8_t > & full_proof_data)<br/>Verifies the proof with the public parameters.  |
| outcome::result< bool > | **[VerifyFullProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-verifyfullproof)**(const std::pair< boost::json::array, boost::json::array > & parameters, const SGProof::BaseProofData & proof_data, std::string proof_bytecode)<br/>Verifies the proof with parameters and bytecode.  |
| boost::json::object | **[GenerateIntParameter](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-generateintparameter)**(uint64_t value)<br/>Generates a JSON object for an integer parameter.  |
| template <std::size_t N\> <br/>boost::json::object | **[GenerateArrayParameter](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-generatearrayparameter)**(const std::array< uint64_t, N > & values)<br/>Generates a JSON object for an array parameter.  |
| boost::json::object | **[GenerateFieldParameter](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-generatefieldparameter)**(uint64_t value)<br/>Generates a JSON object for a field parameter.  |

**Protected Functions inherited from [sgns::IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/)**

|                | Name           |
| -------------- | -------------- |
| void | **[RegisterDeserializer](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-registerdeserializer)**(const std::string & proof_type, [PublicParamDeserializeFn](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#using-publicparamdeserializefn) fn)<br/>Registers a deserializer function for a specific proof type.  |
| void | **[RegisterBytecode](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-registerbytecode)**(const std::string & proof_type, std::string bytecode)<br/>Registers a bytecode for a specific proof type.  |
| outcome::result< SGProof::BaseProofProto > | **[DeSerializeBaseProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-deserializebaseproof)**(const std::vector< uint8_t > & proof_data)<br/>Deserializes a BaseProofProto from the provided proof data.  |

**Protected Attributes inherited from [sgns::IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/)**

|                | Name           |
| -------------- | -------------- |
| std::map< std::string, [PublicParamDeserializeFn](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#using-publicparamdeserializefn) > | **[PublicParamDeSerializers](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#variable-publicparamdeserializers)** <br/>A map of deserialization functions for public parameters by proof type.  |
| std::map< std::string, std::string > | **[ByteCodeMap](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#variable-bytecodemap)** <br/>A map of bytecodes associated with each proof type.  |


## Detailed Description

```cpp
class sgns::ProcessingProof;
```

A class for generating and verifying processing proofs. 



```
         ProcessingProof is a derived class from IBasicProof, providing the specific
         implementation for handling processing of funds proof generation and verification.
```

## Public Functions Documentation

### function ProcessingProof

```cpp
inline explicit ProcessingProof(
    std::string subtask_id
)
```

Constructor for the [ProcessingProof](/source-reference/Classes/df/df1/classsgns_1_1_processing_proof/) class. 

**Parameters**: 

  * **subtask_id** Subtask identifier used in proof context. 


### function ~ProcessingProof

```cpp
~ProcessingProof() =default
```

Destructor for the [ProcessingProof](/source-reference/Classes/df/df1/classsgns_1_1_processing_proof/) class. 

### function GetProofType

```cpp
inline virtual std::string GetProofType() const override
```

Retrieves the type of proof for processings. 

**Return**: A string representing the type of the proof. 

**Reimplements**: [sgns::IBasicProof::GetProofType](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-getprooftype)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
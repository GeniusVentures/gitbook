---
title: sgns::IBasicProof
summary: Base proof class header file. 

---

# sgns::IBasicProof



Base proof class header file.  [More...](#detailed-description)


`#include <IBasicProof.hpp>`

Inherited by [sgns::ProcessingProof](/source-reference/Classes/df/df1/classsgns_1_1_processing_proof/), [sgns::TransferProof](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/)

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[Error](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#enum-error)** { INSUFFICIENT_FUNDS = 0, INVALID_PROOF, BYTECODE_NOT_FOUND, INVALID_CIRCUIT, INVALID_PROTO_PROOF, INVALID_PROOF_TYPE, UNEXPECTED_PROOF_TYPE, INVALID_PUBLIC_PARAMETERS}<br/>Enumeration of error codes used in the proof classes.  |
| using std::function< outcome::result< std::pair< boost::json::array, boost::json::array > >(const std::vector< uint8_t > &)> | **[PublicParamDeserializeFn](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#using-publicparamdeserializefn)** <br/>Alias for the de-serializer method type to be implemented in derived classes.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-ibasicproof)**(std::string bytecode_payload)<br/>Constructs a proof and informs the bytecode that will be used.  |
| virtual | **[~IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-~ibasicproof)**() =default<br/>Virtual destructor for [IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/).  |
| virtual std::string | **[GetProofType](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-getprooftype)**() const =0<br/>Pure virtual function to get the proof type.  |
| outcome::result< std::vector< uint8_t > > | **[GenerateFullProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-generatefullproof)**()<br/>Generates a full proof using the internal class values.  |
| outcome::result< bool > | **[VerifyFullProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-verifyfullproof)**(const std::vector< uint8_t > & full_proof_data)<br/>Verifies the proof with the public parameters.  |
| outcome::result< bool > | **[VerifyFullProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-verifyfullproof)**(const std::pair< boost::json::array, boost::json::array > & parameters, const SGProof::BaseProofData & proof_data, std::string proof_bytecode)<br/>Verifies the proof with parameters and bytecode.  |
| boost::json::object | **[GenerateIntParameter](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-generateintparameter)**(uint64_t value)<br/>Generates a JSON object for an integer parameter.  |
| template <std::size_t N\> <br/>boost::json::object | **[GenerateArrayParameter](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-generatearrayparameter)**(const std::array< uint64_t, N > & values)<br/>Generates a JSON object for an array parameter.  |
| boost::json::object | **[GenerateFieldParameter](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-generatefieldparameter)**(uint64_t value)<br/>Generates a JSON object for a field parameter.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[RegisterDeserializer](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-registerdeserializer)**(const std::string & proof_type, [PublicParamDeserializeFn](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#using-publicparamdeserializefn) fn)<br/>Registers a deserializer function for a specific proof type.  |
| void | **[RegisterBytecode](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-registerbytecode)**(const std::string & proof_type, std::string bytecode)<br/>Registers a bytecode for a specific proof type.  |
| outcome::result< SGProof::BaseProofProto > | **[DeSerializeBaseProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-deserializebaseproof)**(const std::vector< uint8_t > & proof_data)<br/>Deserializes a BaseProofProto from the provided proof data.  |
| virtual outcome::result< std::vector< uint8_t > > | **[SerializeFullProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-serializefullproof)**(const SGProof::BaseProofData & base_proof_data) =0<br/>Pure virtual function to serialize a full proof using the snark and internal public parameters.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| std::map< std::string, [PublicParamDeserializeFn](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#using-publicparamdeserializefn) > | **[PublicParamDeSerializers](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#variable-publicparamdeserializers)** <br/>A map of deserialization functions for public parameters by proof type.  |
| std::map< std::string, std::string > | **[ByteCodeMap](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#variable-bytecodemap)** <br/>A map of bytecodes associated with each proof type.  |

## Detailed Description

```cpp
class sgns::IBasicProof;
```

Base proof class header file. 

This class provides methods for generating full proofs and verifying them, along with virtual methods for derived proofs 

## Public Types Documentation

### enum Error

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| INSUFFICIENT_FUNDS | 0| Insufficient funds error.   |
| INVALID_PROOF | | Invalid proof error.   |
| BYTECODE_NOT_FOUND | | Bytecode not found error.   |
| INVALID_CIRCUIT | | Invalid circuit error.   |
| INVALID_PROTO_PROOF | | Invalid protobuf proof error.   |
| INVALID_PROOF_TYPE | | Invalid proof type error.   |
| UNEXPECTED_PROOF_TYPE | | Unexpected proof type error.   |
| INVALID_PUBLIC_PARAMETERS | | Invalid public parameters error.   |



Enumeration of error codes used in the proof classes. 

### using PublicParamDeserializeFn

```cpp
using sgns::IBasicProof::PublicParamDeserializeFn = std::function<
           outcome::result<std::pair<boost::json::array, boost::json::array>>( const std::vector<uint8_t> & )>;
```

Alias for the de-serializer method type to be implemented in derived classes. 

## Public Functions Documentation

### function IBasicProof

```cpp
explicit IBasicProof(
    std::string bytecode_payload
)
```

Constructs a proof and informs the bytecode that will be used. 

**Parameters**: 

  * **bytecode_payload** Bytecode generated by zkllvm's modified clang 


### function ~IBasicProof

```cpp
virtual ~IBasicProof() =default
```

Virtual destructor for [IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/). 

### function GetProofType

```cpp
virtual std::string GetProofType() const =0
```

Pure virtual function to get the proof type. 

**Return**: A string representing the type of proof. 

**Reimplemented by**: [sgns::ProcessingProof::GetProofType](/source-reference/Classes/df/df1/classsgns_1_1_processing_proof/#function-getprooftype), [sgns::RecursiveTransferProof::GetProofType](/source-reference/Classes/d3/d2f/classsgns_1_1_recursive_transfer_proof/#function-getprooftype), [sgns::TransferProof::GetProofType](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#function-getprooftype)


### function GenerateFullProof

```cpp
outcome::result< std::vector< uint8_t > > GenerateFullProof()
```

Generates a full proof using the internal class values. 

**Return**: A protobuf compatible serialized vector of proof data in bytes. 

### function VerifyFullProof

```cpp
static outcome::result< bool > VerifyFullProof(
    const std::vector< uint8_t > & full_proof_data
)
```

Verifies the proof with the public parameters. 

**Parameters**: 

  * **full_proof_data** The protobuf byte vector representing the proof data and public parameters 


**Return**: If successful returns the validity of the proof. Otherwise it returns [IBasicProof::Error](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#enum-error)

### function VerifyFullProof

```cpp
static outcome::result< bool > VerifyFullProof(
    const std::pair< boost::json::array, boost::json::array > & parameters,
    const SGProof::BaseProofData & proof_data,
    std::string proof_bytecode
)
```

Verifies the proof with parameters and bytecode. 

**Parameters**: 

  * **parameters** Deserialized public parameters and zeroed private parameters. 
  * **proof_data** Proof data to verify. 
  * **proof_bytecode** Serialized proof bytecode. 


**Return**: If successful returns the validity of the proof. Otherwise it returns [IBasicProof::Error](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#enum-error). 

### function GenerateIntParameter

```cpp
static boost::json::object GenerateIntParameter(
    uint64_t value
)
```

Generates a JSON object for an integer parameter. 

**Parameters**: 

  * **value** The integer value to be converted to a JSON object. 


**Return**: A JSON object containing the parameter. 

### function GenerateArrayParameter

```cpp
template <std::size_t N>
static inline boost::json::object GenerateArrayParameter(
    const std::array< uint64_t, N > & values
)
```

Generates a JSON object for an array parameter. 

**Parameters**: 

  * **values** The array of values to be converted to a JSON object. 


**Return**: A JSON object containing the array parameter. 

### function GenerateFieldParameter

```cpp
static boost::json::object GenerateFieldParameter(
    uint64_t value
)
```

Generates a JSON object for a field parameter. 

**Parameters**: 

  * **value** The field value to be converted to a JSON object. 


**Return**: A JSON object containing the field parameter. 

## Protected Functions Documentation

### function RegisterDeserializer

```cpp
static void RegisterDeserializer(
    const std::string & proof_type,
    PublicParamDeserializeFn fn
)
```

Registers a deserializer function for a specific proof type. 

**Parameters**: 

  * **proof_type** The proof type for which the deserializer is registered. 
  * **fn** The deserializer function to be registered. 


### function RegisterBytecode

```cpp
static inline void RegisterBytecode(
    const std::string & proof_type,
    std::string bytecode
)
```

Registers a bytecode for a specific proof type. 

**Parameters**: 

  * **proof_type** The proof type for which the bytecode is registered. 
  * **bytecode** The bytecode to be registered. 


### function DeSerializeBaseProof

```cpp
static outcome::result< SGProof::BaseProofProto > DeSerializeBaseProof(
    const std::vector< uint8_t > & proof_data
)
```

Deserializes a BaseProofProto from the provided proof data. 

**Parameters**: 

  * **proof_data** The byte vector representing the proof data. 


**Return**: A result containing the deserialized BaseProofProto. 

### function SerializeFullProof

```cpp
virtual outcome::result< std::vector< uint8_t > > SerializeFullProof(
    const SGProof::BaseProofData & base_proof_data
) =0
```

Pure virtual function to serialize a full proof using the snark and internal public parameters. 

**Parameters**: 

  * **base_proof_data** The snark that will be embedded on the proof data 


**Return**: A result containing the serialized full proof data in bytes. 

**Reimplemented by**: [sgns::ProcessingProof::SerializeFullProof](/source-reference/Classes/df/df1/classsgns_1_1_processing_proof/#function-serializefullproof), [sgns::RecursiveTransferProof::SerializeFullProof](/source-reference/Classes/d3/d2f/classsgns_1_1_recursive_transfer_proof/#function-serializefullproof), [sgns::TransferProof::SerializeFullProof](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#function-serializefullproof)


## Protected Attributes Documentation

### variable PublicParamDeSerializers

```cpp
static std::map< std::string, PublicParamDeserializeFn > PublicParamDeSerializers;
```

A map of deserialization functions for public parameters by proof type. 

### variable ByteCodeMap

```cpp
static std::map< std::string, std::string > ByteCodeMap;
```

A map of bytecodes associated with each proof type. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
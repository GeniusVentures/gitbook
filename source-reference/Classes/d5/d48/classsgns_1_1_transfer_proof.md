---
title: sgns::TransferProof
summary: A class for generating and verifying transfer proofs. 

---

# sgns::TransferProof



A class for generating and verifying transfer proofs.  [More...](#detailed-description)


`#include <TransferProof.hpp>`

Inherits from [sgns::IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/)

Inherited by [sgns::RecursiveTransferProof](/source-reference/Classes/d3/d2f/classsgns_1_1_recursive_transfer_proof/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[TransferProof](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#function-transferproof)**(uint64_t balance, uint64_t amount, std::optional< std::string > bytecode =std::nullopt)<br/>Constructor for the [TransferProof](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/) class.  |
| | **[~TransferProof](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#function-~transferproof)**() =default<br/>Destructor for the [TransferProof](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/) class.  |
| virtual std::string | **[GetProofType](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#function-getprooftype)**() const override<br/>Retrieves the type of proof for transfers.  |
| boost::json::object | **[GenerateCurveParameter](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#function-generatecurveparameter)**(pallas::template g1_type< coordinates::affine >::value_type value) |
| template <typename T \> <br/>boost::json::object | **[GenerateCurveParameter](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#function-generatecurveparameter)**(T value)<br/>Generates a JSON object for a curve parameter.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| virtual outcome::result< std::vector< uint8_t > > | **[SerializeFullProof](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#function-serializefullproof)**(const SGProof::BaseProofData & base_proof_data) override<br/>Serializes the full proof data and parameters.  |
| virtual std::pair< boost::json::array, boost::json::array > | **[GenerateJsonParameters](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#function-generatejsonparameters)**() override<br/>Generates the parameters in JSON array form.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| uint64_t | **[generator_X_point](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#variable-generator_x_point)** <br/>X coordinate of the generator point.  |
| uint64_t | **[generator_Y_point](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#variable-generator_y_point)** <br/>Y coordinate of the generator point.  |
| uint64_t | **[base_seed](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#variable-base_seed)** <br/>Base seed.  |
| uint64_t | **[provided_totp](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#variable-provided_totp)** <br/>Provided TOTP.  |
| std::array< uint64_t, 4 > | **[ranges](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/#variable-ranges)** <br/>Array of range values used in transfer proofs.  |

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
class sgns::TransferProof;
```

A class for generating and verifying transfer proofs. 



```
         TransferProof is a derived class from IBasicProof, providing the specific
         implementation for handling transfer of funds proof generation and verification.
```

## Public Functions Documentation

### function TransferProof

```cpp
explicit TransferProof(
    uint64_t balance,
    uint64_t amount,
    std::optional< std::string > bytecode =std::nullopt
)
```

Constructor for the [TransferProof](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/) class. 

**Parameters**: 

  * **balance** The balance of the account for the transfer. 
  * **amount** The amount to be transferred. 
  * **bytecode** Optional bytecode override for proof verification. 


### function ~TransferProof

```cpp
~TransferProof() =default
```

Destructor for the [TransferProof](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/) class. 

### function GetProofType

```cpp
inline virtual std::string GetProofType() const override
```

Retrieves the type of proof for transfers. 

**Return**: A string representing the type of the proof. 

**Reimplements**: [sgns::IBasicProof::GetProofType](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-getprooftype)


### function GenerateCurveParameter

```cpp
boost::json::object GenerateCurveParameter(
    pallas::template g1_type< coordinates::affine >::value_type value
)
```


### function GenerateCurveParameter

```cpp
template <typename T >
static boost::json::object GenerateCurveParameter(
    T value
)
```

Generates a JSON object for a curve parameter. 

**Parameters**: 

  * **value** The curve value to be converted to a JSON object. 


**Template Parameters**: 

  * **T** The type of the curve parameter. 


**Return**: A JSON object containing the curve parameter. 

## Protected Functions Documentation

### function SerializeFullProof

```cpp
virtual outcome::result< std::vector< uint8_t > > SerializeFullProof(
    const SGProof::BaseProofData & base_proof_data
) override
```

Serializes the full proof data and parameters. 

**Parameters**: 

  * **base_proof_data** The base proof data to be appended to the public parameters 


**Return**: A result containing the serialized full proof in bytes. 

**Reimplements**: [sgns::IBasicProof::SerializeFullProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-serializefullproof)


### function GenerateJsonParameters

```cpp
virtual std::pair< boost::json::array, boost::json::array > GenerateJsonParameters() override
```

Generates the parameters in JSON array form. 

**Return**: A pair of public and private JSON arrays, respectively. 

**Reimplements**: [sgns::IBasicProof::GenerateJsonParameters](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/#function-generatejsonparameters)


## Protected Attributes Documentation

### variable generator_X_point

```cpp
static uint64_t generator_X_point = 1;
```

X coordinate of the generator point. 

### variable generator_Y_point

```cpp
static uint64_t generator_Y_point = 2;
```

Y coordinate of the generator point. 

### variable base_seed

```cpp
static uint64_t base_seed = 12345;
```

Base seed. 

### variable provided_totp

```cpp
static uint64_t provided_totp = 67890;
```

Provided TOTP. 

### variable ranges

```cpp
static std::array< uint64_t, 4 > ranges = { 1000, 2000, 3000, 4000 };
```

Array of range values used in transfer proofs. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: sgns::MintTransactionV2
summary: Implements a Mint Version 2 transaction. 

---

# sgns::MintTransactionV2



Implements a Mint Version 2 transaction. 


`#include <MintTransactionV2.hpp>`

Inherits from [sgns::GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual EmbeddedTransaction | **[SerializeToEmbeddedTransaction](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-serializetoembeddedtransaction)**(const SGTransaction::DAGStruct & dag) const override<br/>Serializes the transaction into an EmbeddedTransaction proto with the appropriate oneof field set.  |
| | **[~MintTransactionV2](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-~minttransactionv2)**() override =default<br/>Destroy the Mint Transaction V 2 object.  |
| virtual std::vector< uint8_t > | **[SerializeByteVector](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-serializebytevector)**(const SGTransaction::DAGStruct & dag) const override<br/>Serializes the transaction.  |
| uint64_t | **[GetAmount](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-getamount)**() const<br/>Get the amount of the mint.  |
| [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) | **[GetTokenID](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-gettokenid)**() const<br/>Get the Token ID.  |
| virtual std::string | **[GetChainId](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-getchainid)**() const override<br/>Get source chain identifier for bridge mint validation routing.  |
| [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) | **[GetUTXOParameters](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-getutxoparameters)**() const<br/>Returns the UTXOs.  |
| virtual bool | **[HasUTXOParameters](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-hasutxoparameters)**() const override<br/>Returns if transaction supports UTXOs.  |
| virtual std::optional< [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) > | **[GetUTXOParametersOpt](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-getutxoparametersopt)**() const override<br/>Returns the UTXOs.  |
| virtual std::string | **[GetTransactionSpecificPath](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-gettransactionspecificpath)**() const override<br/>Gets the transaction specific path.  |
| virtual std::unordered_set< std::string > | **[GetTopics](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-gettopics)**() const override<br/>Returns the topics of interest of this transaction.  |
| virtual std::string | **[GetSlotID](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-getslotid)**() const override<br/>Generates a slot ID for consensus slot key determination.  |
| std::vector< uint8_t > | **[SerializeByteVector](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-serializebytevector)**() const<br/>Serializes the transaction using the internal DAG metadata.  |
| EmbeddedTransaction | **[SerializeToEmbeddedTransaction](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-serializetoembeddedtransaction)**() const<br/>Serializes using internal DAG metadata.  |
| std::shared_ptr< [MintTransactionV2](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-minttransactionv2) > | **[DeSerializeByteVector](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-deserializebytevector)**(const std::vector< uint8_t > & data)<br/>Deserializes a MintV2 serialized byte vector into an object.  |
| [MintTransactionV2](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-minttransactionv2) | **[New](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-new)**(uint64_t new_amount, std::string chain_id, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id, SGTransaction::DAGStruct dag, std::vector< [InputUTXOInfo](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/) > mint_inputs, std::string mint_destination)<br/>Creates a new MintV2 transaction.  |

## Additional inherited members

**Public Types inherited from [sgns::GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/)**

|                | Name           |
| -------------- | -------------- |
| using std::function< std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-geniustransaction) >(const std::vector< uint8_t > &)> | **[TransactionDeserializeFn](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#using-transactiondeserializefn)** <br/>Alias for the de-serializer method type to be implemented in derived classes.  |

**Public Functions inherited from [sgns::GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/)**

|                | Name           |
| -------------- | -------------- |
| | **[GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-geniustransaction)**(std::string type, SGTransaction::DAGStruct dag)<br/>Constructs a [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) with the specified type and DAG metadata.  |
| virtual | **[~GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-~geniustransaction)**() =default<br/>Virtual destructor to avoid leakage when deleting derived classes through a base pointer.  |
| std::string | **[GetType](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettype)**() const<br/>Returns the transaction type.  |
| std::string | **[GetTransactionFullPath](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettransactionfullpath)**() const<br/>Returns the full storage path for the transaction based on its hash.  |
| std::string | **[GetProofFullPath](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getprooffullpath)**() const<br/>Returns the full storage path for the proof based on the transaction hash.  |
| std::string | **[GetSrcAddress](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getsrcaddress)**() const<br/>Returns the source address for the transaction.  |
| std::string | **[GetHash](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gethash)**() const<br/>Returns the hash of the transaction.  |
| std::string | **[GetPreviousHash](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getprevioushash)**() const<br/>Returns the hash of the previous transaction.  |
| std::string | **[GetUncleHash](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getunclehash)**() const<br/>Returns the hash of the uncle transaction.  |
| uint64_t | **[GetTimestamp](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettimestamp)**() const<br/>Returns the timestamp of the transaction.  |
| uint64_t | **[GetNonce](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getnonce)**() const<br/>Returns the nonce of the transaction.  |
| void | **[FillHash](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-fillhash)**()<br/>Fills the data hash field in the DAG metadata based on the transaction content.  |
| bool | **[CheckHash](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-checkhash)**() const<br/>Checks the integrity of the transaction by verifying that the hash field matches the calculated hash.  |
| std::vector< uint8_t > | **[MakeSignature](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-makesignature)**([GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/) & account)<br/>Creates a signature for the transaction using the provided [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/).  |
| bool | **[CheckSignature](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-checksignature)**() const<br/>Verifies the transaction signature using the source address and the serialized transaction content.  |
| bool | **[CheckDAGSignatureLegacy](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-checkdagsignaturelegacy)**() const<br/>Legacy method to verify the transaction signature using the DAG metadata. This method may be used for backward compatibility with older transaction formats.  |
| outcome::result< SGTransaction::DAGStruct > | **[DeSerializeDAGStruct](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-deserializedagstruct)**(const std::vector< uint8_t > & data)<br/>Deserializes the DAG metadata from a byte vector.  |
| outcome::result< SGTransaction::DAGStruct > | **[DeSerializeDAGStruct](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-deserializedagstruct)**(const std::string & data)<br/>Deserializes the DAG metadata from a string.  |
| SGTransaction::DAGStruct | **[SetDAGWithType](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-setdagwithtype)**(SGTransaction::DAGStruct dag, const std::string & type)<br/>Sets the transaction type in the DAG metadata and returns the modified DAGStruct.  |
| std::string | **[GetTransactionFullPath](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettransactionfullpath)**(const std::string & tx_hash)<br/>Returns the full storage path for the transaction based on its hash.  |
| void | **[RegisterDeserializer](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-registerdeserializer)**(const std::string & transaction_type, [TransactionDeserializeFn](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#using-transactiondeserializefn) fn)<br/>Registers a deserializer function for a specific transaction type.  |
| std::unordered_map< std::string, [TransactionDeserializeFn](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#using-transactiondeserializefn) > & | **[GetDeSerializers](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getdeserializers)**()<br/>Returns the map of registered deserializer functions for transaction types.  |

**Public Attributes inherited from [sgns::GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/)**

|                | Name           |
| -------------- | -------------- |
| std::string_view | **[GENIUS_CHAIN_ID](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#variable-genius_chain_id)** <br/>The chain ID used for transactions that are not associated with a specific external chain.  |
| SGTransaction::DAGStruct | **[dag_st](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#variable-dag_st)** <br/>The DAG metadata struct that is included in all transactions, containing common fields such as source address, hashes, timestamp, nonce, and signature.  |


## Public Functions Documentation

### function SerializeToEmbeddedTransaction

```cpp
virtual EmbeddedTransaction SerializeToEmbeddedTransaction(
    const SGTransaction::DAGStruct & dag
) const override
```

Serializes the transaction into an EmbeddedTransaction proto with the appropriate oneof field set. 

**Parameters**: 

  * **dag** The DAG metadata to be included in the serialization. 


**Return**: EmbeddedTransaction proto with the typed transaction field set. 

**Reimplements**: [sgns::GeniusTransaction::SerializeToEmbeddedTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-serializetoembeddedtransaction)


### function ~MintTransactionV2

```cpp
~MintTransactionV2() override =default
```

Destroy the Mint Transaction V 2 object. 

### function SerializeByteVector

```cpp
virtual std::vector< uint8_t > SerializeByteVector(
    const SGTransaction::DAGStruct & dag
) const override
```

Serializes the transaction. 

**Return**: The serialized byte vector 

**Reimplements**: [sgns::GeniusTransaction::SerializeByteVector](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-serializebytevector)


### function GetAmount

```cpp
uint64_t GetAmount() const
```

Get the amount of the mint. 

**Return**: The amount of tokens minted 

### function GetTokenID

```cpp
TokenID GetTokenID() const
```

Get the Token ID. 

**Return**: The ID which identifies what token was minted 

### function GetChainId

```cpp
virtual std::string GetChainId() const override
```

Get source chain identifier for bridge mint validation routing. 

**Return**: Source chain id 

**Reimplements**: [sgns::GeniusTransaction::GetChainId](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getchainid)


### function GetUTXOParameters

```cpp
UTXOTxParameters GetUTXOParameters() const
```

Returns the UTXOs. 

**Return**: The UTXOs of the MintV2 transaction 

### function HasUTXOParameters

```cpp
virtual bool HasUTXOParameters() const override
```

Returns if transaction supports UTXOs. 

**Return**: True if supported, false otherwise 

**Reimplements**: [sgns::GeniusTransaction::HasUTXOParameters](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-hasutxoparameters)


### function GetUTXOParametersOpt

```cpp
virtual std::optional< UTXOTxParameters > GetUTXOParametersOpt() const override
```

Returns the UTXOs. 

**Return**: If exists, returns the UTXOs of the transaction 

**Reimplements**: [sgns::GeniusTransaction::GetUTXOParametersOpt](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getutxoparametersopt)


### function GetTransactionSpecificPath

```cpp
inline virtual std::string GetTransactionSpecificPath() const override
```

Gets the transaction specific path. 

**Return**: Returns the transaction specific path 

**Reimplements**: [sgns::GeniusTransaction::GetTransactionSpecificPath](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettransactionspecificpath)


### function GetTopics

```cpp
virtual std::unordered_set< std::string > GetTopics() const override
```

Returns the topics of interest of this transaction. 

**Return**: A set of topics 

**Reimplements**: [sgns::GeniusTransaction::GetTopics](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettopics)


### function GetSlotID

```cpp
virtual std::string GetSlotID() const override
```

Generates a slot ID for consensus slot key determination. 

**Return**: Deterministic slot key derived from chain/token/amount/dest/burn_tx_hash. 

**Reimplements**: [sgns::GeniusTransaction::GetSlotID](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getslotid)


### function SerializeByteVector

```cpp
inline std::vector< uint8_t > SerializeByteVector() const
```

Serializes the transaction using the internal DAG metadata. 

**Return**: The serialized byte vector representing the transaction. 

### function SerializeToEmbeddedTransaction

```cpp
inline EmbeddedTransaction SerializeToEmbeddedTransaction() const
```

Serializes using internal DAG metadata. 

### function DeSerializeByteVector

```cpp
static std::shared_ptr< MintTransactionV2 > DeSerializeByteVector(
    const std::vector< uint8_t > & data
)
```

Deserializes a MintV2 serialized byte vector into an object. 

**Parameters**: 

  * **data** The serialized MintV2 data 


**Return**: A shared pointer to a MintV2 object 

### function New

```cpp
static MintTransactionV2 New(
    uint64_t new_amount,
    std::string chain_id,
    TokenID token_id,
    SGTransaction::DAGStruct dag,
    std::vector< InputUTXOInfo > mint_inputs,
    std::string mint_destination
)
```

Creates a new MintV2 transaction. 

**Parameters**: 

  * **new_amount** The amount to be minted 
  * **chain_id** The chain ID from where the mint came from 
  * **token_id** The token ID 
  * **dag** The DAG structure with the common transaction data 
  * **mint_inputs** Explicit input references for the source-chain burn(s) 
  * **mint_destination** The destination of the Mint 


**Return**: A [MintTransactionV2](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/)

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
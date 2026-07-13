---
title: sgns::TransferTransaction
summary: Transaction for transferring funds between UTXO inputs and outputs. 

---

# sgns::TransferTransaction



Transaction for transferring funds between UTXO inputs and outputs. 


`#include <TransferTransaction.hpp>`

Inherits from [sgns::GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| [TransferTransaction](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-transfertransaction) | **[New](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-new)**(std::vector< [InputUTXOInfo](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/) > inputs, std::vector< [OutputDestInfo](/source-reference/Classes/dc/dfd/structsgns_1_1_output_dest_info/) > destinations, SGTransaction::DAGStruct dag) |
| std::shared_ptr< [TransferTransaction](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-transfertransaction) > | **[DeSerializeByteVector](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-deserializebytevector)**(const std::vector< uint8_t > & data)<br/>Deserializes a [TransferTransaction](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/) from bytes.  |
| | **[~TransferTransaction](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-~transfertransaction)**() override =default<br/>Default Transfer Transaction destructor.  |
| virtual std::vector< uint8_t > | **[SerializeByteVector](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-serializebytevector)**(const SGTransaction::DAGStruct & dag) const override<br/>Serializes the transaction into a byte vector, including the DAG metadata.  |
| virtual EmbeddedTransaction | **[SerializeToEmbeddedTransaction](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-serializetoembeddedtransaction)**(const SGTransaction::DAGStruct & dag) const override<br/>Serializes the transaction into an EmbeddedTransaction proto with the appropriate oneof field set.  |
| std::vector< [OutputDestInfo](/source-reference/Classes/dc/dfd/structsgns_1_1_output_dest_info/) > | **[GetDstInfos](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-getdstinfos)**() const |
| std::vector< [InputUTXOInfo](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/) > | **[GetInputInfos](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-getinputinfos)**() const |
| virtual bool | **[HasUTXOParameters](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-hasutxoparameters)**() const override<br/>Returns if transaction supports UTXOs.  |
| virtual std::optional< [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) > | **[GetUTXOParametersOpt](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-getutxoparametersopt)**() const override<br/>Returns the UTXOs.  |
| virtual std::string | **[GetTransactionSpecificPath](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-gettransactionspecificpath)**() const override<br/>Returns the transaction-specific path component for storage and retrieval.  |
| virtual std::unordered_set< std::string > | **[GetTopics](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-gettopics)**() const override<br/>Returns the destination topics associated with the transaction.  |
| std::vector< uint8_t > | **[SerializeByteVector](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-serializebytevector)**() const<br/>Serializes the transaction into a byte vector.  |
| EmbeddedTransaction | **[SerializeToEmbeddedTransaction](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-serializetoembeddedtransaction)**() const<br/>Serializes using internal DAG metadata.  |

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
| virtual std::string | **[GetChainId](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getchainid)**() const<br/>Returns the source chain id for input validation routing.  |
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
| virtual std::string | **[GetSlotID](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getslotid)**() const<br/>Generates a slot ID used by consensus to identify competing transactions.  |
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

### function New

```cpp
static TransferTransaction New(
    std::vector< InputUTXOInfo > inputs,
    std::vector< OutputDestInfo > destinations,
    SGTransaction::DAGStruct dag
)
```


### function DeSerializeByteVector

```cpp
static std::shared_ptr< TransferTransaction > DeSerializeByteVector(
    const std::vector< uint8_t > & data
)
```

Deserializes a [TransferTransaction](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/) from bytes. 

**Parameters**: 

  * **data** Serialized bytes. 


**Return**: Shared pointer to the deserialized transaction. 

### function ~TransferTransaction

```cpp
~TransferTransaction() override =default
```

Default Transfer Transaction destructor. 

### function SerializeByteVector

```cpp
virtual std::vector< uint8_t > SerializeByteVector(
    const SGTransaction::DAGStruct & dag
) const override
```

Serializes the transaction into a byte vector, including the DAG metadata. 

**Parameters**: 

  * **dag** The DAG metadata to be included in the serialization. 


**Return**: The serialized byte vector representing the transaction. 

**Note**: This should be defined in the derived class, but the version without parameters is to used 

**Reimplements**: [sgns::GeniusTransaction::SerializeByteVector](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-serializebytevector)


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


### function GetDstInfos

```cpp
std::vector< OutputDestInfo > GetDstInfos() const
```


### function GetInputInfos

```cpp
std::vector< InputUTXOInfo > GetInputInfos() const
```


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

Returns the transaction-specific path component for storage and retrieval. 

**Return**: The transaction-specific path component, typically derived from the transaction type or other unique attributes. 

**Reimplements**: [sgns::GeniusTransaction::GetTransactionSpecificPath](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettransactionspecificpath)


### function GetTopics

```cpp
virtual std::unordered_set< std::string > GetTopics() const override
```

Returns the destination topics associated with the transaction. 

**Return**: The set of destination topics associated with the transaction. 

**Reimplements**: [sgns::GeniusTransaction::GetTopics](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettopics)


### function SerializeByteVector

```cpp
inline std::vector< uint8_t > SerializeByteVector() const
```

Serializes the transaction into a byte vector. 

**Return**: Serialized bytes. 

### function SerializeToEmbeddedTransaction

```cpp
inline EmbeddedTransaction SerializeToEmbeddedTransaction() const
```

Serializes using internal DAG metadata. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
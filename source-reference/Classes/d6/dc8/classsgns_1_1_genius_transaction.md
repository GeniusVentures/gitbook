---
title: sgns::GeniusTransaction
summary: Base class of the GeniusTransaction. 

---

# sgns::GeniusTransaction



Base class of the [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/). 


`#include <GeniusTransaction.hpp>`

Inherited by [sgns::EscrowTransaction](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/), [sgns::MigrationTransaction](/source-reference/Classes/d3/d30/classsgns_1_1_migration_transaction/), [sgns::MintTransaction](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/), [sgns::MintTransactionV2](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/), [sgns::ProcessingTransaction](/source-reference/Classes/d6/d7f/classsgns_1_1_processing_transaction/), [sgns::TransferTransaction](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/)

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::function< std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-geniustransaction) >(const std::vector< uint8_t > &)> | **[TransactionDeserializeFn](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#using-transactiondeserializefn)** <br/>Alias for the de-serializer method type to be implemented in derived classes.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-geniustransaction)**(std::string type, SGTransaction::DAGStruct dag)<br/>Constructs a [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) with the specified type and DAG metadata.  |
| virtual | **[~GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-~geniustransaction)**() =default<br/>Virtual destructor to avoid leakage when deleting derived classes through a base pointer.  |
| std::string | **[GetType](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettype)**() const<br/>Returns the transaction type.  |
| virtual std::vector< uint8_t > | **[SerializeByteVector](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-serializebytevector)**(const SGTransaction::DAGStruct & dag) const =0<br/>Serializes the transaction into a byte vector, including the DAG metadata.  |
| virtual EmbeddedTransaction | **[SerializeToEmbeddedTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-serializetoembeddedtransaction)**(const SGTransaction::DAGStruct & dag) const =0<br/>Serializes the transaction into an EmbeddedTransaction proto with the appropriate oneof field set.  |
| EmbeddedTransaction | **[SerializeToEmbeddedTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-serializetoembeddedtransaction)**() const<br/>Serializes using internal DAG metadata.  |
| std::vector< uint8_t > | **[SerializeByteVector](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-serializebytevector)**() const<br/>Serializes the transaction using the internal DAG metadata.  |
| virtual bool | **[HasUTXOParameters](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-hasutxoparameters)**() const<br/>Returns if transaction supports UTXOs.  |
| virtual std::optional< [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) > | **[GetUTXOParametersOpt](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getutxoparametersopt)**() const<br/>Returns the UTXOs.  |
| virtual std::string | **[GetChainId](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getchainid)**() const<br/>Returns the source chain id for input validation routing.  |
| virtual std::string | **[GetTransactionSpecificPath](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettransactionspecificpath)**() const =0<br/>Returns the transaction-specific path component for storage and retrieval.  |
| std::string | **[GetTransactionFullPath](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettransactionfullpath)**() const<br/>Returns the full storage path for the transaction based on its hash.  |
| std::string | **[GetProofFullPath](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getprooffullpath)**() const<br/>Returns the full storage path for the proof based on the transaction hash.  |
| std::string | **[GetSrcAddress](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getsrcaddress)**() const<br/>Returns the source address for the transaction.  |
| std::string | **[GetHash](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gethash)**() const<br/>Returns the hash of the transaction.  |
| std::string | **[GetPreviousHash](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getprevioushash)**() const<br/>Returns the hash of the previous transaction.  |
| std::string | **[GetUncleHash](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getunclehash)**() const<br/>Returns the hash of the uncle transaction.  |
| uint64_t | **[GetTimestamp](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettimestamp)**() const<br/>Returns the timestamp of the transaction.  |
| uint64_t | **[GetNonce](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getnonce)**() const<br/>Returns the nonce of the transaction.  |
| virtual std::unordered_set< std::string > | **[GetTopics](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettopics)**() const<br/>Returns the destination topics associated with the transaction.  |
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

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::string_view | **[GENIUS_CHAIN_ID](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#variable-genius_chain_id)** <br/>The chain ID used for transactions that are not associated with a specific external chain.  |
| SGTransaction::DAGStruct | **[dag_st](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#variable-dag_st)** <br/>The DAG metadata struct that is included in all transactions, containing common fields such as source address, hashes, timestamp, nonce, and signature.  |

## Public Types Documentation

### using TransactionDeserializeFn

```cpp
using sgns::GeniusTransaction::TransactionDeserializeFn = 
std::function<std::shared_ptr<GeniusTransaction>( const std::vector<uint8_t> & )>;
```

Alias for the de-serializer method type to be implemented in derived classes. 

## Public Functions Documentation

### function GeniusTransaction

```cpp
inline GeniusTransaction(
    std::string type,
    SGTransaction::DAGStruct dag
)
```

Constructs a [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) with the specified type and DAG metadata. 

**Parameters**: 

  * **type** The transaction type (e.g., "transfer", "mint", "escrow-hold"). 
  * **dag** The DAG metadata for the transaction. 


### function ~GeniusTransaction

```cpp
virtual ~GeniusTransaction() =default
```

Virtual destructor to avoid leakage when deleting derived classes through a base pointer. 

### function GetType

```cpp
inline std::string GetType() const
```

Returns the transaction type. 

**Return**: The transaction type string. 

### function SerializeByteVector

```cpp
virtual std::vector< uint8_t > SerializeByteVector(
    const SGTransaction::DAGStruct & dag
) const =0
```

Serializes the transaction into a byte vector, including the DAG metadata. 

**Parameters**: 

  * **dag** The DAG metadata to be included in the serialization. 


**Return**: The serialized byte vector representing the transaction. 

**Note**: This should be defined in the derived class, but the version without parameters is to used 

**Reimplemented by**: [sgns::EscrowTransaction::SerializeByteVector](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-serializebytevector), [sgns::MigrationTransaction::SerializeByteVector](/source-reference/Classes/d3/d30/classsgns_1_1_migration_transaction/#function-serializebytevector), [sgns::MintTransaction::SerializeByteVector](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-serializebytevector), [sgns::MintTransactionV2::SerializeByteVector](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-serializebytevector), [sgns::ProcessingTransaction::SerializeByteVector](/source-reference/Classes/d6/d7f/classsgns_1_1_processing_transaction/#function-serializebytevector), [sgns::TransferTransaction::SerializeByteVector](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-serializebytevector)


### function SerializeToEmbeddedTransaction

```cpp
virtual EmbeddedTransaction SerializeToEmbeddedTransaction(
    const SGTransaction::DAGStruct & dag
) const =0
```

Serializes the transaction into an EmbeddedTransaction proto with the appropriate oneof field set. 

**Parameters**: 

  * **dag** The DAG metadata to be included in the serialization. 


**Return**: EmbeddedTransaction proto with the typed transaction field set. 

**Reimplemented by**: [sgns::EscrowTransaction::SerializeToEmbeddedTransaction](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-serializetoembeddedtransaction), [sgns::MigrationTransaction::SerializeToEmbeddedTransaction](/source-reference/Classes/d3/d30/classsgns_1_1_migration_transaction/#function-serializetoembeddedtransaction), [sgns::MintTransaction::SerializeToEmbeddedTransaction](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-serializetoembeddedtransaction), [sgns::MintTransactionV2::SerializeToEmbeddedTransaction](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-serializetoembeddedtransaction), [sgns::ProcessingTransaction::SerializeToEmbeddedTransaction](/source-reference/Classes/d6/d7f/classsgns_1_1_processing_transaction/#function-serializetoembeddedtransaction), [sgns::TransferTransaction::SerializeToEmbeddedTransaction](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-serializetoembeddedtransaction)


### function SerializeToEmbeddedTransaction

```cpp
inline EmbeddedTransaction SerializeToEmbeddedTransaction() const
```

Serializes using internal DAG metadata. 

### function SerializeByteVector

```cpp
inline std::vector< uint8_t > SerializeByteVector() const
```

Serializes the transaction using the internal DAG metadata. 

**Return**: The serialized byte vector representing the transaction. 

### function HasUTXOParameters

```cpp
inline virtual bool HasUTXOParameters() const
```

Returns if transaction supports UTXOs. 

**Return**: true if supported, false otherwise 

**Reimplemented by**: [sgns::EscrowTransaction::HasUTXOParameters](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-hasutxoparameters), [sgns::MigrationTransaction::HasUTXOParameters](/source-reference/Classes/d3/d30/classsgns_1_1_migration_transaction/#function-hasutxoparameters), [sgns::MintTransactionV2::HasUTXOParameters](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-hasutxoparameters), [sgns::TransferTransaction::HasUTXOParameters](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-hasutxoparameters)


### function GetUTXOParametersOpt

```cpp
inline virtual std::optional< UTXOTxParameters > GetUTXOParametersOpt() const
```

Returns the UTXOs. 

**Return**: If exists, returns the UTXOs of the transaction 

**Reimplemented by**: [sgns::EscrowTransaction::GetUTXOParametersOpt](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-getutxoparametersopt), [sgns::MigrationTransaction::GetUTXOParametersOpt](/source-reference/Classes/d3/d30/classsgns_1_1_migration_transaction/#function-getutxoparametersopt), [sgns::MintTransactionV2::GetUTXOParametersOpt](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-getutxoparametersopt), [sgns::TransferTransaction::GetUTXOParametersOpt](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-getutxoparametersopt)


### function GetChainId

```cpp
inline virtual std::string GetChainId() const
```

Returns the source chain id for input validation routing. 

**Return**: The source chain id 

**Reimplemented by**: [sgns::MigrationTransaction::GetChainId](/source-reference/Classes/d3/d30/classsgns_1_1_migration_transaction/#function-getchainid), [sgns::MintTransaction::GetChainId](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-getchainid), [sgns::MintTransactionV2::GetChainId](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-getchainid)


### function GetTransactionSpecificPath

```cpp
virtual std::string GetTransactionSpecificPath() const =0
```

Returns the transaction-specific path component for storage and retrieval. 

**Return**: The transaction-specific path component, typically derived from the transaction type or other unique attributes. 

**Reimplemented by**: [sgns::EscrowTransaction::GetTransactionSpecificPath](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-gettransactionspecificpath), [sgns::MigrationTransaction::GetTransactionSpecificPath](/source-reference/Classes/d3/d30/classsgns_1_1_migration_transaction/#function-gettransactionspecificpath), [sgns::MintTransaction::GetTransactionSpecificPath](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-gettransactionspecificpath), [sgns::MintTransactionV2::GetTransactionSpecificPath](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-gettransactionspecificpath), [sgns::ProcessingTransaction::GetTransactionSpecificPath](/source-reference/Classes/d6/d7f/classsgns_1_1_processing_transaction/#function-gettransactionspecificpath), [sgns::TransferTransaction::GetTransactionSpecificPath](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-gettransactionspecificpath)


### function GetTransactionFullPath

```cpp
inline std::string GetTransactionFullPath() const
```

Returns the full storage path for the transaction based on its hash. 

**Return**: The full storage path for the transaction. 

### function GetProofFullPath

```cpp
inline std::string GetProofFullPath() const
```

Returns the full storage path for the proof based on the transaction hash. 

**Return**: The full storage path for the proof. 

### function GetSrcAddress

```cpp
inline std::string GetSrcAddress() const
```

Returns the source address for the transaction. 

**Return**: The source address. 

### function GetHash

```cpp
std::string GetHash() const
```

Returns the hash of the transaction. 

**Return**: The hash of the transaction. 

### function GetPreviousHash

```cpp
std::string GetPreviousHash() const
```

Returns the hash of the previous transaction. 

**Return**: The hash of the previous transaction. 

### function GetUncleHash

```cpp
std::string GetUncleHash() const
```

Returns the hash of the uncle transaction. 

**Return**: The hash of the uncle transaction. 

### function GetTimestamp

```cpp
inline uint64_t GetTimestamp() const
```

Returns the timestamp of the transaction. 

**Return**: The timestamp of the transaction. 

### function GetNonce

```cpp
inline uint64_t GetNonce() const
```

Returns the nonce of the transaction. 

**Return**: The nonce of the transaction. 

### function GetTopics

```cpp
virtual std::unordered_set< std::string > GetTopics() const
```

Returns the destination topics associated with the transaction. 

**Return**: The set of destination topics associated with the transaction. 

**Reimplemented by**: [sgns::MigrationTransaction::GetTopics](/source-reference/Classes/d3/d30/classsgns_1_1_migration_transaction/#function-gettopics), [sgns::MintTransactionV2::GetTopics](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-gettopics), [sgns::TransferTransaction::GetTopics](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/#function-gettopics)


### function FillHash

```cpp
void FillHash()
```

Fills the data hash field in the DAG metadata based on the transaction content. 

**Note**: This should be called after all transaction fields are set and before signing. 

### function CheckHash

```cpp
bool CheckHash() const
```

Checks the integrity of the transaction by verifying that the hash field matches the calculated hash. 

**Return**: true if the hash is valid, false otherwise. 

### function MakeSignature

```cpp
std::vector< uint8_t > MakeSignature(
    GeniusAccount & account
)
```

Creates a signature for the transaction using the provided [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/). 

**Parameters**: 

  * **account** The [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/) used to sign the transaction. 


**Return**: The signature as a byte vector. 

### function CheckSignature

```cpp
bool CheckSignature() const
```

Verifies the transaction signature using the source address and the serialized transaction content. 

**Return**: true if the signature is valid, false otherwise. 

### function CheckDAGSignatureLegacy

```cpp
bool CheckDAGSignatureLegacy() const
```

Legacy method to verify the transaction signature using the DAG metadata. This method may be used for backward compatibility with older transaction formats. 

**Return**: true if the signature is valid and the hash matches, false otherwise. 

### function GetSlotID

```cpp
inline virtual std::string GetSlotID() const
```

Generates a slot ID used by consensus to identify competing transactions. 

**Return**: The unique slot ID, typically derived from the source address 

**Reimplemented by**: [sgns::MintTransactionV2::GetSlotID](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/#function-getslotid)


### function DeSerializeDAGStruct

```cpp
static outcome::result< SGTransaction::DAGStruct > DeSerializeDAGStruct(
    const std::vector< uint8_t > & data
)
```

Deserializes the DAG metadata from a byte vector. 

**Parameters**: 

  * **data** The byte vector containing the serialized DAG metadata. 


**Return**: DAGStruct wrapped in an outcome::result, containing an error if deserialization fails. 

### function DeSerializeDAGStruct

```cpp
static outcome::result< SGTransaction::DAGStruct > DeSerializeDAGStruct(
    const std::string & data
)
```

Deserializes the DAG metadata from a string. 

**Parameters**: 

  * **data** The string containing the serialized DAG metadata. 


**Return**: DAGStruct wrapped in an outcome::result, containing an error if deserialization fails. 

### function SetDAGWithType

```cpp
static inline SGTransaction::DAGStruct SetDAGWithType(
    SGTransaction::DAGStruct dag,
    const std::string & type
)
```

Sets the transaction type in the DAG metadata and returns the modified DAGStruct. 

**Parameters**: 

  * **dag** The original DAGStruct to be modified. 
  * **type** The transaction type to set in the DAG metadata. 


**Return**: The modified DAGStruct with the transaction type set. 

### function GetTransactionFullPath

```cpp
static inline std::string GetTransactionFullPath(
    const std::string & tx_hash
)
```

Returns the full storage path for the transaction based on its hash. 

**Parameters**: 

  * **tx_hash** Hash of the transaction to be included in the path. 


**Return**: The full storage path for the transaction. 

### function RegisterDeserializer

```cpp
static inline void RegisterDeserializer(
    const std::string & transaction_type,
    TransactionDeserializeFn fn
)
```

Registers a deserializer function for a specific transaction type. 

**Parameters**: 

  * **[transaction_type](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#variable-transaction_type)** The transaction type for which the deserializer is registered. 
  * **fn** The deserializer function to be registered. 


### function GetDeSerializers

```cpp
static inline std::unordered_map< std::string, TransactionDeserializeFn > & GetDeSerializers()
```

Returns the map of registered deserializer functions for transaction types. 

**Return**: The map of transaction types to their corresponding deserializer functions. 

## Public Attributes Documentation

### variable GENIUS_CHAIN_ID

```cpp
static std::string_view GENIUS_CHAIN_ID = "supergenius_chain";
```

The chain ID used for transactions that are not associated with a specific external chain. 

### variable dag_st

```cpp
SGTransaction::DAGStruct dag_st;
```

The DAG metadata struct that is included in all transactions, containing common fields such as source address, hashes, timestamp, nonce, and signature. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
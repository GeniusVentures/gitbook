---
title: sgns::MintTransaction
summary: Transaction that mints tokens after proving a corresponding source-chain event. 

---

# sgns::MintTransaction



Transaction that mints tokens after proving a corresponding source-chain event. 


`#include <MintTransaction.hpp>`

Inherits from [sgns::GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[~MintTransaction](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-~minttransaction)**() override =default<br/>Destroys the mint transaction.  |
| virtual EmbeddedTransaction | **[SerializeToEmbeddedTransaction](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-serializetoembeddedtransaction)**(const SGTransaction::DAGStruct & dag) const override<br/>Serializes the transaction into an EmbeddedTransaction proto with the appropriate oneof field set.  |
| virtual std::vector< uint8_t > | **[SerializeByteVector](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-serializebytevector)**(const SGTransaction::DAGStruct & dag) const override<br/>Serializes the mint transaction payload and DAG metadata.  |
| uint64_t | **[GetAmount](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-getamount)**() const<br/>Returns the minted amount.  |
| [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) | **[GetTokenID](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-gettokenid)**() const<br/>Returns the minted token identifier.  |
| virtual std::string | **[GetChainId](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-getchainid)**() const override<br/>Returns the source chain identifier associated with the mint.  |
| virtual std::string | **[GetTransactionSpecificPath](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-gettransactionspecificpath)**() const override<br/>Returns the transaction-specific storage path component.  |
| std::vector< uint8_t > | **[SerializeByteVector](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-serializebytevector)**() const<br/>Serializes the transaction using the internal DAG metadata.  |
| EmbeddedTransaction | **[SerializeToEmbeddedTransaction](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-serializetoembeddedtransaction)**() const<br/>Serializes using internal DAG metadata.  |
| std::shared_ptr< [MintTransaction](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-minttransaction) > | **[DeSerializeByteVector](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-deserializebytevector)**(const std::vector< uint8_t > & data)<br/>Deserializes a serialized mint transaction.  |
| [MintTransaction](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-minttransaction) | **[New](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#function-new)**(uint64_t new_amount, std::string chain_id, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id, SGTransaction::DAGStruct dag)<br/>Creates a new mint transaction instance.  |

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
| virtual bool | **[HasUTXOParameters](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-hasutxoparameters)**() const<br/>Returns if transaction supports UTXOs.  |
| virtual std::optional< [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) > | **[GetUTXOParametersOpt](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getutxoparametersopt)**() const<br/>Returns the UTXOs.  |
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

**Public Attributes inherited from [sgns::GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/)**

|                | Name           |
| -------------- | -------------- |
| std::string_view | **[GENIUS_CHAIN_ID](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#variable-genius_chain_id)** <br/>The chain ID used for transactions that are not associated with a specific external chain.  |
| SGTransaction::DAGStruct | **[dag_st](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#variable-dag_st)** <br/>The DAG metadata struct that is included in all transactions, containing common fields such as source address, hashes, timestamp, nonce, and signature.  |


## Public Functions Documentation

### function ~MintTransaction

```cpp
~MintTransaction() override =default
```

Destroys the mint transaction. 

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


### function SerializeByteVector

```cpp
virtual std::vector< uint8_t > SerializeByteVector(
    const SGTransaction::DAGStruct & dag
) const override
```

Serializes the mint transaction payload and DAG metadata. 

**Parameters**: 

  * **dag** DAG metadata to serialize into the transaction payload. 


**Return**: Serialized `SGTransaction::MintTx` bytes. 

**Reimplements**: [sgns::GeniusTransaction::SerializeByteVector](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-serializebytevector)


### function GetAmount

```cpp
uint64_t GetAmount() const
```

Returns the minted amount. 

**Return**: Amount of token units minted by this transaction. 

### function GetTokenID

```cpp
TokenID GetTokenID() const
```

Returns the minted token identifier. 

**Return**: Token identifier for the asset minted by this transaction. 

### function GetChainId

```cpp
virtual std::string GetChainId() const override
```

Returns the source chain identifier associated with the mint. 

**Return**: Source chain identifier used for input validation routing. 

**Reimplements**: [sgns::GeniusTransaction::GetChainId](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getchainid)


### function GetTransactionSpecificPath

```cpp
inline virtual std::string GetTransactionSpecificPath() const override
```

Returns the transaction-specific storage path component. 

**Return**: Transaction type string used as the path component. 

**Reimplements**: [sgns::GeniusTransaction::GetTransactionSpecificPath](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettransactionspecificpath)


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
static std::shared_ptr< MintTransaction > DeSerializeByteVector(
    const std::vector< uint8_t > & data
)
```

Deserializes a serialized mint transaction. 

**Parameters**: 

  * **data** Serialized `SGTransaction::MintTx` bytes. 


**Return**: Shared pointer to the parsed mint transaction, or nullptr if parsing fails. 

### function New

```cpp
static MintTransaction New(
    uint64_t new_amount,
    std::string chain_id,
    TokenID token_id,
    SGTransaction::DAGStruct dag
)
```

Creates a new mint transaction instance. 

**Parameters**: 

  * **new_amount** Amount of token units to mint. 
  * **[chain_id](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#variable-chain_id)** Source chain identifier associated with the mint event. 
  * **[token_id](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/#variable-token_id)** Token identifier for the asset being minted. 
  * **dag** DAG metadata shared by all transaction types. 


**Return**: Mint transaction with the transaction type set and hash populated. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
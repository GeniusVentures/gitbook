---
title: sgns::EscrowTransaction
summary: Transaction that reserves funds for a job escrow while tracking peer payout metadata. 

---

# sgns::EscrowTransaction



Transaction that reserves funds for a job escrow while tracking peer payout metadata. 


`#include <EscrowTransaction.hpp>`

Inherits from [sgns::GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| [EscrowTransaction](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-escrowtransaction) | **[New](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-new)**([UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) params, uint64_t amount, std::string dev_addr, uint64_t peers_cut, SGTransaction::DAGStruct dag)<br/>Creates a new escrow-hold transaction from signed UTXO parameters.  |
| std::shared_ptr< [EscrowTransaction](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-escrowtransaction) > | **[DeSerializeByteVector](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-deserializebytevector)**(const std::vector< uint8_t > & data)<br/>Deserializes a serialized escrow transaction.  |
| | **[~EscrowTransaction](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-~escrowtransaction)**() override =default<br/>Destroys the escrow transaction.  |
| virtual std::vector< uint8_t > | **[SerializeByteVector](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-serializebytevector)**(const SGTransaction::DAGStruct & dag) const override<br/>Serializes the transaction into a byte vector, including the DAG metadata.  |
| virtual EmbeddedTransaction | **[SerializeToEmbeddedTransaction](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-serializetoembeddedtransaction)**(const SGTransaction::DAGStruct & dag) const override<br/>Serializes the transaction into an EmbeddedTransaction proto with the appropriate oneof field set.  |
| uint64_t | **[GetNumChunks](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-getnumchunks)**() const<br/>Returns the number of chunks reserved for peer payouts.  |
| virtual std::string | **[GetTransactionSpecificPath](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-gettransactionspecificpath)**() const override<br/>Returns the transaction-specific path component for storage and retrieval.  |
| [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) | **[GetUTXOParameters](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-getutxoparameters)**() const<br/>Returns the escrow transaction UTXO inputs and outputs.  |
| virtual bool | **[HasUTXOParameters](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-hasutxoparameters)**() const override<br/>Returns if transaction supports UTXOs.  |
| virtual std::optional< [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) > | **[GetUTXOParametersOpt](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-getutxoparametersopt)**() const override<br/>Returns the UTXOs.  |
| std::string | **[GetDevAddress](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-getdevaddress)**() const<br/>Returns the developer payout address.  |
| uint64_t | **[GetAmount](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-getamount)**() const<br/>Returns the total amount locked in escrow.  |
| uint64_t | **[GetPeersCut](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-getpeerscut)**() const<br/>Returns the configured peer-share multiplier.  |
| std::vector< uint8_t > | **[SerializeByteVector](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-serializebytevector)**() const<br/>Serializes the transaction using the internal DAG metadata.  |
| EmbeddedTransaction | **[SerializeToEmbeddedTransaction](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/#function-serializetoembeddedtransaction)**() const<br/>Serializes using internal DAG metadata.  |

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

### function New

```cpp
static EscrowTransaction New(
    UTXOTxParameters params,
    uint64_t amount,
    std::string dev_addr,
    uint64_t peers_cut,
    SGTransaction::DAGStruct dag
)
```

Creates a new escrow-hold transaction from signed UTXO parameters. 

**Parameters**: 

  * **params** Signed UTXO inputs and escrow/change outputs for the hold. 
  * **amount** Total amount locked in escrow. 
  * **dev_addr** Developer payout address that receives the post-peer remainder. 
  * **peers_cut** Per-peer payout multiplier used when releasing escrow. 
  * **dag** DAG metadata shared by all transaction types. 


**Return**: Escrow transaction with transaction type set and hash populated. 

### function DeSerializeByteVector

```cpp
static std::shared_ptr< EscrowTransaction > DeSerializeByteVector(
    const std::vector< uint8_t > & data
)
```

Deserializes a serialized escrow transaction. 

**Parameters**: 

  * **data** Serialized `SGTransaction::EscrowTx` bytes. 


**Return**: Shared pointer to the parsed escrow transaction, or nullptr if parsing fails. 

### function ~EscrowTransaction

```cpp
~EscrowTransaction() override =default
```

Destroys the escrow transaction. 

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


### function GetNumChunks

```cpp
uint64_t GetNumChunks() const
```

Returns the number of chunks reserved for peer payouts. 

**Return**: Number of chunks associated with this escrow transaction. 

### function GetTransactionSpecificPath

```cpp
inline virtual std::string GetTransactionSpecificPath() const override
```

Returns the transaction-specific path component for storage and retrieval. 

**Return**: The transaction-specific path component, typically derived from the transaction type or other unique attributes. 

**Reimplements**: [sgns::GeniusTransaction::GetTransactionSpecificPath](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-gettransactionspecificpath)


### function GetUTXOParameters

```cpp
inline UTXOTxParameters GetUTXOParameters() const
```

Returns the escrow transaction UTXO inputs and outputs. 

**Return**: UTXO parameters carried by this escrow hold. 

### function HasUTXOParameters

```cpp
inline virtual bool HasUTXOParameters() const override
```

Returns if transaction supports UTXOs. 

**Return**: true if supported, false otherwise 

**Reimplements**: [sgns::GeniusTransaction::HasUTXOParameters](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-hasutxoparameters)


### function GetUTXOParametersOpt

```cpp
inline virtual std::optional< UTXOTxParameters > GetUTXOParametersOpt() const override
```

Returns the UTXOs. 

**Return**: If exists, returns the UTXOs of the transaction 

**Reimplements**: [sgns::GeniusTransaction::GetUTXOParametersOpt](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/#function-getutxoparametersopt)


### function GetDevAddress

```cpp
inline std::string GetDevAddress() const
```

Returns the developer payout address. 

**Return**: Address that receives escrow remainder after peer payouts. 

### function GetAmount

```cpp
inline uint64_t GetAmount() const
```

Returns the total amount locked in escrow. 

**Return**: Total amount locked by this escrow hold. 

### function GetPeersCut

```cpp
inline uint64_t GetPeersCut() const
```

Returns the configured peer-share multiplier. 

**Return**: Peer payout multiplier applied during escrow release. 

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

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
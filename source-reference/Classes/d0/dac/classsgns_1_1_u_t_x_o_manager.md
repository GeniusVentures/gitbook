---
title: sgns::UTXOManager
summary: Owns the local UTXO set, supports coin selection, validation, persistence, reservations, and deterministic snapshot hashing. 

---

# sgns::UTXOManager



Owns the local UTXO set, supports coin selection, validation, persistence, reservations, and deterministic snapshot hashing. 


`#include <UTXOManager.hpp>`

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[UTXOEntry](/source-reference/Classes/d5/d7d/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_entry/)** <br/>Metadata tracked for each outpoint in the local registry.  |
| struct | **[UTXOCheckpoint](/source-reference/Classes/dc/d6b/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_checkpoint/)** <br/>Persisted checkpoint snapshot used to audit finalized UTXO state at a given epoch.  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class uint8_t | **[UTXOState](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enum-utxostate)** { UTXO_READY = 0, UTXO_CONSUMED = 1, UTXO_RESERVED = 2}<br/>Lifecycle state stored for each tracked UTXO.  |
| enum class uint8_t | **[UTXOType](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enum-utxotype)** { UTXO_NORMAL = 0, UTXO_BRIDGE = 1}<br/>Type classification for UTXOs to distinguish standard UTXOs from cross-chain bridge burns.  |
| using std::pair< [UTXOState](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enum-utxostate), [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) > | **[UTXOData](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#using-utxodata)** <br/>UTXO state paired with the actual UTXO.  |
| using std::unordered_map< [OutPoint](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/), [UTXOEntry](/source-reference/Classes/d5/d7d/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_entry/), [OutPointHash](/source-reference/Classes/d5/d40/structsgns_1_1_out_point_hash/) > | **[UTXOOutPointMap](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#using-utxooutpointmap)** <br/>Maps an outpoint to its UTXO Entry.  |
| using std::unordered_map< std::string, std::vector< [OutPoint](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/) > > | **[AddressOutPointList](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#using-addressoutpointlist)** <br/>Maps an owner address to a list of outpoints they own.  |
| using std::function< std::vector< uint8_t >(const std::vector< uint8_t > &data)> | **[SignFunc](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#using-signfunc)** <br/>Method to sign a vector of bytes, returning the signature bytes.  |
| using std::function< bool(const std::string &address, const std::vector< uint8_t > &signature, const std::vector< uint8_t > &data)> | **[VerifySignatureFunc](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#using-verifysignaturefunc)** <br/>Method to verify a signature given an address, signature bytes, and original data.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[UTXOManager](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-utxomanager)**(std::string address, [SignFunc](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#using-signfunc) sign, [VerifySignatureFunc](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#using-verifysignaturefunc) verify_signature)<br/>Construct a new [UTXOManager](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/) object.  |
| uint64_t | **[GetBalance](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-getbalance)**() const<br/>Get the account's balance.  |
| uint64_t | **[GetBalance](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-getbalance)**(const std::string & address) const<br/>Get the informed address balance.  |
| uint64_t | **[GetBalance](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-getbalance)**(const [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) & token_id) const<br/>Get the accounts balance for a specific token.  |
| uint64_t | **[GetBalance](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-getbalance)**(const [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) & token_id, const std::string & address) const<br/>Get the balance of the informed address for a specific token.  |
| outcome::result< bool > | **[PutUTXO](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-pututxo)**([GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) new_utxo, const std::string & address, [UTXOType](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enum-utxotype) type =[UTXOType::UTXO_NORMAL](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enumvalue-utxo_normal))<br/>Add a new UTXO to the account.  |
| outcome::result< bool > | **[PutUTXO](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-pututxo)**(const [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) & new_utxo)<br/>Adds a new UTXO to the account using the manager's default address.  |
| outcome::result< void > | **[DeleteUTXO](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-deleteutxo)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & utxo_id, uint32_t output_idx, const std::string & address)<br/>Delete a UTXO from the account.  |
| outcome::result< bool > | **[ConsumeUTXOs](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-consumeutxos)**(const std::vector< [InputUTXOInfo](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/) > & infos, const std::string & address, [UTXOType](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enum-utxotype) type =[UTXOType::UTXO_NORMAL](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enumvalue-utxo_normal))<br/>Consume UTXOs from the account.  |
| outcome::result< bool > | **[ConsumeUTXOs](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-consumeutxos)**(const std::vector< [InputUTXOInfo](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/) > & infos, [UTXOType](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enum-utxotype) type =[UTXOType::UTXO_NORMAL](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enumvalue-utxo_normal))<br/>Consume UTXOs from the default owner address tracked by this manager.  |
| std::vector< [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) > | **[GetUTXOs](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-getutxos)**(const std::string & address) const<br/>Get UTXOs for a specific address.  |
| std::vector< [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) > | **[GetUTXOs](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-getutxos)**() const<br/>Returns spendable UTXOs owned by the manager's default address.  |
| std::vector< [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) > | **[GetUnconsumedUTXOs](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-getunconsumedutxos)**(const std::string & address) const<br/>Get all unconsumed UTXOs for a specific address.  |
| std::optional< [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) > | **[GetUnconsumedUTXO](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-getunconsumedutxo)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & txid, uint32_t output_idx) const<br/>Returns an unconsumed UTXO by its exact outpoint.  |
| std::unordered_map< std::string, std::vector< [UTXOData](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#using-utxodata) > > | **[GetAllUTXOs](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-getallutxos)**() const<br/>Get all UTXOs tracked by the manager, grouped by owner address.  |
| outcome::result< void > | **[SetUTXOs](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-setutxos)**(const std::vector< [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) > & utxos, const std::string & address)<br/>Set UTXOs for a specific address (replaces existing UTXOs).  |
| outcome::result< void > | **[SetUTXOs](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-setutxos)**(const std::vector< [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) > & utxos)<br/>Set UTXOs for the manager's default address (replaces existing UTXOs).  |
| outcome::result< [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) > | **[CreateTxParameter](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-createtxparameter)**(uint64_t amount, std::string dest_address, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id)<br/>Create the input and output parameters for a single-output transfer, selecting from available UTXOs.  |
| outcome::result< [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) > | **[CreateTxParameter](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-createtxparameter)**(const std::vector< [OutputDestInfo](/source-reference/Classes/dc/dfd/structsgns_1_1_output_dest_info/) > & destinations, const [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) & token_id)<br/>Selects and signs inputs for a multi-output transfer.  |
| void | **[ReserveUTXOs](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-reserveutxos)**(const std::vector< [InputUTXOInfo](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/) > & inputs, const std::string & reservation_id, [UTXOType](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enum-utxotype) type =[UTXOType::UTXO_NORMAL](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enumvalue-utxo_normal))<br/>Marks inputs as reserved so they are not reused by concurrent transaction assembly.  |
| void | **[RollbackUTXOs](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-rollbackutxos)**(const std::vector< [InputUTXOInfo](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/) > & inputs, const std::string & reservation_id, [UTXOType](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enum-utxotype) type =[UTXOType::UTXO_NORMAL](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enumvalue-utxo_normal))<br/>Releases a previous reservation without consuming the inputs.  |
| bool | **[VerifyParameters](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-verifyparameters)**(const [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) & params) const<br/>Verifies ownership and signatures for UTXO transaction parameters using the default address.  |
| bool | **[VerifyParameters](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-verifyparameters)**(const [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) & params, const std::string & address) const<br/>Verifies ownership and signatures for UTXO transaction parameters using an explicit address.  |
| std::optional< [UTXOState](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enum-utxostate) > | **[GetOutPointState](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-getoutpointstate)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & utxo_id, uint32_t output_idx) const<br/>Returns the tracked state of a specific outpoint when present.  |
| bool | **[IsOutPointConsumed](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-isoutpointconsumed)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & utxo_id, uint32_t output_idx) const<br/>Indicates whether a specific outpoint has already been consumed.  |
| bool | **[IsOutPointReserved](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-isoutpointreserved)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & utxo_id, uint32_t output_idx) const<br/>Indicates whether a specific outpoint is in the RESERVED state (burn UTXO awaiting consensus).  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[ComputeUTXOMerkleRoot](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-computeutxomerkleroot)**() const<br/>Compute a deterministic Merkle root for unspent UTXOs owned by this node address.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[ComputeUTXOMerkleRoot](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-computeutxomerkleroot)**(const std::string & address) const<br/>Compute a deterministic Merkle root for unspent UTXOs from a specific address.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[ComputeUTXOMerkleRootFromSnapshot](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-computeutxomerklerootfromsnapshot)**(const std::vector< [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) > & utxos) const<br/>Compute deterministic UTXO Merkle root from an explicit UTXO snapshot.  |
| outcome::result< bool > | **[LoadUTXOs](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-loadutxos)**(std::shared_ptr< [storage::rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/) > db)<br/>Loads the UTXO state for the manager's default address from persistent storage.  |
| void | **[ReleaseStorage](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-releasestorage)**()<br/>Releases the current RocksDB handle used for persistence.  |
| outcome::result< void > | **[StoreUTXOs](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-storeutxos)**(const std::string & address)<br/>Stores the current UTXO state for the manager's default address to persistent storage.  |
| outcome::result< void > | **[CreateCheckpoint](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-createcheckpoint)**(uint64_t epoch, const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & last_finalized_tx, const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & registry_hash)<br/>Creates a checkpoint for the manager's default address.  |
| outcome::result< void > | **[CreateCheckpoint](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-createcheckpoint)**(const std::string & address, uint64_t epoch, const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & last_finalized_tx, const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & registry_hash)<br/>Creates a checkpoint for an explicit owner address.  |
| outcome::result< std::optional< [UTXOCheckpoint](/source-reference/Classes/dc/d6b/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_checkpoint/) > > | **[LoadLatestCheckpoint](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-loadlatestcheckpoint)**() const<br/>Loads the latest checkpoint for the default owner address.  |
| outcome::result< std::optional< [UTXOCheckpoint](/source-reference/Classes/dc/d6b/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_checkpoint/) > > | **[LoadLatestCheckpoint](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#function-loadlatestcheckpoint)**(const std::string & address) const<br/>Loads the latest checkpoint for the provided owner address.  |

## Public Types Documentation

### enum UTXOState

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| UTXO_READY | 0| UTXO is unspent and available for use.   |
| UTXO_CONSUMED | 1| UTXO has been consumed by a transaction and is no longer available.   |
| UTXO_RESERVED | 2| Burn UTXO with mint in consensus — blocks local reuse but allows voting.   |



Lifecycle state stored for each tracked UTXO. 

### enum UTXOType

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| UTXO_NORMAL | 0| Standard UTXO from local transfers or mints.   |
| UTXO_BRIDGE | 1| UTXO from cross-chain bridge burn event.   |



Type classification for UTXOs to distinguish standard UTXOs from cross-chain bridge burns. 

### using UTXOData

```cpp
using sgns::UTXOManager::UTXOData = std::pair<UTXOState, GeniusUTXO>;
```

UTXO state paired with the actual UTXO. 

### using UTXOOutPointMap

```cpp
using sgns::UTXOManager::UTXOOutPointMap = std::unordered_map<OutPoint, UTXOEntry, OutPointHash>;
```

Maps an outpoint to its UTXO Entry. 

### using AddressOutPointList

```cpp
using sgns::UTXOManager::AddressOutPointList = std::unordered_map<std::string, std::vector<OutPoint>>;
```

Maps an owner address to a list of outpoints they own. 

### using SignFunc

```cpp
using sgns::UTXOManager::SignFunc = std::function<std::vector<uint8_t>( const std::vector<uint8_t> &data )>;
```

Method to sign a vector of bytes, returning the signature bytes. 

### using VerifySignatureFunc

```cpp
using sgns::UTXOManager::VerifySignatureFunc = std::function<bool( const std::string          &address,
                                                       const std::vector<uint8_t> &signature,
                                                       const std::vector<uint8_t> &data )>;
```

Method to verify a signature given an address, signature bytes, and original data. 

## Public Functions Documentation

### function UTXOManager

```cpp
inline UTXOManager(
    std::string address,
    SignFunc sign,
    VerifySignatureFunc verify_signature
)
```

Construct a new [UTXOManager](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/) object. 

**Parameters**: 

  * **address** The address of the node 
  * **sign** The signer method 
  * **verify_signature** The verifier method 


### function GetBalance

```cpp
uint64_t GetBalance() const
```

Get the account's balance. 

**Return**: The total balance of the account 

### function GetBalance

```cpp
uint64_t GetBalance(
    const std::string & address
) const
```

Get the informed address balance. 

**Parameters**: 

  * **address** The address to get the balance for 


**Return**: The total balance of the account 

### function GetBalance

```cpp
uint64_t GetBalance(
    const TokenID & token_id
) const
```

Get the accounts balance for a specific token. 

**Parameters**: 

  * **token_id** Token ID to get the balance 


**Return**: The balance of the account for the specific token 

### function GetBalance

```cpp
uint64_t GetBalance(
    const TokenID & token_id,
    const std::string & address
) const
```

Get the balance of the informed address for a specific token. 

**Parameters**: 

  * **token_id** The token ID to get the balance for 
  * **address** The address to get the balance for 


**Return**: The balance of the account for the specific token and address 

### function PutUTXO

```cpp
outcome::result< bool > PutUTXO(
    GeniusUTXO new_utxo,
    const std::string & address,
    UTXOType type =UTXOType::UTXO_NORMAL
)
```

Add a new UTXO to the account. 

**Parameters**: 

  * **new_utxo** The new UTXO to be added 
  * **address** Address to add the UTXO to 
  * **type** UTXO type classification (default UTXO_NORMAL for standard UTXOs) 


**Return**: true if the UTXO was added, false otherwise 

### function PutUTXO

```cpp
inline outcome::result< bool > PutUTXO(
    const GeniusUTXO & new_utxo
)
```

Adds a new UTXO to the account using the manager's default address. 

**Parameters**: 

  * **new_utxo** The UTXO to be added 


**Return**: true if added successfully, false otherwise 

### function DeleteUTXO

```cpp
outcome::result< void > DeleteUTXO(
    const base::Hash256 & utxo_id,
    uint32_t output_idx,
    const std::string & address
)
```

Delete a UTXO from the account. 

**Parameters**: 

  * **utxo_id** The ID of the UTXO to be deleted 
  * **output_idx** The output index of the UTXO 
  * **address** Address to remove the UTXO from 


### function ConsumeUTXOs

```cpp
outcome::result< bool > ConsumeUTXOs(
    const std::vector< InputUTXOInfo > & infos,
    const std::string & address,
    UTXOType type =UTXOType::UTXO_NORMAL
)
```

Consume UTXOs from the account. 

**Parameters**: 

  * **infos** Vector of UTXO information to be consumed 
  * **address** Address to consume UTXOs from 
  * **type** Only consume UTXOs of this type (default NORMAL) 


**Return**: true if all UTXOs were consumed, false otherwise 

### function ConsumeUTXOs

```cpp
inline outcome::result< bool > ConsumeUTXOs(
    const std::vector< InputUTXOInfo > & infos,
    UTXOType type =UTXOType::UTXO_NORMAL
)
```

Consume UTXOs from the default owner address tracked by this manager. 

**Parameters**: 

  * **infos** Vector of UTXO information to be consumed 
  * **type** Only consume UTXOs of this type (default NORMAL) 


**Return**: true if all UTXOs were consumed, false otherwise 

### function GetUTXOs

```cpp
std::vector< GeniusUTXO > GetUTXOs(
    const std::string & address
) const
```

Get UTXOs for a specific address. 

**Parameters**: 

  * **address** The address to get UTXOs for 


**Return**: Vector of UTXOs for the address 

### function GetUTXOs

```cpp
inline std::vector< GeniusUTXO > GetUTXOs() const
```

Returns spendable UTXOs owned by the manager's default address. 

**Return**: The vector of UTXOs for the manager's default address 

### function GetUnconsumedUTXOs

```cpp
std::vector< GeniusUTXO > GetUnconsumedUTXOs(
    const std::string & address
) const
```

Get all unconsumed UTXOs for a specific address. 

**Parameters**: 

  * **address** The address to get UTXOs for 


**Return**: Ready and locally reserved UTXOs for the address 

### function GetUnconsumedUTXO

```cpp
std::optional< GeniusUTXO > GetUnconsumedUTXO(
    const base::Hash256 & txid,
    uint32_t output_idx
) const
```

Returns an unconsumed UTXO by its exact outpoint. 

**Parameters**: 

  * **txid** Transaction hash that created the UTXO 
  * **output_idx** Output index within the transaction 


**Return**: The UTXO when present and not consumed, otherwise std::nullopt 

### function GetAllUTXOs

```cpp
std::unordered_map< std::string, std::vector< UTXOData > > GetAllUTXOs() const
```

Get all UTXOs tracked by the manager, grouped by owner address. 

**Return**: A map of owner addresses to their corresponding vectors of UTXOs 

### function SetUTXOs

```cpp
outcome::result< void > SetUTXOs(
    const std::vector< GeniusUTXO > & utxos,
    const std::string & address
)
```

Set UTXOs for a specific address (replaces existing UTXOs). 

**Parameters**: 

  * **utxos** Vector of UTXOs to set for the address 
  * **address** The address to set UTXOs for 


### function SetUTXOs

```cpp
inline outcome::result< void > SetUTXOs(
    const std::vector< GeniusUTXO > & utxos
)
```

Set UTXOs for the manager's default address (replaces existing UTXOs). 

**Parameters**: 

  * **utxos** Vector of UTXOs to set for the manager's default address 


### function CreateTxParameter

```cpp
outcome::result< UTXOTxParameters > CreateTxParameter(
    uint64_t amount,
    std::string dest_address,
    TokenID token_id
)
```

Create the input and output parameters for a single-output transfer, selecting from available UTXOs. 

**Parameters**: 

  * **amount** The amount to transfer 
  * **dest_address** The destination address for the transfer 
  * **token_id** The token ID to transfer 


**Return**: The combined input and output parameters for the transaction if successful, or an error if selection or signing failed 

### function CreateTxParameter

```cpp
outcome::result< UTXOTxParameters > CreateTxParameter(
    const std::vector< OutputDestInfo > & destinations,
    const TokenID & token_id
)
```

Selects and signs inputs for a multi-output transfer. 

**Parameters**: 

  * **destinations** The list of destination addresses and amounts for the transfer 
  * **token_id** The token ID to transfer 


**Return**: The combined input and output parameters for the transaction if successful, or an error if selection or signing failed 

### function ReserveUTXOs

```cpp
void ReserveUTXOs(
    const std::vector< InputUTXOInfo > & inputs,
    const std::string & reservation_id,
    UTXOType type =UTXOType::UTXO_NORMAL
)
```

Marks inputs as reserved so they are not reused by concurrent transaction assembly. 

**Parameters**: 

  * **inputs** The list of UTXOs to reserve 
  * **reservation_id** The ID for the reservation 
  * **type** Only reserve UTXOs of this type (default NORMAL) 


### function RollbackUTXOs

```cpp
void RollbackUTXOs(
    const std::vector< InputUTXOInfo > & inputs,
    const std::string & reservation_id,
    UTXOType type =UTXOType::UTXO_NORMAL
)
```

Releases a previous reservation without consuming the inputs. 

**Parameters**: 

  * **inputs** The list of UTXOs to release 
  * **reservation_id** The ID for the reservation 
  * **type** Only rollback UTXOs of this type (default NORMAL) 


### function VerifyParameters

```cpp
inline bool VerifyParameters(
    const UTXOTxParameters & params
) const
```

Verifies ownership and signatures for UTXO transaction parameters using the default address. 

**Parameters**: 

  * **params** The transaction parameters to verify, including inputs and outputs 


**Return**: true if all signatures are valid and correspond to the default address, false otherwise 

### function VerifyParameters

```cpp
bool VerifyParameters(
    const UTXOTxParameters & params,
    const std::string & address
) const
```

Verifies ownership and signatures for UTXO transaction parameters using an explicit address. 

**Parameters**: 

  * **params** The transaction parameters to verify, including inputs and outputs 
  * **address** The address to verify ownership against 


**Return**: true if all signatures are valid and correspond to the specified address, false otherwise 

### function GetOutPointState

```cpp
std::optional< UTXOState > GetOutPointState(
    const base::Hash256 & utxo_id,
    uint32_t output_idx
) const
```

Returns the tracked state of a specific outpoint when present. 

**Parameters**: 

  * **utxo_id** The transaction hash that created the UTXO 
  * **output_idx** The output index of the UTXO within the transaction 


**Return**: If the outpoint is tracked, returns its current state (e.g. ready or consumed); if not tracked, returns std::nullopt 

### function IsOutPointConsumed

```cpp
bool IsOutPointConsumed(
    const base::Hash256 & utxo_id,
    uint32_t output_idx
) const
```

Indicates whether a specific outpoint has already been consumed. 

**Parameters**: 

  * **utxo_id** The transaction hash that created the UTXO 
  * **output_idx** The output index of the UTXO within the transaction 


**Return**: true if the outpoint is consumed, false otherwise 

### function IsOutPointReserved

```cpp
bool IsOutPointReserved(
    const base::Hash256 & utxo_id,
    uint32_t output_idx
) const
```

Indicates whether a specific outpoint is in the RESERVED state (burn UTXO awaiting consensus). 

**Parameters**: 

  * **utxo_id** The transaction hash that created the UTXO 
  * **output_idx** The output index of the UTXO within the transaction 


**Return**: true if the outpoint exists and is in UTXO_RESERVED state 

### function ComputeUTXOMerkleRoot

```cpp
base::Hash256 ComputeUTXOMerkleRoot() const
```

Compute a deterministic Merkle root for unspent UTXOs owned by this node address. 

**Return**: The computed UTXO Merkle root for this node address 

### function ComputeUTXOMerkleRoot

```cpp
base::Hash256 ComputeUTXOMerkleRoot(
    const std::string & address
) const
```

Compute a deterministic Merkle root for unspent UTXOs from a specific address. 

**Parameters**: 

  * **address** The address to compute the UTXO Merkle root for 


**Return**: The computed UTXO Merkle root for the specified address 

### function ComputeUTXOMerkleRootFromSnapshot

```cpp
base::Hash256 ComputeUTXOMerkleRootFromSnapshot(
    const std::vector< GeniusUTXO > & utxos
) const
```

Compute deterministic UTXO Merkle root from an explicit UTXO snapshot. 

**Parameters**: 

  * **utxos** The list of UTXOs to include in the Merkle root computation 


**Return**: The computed UTXO Merkle root 

### function LoadUTXOs

```cpp
outcome::result< bool > LoadUTXOs(
    std::shared_ptr< storage::rocksdb > db
)
```

Loads the UTXO state for the manager's default address from persistent storage. 

**Parameters**: 

  * **db** The RocksDB instance to load from 


**Return**: true if loaded successfully, false if no UTXOs were found, or an error if loading failed 

### function ReleaseStorage

```cpp
void ReleaseStorage()
```

Releases the current RocksDB handle used for persistence. 

### function StoreUTXOs

```cpp
outcome::result< void > StoreUTXOs(
    const std::string & address
)
```

Stores the current UTXO state for the manager's default address to persistent storage. 

**Parameters**: 

  * **address** The address to store UTXOs for 


### function CreateCheckpoint

```cpp
outcome::result< void > CreateCheckpoint(
    uint64_t epoch,
    const base::Hash256 & last_finalized_tx,
    const base::Hash256 & registry_hash
)
```

Creates a checkpoint for the manager's default address. 

**Parameters**: 

  * **epoch** The epoch number associated with the checkpoint 
  * **last_finalized_tx** The transaction ID of the last finalized transaction at the time of checkpointing 
  * **registry_hash** The hash of the full registry state at the time of checkpointing 


### function CreateCheckpoint

```cpp
outcome::result< void > CreateCheckpoint(
    const std::string & address,
    uint64_t epoch,
    const base::Hash256 & last_finalized_tx,
    const base::Hash256 & registry_hash
)
```

Creates a checkpoint for an explicit owner address. 

**Parameters**: 

  * **address** The address for which to create a checkpoint 
  * **epoch** The epoch number associated with the checkpoint 
  * **last_finalized_tx** The transaction ID of the last finalized transaction at the time of checkpointing 
  * **registry_hash** The hash of the full registry state at the time of checkpointing 


### function LoadLatestCheckpoint

```cpp
inline outcome::result< std::optional< UTXOCheckpoint > > LoadLatestCheckpoint() const
```

Loads the latest checkpoint for the default owner address. 

**Return**: If successful, returns the latest checkpoint for the manager's default address; if no checkpoint is found, returns std::nullopt; if an error occurs during loading, returns the error 

### function LoadLatestCheckpoint

```cpp
outcome::result< std::optional< UTXOCheckpoint > > LoadLatestCheckpoint(
    const std::string & address
) const
```

Loads the latest checkpoint for the provided owner address. 

**Parameters**: 

  * **address** The owner address to load the checkpoint for 


**Return**: If successful, returns the latest checkpoint for the manager's default address; if no checkpoint is found, returns std::nullopt; if an error occurs during loading, returns the error 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
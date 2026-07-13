---
title: sgns::GeniusAccount

---

# sgns::GeniusAccount






`#include <GeniusAccount.hpp>`

Inherits from std::enable_shared_from_this< GeniusAccount >

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::pair< std::shared_ptr< [ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/) >, ethereum::EthereumKeyGenerator > | **[StorageWithAddress](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#using-storagewithaddress)**  |
| using std::function< std::shared_ptr< [ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/) >(const std::string &identifier)> | **[SecureStorageFactory](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#using-securestoragefactory)** <br/>Factory function type for creating secure storage instances.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| void | **[SetSecureStorageFactory](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-setsecurestoragefactory)**([SecureStorageFactory](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#using-securestoragefactory) factory)<br/>Sets the secure storage factory used by all [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/) factory methods.  |
| const [SecureStorageFactory](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#using-securestoragefactory) & | **[GetSecureStorageFactory](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-getsecurestoragefactory)**()<br/>Returns the current secure storage factory (default if none set).  |
| std::shared_ptr< [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-geniusaccount) > | **[New](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-new)**([TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id, const boost::filesystem::path & base_path, bool full_node =false)<br/>Try creating an account by first loading it from storage, and if failure, create one with [NewFromRandomMnemonic](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-newfromrandommnemonic).  |
| std::shared_ptr< [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-geniusaccount) > | **[NewFromPrivateKey](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-newfromprivatekey)**([TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id, const char * eth_private_key, const boost::filesystem::path & base_path, bool full_node =false)<br/>Creates an account from an Ethereum private key.  |
| std::shared_ptr< [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-geniusaccount) > | **[NewFromPublicKey](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-newfrompublickey)**([TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id, std::string_view public_key, bool full_node =false)<br/>Creates an account by loading directly from storage. If the account wasn't previously stored, returns `nullptr`.  |
| std::shared_ptr< [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-geniusaccount) > | **[NewFromMnemonic](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-newfrommnemonic)**([TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id, const std::string & mnemonic, const boost::filesystem::path & base_path, bool full_node =false)<br/>Creates an account from a BIP39 mnemonic phrase.  |
| std::pair< std::shared_ptr< [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-geniusaccount) >, std::string > | **[NewFromRandomMnemonic](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-newfromrandommnemonic)**([TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id, const boost::filesystem::path & base_path, bool full_node =false)<br/>Creates an account with a newly generated random BIP39 mnemonic.  |
| std::vector< std::string > | **[GetAvailableAccounts](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-getavailableaccounts)**(const boost::filesystem::path & base_path) |
| outcome::result< void > | **[DeleteAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-deleteaccount)**(std::string_view public_address, const boost::filesystem::path & base_path) |
| std::string_view | **[NormalizeAddress](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-normalizeaddress)**(std::string_view address)<br/>Strips the "0x" prefix from an address if present. Stored addresses are prefix-free; this normalizes user input for lookups.  |
| bool | **[IsValidPublicKey](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-isvalidpublickey)**(std::string_view key)<br/>Validates that a string is a valid 512-bit public key in hex format. A valid key is exactly 128 hex characters with no prefix.  |
| bool | **[VerifySignature](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-verifysignature)**(const std::string & address, std::string_view sig, const std::vector< uint8_t > & data)<br/>Verify a signature using the Genius account's public key.  |
| outcome::result< [StorageWithAddress](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#using-storagewithaddress) > | **[GenerateGeniusAddress](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-generategeniusaddress)**(const char * eth_private_key, const boost::filesystem::path & base_path) |
| outcome::result< [StorageWithAddress](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#using-storagewithaddress) > | **[GenerateGeniusAddress](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-generategeniusaddress)**(const TW::PrivateKey & private_key, const boost::filesystem::path & base_path) |
| bool | **[InitMessenger](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-initmessenger)**(std::shared_ptr< ipfs_pubsub::GossipPubSub > pubsub)<br/>Initialize the messenger for the account.  |
| bool | **[ConfigureDatabaseDependencies](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-configuredatabasedependencies)**(std::shared_ptr< [crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) > global_db)<br/>Configures database dependencies: nonce store, block response handler, head request handler, and block CID lookup method.  |
| void | **[DeconfigureDatabaseDependencies](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-deconfiguredatabasedependencies)**()<br/>Clears handlers and methods set by ConfigureDatabaseDependencies.  |
| | **[~GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-~geniusaccount)**()<br/>Destroy the Genius Account object.  |
| std::string | **[GetAddress](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-getaddress)**() const<br/>Get the Address object.  |
| [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) | **[GetToken](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-gettoken)**() const<br/>Get the account's token.  |
| std::string | **[GetNonce](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-getnonce)**() const<br/>Get the proposed (next available) nonce as a string.  |
| std::vector< uint8_t > | **[Sign](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-sign)**(const std::vector< uint8_t > & data) const<br/>Sign data using the Genius account's private key.  |
| std::vector< [InputUTXOInfo](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/) > | **[CreateInputsFromUTXOs](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-createinputsfromutxos)**(const std::vector< [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) > & utxos) const<br/>Build signed transaction inputs from UTXOs.  |
| void | **[SetPeerConfirmedNonce](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-setpeerconfirmednonce)**(uint64_t nonce, const std::string & address, const std::string & tx_hash ="")<br/>Set the confirmed nonce for an address.  |
| void | **[RollBackPeerConfirmedNonce](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-rollbackpeerconfirmednonce)**(uint64_t nonce, const std::string & address)<br/>Rollback the confirmed nonce for the given address. Also rolls back local confirmed nonce and tx history when the address is local.  |
| outcome::result< uint64_t > | **[GetPeerNonce](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-getpeernonce)**(const std::string & address) const<br/>Get the confirmed nonce for a peer.  |
| outcome::result< uint64_t > | **[GetLocalConfirmedNonce](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-getlocalconfirmednonce)**() const<br/>Get the local confirmed nonce.  |
| outcome::result< std::string > | **[GetLocalConfirmedTxHash](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-getlocalconfirmedtxhash)**(uint64_t nonce) const<br/>Get a locally persisted confirmed transaction hash by nonce.  |
| outcome::result< uint64_t > | **[GetConfirmedNonce](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-getconfirmednonce)**(uint64_t timeout_ms) const<br/>Get confirmed nonce from the network.  |
| outcome::result< std::optional< uint64_t > > | **[FetchNetworkNonce](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-fetchnetworknonce)**(uint64_t timeout_ms) const<br/>Fetch the latest nonce from the network without relying on cached values.  |
| uint64_t | **[GetProposedNonce](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-getproposednonce)**() const<br/>Get the next available nonce without reserving it.  |
| uint64_t | **[ReserveNextNonce](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-reservenextnonce)**()<br/>Reserve the next available nonce.  |
| void | **[ReleaseNonce](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-releasenonce)**(uint64_t nonce)<br/>Release a previously reserved nonce.  |
| outcome::result< void > | **[RequestGenesis](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-requestgenesis)**(uint64_t timeout_ms =8000, std::function< void(outcome::result< std::string >)> callback =nullptr) const |
| outcome::result< void > | **[RequestAccountCreation](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-requestaccountcreation)**(uint64_t timeout_ms, std::function< void(outcome::result< std::string >)> callback) const |
| outcome::result< void > | **[RequestValidatorRegistry](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-requestvalidatorregistry)**(uint64_t timeout_ms, std::function< void(outcome::result< std::string >)> callback) const |
| outcome::result< void > | **[RequestRegularBlock](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-requestregularblock)**(uint64_t timeout_ms, const std::string & cid, std::function< void(outcome::result< std::string >)> callback =nullptr) const |
| outcome::result< void > | **[RequestTransaction](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-requesttransaction)**(uint64_t timeout_ms, const std::string & tx_hash, std::function< void(outcome::result< std::string >)> callback =nullptr) const |
| outcome::result< std::unordered_set< std::string > > | **[RequestUTXOs](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-requestutxos)**(uint64_t timeout_ms, const std::string & address, uint64_t silent_time_ms =150) const<br/>Request UTXOs for a specific address and return the selected response.  |
| outcome::result< void > | **[RequestHeads](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-requestheads)**(const std::unordered_set< std::string > & topics) const<br/>Request heads broadcast for specific topics.  |
| outcome::result< void > | **[SaveInSecureStorage](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-saveinsecurestorage)**(const std::string & key, const [ISecureStorage::SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype) & buffer) |
| outcome::result< [ISecureStorage::SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype) > | **[LoadFromSecureStorage](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-loadfromsecurestorage)**(const std::string & key) |
| const [UTXOManager](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/) & | **[GetUTXOManager](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-getutxomanager)**() const |
| [UTXOManager](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/) & | **[GetUTXOManager](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-getutxomanager)**() |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[SetGetBlockChainCIDMethod](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-setgetblockchaincidmethod)**(std::function< outcome::result< std::string >(uint8_t, const std::string &)> method) |
| void | **[ClearGetBlockChainCIDMethod](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-cleargetblockchaincidmethod)**() |
| void | **[SetHasBlockCidMethod](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-sethasblockcidmethod)**(std::function< outcome::result< bool >(const std::string &)> method) |
| void | **[ClearHasBlockCidMethod](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-clearhasblockcidmethod)**() |
| void | **[SetGetValidatorWeightMethod](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-setgetvalidatorweightmethod)**(std::function< outcome::result< std::optional< uint64_t > >(const std::string &)> method) |
| void | **[ClearGetValidatorWeightMethod](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-cleargetvalidatorweightmethod)**() |
| void | **[SetGetTransactionCIDMethod](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-setgettransactioncidmethod)**(std::function< outcome::result< std::string >(const std::string &)> method) |
| void | **[ClearGetTransactionCIDMethod](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-cleargettransactioncidmethod)**() |
| void | **[SetNonceStore](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-setnoncestore)**(std::shared_ptr< [storage::rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/) > db) |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| const std::array< uint8_t, 32 > | **[ELGAMAL_PUBKEY_PREDEFINED](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#variable-elgamal_pubkey_predefined)** <br/>Legacy deterministic seed bytes.  |
| int64_t | **[NONCE_CACHE_DURATION_MS](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#variable-nonce_cache_duration_ms)** <br/>Cache nonce results for 5 seconds.  |

## Friends

|                | Name           |
| -------------- | -------------- |
| class | **[Blockchain](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#friend-blockchain)**  |
| class | **[TransactionManager](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#friend-transactionmanager)**  |

## Public Types Documentation

### using StorageWithAddress

```cpp
using sgns::GeniusAccount::StorageWithAddress = std::pair<std::shared_ptr<ISecureStorage>, ethereum::EthereumKeyGenerator>;
```


### using SecureStorageFactory

```cpp
using sgns::GeniusAccount::SecureStorageFactory = std::function<std::shared_ptr<ISecureStorage>( const std::string &identifier )>;
```

Factory function type for creating secure storage instances. 

**Parameters**: 

  * **identifier** Storage identifier (typically base58-encoded public key). 


**Return**: Shared pointer to the created secure storage backend. 

## Public Functions Documentation

### function SetSecureStorageFactory

```cpp
static void SetSecureStorageFactory(
    SecureStorageFactory factory
)
```

Sets the secure storage factory used by all [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/) factory methods. 

**Parameters**: 

  * **factory** Factory function; pass nullptr to restore the default. 


By default, the factory creates OS-specific secure storage (Apple Keychain, Linux secret service, etc.). Tests can override this to inject [MemorySecureStorage](/source-reference/Classes/d0/d0d/classsgns_1_1_memory_secure_storage/), eliminating keychain prompts entirely.


### function GetSecureStorageFactory

```cpp
static const SecureStorageFactory & GetSecureStorageFactory()
```

Returns the current secure storage factory (default if none set). 

### function New

```cpp
static std::shared_ptr< GeniusAccount > New(
    TokenID token_id,
    const boost::filesystem::path & base_path,
    bool full_node =false
)
```

Try creating an account by first loading it from storage, and if failure, create one with [NewFromRandomMnemonic](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/#function-newfromrandommnemonic). 

**Parameters**: 

  * **token_id** Token ID of the account 
  * **base_path** Base path to store/retrieve keys. 
  * **full_node** Whether to initialize as a full node. 


### function NewFromPrivateKey

```cpp
static std::shared_ptr< GeniusAccount > NewFromPrivateKey(
    TokenID token_id,
    const char * eth_private_key,
    const boost::filesystem::path & base_path,
    bool full_node =false
)
```

Creates an account from an Ethereum private key. 

**Parameters**: 

  * **token_id** Token ID of the account. 
  * **eth_private_key** Ethereum private key in hex format (0x...). 
  * **base_path** Base path to store/retrieve keys. 
  * **full_node** Whether to initialize as a full node. 


**Return**: Valid pointer if succeeds, nullptr otherwise. 

### function NewFromPublicKey

```cpp
static std::shared_ptr< GeniusAccount > NewFromPublicKey(
    TokenID token_id,
    std::string_view public_key,
    bool full_node =false
)
```

Creates an account by loading directly from storage. If the account wasn't previously stored, returns `nullptr`. 

### function NewFromMnemonic

```cpp
static std::shared_ptr< GeniusAccount > NewFromMnemonic(
    TokenID token_id,
    const std::string & mnemonic,
    const boost::filesystem::path & base_path,
    bool full_node =false
)
```

Creates an account from a BIP39 mnemonic phrase. 

**Parameters**: 

  * **token_id** Token ID of the account. 
  * **mnemonic** BIP39 mnemonic phrase. 
  * **base_path** Base path to store/retrieve keys. 
  * **full_node** Whether to initialize as a full node. 


**Return**: Valid pointer if succeeds, nullptr otherwise. 

### function NewFromRandomMnemonic

```cpp
static std::pair< std::shared_ptr< GeniusAccount >, std::string > NewFromRandomMnemonic(
    TokenID token_id,
    const boost::filesystem::path & base_path,
    bool full_node =false
)
```

Creates an account with a newly generated random BIP39 mnemonic. 

**Parameters**: 

  * **token_id** Token ID of the account. 
  * **base_path** Base path to store/retrieve keys. 
  * **full_node** Whether to initialize as a full node. 


**Return**: Pair of shared account instance (nullptr on failure) and the generated mnemonic phrase. 

### function GetAvailableAccounts

```cpp
static std::vector< std::string > GetAvailableAccounts(
    const boost::filesystem::path & base_path
)
```


### function DeleteAccount

```cpp
static outcome::result< void > DeleteAccount(
    std::string_view public_address,
    const boost::filesystem::path & base_path
)
```


### function NormalizeAddress

```cpp
static std::string_view NormalizeAddress(
    std::string_view address
)
```

Strips the "0x" prefix from an address if present. Stored addresses are prefix-free; this normalizes user input for lookups. 

**Parameters**: 

  * **address** The address string, optionally prefixed with "0x". 


**Return**: A string_view pointing past the "0x" prefix if one was present. 

### function IsValidPublicKey

```cpp
static bool IsValidPublicKey(
    std::string_view key
)
```

Validates that a string is a valid 512-bit public key in hex format. A valid key is exactly 128 hex characters with no prefix. 

**Parameters**: 

  * **key** The key string to validate. 


**Return**: true if the key is a valid 128-character hex string, false otherwise. 

### function VerifySignature

```cpp
static bool VerifySignature(
    const std::string & address,
    std::string_view sig,
    const std::vector< uint8_t > & data
)
```

Verify a signature using the Genius account's public key. 

**Parameters**: 

  * **address** public address to verify the signature 
  * **sig** signature to be verified 
  * **data** data to be verified 


**Return**: true if the signature is valid, false otherwise 

### function GenerateGeniusAddress

```cpp
static outcome::result< StorageWithAddress > GenerateGeniusAddress(
    const char * eth_private_key,
    const boost::filesystem::path & base_path
)
```


### function GenerateGeniusAddress

```cpp
static outcome::result< StorageWithAddress > GenerateGeniusAddress(
    const TW::PrivateKey & private_key,
    const boost::filesystem::path & base_path
)
```


### function InitMessenger

```cpp
bool InitMessenger(
    std::shared_ptr< ipfs_pubsub::GossipPubSub > pubsub
)
```

Initialize the messenger for the account. 

**Parameters**: 

  * **pubsub** pubsub instance 


**Return**: true if succeeds, false otherwise 

### function ConfigureDatabaseDependencies

```cpp
bool ConfigureDatabaseDependencies(
    std::shared_ptr< crdt::GlobalDB > global_db
)
```

Configures database dependencies: nonce store, block response handler, head request handler, and block CID lookup method. 

**Parameters**: 

  * **global_db** GlobalDB instance used to store fetched block CIDs. 


**Return**: true if successfully configured, false otherwise. 

### function DeconfigureDatabaseDependencies

```cpp
void DeconfigureDatabaseDependencies()
```

Clears handlers and methods set by ConfigureDatabaseDependencies. 

### function ~GeniusAccount

```cpp
~GeniusAccount()
```

Destroy the Genius Account object. 

### function GetAddress

```cpp
std::string GetAddress() const
```

Get the Address object. 

**Return**: String representation of the address 

### function GetToken

```cpp
TokenID GetToken() const
```

Get the account's token. 

**Return**: The token of the account 

### function GetNonce

```cpp
inline std::string GetNonce() const
```

Get the proposed (next available) nonce as a string. 

**Return**: The proposed nonce in string format 

### function Sign

```cpp
std::vector< uint8_t > Sign(
    const std::vector< uint8_t > & data
) const
```

Sign data using the Genius account's private key. 

**Parameters**: 

  * **data** data to be signed 


**Return**: the signature as a vector of bytes 

### function CreateInputsFromUTXOs

```cpp
std::vector< InputUTXOInfo > CreateInputsFromUTXOs(
    const std::vector< GeniusUTXO > & utxos
) const
```

Build signed transaction inputs from UTXOs. 

**Parameters**: 

  * **utxos** UTXOs to turn into transaction inputs 


**Return**: Signed input descriptors 

### function SetPeerConfirmedNonce

```cpp
void SetPeerConfirmedNonce(
    uint64_t nonce,
    const std::string & address,
    const std::string & tx_hash =""
)
```

Set the confirmed nonce for an address. 

**Parameters**: 

  * **nonce** The nonce value to be set 
  * **address** The address whose nonce is being updated 
  * **tx_hash** The confirmed transaction hash. Persisted only for the local address 


### function RollBackPeerConfirmedNonce

```cpp
void RollBackPeerConfirmedNonce(
    uint64_t nonce,
    const std::string & address
)
```

Rollback the confirmed nonce for the given address. Also rolls back local confirmed nonce and tx history when the address is local. 

**Parameters**: 

  * **nonce** The nonce value to be rolled back from (only rolls back if it matches current) 
  * **address** The address whose nonce is being rolled back 


### function GetPeerNonce

```cpp
outcome::result< uint64_t > GetPeerNonce(
    const std::string & address
) const
```

Get the confirmed nonce for a peer. 

**Parameters**: 

  * **address** The address of the peer 


**Return**: The confirmed nonce of the peer if exists, error otherwise 

### function GetLocalConfirmedNonce

```cpp
outcome::result< uint64_t > GetLocalConfirmedNonce() const
```

Get the local confirmed nonce. 

**Return**: The local confirmed nonce if exists, error otherwise 

### function GetLocalConfirmedTxHash

```cpp
outcome::result< std::string > GetLocalConfirmedTxHash(
    uint64_t nonce
) const
```

Get a locally persisted confirmed transaction hash by nonce. 

**Parameters**: 

  * **nonce** The confirmed nonce to search for 


**Return**: The confirmed transaction hash if it exists, error otherwise 

### function GetConfirmedNonce

```cpp
outcome::result< uint64_t > GetConfirmedNonce(
    uint64_t timeout_ms
) const
```

Get confirmed nonce from the network. 

**Parameters**: 

  * **timeout_ms** Timeout in miliseconds to get the confirmed nonce 


**Return**: The confirmed nonce if success, error otherwise 

### function FetchNetworkNonce

```cpp
outcome::result< std::optional< uint64_t > > FetchNetworkNonce(
    uint64_t timeout_ms
) const
```

Fetch the latest nonce from the network without relying on cached values. 

**Parameters**: 

  * **timeout_ms** Timeout in miliseconds to get the confirmed nonce 


**Return**: Error if no response received, optional nonce if success 

### function GetProposedNonce

```cpp
uint64_t GetProposedNonce() const
```

Get the next available nonce without reserving it. 

**Return**: The nonce that would be assigned to the next transaction 

### function ReserveNextNonce

```cpp
uint64_t ReserveNextNonce()
```

Reserve the next available nonce. 

**Return**: The reserved nonce value 

### function ReleaseNonce

```cpp
void ReleaseNonce(
    uint64_t nonce
)
```

Release a previously reserved nonce. 

**Parameters**: 

  * **nonce** The nonce to release 


### function RequestGenesis

```cpp
outcome::result< void > RequestGenesis(
    uint64_t timeout_ms =8000,
    std::function< void(outcome::result< std::string >)> callback =nullptr
) const
```


### function RequestAccountCreation

```cpp
outcome::result< void > RequestAccountCreation(
    uint64_t timeout_ms,
    std::function< void(outcome::result< std::string >)> callback
) const
```


### function RequestValidatorRegistry

```cpp
outcome::result< void > RequestValidatorRegistry(
    uint64_t timeout_ms,
    std::function< void(outcome::result< std::string >)> callback
) const
```


### function RequestRegularBlock

```cpp
outcome::result< void > RequestRegularBlock(
    uint64_t timeout_ms,
    const std::string & cid,
    std::function< void(outcome::result< std::string >)> callback =nullptr
) const
```


### function RequestTransaction

```cpp
outcome::result< void > RequestTransaction(
    uint64_t timeout_ms,
    const std::string & tx_hash,
    std::function< void(outcome::result< std::string >)> callback =nullptr
) const
```


### function RequestUTXOs

```cpp
outcome::result< std::unordered_set< std::string > > RequestUTXOs(
    uint64_t timeout_ms,
    const std::string & address,
    uint64_t silent_time_ms =150
) const
```

Request UTXOs for a specific address and return the selected response. 

**Parameters**: 

  * **timeout_ms** Total timeout in milliseconds to wait for responses 
  * **address** Address to request UTXOs for 
  * **silent_time_ms** Time to wait for subsequent responses after first one 


**Return**: Set of UTXO strings based on selection criteria, or error otherwise 

### function RequestHeads

```cpp
outcome::result< void > RequestHeads(
    const std::unordered_set< std::string > & topics
) const
```

Request heads broadcast for specific topics. 

**Parameters**: 

  * **topics** Set of topic names to request heads for 


**Return**: outcome::success if request was sent, error otherwise 

### function SaveInSecureStorage

```cpp
inline outcome::result< void > SaveInSecureStorage(
    const std::string & key,
    const ISecureStorage::SecureBufferType & buffer
)
```


### function LoadFromSecureStorage

```cpp
inline outcome::result< ISecureStorage::SecureBufferType > LoadFromSecureStorage(
    const std::string & key
)
```


### function GetUTXOManager

```cpp
inline const UTXOManager & GetUTXOManager() const
```


### function GetUTXOManager

```cpp
inline UTXOManager & GetUTXOManager()
```


## Protected Functions Documentation

### function SetGetBlockChainCIDMethod

```cpp
void SetGetBlockChainCIDMethod(
    std::function< outcome::result< std::string >(uint8_t, const std::string &)> method
)
```


### function ClearGetBlockChainCIDMethod

```cpp
void ClearGetBlockChainCIDMethod()
```


### function SetHasBlockCidMethod

```cpp
void SetHasBlockCidMethod(
    std::function< outcome::result< bool >(const std::string &)> method
)
```


### function ClearHasBlockCidMethod

```cpp
void ClearHasBlockCidMethod()
```


### function SetGetValidatorWeightMethod

```cpp
void SetGetValidatorWeightMethod(
    std::function< outcome::result< std::optional< uint64_t > >(const std::string &)> method
)
```


### function ClearGetValidatorWeightMethod

```cpp
void ClearGetValidatorWeightMethod()
```


### function SetGetTransactionCIDMethod

```cpp
void SetGetTransactionCIDMethod(
    std::function< outcome::result< std::string >(const std::string &)> method
)
```


### function ClearGetTransactionCIDMethod

```cpp
void ClearGetTransactionCIDMethod()
```


### function SetNonceStore

```cpp
void SetNonceStore(
    std::shared_ptr< storage::rocksdb > db
)
```


## Public Attributes Documentation

### variable ELGAMAL_PUBKEY_PREDEFINED

```cpp
static const std::array< uint8_t, 32 > ELGAMAL_PUBKEY_PREDEFINED {
        0xfc, 0x60, 0x52, 0x6c, 0x91, 0xec, 0x81, 0xd5, 0xd4, 0xfa, 0xb2, 0x78, 0x04, 0xad, 0x93, 0xd0,
        0xd4, 0xf9, 0x4b, 0x55, 0xc7, 0x5e, 0xed, 0x6f, 0xda, 0x2e, 0xa0, 0xc9, 0xc8, 0x2c, 0x21, 0x36,
    };
```

Legacy deterministic seed bytes. 

### variable NONCE_CACHE_DURATION_MS

```cpp
static int64_t NONCE_CACHE_DURATION_MS = 5000;
```

Cache nonce results for 5 seconds. 

## Friends

### friend Blockchain

```cpp
friend class Blockchain(
    Blockchain 
);
```


### friend TransactionManager

```cpp
friend class TransactionManager(
    TransactionManager 
);
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
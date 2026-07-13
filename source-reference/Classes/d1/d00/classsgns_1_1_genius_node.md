---
title: sgns::GeniusNode
summary: High-level facade that initializes and coordinates account, networking, transaction, blockchain, and processing subsystems. 

---

# sgns::GeniusNode



High-level facade that initializes and coordinates account, networking, transaction, blockchain, and processing subsystems. 


`#include <GeniusNode.hpp>`

Inherits from [IComponent](/source-reference/Classes/d1/dbf/class_i_component/), [sgns::IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/), std::enable_shared_from_this< GeniusNode >

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class uint8_t | **[NodeState](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#enum-nodestate)** { CREATING = 0, MIGRATING_DATABASE, INITIALIZING_DATABASE, INITIALIZING_BLOCKCHAIN, INITIALIZING_TRANSACTIONS, INITIALIZING_PROCESSING, INITIALIZING_RPC_CATCH_UP, READY}<br/>Lifecycle states reported while the node is bootstrapping.  |
| enum class uint8_t | **[Error](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#enum-error)** { INSUFFICIENT_FUNDS = 1, DATABASE_WRITE_ERROR = 2, INVALID_TRANSACTION_HASH = 3, INVALID_CHAIN_ID = 4, INVALID_TOKEN_ID = 5, TOKEN_ID_MISMATCH = 6, PROCESS_COST_ERROR = 7, PROCESS_INFO_MISSING = 8, INVALID_JSON = 9, INVALID_BLOCK_PARAMETERS = 10, NO_PROCESSOR = 11, NO_PRICE = 12, TRANSACTIONS_NOT_READY = 13, TRANSACTION_NOT_FINALIZED = 14, TRANSACTION_FAILED = 15}<br/>[Error](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#enum-error) codes returned by [GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/) operations.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-geniusnode) > | **[New](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-new)**(const [GeniusNodeConfig](/source-reference/Classes/d2/d8e/struct_genius_node_config/) & dev_config, bool autodht =true, uint16_t base_port =40001, bool is_full_node =false)<br/>Creates a node using a generated or persisted account identity.  |
| std::shared_ptr< [GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-geniusnode) > | **[NewFromPrivateKey](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-newfromprivatekey)**(const [GeniusNodeConfig](/source-reference/Classes/d2/d8e/struct_genius_node_config/) & dev_config, const char * eth_private_key, bool autodht =true, uint16_t base_port =40001, bool is_full_node =false)<br/>Creates a node bound to the provided Ethereum private key.  |
| std::shared_ptr< [GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-geniusnode) > | **[NewFromMnemonic](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-newfrommnemonic)**(const [GeniusNodeConfig](/source-reference/Classes/d2/d8e/struct_genius_node_config/) & dev_config, const std::string & mnemonic, bool autodht =true, uint16_t base_port =40001, bool is_full_node =false)<br/>Creates a node from an existing mnemonic phrase.  |
| | **[~GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-~geniusnode)**() override<br/>Stops node services, joins background threads, and releases processing callbacks.  |
| std::vector< std::string > | **[GetAvailableAccounts](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getavailableaccounts)**()<br/>Lists the account addresses currently available in local storage.  |
| outcome::result< void > | **[AddAccountWithKey](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-addaccountwithkey)**(const char * private_key) const<br/>Adds an account to local storage using an Ethereum private key.  |
| outcome::result< void > | **[AddAccountWithMnemonic](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-addaccountwithmnemonic)**(const std::string & mnemonic) const<br/>Adds an account to local storage using a BIP39 mnemonic phrase.  |
| outcome::result< std::string > | **[AddAccountWithRandomMnemonic](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-addaccountwithrandommnemonic)**() const<br/>Adds an account to local storage using a newly generated random BIP39 mnemonic.  |
| outcome::result< void > | **[SelectAccount](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-selectaccount)**(std::string_view public_address)<br/>Selects the active account for subsequent node operations.  |
| outcome::result< void > | **[TransferAccount](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-transferaccount)**(std::string_view public_address)<br/>Transfers node ownership to another stored account address.  |
| outcome::result< void > | **[DeleteAccount](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-deleteaccount)**(std::string_view public_address)<br/>Deletes a locally stored account.  |
| outcome::result< void > | **[MergeAccount](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-mergeaccount)**(std::string_view public_address)<br/>Merges the active account into another stored account.  |
| outcome::result< void > | **[SetPayoutAddress](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-setpayoutaddress)**(std::string_view payout_address)<br/>Updates the payout address used by processing rewards.  |
| outcome::result< std::string > | **[ProcessImage](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-processimage)**(const std::string & jsondata)<br/>Submits an image-processing request described by JSON input.  |
| std::vector< std::string > | **[GetMyTaskIds](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getmytaskids)**(size_t limit =50, size_t offset =0) const<br/>Returns the task IDs of jobs submitted by the active account.  |
| outcome::result< SGProcessing::TaskResult > | **[GetTaskResult](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-gettaskresult)**(const std::string & taskId)<br/>Retrieves the completed result for a specific job by its task ID.  |
| uint64_t | **[GetProcessCost](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getprocesscost)**(std::shared_ptr< sgns::sgprocessing::ProcessingManager > & procmgr)<br/>Estimates the GNUS cost of a processing request manager.  |
| outcome::result< double > | **[GetGNUSPrice](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getgnusprice)**()<br/>Retrieves the current GNUS market price from the configured pricing service.  |
| virtual std::string | **[GetName](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getname)**() override<br/>Returns the component name used by the component framework.  |
| std::string | **[GetVersion](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getversion)**()<br/>Returns the full SuperGenius version string.  |
| void | **[LoadLogConfig](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-loadlogconfig)**() |
| outcome::result< std::string > | **[MintTokens](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-minttokens)**(uint64_t amount, const std::string & transaction_hash, const std::string & chainid, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) tokenid, std::string destination ="")<br/>Creates and submits a mint transaction.  |
| outcome::result< std::pair< std::string, uint64_t > > | **[MintTokens](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-minttokens)**(uint64_t amount, const std::string & transaction_hash, const std::string & chainid, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) tokenid, std::string destination, std::chrono::milliseconds timeout)<br/>Creates a mint transaction and waits for it to finalize.  |
| void | **[AddPeer](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-addpeer)**(const std::string & peer)<br/>Adds a peer address to the underlying PubSub service.  |
| void | **[RefreshUPNP](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-refreshupnp)**(uint16_t pubsubport)<br/>Starts or restarts the background UPnP port refresh thread.  |
| uint64_t | **[GetBalance](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getbalance)**()<br/>Returns the active account balance across all tokens.  |
| uint64_t | **[GetBalance](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getbalance)**([TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id)<br/>Returns the active account balance for a token.  |
| uint64_t | **[GetBalance](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getbalance)**(const std::string & address)<br/>Returns an address balance across all tokens.  |
| uint64_t | **[GetBalance](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getbalance)**([TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id, const std::string & address)<br/>Returns an address balance for a token.  |
| std::vector< std::vector< uint8_t > > | **[GetInTransactions](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getintransactions)**() const<br/>Returns serialized incoming transactions known to the transaction manager.  |
| std::vector< std::vector< uint8_t > > | **[GetOutTransactions](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getouttransactions)**() const<br/>Returns serialized outgoing transactions known to the transaction manager.  |
| const std::vector< std::vector< uint8_t > > | **[GetTransactions](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-gettransactions)**(std::optional< [TransactionManager::TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) > tx_status =std::nullopt) const<br/>Returns serialized transactions filtered by optional status.  |
| std::string | **[GetAddress](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getaddress)**() const<br/>Returns the active account public address.  |
| std::optional< std::string > | **[GetMnemonicOfActiveAccount](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getmnemonicofactiveaccount)**() const<br/>Retrieves the BIP39 mnemonic of the active account from secure storage.  |
| [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) | **[GetTokenID](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-gettokenid)**() const<br/>Returns the configured child token identifier.  |
| std::pair< float, std::string > | **[GetInitializationStatus](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getinitializationstatus)**() const<br/>Returns the current node initialization progress as a percentage and description. The percentage ranges from 0.0 (CREATING) to 1.0 (READY), with sub-progress reported during database migration and transaction manager initialization.  |
| [processing::ProcessingServiceImpl::ProcessingStatus](/source-reference/Classes/d7/d27/structsgns_1_1processing_1_1_processing_service_impl_1_1_processing_status/) | **[GetProcessingStatus](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getprocessingstatus)**() const<br/>Returns the current processing service status.  |
| outcome::result< std::pair< std::string, uint64_t > > | **[TransferFunds](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-transferfunds)**(uint64_t amount, const std::string & destination, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id, std::chrono::milliseconds timeout)<br/>Transfers funds and waits for the transaction to finalize.  |
| outcome::result< std::string > | **[TransferFunds](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-transferfunds)**(uint64_t amount, const std::string & destination, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id)<br/>Transfers funds without waiting for finalization.  |
| outcome::result< std::string > | **[PayDev](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-paydev)**(uint64_t amount, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id)<br/>Transfers funds to the configured developer address.  |
| outcome::result< std::pair< std::string, uint64_t > > | **[PayDev](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-paydev)**(uint64_t amount, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id, std::chrono::milliseconds timeout)<br/>Transfers funds to the configured developer address and waits for finalization.  |
| outcome::result< std::pair< [TransactionManager::TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus), uint64_t > > | **[WaitForFinalized](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-waitforfinalized)**(const std::string & tx_id, std::chrono::milliseconds timeout)<br/>Waits until an outgoing transaction reaches a terminal state.  |
| std::optional< [TransactionManager::TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) > | **[IsFinalized](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-isfinalized)**(const std::string & tx_id)<br/>Checks whether an outgoing transaction has reached a terminal state.  |
| std::shared_ptr< ipfs_pubsub::GossipPubSub > | **[GetPubSub](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getpubsub)**()<br/>Returns the underlying PubSub service.  |
| void | **[ResetProcessingMembers](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-resetprocessingmembers)**()<br/>Releases processing service, core, queue, and result-storage references.  |
| outcome::result< std::string > | **[FormatTokens](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-formattokens)**(uint64_t amount, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) tokenId)<br/>Formats a fixed-point amount into a human-readable string.  |
| outcome::result< uint64_t > | **[ParseTokens](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-parsetokens)**(const std::string & str, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) tokenId)<br/>Parses a human-readable string into a fixed-point amount.  |
| void | **[PrintDataStore](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-printdatastore)**() const<br/>Prints the transaction GlobalDB datastore for debugging.  |
| void | **[StopProcessing](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-stopprocessing)**()<br/>Stops the processing service if it is initialized.  |
| void | **[StartProcessing](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-startprocessing)**()<br/>Starts the processing service on the configured processing grid channel.  |
| outcome::result< std::map< std::string, double > > | **[GetCoinprice](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getcoinprice)**(const std::vector< std::string > & tokenIds)<br/>Retrieves current USD prices for token identifiers, using a short local cache.  |
| outcome::result< std::map< std::string, std::map< int64_t, double > > > | **[GetCoinPriceByDate](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getcoinpricebydate)**(const std::vector< std::string > & tokenIds, const std::vector< int64_t > & timestamps)<br/>Retrieves historical USD prices for token identifiers at exact timestamps.  |
| outcome::result< std::map< std::string, std::map< int64_t, double > > > | **[GetCoinPricesByDateRange](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getcoinpricesbydaterange)**(const std::vector< std::string > & tokenIds, int64_t from, int64_t to)<br/>Retrieves historical USD prices for token identifiers over a date range.  |
| [TransactionManager::TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) | **[WaitForTransactionIncoming](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-waitfortransactionincoming)**(const std::string & txId, std::chrono::milliseconds timeout)<br/>Waits for an incoming transaction to be processed.  |
| [TransactionManager::TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) | **[WaitForTransactionOutgoing](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-waitfortransactionoutgoing)**(const std::string & txId, std::chrono::milliseconds timeout)<br/>Waits for an outgoing transaction to be processed.  |
| [TransactionManager::TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) | **[WaitForEscrowRelease](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-waitforescrowrelease)**(const std::string & originalEscrowId, std::chrono::milliseconds timeout)<br/>Waits for an escrow release transaction tied to an escrow hold.  |
| [TransactionManager::State](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-state) | **[GetTransactionManagerState](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-gettransactionmanagerstate)**() const<br/>Returns the current transaction manager lifecycle state.  |
| void | **[ConfigureRpcEndpoint](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-configurerpcendpoint)**(const std::string & chain_id, std::vector< [WeightedRpcEndpoint](/source-reference/Classes/d4/d8c/structsgns_1_1_weighted_rpc_endpoint/) > endpoints)<br/>Configures RPC endpoints for a specific EVM chain on the public-chain input validator.  |
| [TransactionManager::TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) | **[GetTransactionStatus](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-gettransactionstatus)**(const std::string & txId) const<br/>Returns a tracked transaction status by transaction hash.  |
| void | **[SetAuthorizedFullNodeAddress](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-setauthorizedfullnodeaddress)**(const std::string & pub_address)<br/>Sets the authorized full-node address for blockchain genesis verification.  |
| const std::string & | **[GetAuthorizedFullNodeAddress](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getauthorizedfullnodeaddress)**() const<br/>Gets the current authorized full-node public address.  |
| [NodeState](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#enum-nodestate) | **[GetState](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getstate)**() const<br/>Returns the current [GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/) lifecycle state.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[SendTransactionAndProof](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-sendtransactionandproof)**(std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > tx, std::vector< uint8_t > proof)<br/>Enqueues a transaction and its proof directly through the transaction manager.  |
| void | **[ConfigureTransactionFilterTimeoutsMs](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-configuretransactionfiltertimeoutsms)**(uint64_t timeframe_limit_ms, uint64_t mutability_window_ms)<br/>Configures transaction filtering time windows for tests.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::chrono::milliseconds | **[TIMEOUT_ESCROW_PAY](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#variable-timeout_escrow_pay)** <br/>Escrow payout timeout.  |
| std::chrono::milliseconds | **[TIMEOUT_TRANSFER](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#variable-timeout_transfer)** <br/>Transfer timeout.  |
| std::chrono::milliseconds | **[TIMEOUT_MINT](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#variable-timeout_mint)** <br/>Mint timeout.  |

## Protected Attributes

|                | Name           |
| -------------- | -------------- |
| std::string | **[write_base_path_](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#variable-write_base_path_)** <br/>Base path for node databases, logs, and account storage.  |
| std::shared_ptr< [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/) > | **[account_](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#variable-account_)** <br/>Active account used by node services.  |

## Friends

|                | Name           |
| -------------- | -------------- |
| class | **[TransactionSyncTest](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#friend-transactionsynctest)**  |
| class | **[MultiAccountTestAccess](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#friend-multiaccounttestaccess)**  |

## Additional inherited members

**Public Functions inherited from [IComponent](/source-reference/Classes/d1/dbf/class_i_component/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IComponent](/source-reference/Classes/d1/dbf/class_i_component/#function-~icomponent)**() =default |

**Public Functions inherited from [sgns::IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/#function-~ibridgeinitobserver)**() =default |


## Public Types Documentation

### enum NodeState

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| CREATING | 0| Object construction is in progress.   |
| MIGRATING_DATABASE | | Versioned database migrations are running.   |
| INITIALIZING_DATABASE | | Primary CRDT database is being initialized.   |
| INITIALIZING_BLOCKCHAIN | | [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) service is being initialized.   |
| INITIALIZING_TRANSACTIONS | | Transaction manager is being initialized.   |
| INITIALIZING_PROCESSING | | Processing modules are being initialized.   |
| INITIALIZING_RPC_CATCH_UP | | RPC catch-up service is being initialized.   |
| READY | | Node is ready for external operations.   |



Lifecycle states reported while the node is bootstrapping. 

### enum Error

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| INSUFFICIENT_FUNDS | 1| Insufficient funds for a transaction.   |
| DATABASE_WRITE_ERROR | 2| [Error](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#enum-error) writing data into the database.   |
| INVALID_TRANSACTION_HASH | 3| Input transaction hash is invalid.   |
| INVALID_CHAIN_ID | 4| Chain ID is invalid.   |
| INVALID_TOKEN_ID | 5| Token ID is invalid.   |
| TOKEN_ID_MISMATCH | 6| Provided token ID does not match the configured token.   |
| PROCESS_COST_ERROR | 7| Processing cost could not be calculated.   |
| PROCESS_INFO_MISSING | 8| Processing information is missing from the JSON request.   |
| INVALID_JSON | 9| JSON cannot be parsed.   |
| INVALID_BLOCK_PARAMETERS | 10| JSON block parameters are incorrect or missing.   |
| NO_PROCESSOR | 11| No processor is available for this request type.   |
| NO_PRICE | 12| GNUS price could not be retrieved.   |
| TRANSACTIONS_NOT_READY | 13| Transaction manager is not ready.   |
| TRANSACTION_NOT_FINALIZED | 14| Requested transaction did not finalize within the timeout.   |
| TRANSACTION_FAILED | 15| Requested transaction failed.   |



[Error](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#enum-error) codes returned by [GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/) operations. 

## Public Functions Documentation

### function New

```cpp
static std::shared_ptr< GeniusNode > New(
    const GeniusNodeConfig & dev_config,
    bool autodht =true,
    uint16_t base_port =40001,
    bool is_full_node =false
)
```

Creates a node using a generated or persisted account identity. 

**Parameters**: 

  * **dev_config** Runtime configuration for paths, token settings, and payout data. 
  * **autodht** Whether to start DHT discovery. 
  * **base_port** Base pubsub port used to derive the node listening port. 
  * **is_full_node** Whether the node should run in full-node mode. 


**Return**: Shared node instance after asynchronous database initialization is scheduled. 

**Note**: Whether this node runs processing services is read from sgns_config.json (`is_processor`, default true). 

### function NewFromPrivateKey

```cpp
static std::shared_ptr< GeniusNode > NewFromPrivateKey(
    const GeniusNodeConfig & dev_config,
    const char * eth_private_key,
    bool autodht =true,
    uint16_t base_port =40001,
    bool is_full_node =false
)
```

Creates a node bound to the provided Ethereum private key. 

**Parameters**: 

  * **dev_config** Runtime configuration for paths, token settings, and payout data. 
  * **eth_private_key** Ethereum private key used to derive the account identity. 
  * **autodht** Whether to start DHT discovery. 
  * **base_port** Base pubsub port used to derive the node listening port. 
  * **is_full_node** Whether the node should run in full-node mode. 


**Return**: Shared node instance after asynchronous database initialization is scheduled. 

**Note**: Whether this node runs processing services is read from sgns_config.json (`is_processor`, default true). 

### function NewFromMnemonic

```cpp
static std::shared_ptr< GeniusNode > NewFromMnemonic(
    const GeniusNodeConfig & dev_config,
    const std::string & mnemonic,
    bool autodht =true,
    uint16_t base_port =40001,
    bool is_full_node =false
)
```

Creates a node from an existing mnemonic phrase. 

**Parameters**: 

  * **dev_config** Runtime configuration for paths, token settings, and payout data. 
  * **mnemonic** Mnemonic phrase used to restore the account identity. 
  * **autodht** Whether to start DHT discovery. 
  * **base_port** Base pubsub port used to derive the node listening port. 
  * **is_full_node** Whether the node should run in full-node mode. 


**Return**: Shared node instance after asynchronous database initialization is scheduled, or nullptr on restore failure. 

**Note**: Whether this node runs processing services is read from sgns_config.json (`is_processor`, default true). 

### function ~GeniusNode

```cpp
~GeniusNode() override
```

Stops node services, joins background threads, and releases processing callbacks. 

### function GetAvailableAccounts

```cpp
std::vector< std::string > GetAvailableAccounts()
```

Lists the account addresses currently available in local storage. 

**Return**: Public addresses stored under the configured base write path. 

### function AddAccountWithKey

```cpp
outcome::result< void > AddAccountWithKey(
    const char * private_key
) const
```

Adds an account to local storage using an Ethereum private key. 

**Parameters**: 

  * **private_key** Ethereum private key in hex format. 


**Return**: Success if the account was created and stored, or an error. 

### function AddAccountWithMnemonic

```cpp
outcome::result< void > AddAccountWithMnemonic(
    const std::string & mnemonic
) const
```

Adds an account to local storage using a BIP39 mnemonic phrase. 

**Parameters**: 

  * **mnemonic** BIP39 mnemonic phrase. 


**Return**: Success if the account was created and stored, or an error. 

### function AddAccountWithRandomMnemonic

```cpp
outcome::result< std::string > AddAccountWithRandomMnemonic() const
```

Adds an account to local storage using a newly generated random BIP39 mnemonic. 

**Return**: The generated mnemonic phrase on success, or an error. 

### function SelectAccount

```cpp
outcome::result< void > SelectAccount(
    std::string_view public_address
)
```

Selects the active account for subsequent node operations. 

**Parameters**: 

  * **public_address** Stored account address to activate. 


**Return**: Success after services are reset and database initialization is restarted, or an address error. 

### function TransferAccount

```cpp
outcome::result< void > TransferAccount(
    std::string_view public_address
)
```

Transfers node ownership to another stored account address. 

**Parameters**: 

  * **public_address** Stored account address that should receive the current balance and become active. 


**Return**: Success after funds are transferred and the target account is selected, or an address/transaction error. 

### function DeleteAccount

```cpp
outcome::result< void > DeleteAccount(
    std::string_view public_address
)
```

Deletes a locally stored account. 

**Parameters**: 

  * **public_address** Stored account address to delete. 


**Return**: Success when the account is deleted; failure when the address is active or unavailable. 

### function MergeAccount

```cpp
outcome::result< void > MergeAccount(
    std::string_view public_address
)
```

Merges the active account into another stored account. 

**Parameters**: 

  * **public_address** Stored account address to receive the configured-token balance and become active. 


**Return**: Success when transfer, selection, and deletion of the previous active account complete. 

### function SetPayoutAddress

```cpp
outcome::result< void > SetPayoutAddress(
    std::string_view payout_address
)
```

Updates the payout address used by processing rewards. 

**Parameters**: 

  * **payout_address** Address to save as the processing payout destination. 


**Return**: Success when the address is persisted and processing reinitialization is scheduled. 

### function ProcessImage

```cpp
outcome::result< std::string > ProcessImage(
    const std::string & jsondata
)
```

Submits an image-processing request described by JSON input. 

**Parameters**: 

  * **jsondata** Processing request JSON. 


**Return**: Escrow transaction hash on success, or a validation, balance, or database error. 

### function GetMyTaskIds

```cpp
std::vector< std::string > GetMyTaskIds(
    size_t limit =50,
    size_t offset =0
) const
```

Returns the task IDs of jobs submitted by the active account. 

**Parameters**: 

  * **limit** Maximum number of task IDs to return (default: 50). 
  * **offset** Number of task IDs to skip from the end of the list (default: 0). 


**Return**: Vector of task IDs from the in-memory set, newest last. 

**Note**: The on-disk file retains full history; only the most recent entries are kept in memory for polling. 

### function GetTaskResult

```cpp
outcome::result< SGProcessing::TaskResult > GetTaskResult(
    const std::string & taskId
)
```

Retrieves the completed result for a specific job by its task ID. 

**Parameters**: 

  * **taskId** The task ID (ipfs_block_id) of the job. 


**Return**: The TaskResult if the task has completed, or an error if not found/incomplete. 

### function GetProcessCost

```cpp
uint64_t GetProcessCost(
    std::shared_ptr< sgns::sgprocessing::ProcessingManager > & procmgr
)
```

Estimates the GNUS cost of a processing request manager. 

**Parameters**: 

  * **procmgr** Processing manager containing parsed request data. 


**Return**: Estimated cost in minions, or 0 when the request size, price, or cost calculation fails. 

### function GetGNUSPrice

```cpp
outcome::result< double > GetGNUSPrice()
```

Retrieves the current GNUS market price from the configured pricing service. 

**Return**: Current GNUS price in USD, or [Error::NO_PRICE](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#enumvalue-no_price) when unavailable. 

### function GetName

```cpp
inline virtual std::string GetName() override
```

Returns the component name used by the component framework. 

**Return**: Static component name "GeniusNode". 

**Reimplements**: [IComponent::GetName](/source-reference/Classes/d1/dbf/class_i_component/#function-getname)


### function GetVersion

```cpp
std::string GetVersion()
```

Returns the full SuperGenius version string. 

**Return**: Version string built from the compiled version metadata. 

### function LoadLogConfig

```cpp
void LoadLogConfig()
```


Reloads log level overrides from log_config.json at runtime. 


### function MintTokens

```cpp
outcome::result< std::string > MintTokens(
    uint64_t amount,
    const std::string & transaction_hash,
    const std::string & chainid,
    TokenID tokenid,
    std::string destination =""
)
```

Creates and submits a mint transaction. 

**Parameters**: 

  * **amount** Amount to mint in token base units. 
  * **transaction_hash** Source-chain transaction hash that justifies the mint. 
  * **chainid** Source chain identifier where the burn or lock event occurred. 
  * **tokenid** Token identifier to mint. 
  * **destination** Recipient address; defaults to the active account address when empty. 


**Return**: Mint transaction hash on success, or a transaction readiness/submission error. 

### function MintTokens

```cpp
outcome::result< std::pair< std::string, uint64_t > > MintTokens(
    uint64_t amount,
    const std::string & transaction_hash,
    const std::string & chainid,
    TokenID tokenid,
    std::string destination,
    std::chrono::milliseconds timeout
)
```

Creates a mint transaction and waits for it to finalize. 

**Parameters**: 

  * **amount** Amount to mint in token base units. 
  * **transaction_hash** Source-chain transaction hash that justifies the mint. 
  * **chainid** Source chain identifier where the burn or lock event occurred. 
  * **tokenid** Token identifier to mint. 
  * **destination** Recipient address for the minted tokens. 
  * **timeout** Maximum time to wait for finalization. 


**Return**: Pair of transaction hash and elapsed milliseconds on success, or a transaction/finalization error. 

### function AddPeer

```cpp
void AddPeer(
    const std::string & peer
)
```

Adds a peer address to the underlying PubSub service. 

**Parameters**: 

  * **peer** Peer multiaddress to add. 


### function RefreshUPNP

```cpp
void RefreshUPNP(
    uint16_t pubsubport
)
```

Starts or restarts the background UPnP port refresh thread. 

**Parameters**: 

  * **pubsubport** TCP port to keep mapped through UPnP. 


### function GetBalance

```cpp
uint64_t GetBalance()
```

Returns the active account balance across all tokens. 

**Return**: Total local UTXO balance for the active account. 

### function GetBalance

```cpp
uint64_t GetBalance(
    TokenID token_id
)
```

Returns the active account balance for a token. 

**Parameters**: 

  * **token_id** Token identifier to filter by. 


**Return**: Local UTXO balance for `token_id`. 

### function GetBalance

```cpp
uint64_t GetBalance(
    const std::string & address
)
```

Returns an address balance across all tokens. 

**Parameters**: 

  * **address** Address whose UTXO balance should be queried. 


**Return**: Total local UTXO balance for `address`. 

### function GetBalance

```cpp
uint64_t GetBalance(
    TokenID token_id,
    const std::string & address
)
```

Returns an address balance for a token. 

**Parameters**: 

  * **token_id** Token identifier to filter by. 
  * **address** Address whose UTXO balance should be queried. 


**Return**: Local UTXO balance for `address` and `token_id`. 

### function GetInTransactions

```cpp
std::vector< std::vector< uint8_t > > GetInTransactions() const
```

Returns serialized incoming transactions known to the transaction manager. 

**Return**: Incoming transaction byte vectors, or an empty vector when transactions are not ready. 

### function GetOutTransactions

```cpp
std::vector< std::vector< uint8_t > > GetOutTransactions() const
```

Returns serialized outgoing transactions known to the transaction manager. 

**Return**: Outgoing transaction byte vectors, or an empty vector when transactions are not ready. 

### function GetTransactions

```cpp
const std::vector< std::vector< uint8_t > > GetTransactions(
    std::optional< TransactionManager::TransactionStatus > tx_status =std::nullopt
) const
```

Returns serialized transactions filtered by optional status. 

**Parameters**: 

  * **tx_status** Optional transaction status filter. 


**Return**: Transaction byte vectors, or an empty vector when transactions are not ready. 

### function GetAddress

```cpp
std::string GetAddress() const
```

Returns the active account public address. 

**Return**: Public address of the active account. 

### function GetMnemonicOfActiveAccount

```cpp
std::optional< std::string > GetMnemonicOfActiveAccount() const
```

Retrieves the BIP39 mnemonic of the active account from secure storage. 

**Return**: The mnemonic phrase if found, or std::nullopt. 

### function GetTokenID

```cpp
inline TokenID GetTokenID() const
```

Returns the configured child token identifier. 

**Return**: Token identifier from the node runtime configuration. 

### function GetInitializationStatus

```cpp
std::pair< float, std::string > GetInitializationStatus() const
```

Returns the current node initialization progress as a percentage and description. The percentage ranges from 0.0 (CREATING) to 1.0 (READY), with sub-progress reported during database migration and transaction manager initialization. 

**Return**: Pair of progress fraction and a human-readable status description. 

### function GetProcessingStatus

```cpp
inline processing::ProcessingServiceImpl::ProcessingStatus GetProcessingStatus() const
```

Returns the current processing service status. 

**Return**: Processing status, or DISABLED when the service is not initialized. 

### function TransferFunds

```cpp
outcome::result< std::pair< std::string, uint64_t > > TransferFunds(
    uint64_t amount,
    const std::string & destination,
    TokenID token_id,
    std::chrono::milliseconds timeout
)
```

Transfers funds and waits for the transaction to finalize. 

**Parameters**: 

  * **amount** Amount to transfer in token base units. 
  * **destination** Recipient address. 
  * **token_id** Token identifier to transfer. 
  * **timeout** Maximum time to wait for finalization. 


**Return**: Pair of transaction hash and elapsed milliseconds on success, or a transfer/finalization error. 

### function TransferFunds

```cpp
outcome::result< std::string > TransferFunds(
    uint64_t amount,
    const std::string & destination,
    TokenID token_id
)
```

Transfers funds without waiting for finalization. 

**Parameters**: 

  * **amount** Amount to transfer in token base units. 
  * **destination** Recipient address. 
  * **token_id** Token identifier to transfer. 


**Return**: Transfer transaction hash on success, or a readiness, balance, or submission error. 

### function PayDev

```cpp
outcome::result< std::string > PayDev(
    uint64_t amount,
    TokenID token_id
)
```

Transfers funds to the configured developer address. 

**Parameters**: 

  * **amount** Amount to transfer in token base units. 
  * **token_id** Token identifier to transfer. 


**Return**: Transfer transaction hash on success, or a readiness, balance, or submission error. 

### function PayDev

```cpp
outcome::result< std::pair< std::string, uint64_t > > PayDev(
    uint64_t amount,
    TokenID token_id,
    std::chrono::milliseconds timeout
)
```

Transfers funds to the configured developer address and waits for finalization. 

**Parameters**: 

  * **amount** Amount to transfer in token base units. 
  * **token_id** Token identifier to transfer. 
  * **timeout** Maximum time to wait for finalization. 


**Return**: Pair of transaction hash and elapsed milliseconds on success, or a transfer/finalization error. 

### function WaitForFinalized

```cpp
outcome::result< std::pair< TransactionManager::TransactionStatus, uint64_t > > WaitForFinalized(
    const std::string & tx_id,
    std::chrono::milliseconds timeout
)
```

Waits until an outgoing transaction reaches a terminal state. 

**Parameters**: 

  * **tx_id** Transaction hash to poll. 
  * **timeout** Maximum time to wait. 


**Return**: Pair of terminal status and elapsed milliseconds, or [Error::TRANSACTION_NOT_FINALIZED](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#enumvalue-transaction_not_finalized) on timeout. 

### function IsFinalized

```cpp
std::optional< TransactionManager::TransactionStatus > IsFinalized(
    const std::string & tx_id
)
```

Checks whether an outgoing transaction has reached a terminal state. 

**Parameters**: 

  * **tx_id** Transaction hash to check. 


**Return**: Terminal transaction status when available; otherwise std::nullopt. 

### function GetPubSub

```cpp
inline std::shared_ptr< ipfs_pubsub::GossipPubSub > GetPubSub()
```

Returns the underlying PubSub service. 

**Return**: Shared PubSub instance used by the node. 

### function ResetProcessingMembers

```cpp
void ResetProcessingMembers()
```

Releases processing service, core, queue, and result-storage references. 

### function FormatTokens

```cpp
outcome::result< std::string > FormatTokens(
    uint64_t amount,
    TokenID tokenId
)
```

Formats a fixed-point amount into a human-readable string. 

**Parameters**: 

  * **amount** Amount in Minion Tokens (1e-6 GNUS). 
  * **tokenId** Optional token identifier: – empty: default (minion to GNUS) formatting – matches [GeniusNodeConfig.TokenID](/source-reference/Classes/d2/d8e/struct_genius_node_config/#variable-tokenid): child-token formatting – otherwise: returns [Error::TOKEN_ID_MISMATCH](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#enumvalue-token_id_mismatch)


**Return**: Outcome result with the formatted string in GNUS or an error. 

### function ParseTokens

```cpp
outcome::result< uint64_t > ParseTokens(
    const std::string & str,
    TokenID tokenId
)
```

Parses a human-readable string into a fixed-point amount. 

**Parameters**: 

  * **str** String representation of an amount in GNUS. 
  * **tokenId** Optional token identifier: – empty: default (GNUS to minion) parsing – matches [GeniusNodeConfig.TokenID](/source-reference/Classes/d2/d8e/struct_genius_node_config/#variable-tokenid): child-token parsing – otherwise: returns [Error::TOKEN_ID_MISMATCH](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#enumvalue-token_id_mismatch)


**Return**: Outcome result with the parsed amount in Minion Tokens (1e-6 GNUS) or an error. 

### function PrintDataStore

```cpp
void PrintDataStore() const
```

Prints the transaction GlobalDB datastore for debugging. 

### function StopProcessing

```cpp
void StopProcessing()
```

Stops the processing service if it is initialized. 

### function StartProcessing

```cpp
void StartProcessing()
```

Starts the processing service on the configured processing grid channel. 

### function GetCoinprice

```cpp
outcome::result< std::map< std::string, double > > GetCoinprice(
    const std::vector< std::string > & tokenIds
)
```

Retrieves current USD prices for token identifiers, using a short local cache. 

**Parameters**: 

  * **tokenIds** CoinGecko token identifiers to price. 


**Return**: Map from token identifier to current USD price, or a price-retrieval error. 

### function GetCoinPriceByDate

```cpp
outcome::result< std::map< std::string, std::map< int64_t, double > > > GetCoinPriceByDate(
    const std::vector< std::string > & tokenIds,
    const std::vector< int64_t > & timestamps
)
```

Retrieves historical USD prices for token identifiers at exact timestamps. 

**Parameters**: 

  * **tokenIds** CoinGecko token identifiers to price. 
  * **timestamps** Unix timestamps to query. 


**Return**: Nested map from token identifier to timestamp to USD price. 

### function GetCoinPricesByDateRange

```cpp
outcome::result< std::map< std::string, std::map< int64_t, double > > > GetCoinPricesByDateRange(
    const std::vector< std::string > & tokenIds,
    int64_t from,
    int64_t to
)
```

Retrieves historical USD prices for token identifiers over a date range. 

**Parameters**: 

  * **tokenIds** CoinGecko token identifiers to price. 
  * **from** Start Unix timestamp for the range. 
  * **to** End Unix timestamp for the range. 


**Return**: Nested map from token identifier to timestamp to USD price. 

### function WaitForTransactionIncoming

```cpp
TransactionManager::TransactionStatus WaitForTransactionIncoming(
    const std::string & txId,
    std::chrono::milliseconds timeout
)
```

Waits for an incoming transaction to be processed. 

**Parameters**: 

  * **txId** Transaction hash to wait for. 
  * **timeout** Maximum time to wait. 


**Return**: Incoming transaction status, or INVALID when transactions are not ready. 

### function WaitForTransactionOutgoing

```cpp
TransactionManager::TransactionStatus WaitForTransactionOutgoing(
    const std::string & txId,
    std::chrono::milliseconds timeout
)
```

Waits for an outgoing transaction to be processed. 

**Parameters**: 

  * **txId** Transaction hash to wait for. 
  * **timeout** Maximum time to wait. 


**Return**: Outgoing transaction status, or INVALID when transactions are not ready. 

### function WaitForEscrowRelease

```cpp
TransactionManager::TransactionStatus WaitForEscrowRelease(
    const std::string & originalEscrowId,
    std::chrono::milliseconds timeout
)
```

Waits for an escrow release transaction tied to an escrow hold. 

**Parameters**: 

  * **originalEscrowId** Hash of the original escrow hold transaction. 
  * **timeout** Maximum time to wait. 


**Return**: Escrow release transaction status, or INVALID when transactions are not ready. 

### function GetTransactionManagerState

```cpp
TransactionManager::State GetTransactionManagerState() const
```

Returns the current transaction manager lifecycle state. 

**Return**: Transaction manager state, or CREATING when the manager is not available. 

### function ConfigureRpcEndpoint

```cpp
void ConfigureRpcEndpoint(
    const std::string & chain_id,
    std::vector< WeightedRpcEndpoint > endpoints
)
```

Configures RPC endpoints for a specific EVM chain on the public-chain input validator. 

**Parameters**: 

  * **chain_id** Numeric EVM chain ID as a string (e.g. "11155111" for Sepolia). 
  * **endpoints** Vector of weighted RPC endpoints for the chain. 


Allows callers (including E2E tests) to register RPC endpoints for chains that are not in the default mainnet set (e.g. Sepolia testnet). The transaction manager must be in READY state.


### function GetTransactionStatus

```cpp
TransactionManager::TransactionStatus GetTransactionStatus(
    const std::string & txId
) const
```

Returns a tracked transaction status by transaction hash. 

**Parameters**: 

  * **txId** Transaction hash to look up. 


**Return**: Outgoing status when present, then incoming status, or INVALID when unknown/not ready. 

### function SetAuthorizedFullNodeAddress

```cpp
void SetAuthorizedFullNodeAddress(
    const std::string & pub_address
)
```

Sets the authorized full-node address for blockchain genesis verification. 

**Parameters**: 

  * **pub_address** Public address authorized to create genesis blocks. 


### function GetAuthorizedFullNodeAddress

```cpp
const std::string & GetAuthorizedFullNodeAddress() const
```

Gets the current authorized full-node public address. 

**Return**: Public address authorized to create genesis blocks. 

### function GetState

```cpp
inline NodeState GetState() const
```

Returns the current [GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/) lifecycle state. 

**Return**: Current node state. 

## Protected Functions Documentation

### function SendTransactionAndProof

```cpp
void SendTransactionAndProof(
    std::shared_ptr< GeniusTransaction > tx,
    std::vector< uint8_t > proof
)
```

Enqueues a transaction and its proof directly through the transaction manager. 

**Parameters**: 

  * **tx** Transaction to enqueue. 
  * **proof** Serialized proof bytes associated with `tx`. 


### function ConfigureTransactionFilterTimeoutsMs

```cpp
void ConfigureTransactionFilterTimeoutsMs(
    uint64_t timeframe_limit_ms,
    uint64_t mutability_window_ms
)
```

Configures transaction filtering time windows for tests. 

**Parameters**: 

  * **timeframe_limit_ms** Timestamp tolerance in milliseconds. 
  * **mutability_window_ms** Mutability window in milliseconds. 


## Public Attributes Documentation

### variable TIMEOUT_ESCROW_PAY

```cpp
static std::chrono::milliseconds TIMEOUT_ESCROW_PAY { 30000 };
```

Escrow payout timeout. 

### variable TIMEOUT_TRANSFER

```cpp
static std::chrono::milliseconds TIMEOUT_TRANSFER { 30000 };
```

Transfer timeout. 

### variable TIMEOUT_MINT

```cpp
static std::chrono::milliseconds TIMEOUT_MINT { 30000 };
```

Mint timeout. 

## Protected Attributes Documentation

### variable write_base_path_

```cpp
std::string write_base_path_;
```

Base path for node databases, logs, and account storage. 

### variable account_

```cpp
std::shared_ptr< GeniusAccount > account_;
```

Active account used by node services. 

## Friends

### friend TransactionSyncTest

```cpp
friend class TransactionSyncTest(
    TransactionSyncTest 
);
```


### friend MultiAccountTestAccess

```cpp
friend class MultiAccountTestAccess(
    MultiAccountTestAccess 
);
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
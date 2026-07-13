---
title: sgns::TransactionManager
summary: Coordinates transaction creation, CRDT propagation, verification, and status tracking. 

---

# sgns::TransactionManager



Coordinates transaction creation, CRDT propagation, verification, and status tracking. 


`#include <TransactionManager.hpp>`

Inherits from std::enable_shared_from_this< TransactionManager >

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class uint8_t | **[State](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-state)** { CREATING = 0, INITIALIZING, SYNCING, READY}<br/>[State](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-state) of the Transaction Manager.  |
| enum class uint8_t | **[TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus)** { CREATED, SENDING, CONFIRMED, VERIFYING, UNCONFIRMED, FAILED, INVALID}<br/>Status of a transaction.  |
| enum class uint8_t | **[WitnessValidationResult](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-witnessvalidationresult)** { VALID, DRIFT, INVALID} |
| using std::pair< std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) >, std::optional< std::vector< uint8_t > > > | **[TransactionPair](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#using-transactionpair)**  |
| using std::vector< [TransactionPair](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#using-transactionpair) > | **[TransactionBatch](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#using-transactionbatch)**  |
| using std::pair< [TransactionBatch](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#using-transactionbatch), std::optional< std::shared_ptr< [crdt::AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/) > > > | **[TransactionItem](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#using-transactionitem)**  |
| using std::function< void(const [State](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-state) &previous, const [State](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-state) &current)> | **[StateChangeCallback](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#using-statechangecallback)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [TransactionManager](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-transactionmanager) > | **[New](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-new)**(std::shared_ptr< [crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) > processing_db, std::shared_ptr< boost::asio::io_context > ctx, std::shared_ptr< [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/) > account, std::shared_ptr< [crypto::Hasher](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/) > hasher, std::shared_ptr< [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) > blockchain, bool full_node =false, uint16_t subnet_id =0, std::chrono::milliseconds timestamp_tolerance =std::chrono::milliseconds(300000), std::chrono::milliseconds mutability_window =std::chrono::milliseconds(0))<br/>Factory constructor of the [TransactionManager](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/).  |
| std::string | **[GetTransactionPath](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-gettransactionpath)**(uint16_t base, const std::string & tx_hash) |
| std::string | **[GetTransactionPath](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-gettransactionpath)**(const [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) & element) |
| std::string | **[GetTransactionPath](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-gettransactionpath)**(const std::string & tx_hash) |
| std::string | **[GetTransactionProofPath](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-gettransactionproofpath)**(const [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) & element) |
| outcome::result< std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > > | **[FetchTransaction](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-fetchtransaction)**(const std::shared_ptr< [crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) > & db, std::string_view transaction_key)<br/>Fetches and deserializes a transaction from the CRDT by key.  |
| outcome::result< std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > > | **[DeSerializeTransaction](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-deserializetransaction)**(const [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) & tx_data) |
| std::string | **[StateToString](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-statetostring)**([State](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-state) state) |
| std::string | **[GetBlockChainBase](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getblockchainbase)**(uint16_t network_id)<br/>Builds the blockchain key prefix "/bc-<network_id>/" for the given network.  |
| std::string | **[GetBlockChainBase](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getblockchainbase)**()<br/>Overload using the current network ID.  |
| outcome::result< std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > > | **[DeSerializeTransaction](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-deserializetransaction)**(std::string tx_data) |
| outcome::result< std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > > | **[DeSerializeEmbeddedTransaction](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-deserializeembeddedtransaction)**(const EmbeddedTransaction & embedded)<br/>Deserializes from EmbeddedTransaction proto oneof field. Dispatches on the oneof case instead of manual type string lookup.  |
| | **[~TransactionManager](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-~transactionmanager)**() |
| void | **[Start](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-start)**() |
| void | **[RegisterTopicNames](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-registertopicnames)**() |
| void | **[StartListeningTopics](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-startlisteningtopics)**() |
| void | **[StartCore](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-startcore)**() |
| void | **[PrintAccountInfo](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-printaccountinfo)**() const |
| std::vector< std::vector< uint8_t > > | **[GetOutTransactions](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getouttransactions)**() const |
| std::vector< std::vector< uint8_t > > | **[GetInTransactions](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getintransactions)**() const |
| std::vector< std::vector< uint8_t > > | **[GetTransactions](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-gettransactions)**(std::optional< [TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) > tx_status =std::nullopt) const |
| std::vector< std::vector< uint8_t > > | **[GetTransactions](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-gettransactions)**() const |
| outcome::result< std::string > | **[TransferFunds](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-transferfunds)**(uint64_t amount, std::string destination, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id)<br/>Creates and enqueues a transfer transaction.  |
| outcome::result< std::string > | **[MintFunds](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-mintfunds)**(uint64_t amount, std::string transaction_hash, std::string chainid, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) tokenid, std::string destination ="")<br/>Creates and enqueues a mint transaction.  |
| outcome::result< std::string > | **[MigrationFunds](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-migrationfunds)**(uint64_t amount, std::string from_version, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) tokenid, std::string destination ="")<br/>Creates and enqueues a one-time migration mint transaction.  |
| outcome::result< std::pair< std::string, [EscrowDataPair](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-escrowdatapair) > > | **[HoldEscrow](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-holdescrow)**(uint64_t amount, const std::string & dev_addr, uint64_t peers_cut, const std::string & job_id)<br/>Creates and enqueues an escrow-hold transaction.  |
| outcome::result< std::string > | **[PayEscrow](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-payescrow)**(const std::string & escrow_path, const SGProcessing::TaskResult & task_result, std::shared_ptr< [crdt::AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/) > crdt_transaction) |
| [TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) | **[WaitForTransactionIncoming](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-waitfortransactionincoming)**(const std::string & txId, std::chrono::milliseconds timeout) const |
| [TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) | **[WaitForTransactionOutgoing](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-waitfortransactionoutgoing)**(const std::string & txId, std::chrono::milliseconds timeout) const |
| [TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) | **[WaitForEscrowRelease](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-waitforescrowrelease)**(const std::string & originalEscrowId, std::chrono::milliseconds timeout) const<br/>Polls until an EscrowReleaseTransaction referencing `originalEscrowId` reaches a terminal state or `timeout` expires.  |
| [State](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-state) | **[GetState](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getstate)**() const |
| [TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) | **[GetOutgoingStatusByTxId](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getoutgoingstatusbytxid)**(const std::string & txId) const |
| [TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) | **[GetIncomingStatusByTxId](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getincomingstatusbytxid)**(const std::string & txId) const |
| outcome::result< std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > > | **[GetConflictingTransaction](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getconflictingtransaction)**(const [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) & element) const<br/>Finds a tracked transaction that shares the same nonce and source address as `element`.  |
| void | **[Stop](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-stop)**()<br/>Idempotent stop. Sets the stopped flag and wakes the tick loop.  |
| void | **[RegisterStateChangeCallback](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-registerstatechangecallback)**([StateChangeCallback](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#using-statechangecallback) callback) |
| void | **[UnregisterStateChangeCallback](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-unregisterstatechangecallback)**() |
| outcome::result< void > | **[QueryTransactions](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-querytransactions)**()<br/>Queries all transaction keys from the CRDT across monitored networks and processes each one via FetchAndProcessTransaction.  |
| outcome::result< void > | **[FetchAndProcessTransaction](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-fetchandprocesstransaction)**(const std::string & tx_key, std::optional< [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) > tx_data =std::nullopt)<br/>Deserializes, parses, and adds a single transaction to the processed map.  |
| outcome::result< std::string > | **[GetTransactionCID](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-gettransactioncid)**(const std::string & tx_hash) const<br/>Looks up the CID associated with a transaction hash in RocksDB, searching across all monitored networks.  |
| outcome::result< [ConsensusManager::ValidationResult](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/) > | **[HandleNonceConsensusSubject](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-handlenonceconsensussubject)**(const [ConsensusManager::Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) & subject) |
| [ConsensusManager::ValidationResult](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/) | **[ValidateTransactionForConsensus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-validatetransactionforconsensus)**(const std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > & tx) const |
| bool | **[CheckTransactionWellFormed](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-checktransactionwellformed)**(const [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) & tx) const |
| bool | **[CheckTransactionAuthorization](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-checktransactionauthorization)**(const [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) & tx) const |
| bool | **[CheckTransactionTimestamp](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-checktransactiontimestamp)**(const [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) & tx) const |
| bool | **[CheckTransactionReplayProtection](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-checktransactionreplayprotection)**(const [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) & tx) const |
| [ReplayProtectionResult](/source-reference/Classes/d5/da9/structsgns_1_1_transaction_manager_1_1_replay_protection_result/) | **[EvaluateTransactionReplayProtection](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-evaluatetransactionreplayprotection)**(const [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) & tx) const |
| bool | **[CheckTransactionTypeRules](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-checktransactiontyperules)**(const std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > & tx) const |
| std::optional< UTXOTransitionCommitment > | **[BuildUTXOTransitionCommitment](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-buildutxotransitioncommitment)**(const std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > & tx) const |
| std::optional< UTXOWitness > | **[BuildUTXOWitness](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-buildutxowitness)**(const std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > & tx) const |
| bool | **[ApplyTransactionToUTXOSnapshot](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-applytransactiontoutxosnapshot)**(const std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > & tx, std::vector< [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) > & snapshot) const |
| [WitnessValidationResult](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-witnessvalidationresult) | **[ValidateWitnessForConsensus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-validatewitnessforconsensus)**(const ConsensusSubject & subject, const std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > & tx) const |
| bool | **[ValidateUTXOParametersForConsensus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-validateutxoparametersforconsensus)**(const [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) & params, const std::string & address) const |
| void | **[SetNonceWindow](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-setnoncewindow)**(uint64_t window) |
| outcome::result< void > | **[ChangeTransactionState](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-changetransactionstate)**(const std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > & tx, [TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) new_status) |
| bool | **[HasConfirmedInputConflict](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-hasconfirmedinputconflict)**(const std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > & candidate_tx) const |
| bool | **[KeyExistsInDB](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-keyexistsindb)**(const std::string & key) const |
| [PublicChainInputValidator](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/) & | **[GetPublicChainInputValidator](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getpublicchaininputvalidator)**()<br/>Obtains the public-chain input validator for RPC endpoint wiring.  |
| const [PublicChainInputValidator](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/) & | **[GetPublicChainInputValidator](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getpublicchaininputvalidator)**() const<br/>Obtains the public-chain input validator for RPC endpoint wiring (const).  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[EnqueueTransaction](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-enqueuetransaction)**([TransactionPair](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#using-transactionpair) element) |
| void | **[EnqueueTransaction](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-enqueuetransaction)**([TransactionItem](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#using-transactionitem) element) |
| void | **[SetTimeFrameToleranceMs](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-settimeframetolerancems)**(uint64_t timeframe_tolerance) |
| void | **[SetMutabilityWindowMs](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-setmutabilitywindowms)**(uint64_t mutability_window) |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::string_view | **[GNUS_FULL_NODES_TOPIC](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#variable-gnus_full_nodes_topic)**  |
| std::string_view | **[GNUS_FULL_NODES_TOPIC_LEGACY](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#variable-gnus_full_nodes_topic_legacy)**  |
| uint64_t | **[NONCE_REQUEST_TIMEOUT_MS](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#variable-nonce_request_timeout_ms)** <br/>Unified timeout for all nonce requests (10 seconds).  |

## Friends

|                | Name           |
| -------------- | -------------- |
| class | **[GeniusNode](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#friend-geniusnode)**  |
| class | **[Migration3_6_0To3_7_0](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#friend-migration3_6_0to3_7_0)**  |
| class | **[CertificateFallbackTestAccess](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#friend-certificatefallbacktestaccess)**  |
| class | **[TransactionManagerPendingLifecycleTestAccess](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#friend-transactionmanagerpendinglifecycletestaccess)**  |

## Public Types Documentation

### enum State

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| CREATING | 0| Creating the object.   |
| INITIALIZING | | Initializing the object.   |
| SYNCING | | Syncing the transactions.   |
| READY | | Ready to process transactions.   |



[State](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-state) of the Transaction Manager. 

### enum TransactionStatus

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| CREATED | | Transaction created but not yet sent.   |
| SENDING | | Transaction is being sent.   |
| CONFIRMED | | Transaction confirmed.   |
| VERIFYING | | Transaction being verified.   |
| UNCONFIRMED | | Local outgoing transaction expired inconclusively.   |
| FAILED | | Transaction failed.   |
| INVALID | | Invalid transaction.   |



Status of a transaction. 

### enum WitnessValidationResult

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| VALID | |   |
| DRIFT | |   |
| INVALID | |   |




### using TransactionPair

```cpp
using sgns::TransactionManager::TransactionPair = std::pair<std::shared_ptr<GeniusTransaction>, std::optional<std::vector<uint8_t>>>;
```


### using TransactionBatch

```cpp
using sgns::TransactionManager::TransactionBatch = std::vector<TransactionPair>;
```


### using TransactionItem

```cpp
using sgns::TransactionManager::TransactionItem = std::pair<TransactionBatch, std::optional<std::shared_ptr<crdt::AtomicTransaction>>>;
```


### using StateChangeCallback

```cpp
using sgns::TransactionManager::StateChangeCallback = std::function<void( const State &previous, const State &current )>;
```


## Public Functions Documentation

### function New

```cpp
static std::shared_ptr< TransactionManager > New(
    std::shared_ptr< crdt::GlobalDB > processing_db,
    std::shared_ptr< boost::asio::io_context > ctx,
    std::shared_ptr< GeniusAccount > account,
    std::shared_ptr< crypto::Hasher > hasher,
    std::shared_ptr< Blockchain > blockchain,
    bool full_node =false,
    uint16_t subnet_id =0,
    std::chrono::milliseconds timestamp_tolerance =std::chrono::milliseconds(300000),
    std::chrono::milliseconds mutability_window =std::chrono::milliseconds(0)
)
```

Factory constructor of the [TransactionManager](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/). 

**Parameters**: 

  * **processing_db** Database of the CRDT 
  * **ctx** The io context used to run its inner methods 
  * **account** Genius account to be used 
  * **hasher** Hasher to be used 
  * **full_node** Parameter to indicate if the account is a full node 
  * **timestamp_tolerance** Time to analyze a transaction with the same nonce/key 
  * **mutability_window** Window of time where a transaction can be modified 


**Return**: shared_ptr to the fully-wired [TransactionManager](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/) instance 

**Note**: 

  * Default timestamp_tolerance is 5 minutes (300000 ms) 
  * Default mutability_window is 10 minutes (600000 ms) 
  * timestamp_tolerance must be smaller than mutability_window 


### function GetTransactionPath

```cpp
static std::string GetTransactionPath(
    uint16_t base,
    const std::string & tx_hash
)
```


### function GetTransactionPath

```cpp
static std::string GetTransactionPath(
    const GeniusTransaction & element
)
```


### function GetTransactionPath

```cpp
static std::string GetTransactionPath(
    const std::string & tx_hash
)
```


### function GetTransactionProofPath

```cpp
static std::string GetTransactionProofPath(
    const GeniusTransaction & element
)
```


### function FetchTransaction

```cpp
static outcome::result< std::shared_ptr< GeniusTransaction > > FetchTransaction(
    const std::shared_ptr< crdt::GlobalDB > & db,
    std::string_view transaction_key
)
```

Fetches and deserializes a transaction from the CRDT by key. 

### function DeSerializeTransaction

```cpp
static outcome::result< std::shared_ptr< GeniusTransaction > > DeSerializeTransaction(
    const base::Buffer & tx_data
)
```


### function StateToString

```cpp
static inline std::string StateToString(
    State state
)
```


### function GetBlockChainBase

```cpp
static std::string GetBlockChainBase(
    uint16_t network_id
)
```

Builds the blockchain key prefix "/bc-<network_id>/" for the given network. 

### function GetBlockChainBase

```cpp
static std::string GetBlockChainBase()
```

Overload using the current network ID. 

### function DeSerializeTransaction

```cpp
static outcome::result< std::shared_ptr< GeniusTransaction > > DeSerializeTransaction(
    std::string tx_data
)
```


### function DeSerializeEmbeddedTransaction

```cpp
static outcome::result< std::shared_ptr< GeniusTransaction > > DeSerializeEmbeddedTransaction(
    const EmbeddedTransaction & embedded
)
```

Deserializes from EmbeddedTransaction proto oneof field. Dispatches on the oneof case instead of manual type string lookup. 

### function ~TransactionManager

```cpp
~TransactionManager()
```


### function Start

```cpp
void Start()
```


### function RegisterTopicNames

```cpp
void RegisterTopicNames()
```


### function StartListeningTopics

```cpp
void StartListeningTopics()
```


### function StartCore

```cpp
void StartCore()
```


### function PrintAccountInfo

```cpp
void PrintAccountInfo() const
```


### function GetOutTransactions

```cpp
std::vector< std::vector< uint8_t > > GetOutTransactions() const
```


### function GetInTransactions

```cpp
std::vector< std::vector< uint8_t > > GetInTransactions() const
```


### function GetTransactions

```cpp
std::vector< std::vector< uint8_t > > GetTransactions(
    std::optional< TransactionStatus > tx_status =std::nullopt
) const
```


### function GetTransactions

```cpp
std::vector< std::vector< uint8_t > > GetTransactions() const
```


### function TransferFunds

```cpp
outcome::result< std::string > TransferFunds(
    uint64_t amount,
    std::string destination,
    TokenID token_id
)
```

Creates and enqueues a transfer transaction. 

**Parameters**: 

  * **amount** Amount to transfer. 
  * **destination** Recipient address. 
  * **token_id** Token being transferred. 


**Return**: Transaction hash on success. 

### function MintFunds

```cpp
outcome::result< std::string > MintFunds(
    uint64_t amount,
    std::string transaction_hash,
    std::string chainid,
    TokenID tokenid,
    std::string destination =""
)
```

Creates and enqueues a mint transaction. 

**Parameters**: 

  * **amount** Amount to mint. 
  * **transaction_hash** Source-chain transaction hash used as the previous hash in the DAG. 
  * **chainid** Originating chain identifier. 
  * **tokenid** Token to mint. 
  * **destination** Recipient address; defaults to the local account address when empty. 


**Return**: Transaction hash on success. 

### function MigrationFunds

```cpp
outcome::result< std::string > MigrationFunds(
    uint64_t amount,
    std::string from_version,
    TokenID tokenid,
    std::string destination =""
)
```

Creates and enqueues a one-time migration mint transaction. 

**Parameters**: 

  * **amount** Amount to migrate. 
  * **from_version** Legacy version namespace for the migration source key. 
  * **tokenid** Token to mint. 
  * **destination** Recipient address; defaults to the local account address when empty. 


**Return**: Transaction hash on success. 

### function HoldEscrow

```cpp
outcome::result< std::pair< std::string, EscrowDataPair > > HoldEscrow(
    uint64_t amount,
    const std::string & dev_addr,
    uint64_t peers_cut,
    const std::string & job_id
)
```

Creates and enqueues an escrow-hold transaction. 

**Parameters**: 

  * **amount** Total amount to lock in escrow. 
  * **dev_addr** Developer address that receives the remainder after peer payouts. 
  * **peers_cut** Multiplier (as a [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/)) applied to the escrow amount to calculate the per-peer share. 
  * **job_id** Job identifier whose blake2b-256 hash becomes the escrow destination address. 


**Return**: Pair of (transaction hash, (escrow address, serialized transaction)) on success. 

Hashes `job_id` with blake2b-256 to derive the escrow destination address, selects UTXOs, reserves them, and signs the transaction.


### function PayEscrow

```cpp
outcome::result< std::string > PayEscrow(
    const std::string & escrow_path,
    const SGProcessing::TaskResult & task_result,
    std::shared_ptr< crdt::AtomicTransaction > crdt_transaction
)
```


### function WaitForTransactionIncoming

```cpp
TransactionStatus WaitForTransactionIncoming(
    const std::string & txId,
    std::chrono::milliseconds timeout
) const
```


### function WaitForTransactionOutgoing

```cpp
TransactionStatus WaitForTransactionOutgoing(
    const std::string & txId,
    std::chrono::milliseconds timeout
) const
```


### function WaitForEscrowRelease

```cpp
TransactionStatus WaitForEscrowRelease(
    const std::string & originalEscrowId,
    std::chrono::milliseconds timeout
) const
```

Polls until an EscrowReleaseTransaction referencing `originalEscrowId` reaches a terminal state or `timeout` expires. 

**Return**: [TransactionStatus](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#enum-transactionstatus) of the release tx, or INVALID if not found within timeout. 

### function GetState

```cpp
inline State GetState() const
```


### function GetOutgoingStatusByTxId

```cpp
TransactionStatus GetOutgoingStatusByTxId(
    const std::string & txId
) const
```


### function GetIncomingStatusByTxId

```cpp
TransactionStatus GetIncomingStatusByTxId(
    const std::string & txId
) const
```


### function GetConflictingTransaction

```cpp
outcome::result< std::shared_ptr< GeniusTransaction > > GetConflictingTransaction(
    const GeniusTransaction & element
) const
```

Finds a tracked transaction that shares the same nonce and source address as `element`. 

**Return**: The conflicting transaction, or failure if none exists. 

### function Stop

```cpp
void Stop()
```

Idempotent stop. Sets the stopped flag and wakes the tick loop. 

### function RegisterStateChangeCallback

```cpp
void RegisterStateChangeCallback(
    StateChangeCallback callback
)
```


### function UnregisterStateChangeCallback

```cpp
void UnregisterStateChangeCallback()
```


### function QueryTransactions

```cpp
outcome::result< void > QueryTransactions()
```

Queries all transaction keys from the CRDT across monitored networks and processes each one via FetchAndProcessTransaction. 

### function FetchAndProcessTransaction

```cpp
outcome::result< void > FetchAndProcessTransaction(
    const std::string & tx_key,
    std::optional< base::Buffer > tx_data =std::nullopt
)
```

Deserializes, parses, and adds a single transaction to the processed map. 

**Parameters**: 

  * **tx_key** Full CRDT key of the transaction. 
  * **tx_data** Optional pre-fetched serialized data (avoids a CRDT read). 


Skips transactions that are already tracked. When `tx_data` is provided it is deserialized directly; otherwise the transaction is fetched from the CRDT by `tx_key`. On success the peer nonce is updated and the transaction is recorded as CONFIRMED.


### function GetTransactionCID

```cpp
outcome::result< std::string > GetTransactionCID(
    const std::string & tx_hash
) const
```

Looks up the CID associated with a transaction hash in RocksDB, searching across all monitored networks. 

### function HandleNonceConsensusSubject

```cpp
outcome::result< ConsensusManager::ValidationResult > HandleNonceConsensusSubject(
    const ConsensusManager::Subject & subject
)
```


### function ValidateTransactionForConsensus

```cpp
ConsensusManager::ValidationResult ValidateTransactionForConsensus(
    const std::shared_ptr< GeniusTransaction > & tx
) const
```


### function CheckTransactionWellFormed

```cpp
bool CheckTransactionWellFormed(
    const GeniusTransaction & tx
) const
```


### function CheckTransactionAuthorization

```cpp
bool CheckTransactionAuthorization(
    const GeniusTransaction & tx
) const
```


### function CheckTransactionTimestamp

```cpp
bool CheckTransactionTimestamp(
    const GeniusTransaction & tx
) const
```


### function CheckTransactionReplayProtection

```cpp
bool CheckTransactionReplayProtection(
    const GeniusTransaction & tx
) const
```


### function EvaluateTransactionReplayProtection

```cpp
ReplayProtectionResult EvaluateTransactionReplayProtection(
    const GeniusTransaction & tx
) const
```


### function CheckTransactionTypeRules

```cpp
bool CheckTransactionTypeRules(
    const std::shared_ptr< GeniusTransaction > & tx
) const
```


### function BuildUTXOTransitionCommitment

```cpp
std::optional< UTXOTransitionCommitment > BuildUTXOTransitionCommitment(
    const std::shared_ptr< GeniusTransaction > & tx
) const
```


### function BuildUTXOWitness

```cpp
std::optional< UTXOWitness > BuildUTXOWitness(
    const std::shared_ptr< GeniusTransaction > & tx
) const
```


### function ApplyTransactionToUTXOSnapshot

```cpp
bool ApplyTransactionToUTXOSnapshot(
    const std::shared_ptr< GeniusTransaction > & tx,
    std::vector< GeniusUTXO > & snapshot
) const
```


### function ValidateWitnessForConsensus

```cpp
WitnessValidationResult ValidateWitnessForConsensus(
    const ConsensusSubject & subject,
    const std::shared_ptr< GeniusTransaction > & tx
) const
```


### function ValidateUTXOParametersForConsensus

```cpp
bool ValidateUTXOParametersForConsensus(
    const UTXOTxParameters & params,
    const std::string & address
) const
```


### function SetNonceWindow

```cpp
void SetNonceWindow(
    uint64_t window
)
```


### function ChangeTransactionState

```cpp
outcome::result< void > ChangeTransactionState(
    const std::shared_ptr< GeniusTransaction > & tx,
    TransactionStatus new_status
)
```


### function HasConfirmedInputConflict

```cpp
bool HasConfirmedInputConflict(
    const std::shared_ptr< GeniusTransaction > & candidate_tx
) const
```


### function KeyExistsInDB

```cpp
bool KeyExistsInDB(
    const std::string & key
) const
```


### function GetPublicChainInputValidator

```cpp
inline PublicChainInputValidator & GetPublicChainInputValidator()
```

Obtains the public-chain input validator for RPC endpoint wiring. 

**Return**: Mutable reference to the [PublicChainInputValidator](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/). 

### function GetPublicChainInputValidator

```cpp
inline const PublicChainInputValidator & GetPublicChainInputValidator() const
```

Obtains the public-chain input validator for RPC endpoint wiring (const). 

**Return**: Const reference to the [PublicChainInputValidator](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/). 

## Protected Functions Documentation

### function EnqueueTransaction

```cpp
void EnqueueTransaction(
    TransactionPair element
)
```


### function EnqueueTransaction

```cpp
void EnqueueTransaction(
    TransactionItem element
)
```


### function SetTimeFrameToleranceMs

```cpp
void SetTimeFrameToleranceMs(
    uint64_t timeframe_tolerance
)
```


### function SetMutabilityWindowMs

```cpp
void SetMutabilityWindowMs(
    uint64_t mutability_window
)
```


## Public Attributes Documentation

### variable GNUS_FULL_NODES_TOPIC

```cpp
static std::string_view GNUS_FULL_NODES_TOPIC = "SuperGNUSNode.TestNet.FullNode";
```


### variable GNUS_FULL_NODES_TOPIC_LEGACY

```cpp
static std::string_view GNUS_FULL_NODES_TOPIC_LEGACY = "SuperGNUSNode.TestNet.FullNode.963";
```


### variable NONCE_REQUEST_TIMEOUT_MS

```cpp
static uint64_t NONCE_REQUEST_TIMEOUT_MS                                                        =
5000;
```

Unified timeout for all nonce requests (10 seconds). 

## Friends

### friend GeniusNode

```cpp
friend class GeniusNode(
    GeniusNode 
);
```


### friend Migration3_6_0To3_7_0

```cpp
friend class Migration3_6_0To3_7_0(
    Migration3_6_0To3_7_0 
);
```


### friend CertificateFallbackTestAccess

```cpp
friend class CertificateFallbackTestAccess(
    CertificateFallbackTestAccess 
);
```


### friend TransactionManagerPendingLifecycleTestAccess

```cpp
friend class TransactionManagerPendingLifecycleTestAccess(
    TransactionManagerPendingLifecycleTestAccess 
);
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
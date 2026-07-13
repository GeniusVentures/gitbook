---
title: sgns::Blockchain
summary: Manages genesis/account-creation blocks and consensus integration. 

---

# sgns::Blockchain



Manages genesis/account-creation blocks and consensus integration.  [More...](#detailed-description)


`#include <Blockchain.hpp>`

Inherits from std::enable_shared_from_this< Blockchain >

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[Error](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#enum-error)** { GENESIS_BLOCK_CREATION_FAILED = 0, GENESIS_BLOCK_INVALID_SIGNATURE, GENESIS_BLOCK_UNAUTHORIZED_CREATOR, GENESIS_BLOCK_SERIALIZATION_FAILED, GENESIS_BLOCK_MISSING, ACCOUNT_CREATION_BLOCK_MISSING, ACCOUNT_CREATION_BLOCK_CREATION_FAILED, ACCOUNT_CREATION_BLOCK_INVALID_SIGNATURE, ACCOUNT_CREATION_BLOCK_SERIALIZATION_FAILED, ACCOUNT_CREATION_BLOCK_INVALID_GENESIS_LINK, VALIDATOR_REGISTRY_CREATION_FAILED, BLOCKCHAIN_NOT_INITIALIZED}<br/>[Error](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#enum-error) class of the [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) module.  |
| using std::function< void(outcome::result< void >)> | **[BlockchainCallback](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#using-blockchaincallback)** <br/>Callback invoked when blockchain initialization/processing finishes.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-blockchain) > | **[New](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-new)**(std::shared_ptr< [crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) > global_db, std::shared_ptr< [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/) > account, std::shared_ptr< ipfs_pubsub::GossipPubSub > pubsub, [BlockchainCallback](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#using-blockchaincallback) callback)<br/>Factory method to create [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) as shared_ptr.  |
| void | **[SetAuthorizedFullNodeAddress](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-setauthorizedfullnodeaddress)**(const std::string & pub_address)<br/>Set the authorized full node public address (for testing purposes).  |
| const std::string & | **[GetAuthorizedFullNodeAddress](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-getauthorizedfullnodeaddress)**()<br/>Get the current authorized full node public address.  |
| | **[~Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-~blockchain)**()<br/>Destroys the blockchain instance.  |
| outcome::result< void > | **[Start](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-start)**()<br/>Start the blockchain with async genesis block handling.  |
| outcome::result< void > | **[Stop](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-stop)**()<br/>Stops blockchain background processing and callbacks.  |
| outcome::result< void > | **[OnGenesisBlockReceived](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-ongenesisblockreceived)**(const [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) & serialized_genesis)<br/>Handle received genesis block from pubsub.  |
| outcome::result< void > | **[OnAccountCreationBlockReceived](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-onaccountcreationblockreceived)**(const [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) & serialized_account_creation)<br/>Handle received account creation block from pubsub.  |
| outcome::result< std::string > | **[GetGenesisCID](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-getgenesiscid)**() const<br/>Returns the stored CID of the selected genesis block.  |
| outcome::result< std::string > | **[GetAccountCreationCID](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-getaccountcreationcid)**() const<br/>Returns the stored CID of the selected account-creation block.  |
| std::shared_ptr< [ValidatorRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/) > | **[GetValidatorRegistry](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-getvalidatorregistry)**() const<br/>Returns validator registry owned by this blockchain instance.  |
| void | **[SetFullNodeMode](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-setfullnodemode)**()<br/>Forces full-node mode behavior for bootstrap/generation flow.  |
| bool | **[RegisterSubjectHandler](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-registersubjecthandler)**(std::string_view subject_type, [ConsensusManager::SubjectHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subjecthandler) handler)<br/>Registers a consensus subject handler by canonical subject type string.  |
| void | **[UnregisterSubjectHandler](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-unregistersubjecthandler)**(std::string_view subject_type)<br/>Unregisters a consensus subject handler by canonical subject type string.  |
| bool | **[RegisterCertificateHandler](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-registercertificatehandler)**(std::string_view subject_type, [ConsensusManager::CertificateSubjectHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificatesubjecthandler) handler)<br/>Registers a consensus certificate handler by canonical subject type string.  |
| void | **[UnregisterCertificateHandler](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-unregistercertificatehandler)**(std::string_view subject_type)<br/>Unregisters a consensus certificate handler by canonical subject type string.  |
| bool | **[RegisterProposalCleanupHandler](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-registerproposalcleanuphandler)**(std::string_view subject_type, [ConsensusManager::ProposalCleanupHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposalcleanuphandler) handler)<br/>Registers a proposal cleanup callback by canonical subject type string.  |
| void | **[RegisterSlotKeyHandler](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-registerslotkeyhandler)**(std::string_view subject_type, [ConsensusManager::SlotKeyHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-slotkeyhandler) handler)<br/>Registers a slot key handler for a specific embedded transaction oneof case.  |
| void | **[SetSlotHashPopulator](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-setslothashpopulator)**([ConsensusManager::SlotHashPopulator](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-slothashpopulator) populator)<br/>Forwards a slot-hash populator to the consensus manager (Phase 6, D-01).  |
| void | **[UnregisterSlotKeyHandler](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-unregisterslotkeyhandler)**(std::string_view subject_type) |
| outcome::result< [ConsensusManager::Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) > | **[CreateConsensusNonceSubject](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-createconsensusnoncesubject)**(const std::string & account_id, uint64_t nonce, const std::string & tx_hash, const EmbeddedTransaction & transaction, const std::optional< UTXOTransitionCommitment > & utxo_commitment, const std::optional< UTXOWitness > & utxo_witness)<br/>Creates a consensus subject for nonce/transaction transition.  |
| outcome::result< [ConsensusManager::Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) > | **[CreateConsensusProposal](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-createconsensusproposal)**(const std::string & account_id, uint64_t nonce, const std::string & tx_hash, const EmbeddedTransaction & transaction, const std::optional< UTXOTransitionCommitment > & utxo_commitment, const std::optional< UTXOWitness > & utxo_witness)<br/>Creates a signed proposal for nonce/transaction transition.  |
| outcome::result< void > | **[SubmitProposal](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-submitproposal)**(const [ConsensusManager::Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) & proposal)<br/>Submits a proposal through consensus manager.  |
| outcome::result< void > | **[TryResumeProposal](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-tryresumeproposal)**(const std::string & hash)<br/>Attempts to resume deferred handling for a subject hash.  |
| outcome::result< void > | **[TryResumePendingDependency](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-tryresumependingdependency)**(const [ConsensusManager::PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/) & dependency)<br/>Attempts to resume deferred handling for a typed pending dependency.  |
| bool | **[CheckCertificate](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-checkcertificate)**(const std::string & subject_hash) const<br/>Checks whether any certificate exists for subject hash.  |
| bool | **[CheckCertificateStrict](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-checkcertificatestrict)**(const [ConsensusManager::Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) & subject) const<br/>Performs strict certificate check for a specific subject object.  |
| outcome::result< [ConsensusManager::Certificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificate) > | **[GetCertificateBySubjectHash](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-getcertificatebysubjecthash)**(const std::string & subject_hash) const<br/>Loads certificate by subject hash.  |
| const std::string & | **[BestHash](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-besthash)**(const std::string & a, const std::string & b) const<br/>Chooses the preferred hash among two candidates.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| outcome::result< void > | **[MigrateCids](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-migratecids)**(const std::shared_ptr< [crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) > & old_db, const std::shared_ptr< [crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) > & new_db)<br/>Migrates blockchain-related CIDs between GlobalDB instances.  |

## Friends

|                | Name           |
| -------------- | -------------- |
| class | **[Migration3_5_0To3_6_0](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#friend-migration3_5_0to3_6_0)**  |
| class | **[Migration3_6_0To3_7_0](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#friend-migration3_6_0to3_7_0)**  |
| class | **[MultiAccountTestAccess](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#friend-multiaccounttestaccess)**  |

## Detailed Description

```cpp
class sgns::Blockchain;
```

Manages genesis/account-creation blocks and consensus integration. 

This class coordinates CRDT-backed persistence of blockchain bootstrap blocks, validates signatures, tracks authoritative CIDs, and exposes a high-level interface to submit and verify consensus subjects/proposals. 

## Public Types Documentation

### enum Error

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| GENESIS_BLOCK_CREATION_FAILED | 0| Failed to create the genesis block.   |
| GENESIS_BLOCK_INVALID_SIGNATURE | | Genesis block has invalid signature.   |
| GENESIS_BLOCK_UNAUTHORIZED_CREATOR | | Genesis block created by unauthorized key.   |
| GENESIS_BLOCK_SERIALIZATION_FAILED | | Failed to serialize/deserialize genesis block.   |
| GENESIS_BLOCK_MISSING | | Genesis block wasn't received.   |
| ACCOUNT_CREATION_BLOCK_MISSING | | Account creation is missing.   |
| ACCOUNT_CREATION_BLOCK_CREATION_FAILED | | Failed to create account creation block.   |
| ACCOUNT_CREATION_BLOCK_INVALID_SIGNATURE | | Account creation block has invalid signature.   |
| ACCOUNT_CREATION_BLOCK_SERIALIZATION_FAILED | | Failed to serialize/deserialize account creation block.   |
| ACCOUNT_CREATION_BLOCK_INVALID_GENESIS_LINK | | Account creation block not properly linked to genesis.   |
| VALIDATOR_REGISTRY_CREATION_FAILED | | Failed to create validator registry.   |
| BLOCKCHAIN_NOT_INITIALIZED | | [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) not fully initialized yet.   |



[Error](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#enum-error) class of the [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) module. 

### using BlockchainCallback

```cpp
using sgns::Blockchain::BlockchainCallback = std::function<void( outcome::result<void> )>;
```

Callback invoked when blockchain initialization/processing finishes. 

## Public Functions Documentation

### function New

```cpp
static std::shared_ptr< Blockchain > New(
    std::shared_ptr< crdt::GlobalDB > global_db,
    std::shared_ptr< GeniusAccount > account,
    std::shared_ptr< ipfs_pubsub::GossipPubSub > pubsub,
    BlockchainCallback callback
)
```

Factory method to create [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) as shared_ptr. 

**Parameters**: 

  * **global_db** CRDT database instance. 
  * **account** [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/) instance. 
  * **pubsub** PubSub instance used by consensus manager. 
  * **callback** Called when initialization completes. 


**Return**: Shared pointer to blockchain instance. 

### function SetAuthorizedFullNodeAddress

```cpp
static void SetAuthorizedFullNodeAddress(
    const std::string & pub_address
)
```

Set the authorized full node public address (for testing purposes). 

**Parameters**: 

  * **pub_address** The public address that is authorized to create genesis blocks 


### function GetAuthorizedFullNodeAddress

```cpp
static const std::string & GetAuthorizedFullNodeAddress()
```

Get the current authorized full node public address. 

**Return**: The authorized full node public address 

### function ~Blockchain

```cpp
~Blockchain()
```

Destroys the blockchain instance. 

### function Start

```cpp
outcome::result< void > Start()
```

Start the blockchain with async genesis block handling. 

**Return**: outcome::success on success, otherwise an error. 

### function Stop

```cpp
outcome::result< void > Stop()
```

Stops blockchain background processing and callbacks. 

**Return**: outcome::success on success, otherwise an error. 

### function OnGenesisBlockReceived

```cpp
outcome::result< void > OnGenesisBlockReceived(
    const base::Buffer & serialized_genesis
)
```

Handle received genesis block from pubsub. 

**Parameters**: 

  * **serialized_genesis** The received genesis block data 


**Return**: outcome::success when processed, otherwise an error. 

### function OnAccountCreationBlockReceived

```cpp
outcome::result< void > OnAccountCreationBlockReceived(
    const base::Buffer & serialized_account_creation
)
```

Handle received account creation block from pubsub. 

**Parameters**: 

  * **serialized_account_creation** The received account creation block data 


**Return**: outcome::success when processed, otherwise an error. 

### function GetGenesisCID

```cpp
outcome::result< std::string > GetGenesisCID() const
```

Returns the stored CID of the selected genesis block. 

**Return**: Genesis CID on success, otherwise an error. 

### function GetAccountCreationCID

```cpp
outcome::result< std::string > GetAccountCreationCID() const
```

Returns the stored CID of the selected account-creation block. 

**Return**: Account-creation CID on success, otherwise an error. 

### function GetValidatorRegistry

```cpp
std::shared_ptr< ValidatorRegistry > GetValidatorRegistry() const
```

Returns validator registry owned by this blockchain instance. 

**Return**: Shared pointer to validator registry, possibly null when unavailable. 

### function SetFullNodeMode

```cpp
void SetFullNodeMode()
```

Forces full-node mode behavior for bootstrap/generation flow. 

### function RegisterSubjectHandler

```cpp
bool RegisterSubjectHandler(
    std::string_view subject_type,
    ConsensusManager::SubjectHandler handler
)
```

Registers a consensus subject handler by canonical subject type string. 

**Parameters**: 

  * **subject_type** Canonical subject type to handle. 
  * **handler** Callback invoked for matching subjects. 


**Return**: `true` on successful registration. 

### function UnregisterSubjectHandler

```cpp
void UnregisterSubjectHandler(
    std::string_view subject_type
)
```

Unregisters a consensus subject handler by canonical subject type string. 

**Parameters**: 

  * **subject_type** Canonical subject type to remove. 


### function RegisterCertificateHandler

```cpp
bool RegisterCertificateHandler(
    std::string_view subject_type,
    ConsensusManager::CertificateSubjectHandler handler
)
```

Registers a consensus certificate handler by canonical subject type string. 

**Parameters**: 

  * **subject_type** Canonical subject type associated with certificate callback. 
  * **handler** Callback invoked for matching certificates. 


**Return**: `true` on successful registration. 

### function UnregisterCertificateHandler

```cpp
void UnregisterCertificateHandler(
    std::string_view subject_type
)
```

Unregisters a consensus certificate handler by canonical subject type string. 

**Parameters**: 

  * **subject_type** Canonical subject type to remove. 


### function RegisterProposalCleanupHandler

```cpp
bool RegisterProposalCleanupHandler(
    std::string_view subject_type,
    ConsensusManager::ProposalCleanupHandler handler
)
```

Registers a proposal cleanup callback by canonical subject type string. 

**Parameters**: 

  * **subject_type** Canonical subject type to handle. 
  * **handler** Callback invoked when a proposal slot is cleaned up due to timeout. 


**Return**: `true` on successful registration via the consensus manager. 

### function RegisterSlotKeyHandler

```cpp
void RegisterSlotKeyHandler(
    std::string_view subject_type,
    ConsensusManager::SlotKeyHandler handler
)
```

Registers a slot key handler for a specific embedded transaction oneof case. 

**Parameters**: 

  * **transaction_case** EmbeddedTransaction oneof case number (e.g. kMintV2). 
  * **handler** Callback that produces a deterministic slot key for proposals carrying this embedded transaction type. 


### function SetSlotHashPopulator

```cpp
void SetSlotHashPopulator(
    ConsensusManager::SlotHashPopulator populator
)
```

Forwards a slot-hash populator to the consensus manager (Phase 6, D-01). 

**Parameters**: 

  * **populator** Callback invoked during CreateVote before signing.


[GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/) wires this during blockchain initialization to bridge [TransactionManager::GetPublicChainInputValidator()](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getpublicchaininputvalidator) into vote creation. 


### function UnregisterSlotKeyHandler

```cpp
void UnregisterSlotKeyHandler(
    std::string_view subject_type
)
```


### function CreateConsensusNonceSubject

```cpp
outcome::result< ConsensusManager::Subject > CreateConsensusNonceSubject(
    const std::string & account_id,
    uint64_t nonce,
    const std::string & tx_hash,
    const EmbeddedTransaction & transaction,
    const std::optional< UTXOTransitionCommitment > & utxo_commitment,
    const std::optional< UTXOWitness > & utxo_witness
)
```

Creates a consensus subject for nonce/transaction transition. 

**Parameters**: 

  * **account_id** Account identifier. 
  * **nonce** Account nonce. 
  * **tx_hash** Transaction hash. 
  * **transaction** EmbeddedTransaction proto with typed oneof field set. 
  * **utxo_commitment** Optional UTXO commitment payload. 
  * **utxo_witness** Optional UTXO witness payload. 


**Return**: Constructed subject or an error. 

### function CreateConsensusProposal

```cpp
outcome::result< ConsensusManager::Proposal > CreateConsensusProposal(
    const std::string & account_id,
    uint64_t nonce,
    const std::string & tx_hash,
    const EmbeddedTransaction & transaction,
    const std::optional< UTXOTransitionCommitment > & utxo_commitment,
    const std::optional< UTXOWitness > & utxo_witness
)
```

Creates a signed proposal for nonce/transaction transition. 

**Parameters**: 

  * **account_id** Account identifier. 
  * **nonce** Account nonce. 
  * **tx_hash** Transaction hash. 
  * **transaction** EmbeddedTransaction proto with typed oneof field set. 
  * **utxo_commitment** Optional UTXO commitment payload. 
  * **utxo_witness** Optional UTXO witness payload. 


**Return**: Constructed proposal or an error. 

### function SubmitProposal

```cpp
outcome::result< void > SubmitProposal(
    const ConsensusManager::Proposal & proposal
)
```

Submits a proposal through consensus manager. 

**Parameters**: 

  * **proposal** Proposal to submit. 


**Return**: outcome::success on success, otherwise an error. 

### function TryResumeProposal

```cpp
outcome::result< void > TryResumeProposal(
    const std::string & hash
)
```

Attempts to resume deferred handling for a subject hash. 

**Parameters**: 

  * **hash** Subject hash key. 


**Return**: outcome::success on success, otherwise an error. 

### function TryResumePendingDependency

```cpp
outcome::result< void > TryResumePendingDependency(
    const ConsensusManager::PendingDependencyKey & dependency
)
```

Attempts to resume deferred handling for a typed pending dependency. 

**Parameters**: 

  * **dependency** Dependency key that became available. 


**Return**: outcome::success on success, otherwise an error. 

### function CheckCertificate

```cpp
bool CheckCertificate(
    const std::string & subject_hash
) const
```

Checks whether any certificate exists for subject hash. 

**Parameters**: 

  * **subject_hash** Subject hash key. 


**Return**: `true` when certificate exists. 

### function CheckCertificateStrict

```cpp
bool CheckCertificateStrict(
    const ConsensusManager::Subject & subject
) const
```

Performs strict certificate check for a specific subject object. 

**Parameters**: 

  * **subject** Subject to evaluate. 


**Return**: `true` when certificate exists and matches strictly. 

### function GetCertificateBySubjectHash

```cpp
outcome::result< ConsensusManager::Certificate > GetCertificateBySubjectHash(
    const std::string & subject_hash
) const
```

Loads certificate by subject hash. 

**Parameters**: 

  * **subject_hash** Subject hash key. 


**Return**: Certificate on success, otherwise an error. 

### function BestHash

```cpp
const std::string & BestHash(
    const std::string & a,
    const std::string & b
) const
```

Chooses the preferred hash among two candidates. 

**Parameters**: 

  * **a** First hash candidate. 
  * **b** Second hash candidate. 


**Return**: Reference to selected hash. 

## Protected Functions Documentation

### function MigrateCids

```cpp
static outcome::result< void > MigrateCids(
    const std::shared_ptr< crdt::GlobalDB > & old_db,
    const std::shared_ptr< crdt::GlobalDB > & new_db
)
```

Migrates blockchain-related CIDs between GlobalDB instances. 

**Parameters**: 

  * **old_db** Source GlobalDB. 
  * **new_db** Target GlobalDB. 


**Return**: outcome::success on success, otherwise an error. 

## Friends

### friend Migration3_5_0To3_6_0

```cpp
friend class Migration3_5_0To3_6_0(
    Migration3_5_0To3_6_0 
);
```


### friend Migration3_6_0To3_7_0

```cpp
friend class Migration3_6_0To3_7_0(
    Migration3_6_0To3_7_0 
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
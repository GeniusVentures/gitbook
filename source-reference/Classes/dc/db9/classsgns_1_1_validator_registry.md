---
title: sgns::ValidatorRegistry
summary: Maintains validator registry state and applies certificate-driven updates. 

---

# sgns::ValidatorRegistry



Maintains validator registry state and applies certificate-driven updates.  [More...](#detailed-description)


`#include <ValidatorRegistry.hpp>`

Inherits from std::enable_shared_from_this< ValidatorRegistry >

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[WeightConfig](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/)** <br/>Weight policy used to score validators and update penalties.  |
| struct | **[SlotQuorumResult](/source-reference/Classes/dd/d8c/structsgns_1_1_validator_registry_1_1_slot_quorum_result/)** <br/>Result of the Phase 6 cumulative slot-quorum tally (D-06).  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[BatchSubjectDecision](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#enum-batchsubjectdecision)** { Approve, Reject, Pending}<br/>Decision result when evaluating a registry-batch subject.  |
| enum class| **[BatchCertificateDecision](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#enum-batchcertificatedecision)** { Approve, Reject, Pending, Stalled}<br/>Decision result when handling a registry-batch certificate.  |
| using validator::ValidatorEntry | **[ValidatorEntry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-validatorentry)**  |
| using validator::Registry | **[Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry)**  |
| using validator::SignatureEntry | **[SignatureEntry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-signatureentry)**  |
| using validator::RegistryUpdate | **[RegistryUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registryupdate)**  |
| using validator::Role | **[Role](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-role)**  |
| using validator::Status | **[Status](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-status)**  |
| using std::function< void(bool)> | **[InitCallback](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-initcallback)**  |
| using std::function< void(const std::string &, std::function< void(outcome::result< std::string >)>)> | **[BlockRequestMethod](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-blockrequestmethod)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [ValidatorRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-validatorregistry) > | **[New](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-new)**(std::shared_ptr< [crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) > db, uint64_t quorum_numerator, uint64_t quorum_denominator, [WeightConfig](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/) weight_config, std::string genesis_authority, [BlockRequestMethod](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-blockrequestmethod) block_request_method, [InitCallback](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-initcallback) init_callback =nullptr)<br/>Creates and initializes a validator registry instance.  |
| uint64_t | **[TotalWeight](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-totalweight)**(const [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) & registry)<br/>Computes total effective weight in a registry snapshot.  |
| [SlotQuorumResult](/source-reference/Classes/dd/d8c/structsgns_1_1_validator_registry_1_1_slot_quorum_result/) | **[EvaluateSlotQuorumStatic](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-evaluateslotquorumstatic)**(const std::vector< sgns::ConsensusVote > & votes, const [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) & registry, const [WeightConfig](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/) & weight_config)<br/>Pure (stateless) slot-quorum tally for deterministic unit testing.  |
| bool | **[EvaluateRegularPromotionStatic](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-evaluateregularpromotionstatic)**(const [ValidatorEntry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-validatorentry) & entry, const [WeightConfig](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/) & weight_config)<br/>Pure (stateless) REGULAR -> FULL promotion decision (D-08).  |
| std::string_view | **[RegistryKey](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-registrykey)**()<br/>[Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) object key used in datastore.  |
| std::string_view | **[ValidatorTopic](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-validatortopic)**()<br/>Topic used to publish/subscribe validator registry updates.  |
| std::string_view | **[RegistryCidKey](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-registrycidkey)**()<br/>Key used to persist the current registry CID.  |
| const [ValidatorEntry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-validatorentry) * | **[FindValidator](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-findvalidator)**(const [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) & registry, const std::string & validator_id)<br/>Finds validator entry by id in a registry snapshot.  |
| | **[~ValidatorRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-~validatorregistry)**()<br/>Destroys the registry instance.  |
| uint64_t | **[ComputeWeight](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-computeweight)**([Role](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-role) role) const<br/>Computes default weight for a validator role.  |
| uint64_t | **[QuorumThreshold](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-quorumthreshold)**(uint64_t total_weight) const<br/>Computes minimum accumulated weight required for quorum.  |
| bool | **[IsQuorum](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-isquorum)**(uint64_t accumulated_weight, uint64_t total_weight) const<br/>Checks whether accumulated weight satisfies quorum.  |
| [SlotQuorumResult](/source-reference/Classes/dd/d8c/structsgns_1_1_validator_registry_1_1_slot_quorum_result/) | **[EvaluateSlotQuorum](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-evaluateslotquorum)**(const std::vector< sgns::ConsensusVote > & votes, const [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) & registry) const<br/>Phase 6 cumulative slot-quorum tally for bridge-mint subjects (D-06).  |
| [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) | **[CreateGenesisRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-creategenesisregistry)**(const std::string & genesis_validator_id) const<br/>Creates an in-memory genesis registry snapshot.  |
| outcome::result< void > | **[StoreGenesisRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-storegenesisregistry)**(const std::string & genesis_validator_id, std::function< std::vector< uint8_t >(std::vector< uint8_t >)> sign)<br/>Persists a signed genesis registry update.  |
| outcome::result< [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) > | **[LoadRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-loadregistry)**() const<br/>Loads the currently active registry.  |
| outcome::result< [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) > | **[LoadRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-loadregistry)**(const std::string & cid) const<br/>Loads a registry by CID.  |
| outcome::result< [RegistryUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registryupdate) > | **[LoadRegistryUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-loadregistryupdate)**() const<br/>Loads the currently active registry update payload.  |
| outcome::result< std::optional< uint64_t > > | **[GetValidatorWeight](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-getvalidatorweight)**(const std::string & validator_id) const<br/>Looks up validator weight by validator id.  |
| bool | **[RegisterFilter](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-registerfilter)**()<br/>Registers CRDT filter/callbacks for registry updates.  |
| outcome::result< [RegistryUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registryupdate) > | **[CreateUpdateFromCertificate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-createupdatefromcertificate)**(const sgns::ConsensusCertificate & certificate)<br/>Builds a registry update from a finalized certificate.  |
| outcome::result< void > | **[StoreRegistryUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-storeregistryupdate)**(const [RegistryUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registryupdate) & update)<br/>Persists a registry update.  |
| outcome::result< std::shared_ptr< [crdt::AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/) > > | **[BeginRegistryUpdateTransaction](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-beginregistryupdatetransaction)**(const [RegistryUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registryupdate) & update)<br/>Starts an atomic transaction to apply a registry update.  |
| void | **[SetMaxNewValidatorsPerUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-setmaxnewvalidatorsperupdate)**(size_t max_new)<br/>Sets the maximum number of unregistered validators added per update.  |
| outcome::result< std::vector< uint8_t > > | **[SerializeRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-serializeregistry)**(const [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) & registry) const<br/>Serializes a registry protobuf.  |
| outcome::result< [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) > | **[DeserializeRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-deserializeregistry)**(const std::vector< uint8_t > & buffer) const<br/>Deserializes a registry protobuf.  |
| outcome::result< std::vector< uint8_t > > | **[SerializeRegistryUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-serializeregistryupdate)**(const [RegistryUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registryupdate) & update) const<br/>Serializes a registry update protobuf.  |
| outcome::result< [RegistryUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registryupdate) > | **[DeserializeRegistryUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-deserializeregistryupdate)**(const std::vector< uint8_t > & buffer) const<br/>Deserializes a registry update protobuf.  |
| std::string | **[GetRegistryCid](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-getregistrycid)**() const<br/>Returns cached/current registry CID.  |
| uint64_t | **[GetRegistryEpoch](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-getregistryepoch)**() const<br/>Returns cached/current registry epoch.  |
| void | **[SetCertificatesPerBatch](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-setcertificatesperbatch)**(size_t batch_size)<br/>Sets certificate count threshold used when creating batch subjects.  |
| void | **[SetBatchSubjectSubmitter](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-setbatchsubjectsubmitter)**(std::function< outcome::result< void >(const ConsensusSubject &subject)> submitter)<br/>Sets callback used to submit generated batch subjects.  |
| void | **[OnFinalizedCertificate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-onfinalizedcertificate)**(const sgns::ConsensusCertificate & certificate)<br/>Handles a finalized consensus certificate.  |
| outcome::result< [BatchSubjectDecision](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#enum-batchsubjectdecision) > | **[EvaluateBatchSubject](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-evaluatebatchsubject)**(const ConsensusSubject & subject)<br/>Evaluates a registry-batch subject payload.  |
| outcome::result< [BatchCertificateDecision](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#enum-batchcertificatedecision) > | **[HandleBatchCertificate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-handlebatchcertificate)**(const std::string & subject_hash, const sgns::ConsensusCertificate & certificate)<br/>Handles certificate associated with a registry-batch subject.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| outcome::result< void > | **[MigrateCids](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-migratecids)**(const std::shared_ptr< [crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) > & old_db, const std::shared_ptr< [crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) > & new_db)<br/>Migrates registry-related CIDs from old to new datastore.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| size_t | **[DefaultMaxNewValidatorsPerUpdate](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#variable-defaultmaxnewvalidatorsperupdate)** <br/>Default cap for new validators added per update.  |
| size_t | **[DefaultCertificatesPerBatch](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#variable-defaultcertificatesperbatch)** <br/>Default number of certificates grouped per batch.  |

## Friends

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::Migration3_5_0To3_6_0](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#friend-sgnsmigration3_5_0to3_6_0)**  |

## Detailed Description

```cpp
class sgns::ValidatorRegistry;
```

Maintains validator registry state and applies certificate-driven updates. 

This component stores the active validator set in GlobalDB/CRDT, computes quorum thresholds, validates registry updates, and derives next registry snapshots from consensus certificates. 

## Public Types Documentation

### enum BatchSubjectDecision

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| Approve | | Subject is valid and should proceed.   |
| Reject | | Subject is invalid and should be rejected.   |
| Pending | | Subject cannot be decided yet.   |



Decision result when evaluating a registry-batch subject. 

### enum BatchCertificateDecision

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| Approve | | Certificate is accepted.   |
| Reject | | Certificate is rejected.   |
| Pending | | Decision is deferred due to missing prerequisites.   |
| Stalled | | Processing is stalled and should be retried later.   |



Decision result when handling a registry-batch certificate. 

### using ValidatorEntry

```cpp
using sgns::ValidatorRegistry::ValidatorEntry = validator::ValidatorEntry;
```


### using Registry

```cpp
using sgns::ValidatorRegistry::Registry = validator::Registry;
```


### using SignatureEntry

```cpp
using sgns::ValidatorRegistry::SignatureEntry = validator::SignatureEntry;
```


### using RegistryUpdate

```cpp
using sgns::ValidatorRegistry::RegistryUpdate = validator::RegistryUpdate;
```


### using Role

```cpp
using sgns::ValidatorRegistry::Role = validator::Role;
```


### using Status

```cpp
using sgns::ValidatorRegistry::Status = validator::Status;
```


### using InitCallback

```cpp
using sgns::ValidatorRegistry::InitCallback = std::function<void( bool )>;
```


### using BlockRequestMethod

```cpp
using sgns::ValidatorRegistry::BlockRequestMethod = 
std::function<void( const std::string &, std::function<void( outcome::result<std::string> )> )>;
```


## Public Functions Documentation

### function New

```cpp
static std::shared_ptr< ValidatorRegistry > New(
    std::shared_ptr< crdt::GlobalDB > db,
    uint64_t quorum_numerator,
    uint64_t quorum_denominator,
    WeightConfig weight_config,
    std::string genesis_authority,
    BlockRequestMethod block_request_method,
    InitCallback init_callback =nullptr
)
```

Creates and initializes a validator registry instance. 

**Parameters**: 

  * **db** GlobalDB backing store. 
  * **quorum_numerator** Numerator used for quorum threshold computation. 
  * **quorum_denominator** Denominator used for quorum threshold computation. 
  * **weight_config** Validator weighting and penalty configuration. 
  * **genesis_authority** Validator id treated as genesis authority. 
  * **block_request_method** Callback used to fetch blocks by CID. 
  * **init_callback** Optional callback notified after initialization. 


**Return**: Shared pointer to the created registry. 

### function TotalWeight

```cpp
static uint64_t TotalWeight(
    const Registry & registry
)
```

Computes total effective weight in a registry snapshot. 

**Parameters**: 

  * **registry** [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) snapshot. 


**Return**: Sum of validator weights. 

### function EvaluateSlotQuorumStatic

```cpp
static SlotQuorumResult EvaluateSlotQuorumStatic(
    const std::vector< sgns::ConsensusVote > & votes,
    const Registry & registry,
    const WeightConfig & weight_config
)
```

Pure (stateless) slot-quorum tally for deterministic unit testing. 

**Parameters**: 

  * **votes** Consensus votes (only approve votes counted). 
  * **registry** [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) snapshot used to resolve voter weights. 
  * **weight_config** Slot ratio configuration. 


**Return**: Slot tally result. 

Identical arithmetic to EvaluateSlotQuorum, but takes the [WeightConfig](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/) explicitly so it can be exercised without a GlobalDB-backed [ValidatorRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/) instance. The member function delegates here.


### function EvaluateRegularPromotionStatic

```cpp
static bool EvaluateRegularPromotionStatic(
    const ValidatorEntry & entry,
    const WeightConfig & weight_config
)
```

Pure (stateless) REGULAR -> FULL promotion decision (D-08). 

**Parameters**: 

  * **entry** Validator entry under consideration. 
  * **weight_config** Weight policy supplying thresholds. 


**Return**: true if the entry should be promoted from REGULAR to FULL. 

Returns true iff the entry is currently Role::REGULAR, its accumulated weight has reached full_promotion_weight_, AND its penalty_score is strictly below penalty_threshold_. GENESIS, SHARDED, and already-FULL entries never qualify (no GENESIS demotion, idempotent on FULL). Extracted as a pure static helper so the promotion decision is unit-testable without a GlobalDB-backed [ValidatorRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/) instance &ndash; ApplyVoteEffects delegates here. The function reads ONLY its inputs (REQ-DETERM-01), so every peer mutates the entry identically.


### function RegistryKey

```cpp
static inline std::string_view RegistryKey()
```

[Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) object key used in datastore. 

**Return**: Constant registry key. 

### function ValidatorTopic

```cpp
static inline std::string_view ValidatorTopic()
```

Topic used to publish/subscribe validator registry updates. 

**Return**: Constant validator topic. 

### function RegistryCidKey

```cpp
static inline std::string_view RegistryCidKey()
```

Key used to persist the current registry CID. 

**Return**: Constant CID key. 

### function FindValidator

```cpp
static const ValidatorEntry * FindValidator(
    const Registry & registry,
    const std::string & validator_id
)
```

Finds validator entry by id in a registry snapshot. 

**Parameters**: 

  * **registry** [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) snapshot. 
  * **validator_id** Validator identifier. 


**Return**: Pointer to entry when found, otherwise `nullptr`. 

### function ~ValidatorRegistry

```cpp
~ValidatorRegistry()
```

Destroys the registry instance. 

### function ComputeWeight

```cpp
uint64_t ComputeWeight(
    Role role
) const
```

Computes default weight for a validator role. 

**Parameters**: 

  * **role** Validator role. 


**Return**: Weight associated with the role. 

### function QuorumThreshold

```cpp
uint64_t QuorumThreshold(
    uint64_t total_weight
) const
```

Computes minimum accumulated weight required for quorum. 

**Parameters**: 

  * **total_weight** Total eligible weight. 


**Return**: Quorum threshold. 

### function IsQuorum

```cpp
bool IsQuorum(
    uint64_t accumulated_weight,
    uint64_t total_weight
) const
```

Checks whether accumulated weight satisfies quorum. 

**Parameters**: 

  * **accumulated_weight** Weight accumulated by votes. 
  * **total_weight** Total eligible weight. 


**Return**: `true` when quorum is reached. 

### function EvaluateSlotQuorum

```cpp
SlotQuorumResult EvaluateSlotQuorum(
    const std::vector< sgns::ConsensusVote > & votes,
    const Registry & registry
) const
```

Phase 6 cumulative slot-quorum tally for bridge-mint subjects (D-06). 

**Parameters**: 

  * **votes** Consensus votes (only approve votes are counted). 
  * **registry** [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) snapshot used to resolve voter weights. 


**Return**: Slot tally result. 

Reads ONLY the supplied votes and registry snapshot (REQ-DETERM-01). Slot 0: each distinct approver with a non-empty slot_0_hash contributes weight * slot_direct_numerator_ / slot_direct_denominator_ (D-02). Slots 1-2: votes are grouped by slot_N_hash; only groups with at least slot_public_min_group_ distinct validators contribute sum(weight) * slot_public_numerator_ / slot_public_denominator_ (D-03). Solo hashes contribute zero. Abstainers (all slot hashes empty) still count toward total_voting_reputation but zero toward qualified_sum (D-05). has_quorum = (qualified_sum > threshold) &ndash; STRICT (D-06).


### function CreateGenesisRegistry

```cpp
Registry CreateGenesisRegistry(
    const std::string & genesis_validator_id
) const
```

Creates an in-memory genesis registry snapshot. 

**Parameters**: 

  * **genesis_validator_id** Validator id for the genesis authority. 


**Return**: Genesis registry snapshot. 

### function StoreGenesisRegistry

```cpp
outcome::result< void > StoreGenesisRegistry(
    const std::string & genesis_validator_id,
    std::function< std::vector< uint8_t >(std::vector< uint8_t >)> sign
)
```

Persists a signed genesis registry update. 

**Parameters**: 

  * **genesis_validator_id** Validator id for the genesis authority. 
  * **sign** Signing callback used for registry-update signatures. 


**Return**: outcome::success on success, otherwise an error. 

### function LoadRegistry

```cpp
outcome::result< Registry > LoadRegistry() const
```

Loads the currently active registry. 

**Return**: [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) snapshot or an error. 

### function LoadRegistry

```cpp
outcome::result< Registry > LoadRegistry(
    const std::string & cid
) const
```

Loads a registry by CID. 

**Parameters**: 

  * **cid** [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) CID. 


**Return**: [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) snapshot or an error. 

### function LoadRegistryUpdate

```cpp
outcome::result< RegistryUpdate > LoadRegistryUpdate() const
```

Loads the currently active registry update payload. 

**Return**: [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) update or an error. 

### function GetValidatorWeight

```cpp
outcome::result< std::optional< uint64_t > > GetValidatorWeight(
    const std::string & validator_id
) const
```

Looks up validator weight by validator id. 

**Parameters**: 

  * **validator_id** Validator identifier. 


**Return**: Optional weight when validator exists, or an error. 

### function RegisterFilter

```cpp
bool RegisterFilter()
```

Registers CRDT filter/callbacks for registry updates. 

**Return**: `true` when registration succeeds. 

### function CreateUpdateFromCertificate

```cpp
outcome::result< RegistryUpdate > CreateUpdateFromCertificate(
    const sgns::ConsensusCertificate & certificate
)
```

Builds a registry update from a finalized certificate. 

**Parameters**: 

  * **certificate** Consensus certificate. 


**Return**: [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) update or an error. 

### function StoreRegistryUpdate

```cpp
outcome::result< void > StoreRegistryUpdate(
    const RegistryUpdate & update
)
```

Persists a registry update. 

**Parameters**: 

  * **update** [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) update to store. 


**Return**: outcome::success on success, otherwise an error. 

### function BeginRegistryUpdateTransaction

```cpp
outcome::result< std::shared_ptr< crdt::AtomicTransaction > > BeginRegistryUpdateTransaction(
    const RegistryUpdate & update
)
```

Starts an atomic transaction to apply a registry update. 

**Parameters**: 

  * **update** [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) update being applied. 


**Return**: Transaction handle or an error. 

### function SetMaxNewValidatorsPerUpdate

```cpp
void SetMaxNewValidatorsPerUpdate(
    size_t max_new
)
```

Sets the maximum number of unregistered validators added per update. 

**Parameters**: 

  * **max_new** New cap value. 


### function SerializeRegistry

```cpp
outcome::result< std::vector< uint8_t > > SerializeRegistry(
    const Registry & registry
) const
```

Serializes a registry protobuf. 

**Parameters**: 

  * **registry** [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) to serialize. 


**Return**: Serialized bytes or an error. 

### function DeserializeRegistry

```cpp
outcome::result< Registry > DeserializeRegistry(
    const std::vector< uint8_t > & buffer
) const
```

Deserializes a registry protobuf. 

**Parameters**: 

  * **buffer** Serialized registry bytes. 


**Return**: Parsed registry or an error. 

### function SerializeRegistryUpdate

```cpp
outcome::result< std::vector< uint8_t > > SerializeRegistryUpdate(
    const RegistryUpdate & update
) const
```

Serializes a registry update protobuf. 

**Parameters**: 

  * **update** [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) update to serialize. 


**Return**: Serialized bytes or an error. 

### function DeserializeRegistryUpdate

```cpp
outcome::result< RegistryUpdate > DeserializeRegistryUpdate(
    const std::vector< uint8_t > & buffer
) const
```

Deserializes a registry update protobuf. 

**Parameters**: 

  * **buffer** Serialized registry update bytes. 


**Return**: Parsed update or an error. 

### function GetRegistryCid

```cpp
std::string GetRegistryCid() const
```

Returns cached/current registry CID. 

**Return**: [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) CID string. 

### function GetRegistryEpoch

```cpp
uint64_t GetRegistryEpoch() const
```

Returns cached/current registry epoch. 

**Return**: [Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) epoch. 

### function SetCertificatesPerBatch

```cpp
void SetCertificatesPerBatch(
    size_t batch_size
)
```

Sets certificate count threshold used when creating batch subjects. 

**Parameters**: 

  * **batch_size** Number of certificates per batch. 


### function SetBatchSubjectSubmitter

```cpp
void SetBatchSubjectSubmitter(
    std::function< outcome::result< void >(const ConsensusSubject &subject)> submitter
)
```

Sets callback used to submit generated batch subjects. 

**Parameters**: 

  * **submitter** Subject submitter callback. 


### function OnFinalizedCertificate

```cpp
void OnFinalizedCertificate(
    const sgns::ConsensusCertificate & certificate
)
```

Handles a finalized consensus certificate. 

**Parameters**: 

  * **certificate** Finalized certificate. 


### function EvaluateBatchSubject

```cpp
outcome::result< BatchSubjectDecision > EvaluateBatchSubject(
    const ConsensusSubject & subject
)
```

Evaluates a registry-batch subject payload. 

**Parameters**: 

  * **subject** Subject to evaluate. 


**Return**: Subject decision or an error. 

### function HandleBatchCertificate

```cpp
outcome::result< BatchCertificateDecision > HandleBatchCertificate(
    const std::string & subject_hash,
    const sgns::ConsensusCertificate & certificate
)
```

Handles certificate associated with a registry-batch subject. 

**Parameters**: 

  * **subject_hash** Subject hash key. 
  * **certificate** Certificate to process. 


**Return**: Certificate handling decision or an error. 

## Protected Functions Documentation

### function MigrateCids

```cpp
static outcome::result< void > MigrateCids(
    const std::shared_ptr< crdt::GlobalDB > & old_db,
    const std::shared_ptr< crdt::GlobalDB > & new_db
)
```

Migrates registry-related CIDs from old to new datastore. 

**Parameters**: 

  * **old_db** Source GlobalDB. 
  * **new_db** Target GlobalDB. 


**Return**: outcome::success on success, otherwise an error. 

## Public Attributes Documentation

### variable DefaultMaxNewValidatorsPerUpdate

```cpp
static size_t DefaultMaxNewValidatorsPerUpdate                                                      =
10;
```

Default cap for new validators added per update. 

### variable DefaultCertificatesPerBatch

```cpp
static size_t DefaultCertificatesPerBatch = 5;
```

Default number of certificates grouped per batch. 

## Friends

### friend sgns::Migration3_5_0To3_6_0

```cpp
friend class sgns::Migration3_5_0To3_6_0(
    sgns::Migration3_5_0To3_6_0 
);
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
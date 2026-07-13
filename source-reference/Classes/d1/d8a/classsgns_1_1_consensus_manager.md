---
title: sgns::ConsensusManager
summary: Implements Consensus with weighted voting. 

---

# sgns::ConsensusManager



Implements Consensus with weighted voting.  [More...](#detailed-description)


`#include <Consensus.hpp>`

Inherits from std::enable_shared_from_this< ConsensusManager >

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/)** <br/>Local-only dependency key for deferred subject validation.  |
| struct | **[PendingDependencyKeyHash](/source-reference/Classes/d3/dbe/structsgns_1_1_consensus_manager_1_1_pending_dependency_key_hash/)** <br/>Hash functor for [PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/) unordered containers.  |
| struct | **[ValidationResult](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/)** <br/>Local structured validation result for subject handlers.  |
| struct | **[PendingLifecycleConfig](/source-reference/Classes/d4/dbf/structsgns_1_1_consensus_manager_1_1_pending_lifecycle_config/)** <br/>Local pending proposal lifecycle limits.  |
| struct | **[QuorumTally](/source-reference/Classes/d1/dce/structsgns_1_1_consensus_manager_1_1_quorum_tally/)** <br/>Quorum tally structure.  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[Check](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#enum-check)** { Approve, Reject, Pending, Stalled}<br/>Object checking values.  |
| using ConsensusProposal | **[Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal)** <br/>Alias for Consensus [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) protobuf type.  |
| using ConsensusVote | **[Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote)** <br/>Alias for Consensus [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) protobuf type.  |
| using ConsensusVoteBundle | **[VoteBundle](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-votebundle)** <br/>Alias for Consensus [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) Bundle protobuf type.  |
| using ConsensusCertificate | **[Certificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificate)** <br/>Alias for Consensus [Certificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificate) protobuf type.  |
| using ConsensusSubject | **[Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject)** <br/>Alias for Consensus [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) protobuf type.  |
| using std::function< outcome::result< std::vector< uint8_t > >(std::vector< uint8_t > payload)> | **[Signer](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-signer)** <br/>Alias for a signer method type.  |
| using std::function< void(ConsensusVote &vote)> | **[SlotHashPopulator](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-slothashpopulator)** <br/>Callback invoked during CreateVote to populate slot_N_hash fields before signing (Phase 6, D-01).  |
| using std::function< outcome::result< [ValidationResult](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/) >(const [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) &subject)> | **[SubjectHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subjecthandler)** <br/>Alias for a subject handler method type.  |
| using std::function< outcome::result< [Check](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#enum-check) >(const std::string &subject_hash, const [Certificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificate) &certificate)> | **[CertificateSubjectHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificatesubjecthandler)** <br/>Alias for a certificate handler method type.  |
| using std::function< void(const std::string &tx_hash)> | **[ProposalCleanupHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposalcleanuphandler)** <br/>Alias for a proposal cleanup handler method type Callback invoked when a proposal slot is cleaned up due to timeout. Receives the transaction hash so the handler can clean up associated tracking entries.  |
| using std::function< std::string(const [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) &subject)> | **[SlotKeyHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-slotkeyhandler)** <br/>Alias for a slot key handler — produces a deterministic slot key for a proposal. Takes the raw subject, called from GetSlotKey by subject type hash.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [ConsensusManager](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-consensusmanager) > | **[New](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-new)**(std::shared_ptr< [ValidatorRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/) > registry, std::shared_ptr< [crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/) > db, std::shared_ptr< ipfs_pubsub::GossipPubSub > pubsub, [Signer](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-signer) signer, std::string address, std::string consensus_topic ="")<br/>Creates a [ConsensusManager](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/) instance.  |
| void | **[RegisterSlotKeyHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-registerslotkeyhandler)**(std::string_view subject_type, [SlotKeyHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-slotkeyhandler) handler)<br/>Registers a slot key handler for a canonical subject type.  |
| void | **[UnregisterSlotKeyHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-unregisterslotkeyhandler)**(std::string_view subject_type)<br/>Unregisters the slot key handler for a canonical subject type.  |
| outcome::result< [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) > | **[CreateProposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-createproposal)**(const [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) & subject, const std::string & proposer_id, const std::string & registry_cid, uint64_t registry_epoch, [Signer](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-signer) sign)<br/>Builds and signs a proposal using an explicit signer.  |
| bool | **[IsBridgeMintSubject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-isbridgemintsubject)**(const [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) & proposal)<br/>Phase 6 (D-06): classifies a proposal's subject as a bridge mint.  |
| outcome::result< std::vector< uint8_t > > | **[ProposalSigningBytes](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-proposalsigningbytes)**(const [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) & proposal)<br/>Computes canonical bytes to sign a proposal.  |
| outcome::result< std::vector< uint8_t > > | **[VoteSigningBytes](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-votesigningbytes)**(const [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) & vote)<br/>Computes canonical bytes to sign a vote.  |
| outcome::result< std::vector< uint8_t > > | **[VoteBundleSigningBytes](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-votebundlesigningbytes)**(const [VoteBundle](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-votebundle) & bundle)<br/>Computes canonical bytes to sign a vote bundle.  |
| outcome::result< std::string > | **[ComputeSubjectId](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-computesubjectid)**(const [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) & subject)<br/>Computes deterministic subject id/hash.  |
| outcome::result< std::string > | **[ComputeSubjectTypeHash](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-computesubjecttypehash)**(std::string_view subject_type)<br/>Computes deterministic bytes for a canonical subject type string.  |
| outcome::result< NonceSubject > | **[DecodeNonceSubject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-decodenoncesubject)**(const [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) & subject) |
| outcome::result< TaskResultSubject > | **[DecodeTaskResultSubject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-decodetaskresultsubject)**(const [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) & subject) |
| outcome::result< RegistryBatchSubject > | **[DecodeRegistryBatchSubject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-decoderegistrybatchsubject)**(const [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) & subject) |
| bool | **[SubjectTypeMatches](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-subjecttypematches)**(const [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) & subject, std::string_view subject_type) |
| outcome::result< [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) > | **[CreateNonceSubject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-createnoncesubject)**(const std::string & account_id, uint64_t nonce, const std::string & tx_hash, const EmbeddedTransaction & transaction, const std::optional< UTXOTransitionCommitment > & utxo_commitment, const std::optional< UTXOWitness > & utxo_witness)<br/>Creates a nonce subject.  |
| outcome::result< [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) > | **[CreateTaskResultSubject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-createtaskresultsubject)**(const std::string & account_id, const std::string & escrow_path, const std::string & task_result_hash, uint64_t result_epoch)<br/>Creates a task-result subject.  |
| outcome::result< [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) > | **[CreateRegistryBatchSubject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-createregistrybatchsubject)**(const std::string & account_id, const std::string & base_registry_cid, uint64_t base_registry_epoch, uint64_t target_registry_epoch, uint32_t certificate_count, const std::string & batch_root)<br/>Creates a registry-batch subject.  |
| outcome::result< [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) > | **[CreateGenericSubject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-creategenericsubject)**(const std::string & account_id, std::string_view subject_type, const std::vector< uint8_t > & payload)<br/>Creates a generic typed subject for application-owned payload schemas.  |
| const std::string & | **[BestHash](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-besthash)**(const std::string & a, const std::string & b)<br/>Returns the lexicographically better hash among two values.  |
| | **[~ConsensusManager](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-~consensusmanager)**()<br/>Destroys the Consensus Manager object.  |
| void | **[Close](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-close)**()<br/>Close and cleanup members of the Consensus Manager.  |
| bool | **[RegisterSubjectHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-registersubjecthandler)**(std::string_view subject_type, [SubjectHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subjecthandler) handler)<br/>Registers a subject validation/handling callback by canonical subject type string.  |
| void | **[UnregisterSubjectHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-unregistersubjecthandler)**(std::string_view subject_type)<br/>Unregisters a subject handler by canonical subject type string.  |
| bool | **[RegisterCertificateHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-registercertificatehandler)**(std::string_view subject_type, [CertificateSubjectHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificatesubjecthandler) handler)<br/>Registers a certificate handling callback by canonical subject type string.  |
| void | **[UnregisterCertificateHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-unregistercertificatehandler)**(std::string_view subject_type)<br/>Unregisters a certificate handler by canonical subject type string.  |
| bool | **[RegisterProposalCleanupHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-registerproposalcleanuphandler)**(std::string_view subject_type, [ProposalCleanupHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposalcleanuphandler) handler)<br/>Registers a proposal cleanup callback by canonical subject type string.  |
| void | **[UnregisterProposalCleanupHandler](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-unregisterproposalcleanuphandler)**(std::string_view subject_type)<br/>Unregisters all proposal cleanup handlers for a canonical subject type string.  |
| void | **[SetPendingLifecycleConfig](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-setpendinglifecycleconfig)**([PendingLifecycleConfig](/source-reference/Classes/d4/dbf/structsgns_1_1_consensus_manager_1_1_pending_lifecycle_config/) config)<br/>Overrides local pending lifecycle limits for deterministic tests/configuration.  |
| outcome::result< void > | **[Publish](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-publish)**(const ConsensusMessage & message)<br/>Publishes a consensus envelope to pubsub.  |
| outcome::result< [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) > | **[CreateProposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-createproposal)**(const [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) & subject, const std::string & proposer_id, const std::string & registry_cid, uint64_t registry_epoch)<br/>Builds and signs a proposal using the manager signer.  |
| outcome::result< [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) > | **[CreateVote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-createvote)**(const std::string & proposal_id, const std::string & voter_id, bool approve, [Signer](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-signer) sign)<br/>Builds and signs a vote for a proposal.  |
| void | **[SetSlotHashPopulator](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-setslothashpopulator)**([SlotHashPopulator](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-slothashpopulator) populator)<br/>Injects the slot-hash populator used by CreateVote (Phase 6, D-01).  |
| outcome::result< [VoteBundle](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-votebundle) > | **[CreateVoteBundle](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-createvotebundle)**(const std::string & proposal_id, const std::string & aggregator_id, const std::vector< [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) > & votes, [Signer](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-signer) sign)<br/>Builds and signs an aggregated vote bundle.  |
| outcome::result< [Certificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificate) > | **[CreateCertificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-createcertificate)**(const [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) & proposal, const std::vector< [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) > & votes)<br/>Creates a certificate from a proposal and votes.  |
| outcome::result< [QuorumTally](/source-reference/Classes/d1/dce/structsgns_1_1_consensus_manager_1_1_quorum_tally/) > | **[TallyVotes](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-tallyvotes)**(const [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) & proposal, const std::vector< [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) > & votes, const [ValidatorRegistry::Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) & registry, const std::string & registry_cid) const<br/>Tallies votes against an explicit registry snapshot.  |
| outcome::result< [QuorumTally](/source-reference/Classes/d1/dce/structsgns_1_1_consensus_manager_1_1_quorum_tally/) > | **[TallyVotes](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-tallyvotes)**(const [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) & proposal, const std::vector< [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) > & votes) const<br/>Tallies votes using the manager registry source.  |
| outcome::result< [QuorumTally](/source-reference/Classes/d1/dce/structsgns_1_1_consensus_manager_1_1_quorum_tally/) > | **[EvaluateQuorum](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-evaluatequorum)**(const [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) & proposal, const std::vector< [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) > & votes, const [ValidatorRegistry::Registry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#using-registry) & registry) const<br/>Phase 6 (D-06): single quorum dispatcher.  |
| outcome::result< void > | **[SubmitProposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-submitproposal)**(const [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) & proposal, bool self_vote =true)<br/>Submits a proposal for local handling and broadcast.  |
| outcome::result< void > | **[SubmitVote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-submitvote)**(const [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) & vote, bool self_handle =true)<br/>Submits a vote for local handling and broadcast.  |
| outcome::result< void > | **[SubmitCertificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-submitcertificate)**(const [Certificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificate) & certificate)<br/>Submits a certificate for local handling and broadcast.  |
| outcome::result< void > | **[ResumeProposalHandling](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-resumeproposalhandling)**(const std::string & subject_hash)<br/>Retries proposal handling once its subject becomes ready.  |
| outcome::result< void > | **[WakePendingDependency](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-wakependingdependency)**(const [PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/) & dependency)<br/>Retries pending proposals waiting on a typed dependency key.  |
| void | **[ProcessCertificates](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-processcertificates)**()<br/>Processes queued certificate work entries.  |
| void | **[ConfigureCertificateDelay](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-configurecertificatedelay)**(std::chrono::milliseconds delay)<br/>Configures local delayed processing for received certificates.  |
| outcome::result< [Certificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificate) > | **[GetCertificateBySubjectHash](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-getcertificatebysubjecthash)**(const std::string & subject_hash) const<br/>Retrieves a certificate by subject hash.  |
| bool | **[CheckCertificateForSubject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-checkcertificateforsubject)**(const std::string & subject_hash) const<br/>Checks whether a certificate exists for a subject hash.  |
| bool | **[CheckCertificateForSubject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-checkcertificateforsubject)**(const [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) & subject) const<br/>Checks whether a certificate exists for a subject.  |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[ConfigureTimestampWindow](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-configuretimestampwindow)**(std::chrono::milliseconds window)<br/>Sets timestamp validation window for received objects.  |
| void | **[ConfigureRoundDuration](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-configureroundduration)**(std::chrono::milliseconds duration)<br/>Sets consensus round duration.  |
| void | **[ConfigureRoundSkew](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#function-configureroundskew)**(std::chrono::milliseconds skew)<br/>Sets allowable round skew tolerance.  |

## Friends

|                | Name           |
| -------------- | -------------- |
| class | **[ConsensusManagerTestAccess](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#friend-consensusmanagertestaccess)**  |
| class | **[ConsensusPendingLifecycleTestAccess](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#friend-consensuspendinglifecycletestaccess)**  |
| class | **[ConsensusSlotKeyTestAccess](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#friend-consensusslotkeytestaccess)**  |

## Detailed Description

```cpp
class sgns::ConsensusManager;
```

Implements Consensus with weighted voting. 



```
 This class implements a consensus algorithm using pubsub messages.
```

 A subject needs to be created and with it a proposal as well. The proposal gets sent to the network and gets voted by peers who receive it. This class has hooks to be filled by the caller to register methods to handle subject and proposal. The idea is to leave out the validation of specific data (transaction, job result and etc) for whomever creates the subject. It relies on [ValidatorRegistry](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/) class to get the voters and their weights. Once consensus is reached a round scheme determines who amongst the validators will create the certificate which is the finality of the subject. The certificate also enabled registry updates to register new validators according to peer who voted correctly or penalize people who votes incorrectly. 

## Public Types Documentation

### enum Check

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| Approve | | Object is approved.   |
| Reject | | Object is rejected.   |
| Pending | | Object evaluation is pending.   |
| Stalled | | Object evaluation is stalled.   |



Object checking values. 

### using Proposal

```cpp
using sgns::ConsensusManager::Proposal = ConsensusProposal;
```

Alias for Consensus [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) protobuf type. 

### using Vote

```cpp
using sgns::ConsensusManager::Vote = ConsensusVote;
```

Alias for Consensus [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) protobuf type. 

### using VoteBundle

```cpp
using sgns::ConsensusManager::VoteBundle = ConsensusVoteBundle;
```

Alias for Consensus [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) Bundle protobuf type. 

### using Certificate

```cpp
using sgns::ConsensusManager::Certificate = ConsensusCertificate;
```

Alias for Consensus [Certificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificate) protobuf type. 

### using Subject

```cpp
using sgns::ConsensusManager::Subject = ConsensusSubject;
```

Alias for Consensus [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) protobuf type. 

### using Signer

```cpp
using sgns::ConsensusManager::Signer = std::function<outcome::result<std::vector<uint8_t>>( std::vector<uint8_t> payload )>;
```

Alias for a signer method type. 

### using SlotHashPopulator

```cpp
using sgns::ConsensusManager::SlotHashPopulator = std::function<void( ConsensusVote &vote )>;
```

Callback invoked during CreateVote to populate slot_N_hash fields before signing (Phase 6, D-01). 

Set once at init time by [GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/) (via [Blockchain::SetSlotHashPopulator](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/#function-setslothashpopulator)) to bridge [TransactionManager::GetPublicChainInputValidator](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getpublicchaininputvalidator) into [ConsensusManager](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/)'s vote-creation path. When unset, CreateVote behaves exactly as before (backward compatible). The callback is invoked AFTER proposal_id/voter_id/approve/ timestamp are set but BEFORE VoteSigningBytes, so the resulting signature commits to the slot hashes (T-06-01). 


### using SubjectHandler

```cpp
using sgns::ConsensusManager::SubjectHandler = std::function<outcome::result<ValidationResult>( const Subject &subject )>;
```

Alias for a subject handler method type. 

### using CertificateSubjectHandler

```cpp
using sgns::ConsensusManager::CertificateSubjectHandler = 
std::function<outcome::result<Check>( const std::string &subject_hash, const Certificate &certificate )>;
```

Alias for a certificate handler method type. 

### using ProposalCleanupHandler

```cpp
using sgns::ConsensusManager::ProposalCleanupHandler = std::function<void( const std::string &tx_hash )>;
```

Alias for a proposal cleanup handler method type Callback invoked when a proposal slot is cleaned up due to timeout. Receives the transaction hash so the handler can clean up associated tracking entries. 

### using SlotKeyHandler

```cpp
using sgns::ConsensusManager::SlotKeyHandler = std::function<std::string( const Subject &subject )>;
```

Alias for a slot key handler — produces a deterministic slot key for a proposal. Takes the raw subject, called from GetSlotKey by subject type hash. 

## Public Functions Documentation

### function New

```cpp
static std::shared_ptr< ConsensusManager > New(
    std::shared_ptr< ValidatorRegistry > registry,
    std::shared_ptr< crdt::GlobalDB > db,
    std::shared_ptr< ipfs_pubsub::GossipPubSub > pubsub,
    Signer signer,
    std::string address,
    std::string consensus_topic =""
)
```

Creates a [ConsensusManager](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/) instance. 

**Parameters**: 

  * **registry** Validator registry used for voter set and weights. 
  * **db** GlobalDB instance used for persistence and CRDT interactions. 
  * **pubsub** PubSub transport for consensus message propagation. 
  * **signer** Local signing callback for outbound signed objects. 
  * **address** Local validator/account identifier. 
  * **consensus_topic** Optional topic override used to derive consensus channels. 


**Return**: Shared pointer to a new manager instance. 

### function RegisterSlotKeyHandler

```cpp
static void RegisterSlotKeyHandler(
    std::string_view subject_type,
    SlotKeyHandler handler
)
```

Registers a slot key handler for a canonical subject type. 

**Parameters**: 

  * **subject_type** Canonical subject type (e.g. "sgns.nonce.v1"). 
  * **handler** Callback that produces a slot key from the raw subject. 


RegisterSlotKeyHandler also changed to match subject type pattern: 


### function UnregisterSlotKeyHandler

```cpp
static void UnregisterSlotKeyHandler(
    std::string_view subject_type
)
```

Unregisters the slot key handler for a canonical subject type. 

**Parameters**: 

  * **subject_type** Canonical subject type to remove. 


### function CreateProposal

```cpp
static outcome::result< Proposal > CreateProposal(
    const Subject & subject,
    const std::string & proposer_id,
    const std::string & registry_cid,
    uint64_t registry_epoch,
    Signer sign
)
```

Builds and signs a proposal using an explicit signer. 

**Parameters**: 

  * **subject** Consensus subject to propose. 
  * **proposer_id** Validator identifier of the proposer. 
  * **registry_cid** CID of the validator registry snapshot. 
  * **registry_epoch** Epoch of the validator registry snapshot. 
  * **sign** Signing callback. 


**Return**: Signed proposal on success, otherwise an error. 

### function IsBridgeMintSubject

```cpp
static bool IsBridgeMintSubject(
    const Proposal & proposal
)
```

Phase 6 (D-06): classifies a proposal's subject as a bridge mint. 

**Parameters**: 

  * **proposal** [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) whose subject is inspected. 


**Return**: `true` when the subject is a bridge mint; `false` otherwise. 

A bridge mint is a NonceSubject whose embedded transaction case is kMintV2 AND whose chain_id is non-empty (mirror [TransactionManager::GetValidationChainId](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/#function-getvalidationchainid)). Any decode failure returns false (fail-closed: single-pool quorum applies).


### function ProposalSigningBytes

```cpp
static outcome::result< std::vector< uint8_t > > ProposalSigningBytes(
    const Proposal & proposal
)
```

Computes canonical bytes to sign a proposal. 

**Parameters**: 

  * **proposal** [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) to encode. 


**Return**: Signing bytes on success, otherwise an error. 

### function VoteSigningBytes

```cpp
static outcome::result< std::vector< uint8_t > > VoteSigningBytes(
    const Vote & vote
)
```

Computes canonical bytes to sign a vote. 

**Parameters**: 

  * **vote** [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) to encode. 


**Return**: Signing bytes on success, otherwise an error. 

### function VoteBundleSigningBytes

```cpp
static outcome::result< std::vector< uint8_t > > VoteBundleSigningBytes(
    const VoteBundle & bundle
)
```

Computes canonical bytes to sign a vote bundle. 

**Parameters**: 

  * **bundle** [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) bundle to encode. 


**Return**: Signing bytes on success, otherwise an error. 

### function ComputeSubjectId

```cpp
static outcome::result< std::string > ComputeSubjectId(
    const Subject & subject
)
```

Computes deterministic subject id/hash. 

**Parameters**: 

  * **subject** [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) to hash. 


**Return**: [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) identifier on success, otherwise an error. 

### function ComputeSubjectTypeHash

```cpp
static outcome::result< std::string > ComputeSubjectTypeHash(
    std::string_view subject_type
)
```

Computes deterministic bytes for a canonical subject type string. 

**Parameters**: 

  * **subject_type** Canonical subject type, e.g. "gnus.bridge_event.v1". 


**Return**: 32-byte subject type hash on success, otherwise an error. 

### function DecodeNonceSubject

```cpp
static outcome::result< NonceSubject > DecodeNonceSubject(
    const Subject & subject
)
```


### function DecodeTaskResultSubject

```cpp
static outcome::result< TaskResultSubject > DecodeTaskResultSubject(
    const Subject & subject
)
```


### function DecodeRegistryBatchSubject

```cpp
static outcome::result< RegistryBatchSubject > DecodeRegistryBatchSubject(
    const Subject & subject
)
```


### function SubjectTypeMatches

```cpp
static bool SubjectTypeMatches(
    const Subject & subject,
    std::string_view subject_type
)
```


### function CreateNonceSubject

```cpp
static outcome::result< Subject > CreateNonceSubject(
    const std::string & account_id,
    uint64_t nonce,
    const std::string & tx_hash,
    const EmbeddedTransaction & transaction,
    const std::optional< UTXOTransitionCommitment > & utxo_commitment,
    const std::optional< UTXOWitness > & utxo_witness
)
```

Creates a nonce subject. 

**Parameters**: 

  * **account_id** Account identifier bound to the subject. 
  * **nonce** Account nonce. 
  * **tx_hash** Transaction hash associated with the nonce transition. 
  * **transaction_data** Full serialized transaction bytes (SerializeByteVector output). 
  * **utxo_commitment** Optional UTXO commitment payload. 
  * **utxo_witness** Optional UTXO witness payload. 


**Return**: Constructed subject or an error. 

### function CreateTaskResultSubject

```cpp
static outcome::result< Subject > CreateTaskResultSubject(
    const std::string & account_id,
    const std::string & escrow_path,
    const std::string & task_result_hash,
    uint64_t result_epoch
)
```

Creates a task-result subject. 

**Parameters**: 

  * **account_id** Account identifier bound to the subject. 
  * **escrow_path** Escrow path associated with task execution. 
  * **task_result_hash** Result hash for the task output. 
  * **result_epoch** Epoch for the task result. 


**Return**: Constructed subject or an error. 

### function CreateRegistryBatchSubject

```cpp
static outcome::result< Subject > CreateRegistryBatchSubject(
    const std::string & account_id,
    const std::string & base_registry_cid,
    uint64_t base_registry_epoch,
    uint64_t target_registry_epoch,
    uint32_t certificate_count,
    const std::string & batch_root
)
```

Creates a registry-batch subject. 

**Parameters**: 

  * **account_id** Account identifier bound to the subject. 
  * **base_registry_cid** Base registry CID used for the batch. 
  * **base_registry_epoch** Base registry epoch. 
  * **target_registry_epoch** Target registry epoch after applying batch. 
  * **certificate_count** Number of certificates in the batch. 
  * **batch_root** Merkle/root hash of the batch payload. 


**Return**: Constructed subject or an error. 

### function CreateGenericSubject

```cpp
static outcome::result< Subject > CreateGenericSubject(
    const std::string & account_id,
    std::string_view subject_type,
    const std::vector< uint8_t > & payload
)
```

Creates a generic typed subject for application-owned payload schemas. 

**Parameters**: 

  * **account_id** Account identifier bound to the subject. 
  * **subject_type** Canonical subject type, e.g. "gnus.bridge_event.v1". 
  * **payload** Canonical serialized application payload. 


**Return**: Constructed subject or an error. 

### function BestHash

```cpp
static const std::string & BestHash(
    const std::string & a,
    const std::string & b
)
```

Returns the lexicographically better hash among two values. 

**Parameters**: 

  * **a** First hash candidate. 
  * **b** Second hash candidate. 


**Return**: Reference to the selected hash string. 

### function ~ConsensusManager

```cpp
~ConsensusManager()
```

Destroys the Consensus Manager object. 

### function Close

```cpp
void Close()
```

Close and cleanup members of the Consensus Manager. 

### function RegisterSubjectHandler

```cpp
bool RegisterSubjectHandler(
    std::string_view subject_type,
    SubjectHandler handler
)
```

Registers a subject validation/handling callback by canonical subject type string. 

**Parameters**: 

  * **subject_type** Canonical subject type, e.g. "gnus.bridge_event.v1". 
  * **handler** Callback invoked for matching subject type hash. 


**Return**: `true` when registered, `false` when input is invalid. 

### function UnregisterSubjectHandler

```cpp
void UnregisterSubjectHandler(
    std::string_view subject_type
)
```

Unregisters a subject handler by canonical subject type string. 

**Parameters**: 

  * **subject_type** Canonical subject type associated with the handler. 


### function RegisterCertificateHandler

```cpp
bool RegisterCertificateHandler(
    std::string_view subject_type,
    CertificateSubjectHandler handler
)
```

Registers a certificate handling callback by canonical subject type string. 

**Parameters**: 

  * **subject_type** Canonical subject type associated with certificates. 
  * **handler** Callback invoked for matching certificate subjects. 


**Return**: `true` when registered, `false` when input is invalid. 

### function UnregisterCertificateHandler

```cpp
void UnregisterCertificateHandler(
    std::string_view subject_type
)
```

Unregisters a certificate handler by canonical subject type string. 

**Parameters**: 

  * **subject_type** Canonical subject type associated with the handler. 


### function RegisterProposalCleanupHandler

```cpp
bool RegisterProposalCleanupHandler(
    std::string_view subject_type,
    ProposalCleanupHandler handler
)
```

Registers a proposal cleanup callback by canonical subject type string. 

**Parameters**: 

  * **subject_type** Canonical subject type to handle. 
  * **handler** Callback invoked when a proposal is cleaned up due to timeout. 


**Return**: `true` on successful registration. 

### function UnregisterProposalCleanupHandler

```cpp
void UnregisterProposalCleanupHandler(
    std::string_view subject_type
)
```

Unregisters all proposal cleanup handlers for a canonical subject type string. 

**Parameters**: 

  * **subject_type** Canonical subject type to remove. 


### function SetPendingLifecycleConfig

```cpp
void SetPendingLifecycleConfig(
    PendingLifecycleConfig config
)
```

Overrides local pending lifecycle limits for deterministic tests/configuration. 

**Parameters**: 

  * **config** Pending lifecycle configuration. 


### function Publish

```cpp
outcome::result< void > Publish(
    const ConsensusMessage & message
)
```

Publishes a consensus envelope to pubsub. 

**Parameters**: 

  * **message** Consensus message envelope. 


**Return**: outcome::success on publish success, or an error otherwise. 

### function CreateProposal

```cpp
outcome::result< Proposal > CreateProposal(
    const Subject & subject,
    const std::string & proposer_id,
    const std::string & registry_cid,
    uint64_t registry_epoch
)
```

Builds and signs a proposal using the manager signer. 

**Parameters**: 

  * **subject** Consensus subject to propose. 
  * **proposer_id** Validator identifier of the proposer. 
  * **registry_cid** CID of the validator registry snapshot. 
  * **registry_epoch** Epoch of the validator registry snapshot. 


**Return**: Signed proposal on success, otherwise an error. 

### function CreateVote

```cpp
outcome::result< Vote > CreateVote(
    const std::string & proposal_id,
    const std::string & voter_id,
    bool approve,
    Signer sign
)
```

Builds and signs a vote for a proposal. 

**Parameters**: 

  * **proposal_id** [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) identifier being voted on. 
  * **voter_id** Validator identifier of the voter. 
  * **approve** `true` for approval vote, `false` for rejection vote. 
  * **sign** Signing callback. 


**Return**: Signed vote on success, otherwise an error. 

### function SetSlotHashPopulator

```cpp
inline void SetSlotHashPopulator(
    SlotHashPopulator populator
)
```

Injects the slot-hash populator used by CreateVote (Phase 6, D-01). 

**Parameters**: 

  * **populator** Callback that fills slot_N_hash fields on a vote.



Set by [GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/) during blockchain initialization. When the callback is unset (default), CreateVote skips slot population. 


### function CreateVoteBundle

```cpp
outcome::result< VoteBundle > CreateVoteBundle(
    const std::string & proposal_id,
    const std::string & aggregator_id,
    const std::vector< Vote > & votes,
    Signer sign
)
```

Builds and signs an aggregated vote bundle. 

**Parameters**: 

  * **proposal_id** [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) identifier associated with the votes. 
  * **aggregator_id** Validator identifier of the aggregator. 
  * **votes** Votes to aggregate in the bundle. 
  * **sign** Signing callback. 


**Return**: Signed vote bundle on success, otherwise an error. 

### function CreateCertificate

```cpp
outcome::result< Certificate > CreateCertificate(
    const Proposal & proposal,
    const std::vector< Vote > & votes
)
```

Creates a certificate from a proposal and votes. 

**Parameters**: 

  * **proposal** [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) to certify. 
  * **votes** Votes used for quorum/certificate construction. 


**Return**: [Certificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificate) on success, otherwise an error. 

### function TallyVotes

```cpp
outcome::result< QuorumTally > TallyVotes(
    const Proposal & proposal,
    const std::vector< Vote > & votes,
    const ValidatorRegistry::Registry & registry,
    const std::string & registry_cid
) const
```

Tallies votes against an explicit registry snapshot. 

**Parameters**: 

  * **proposal** [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) being evaluated. 
  * **votes** Votes to tally. 
  * **registry** Registry snapshot used to compute weight. 
  * **registry_cid** Registry CID expected by the proposal. 


**Return**: Quorum tally result or an error. 

### function TallyVotes

```cpp
outcome::result< QuorumTally > TallyVotes(
    const Proposal & proposal,
    const std::vector< Vote > & votes
) const
```

Tallies votes using the manager registry source. 

**Parameters**: 

  * **proposal** [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) being evaluated. 
  * **votes** Votes to tally. 


**Return**: Quorum tally result or an error. 

### function EvaluateQuorum

```cpp
outcome::result< QuorumTally > EvaluateQuorum(
    const Proposal & proposal,
    const std::vector< Vote > & votes,
    const ValidatorRegistry::Registry & registry
) const
```

Phase 6 (D-06): single quorum dispatcher. 

**Parameters**: 

  * **proposal** [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) being evaluated. 
  * **votes** Votes to tally. 
  * **registry** Registry snapshot used for weight resolution. 


**Return**: Quorum tally result. 

For non-bridge subjects: computes the single-pool tally (total weight, approved weight, IsQuorum) &ndash; identical to the pre-Phase-6 behavior. For bridge-mint subjects: delegates to [ValidatorRegistry::EvaluateSlotQuorum](/source-reference/Classes/dc/db9/classsgns_1_1_validator_registry/#function-evaluateslotquorum) (cumulative slot model with 50/25/75 weighting and >=2-validator PUBLIC deduplication).

Used by BOTH TallyVotes (certificate creation) and the incremental HandleVote tally so the two sites agree on bridge-mint quorum (RESEARCH Pitfall 1 mitigation / T-06-10).


### function SubmitProposal

```cpp
outcome::result< void > SubmitProposal(
    const Proposal & proposal,
    bool self_vote =true
)
```

Submits a proposal for local handling and broadcast. 

**Parameters**: 

  * **proposal** [Proposal](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-proposal) to submit. 
  * **self_vote** Whether the local node should auto-vote for its own proposal. 


**Return**: outcome::success on success, otherwise an error. 

### function SubmitVote

```cpp
outcome::result< void > SubmitVote(
    const Vote & vote,
    bool self_handle =true
)
```

Submits a vote for local handling and broadcast. 

**Parameters**: 

  * **vote** [Vote](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-vote) to submit. 
  * **self_handle** Whether the local node should handle the vote immediately. 


**Return**: outcome::success on success, otherwise an error. 

### function SubmitCertificate

```cpp
outcome::result< void > SubmitCertificate(
    const Certificate & certificate
)
```

Submits a certificate for local handling and broadcast. 

**Parameters**: 

  * **certificate** [Certificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificate) to submit. 


**Return**: outcome::success on success, otherwise an error. 

### function ResumeProposalHandling

```cpp
outcome::result< void > ResumeProposalHandling(
    const std::string & subject_hash
)
```

Retries proposal handling once its subject becomes ready. 

**Parameters**: 

  * **subject_hash** [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) hash used to locate pending proposals. 


**Return**: outcome::success on success, otherwise an error. 

### function WakePendingDependency

```cpp
outcome::result< void > WakePendingDependency(
    const PendingDependencyKey & dependency
)
```

Retries pending proposals waiting on a typed dependency key. 

**Parameters**: 

  * **dependency** Dependency key that became available. 


**Return**: outcome::success on success, otherwise an error. 

### function ProcessCertificates

```cpp
void ProcessCertificates()
```

Processes queued certificate work entries. 

### function ConfigureCertificateDelay

```cpp
void ConfigureCertificateDelay(
    std::chrono::milliseconds delay
)
```

Configures local delayed processing for received certificates. 

**Parameters**: 

  * **delay** Delay applied before certificate processing. 


### function GetCertificateBySubjectHash

```cpp
outcome::result< Certificate > GetCertificateBySubjectHash(
    const std::string & subject_hash
) const
```

Retrieves a certificate by subject hash. 

**Parameters**: 

  * **subject_hash** [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) hash key. 


**Return**: [Certificate](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-certificate) when present, or an error. 

### function CheckCertificateForSubject

```cpp
bool CheckCertificateForSubject(
    const std::string & subject_hash
) const
```

Checks whether a certificate exists for a subject hash. 

**Parameters**: 

  * **subject_hash** [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) hash key. 


**Return**: `true` if a certificate exists, otherwise `false`. 

### function CheckCertificateForSubject

```cpp
bool CheckCertificateForSubject(
    const Subject & subject
) const
```

Checks whether a certificate exists for a subject. 

**Parameters**: 

  * **subject** [Subject](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/#using-subject) instance to hash and lookup. 


**Return**: `true` if a certificate exists, otherwise `false`. 

## Protected Functions Documentation

### function ConfigureTimestampWindow

```cpp
void ConfigureTimestampWindow(
    std::chrono::milliseconds window
)
```

Sets timestamp validation window for received objects. 

**Parameters**: 

  * **window** Allowed timestamp drift window. 


### function ConfigureRoundDuration

```cpp
void ConfigureRoundDuration(
    std::chrono::milliseconds duration
)
```

Sets consensus round duration. 

**Parameters**: 

  * **duration** Round duration. 


### function ConfigureRoundSkew

```cpp
void ConfigureRoundSkew(
    std::chrono::milliseconds skew
)
```

Sets allowable round skew tolerance. 

**Parameters**: 

  * **skew** Allowed round skew. 


## Friends

### friend ConsensusManagerTestAccess

```cpp
friend class ConsensusManagerTestAccess(
    ConsensusManagerTestAccess 
);
```


### friend ConsensusPendingLifecycleTestAccess

```cpp
friend class ConsensusPendingLifecycleTestAccess(
    ConsensusPendingLifecycleTestAccess 
);
```


### friend ConsensusSlotKeyTestAccess

```cpp
friend class ConsensusSlotKeyTestAccess(
    ConsensusSlotKeyTestAccess 
);
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/blockchain/Consensus.hpp
summary: Consensus proposal/vote/certificate helpers. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/blockchain/Consensus.hpp



Consensus proposal/vote/certificate helpers.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::ConsensusManager](/source-reference/Classes/d1/d8a/classsgns_1_1_consensus_manager/)** <br/>Implements Consensus with weighted voting.  |
| struct | **[sgns::ConsensusManager::PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/)** <br/>Local-only dependency key for deferred subject validation.  |
| struct | **[sgns::ConsensusManager::PendingDependencyKeyHash](/source-reference/Classes/d3/dbe/structsgns_1_1_consensus_manager_1_1_pending_dependency_key_hash/)** <br/>Hash functor for [PendingDependencyKey](/source-reference/Classes/d9/d37/structsgns_1_1_consensus_manager_1_1_pending_dependency_key/) unordered containers.  |
| struct | **[sgns::ConsensusManager::ValidationResult](/source-reference/Classes/da/d26/structsgns_1_1_consensus_manager_1_1_validation_result/)** <br/>Local structured validation result for subject handlers.  |
| struct | **[sgns::ConsensusManager::PendingLifecycleConfig](/source-reference/Classes/d4/dbf/structsgns_1_1_consensus_manager_1_1_pending_lifecycle_config/)** <br/>Local pending proposal lifecycle limits.  |
| struct | **[sgns::ConsensusManager::QuorumTally](/source-reference/Classes/d1/dce/structsgns_1_1_consensus_manager_1_1_quorum_tally/)** <br/>Quorum tally structure.  |

## Attributes

|                | Name           |
| -------------- | -------------- |
| std::string_view | **[NONCE_SUBJECT_TYPE](/source-reference/Files/d0/dc1/_consensus_8hpp/#variable-nonce_subject_type)**  |
| std::string_view | **[TASK_RESULT_SUBJECT_TYPE](/source-reference/Files/d0/dc1/_consensus_8hpp/#variable-task_result_subject_type)**  |
| std::string_view | **[REGISTRY_BATCH_SUBJECT_TYPE](/source-reference/Files/d0/dc1/_consensus_8hpp/#variable-registry_batch_subject_type)**  |

## Detailed Description

Consensus proposal/vote/certificate helpers. 

**Date**: 2025-10-16 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 


## Attributes Documentation

### variable NONCE_SUBJECT_TYPE

```cpp
static std::string_view NONCE_SUBJECT_TYPE = "sgns.nonce.v1";
```


### variable TASK_RESULT_SUBJECT_TYPE

```cpp
static std::string_view TASK_RESULT_SUBJECT_TYPE = "sgns.task_result.v1";
```


### variable REGISTRY_BATCH_SUBJECT_TYPE

```cpp
static std::string_view REGISTRY_BATCH_SUBJECT_TYPE = "sgns.registry_batch.v1";
```



## Source code

```cpp

#ifndef SGNS_CONSENSUS_HPP
#define SGNS_CONSENSUS_HPP

#include <chrono>
#include <cstdint>
#include <functional>
#include <memory>
#include <optional>
#include <string>
#include <string_view>
#include <shared_mutex>
#include <thread>
#include <vector>
#include <unordered_map>
#include <unordered_set>
#include <mutex>
#include <condition_variable>
#include <atomic>
#include <limits>

#include "blockchain/ValidatorRegistry.hpp"
#include "blockchain/impl/proto/Consensus.pb.h"
#include "crdt/globaldb/crdt_work_journal.hpp"
#include "crdt/globaldb/globaldb.hpp"
#include "crdt/proto/delta.pb.h"
#include "ipfs_pubsub/gossip_pubsub.hpp"
#include "outcome/outcome.hpp"

namespace sgns
{
    static constexpr std::string_view NONCE_SUBJECT_TYPE          = "sgns.nonce.v1";
    static constexpr std::string_view TASK_RESULT_SUBJECT_TYPE    = "sgns.task_result.v1";
    static constexpr std::string_view REGISTRY_BATCH_SUBJECT_TYPE = "sgns.registry_batch.v1";

    class ConsensusManager : public std::enable_shared_from_this<ConsensusManager>
    {
    public:
        using Proposal    = ConsensusProposal;    
        using Vote        = ConsensusVote;        
        using VoteBundle  = ConsensusVoteBundle;  
        using Certificate = ConsensusCertificate; 
        using Subject     = ConsensusSubject;     

        using Signer = std::function<outcome::result<std::vector<uint8_t>>( std::vector<uint8_t> payload )>;

        using SlotHashPopulator = std::function<void( ConsensusVote &vote )>;

        static std::shared_ptr<ConsensusManager> New( std::shared_ptr<ValidatorRegistry>         registry,
                                                      std::shared_ptr<crdt::GlobalDB>            db,
                                                      std::shared_ptr<ipfs_pubsub::GossipPubSub> pubsub,
                                                      Signer                                     signer,
                                                      std::string                                address,
                                                      std::string                                consensus_topic = "" );
        ~ConsensusManager();

        void Close();

        enum class Check
        {
            Approve, 
            Reject,  
            Pending, 
            Stalled  
        };

        struct PendingDependencyKey
        {
            enum class Type
            {
                Certificate, 
            };

            Type        type{ Type::Certificate };
            std::string value;

            bool operator==( const PendingDependencyKey &other ) const
            {
                return type == other.type && value == other.value;
            }

            static PendingDependencyKey Certificate( std::string subject_hash )
            {
                return PendingDependencyKey{ Type::Certificate, std::move( subject_hash ) };
            }
        };

        struct PendingDependencyKeyHash
        {
            std::size_t operator()( const PendingDependencyKey &key ) const
            {
                const auto type_hash  = std::hash<int>{}( static_cast<int>( key.type ) );
                const auto value_hash = std::hash<std::string>{}( key.value );
                return type_hash ^ ( value_hash + 0x9e3779b97f4a7c15ULL + ( type_hash << 6 ) + ( type_hash >> 2 ) );
            }
        };

        struct ValidationResult
        {
            Check                                    check{ Check::Reject };
            std::vector<PendingDependencyKey>        dependencies;
            std::optional<std::chrono::milliseconds> retry_after;

            ValidationResult() = default;

            ValidationResult( Check result ) : check( result )
            {
            }

            static ValidationResult Approve()
            {
                return ValidationResult{ Check::Approve };
            }

            static ValidationResult Reject()
            {
                return ValidationResult{ Check::Reject };
            }

            static ValidationResult Stalled()
            {
                return ValidationResult{ Check::Stalled };
            }

            static ValidationResult Pending( std::vector<PendingDependencyKey>        deps  = {},
                                             std::optional<std::chrono::milliseconds> retry = std::nullopt )
            {
                ValidationResult result{ Check::Pending };
                result.dependencies = std::move( deps );
                result.retry_after  = retry;
                return result;
            }
        };

        struct PendingLifecycleConfig
        {
            std::size_t                            max_pending_proposals         = 1024;
            std::size_t                            max_pending_per_proposer      = 64;
            std::size_t                            max_retained_pending_bytes    = 64ULL * 1024ULL * 1024ULL;
            std::chrono::milliseconds              pending_ttl                   = std::chrono::minutes( 3 );
            std::chrono::milliseconds              min_dependency_retry_interval = std::chrono::seconds( 1 );
            std::vector<std::chrono::milliseconds> scheduled_retry_delays        = { std::chrono::seconds( 1 ),
                                                                                     std::chrono::seconds( 2 ),
                                                                                     std::chrono::seconds( 5 ),
                                                                                     std::chrono::seconds( 10 ) };
        };

        using SubjectHandler = std::function<outcome::result<ValidationResult>( const Subject &subject )>;
        using CertificateSubjectHandler =
            std::function<outcome::result<Check>( const std::string &subject_hash, const Certificate &certificate )>;
        using ProposalCleanupHandler = std::function<void( const std::string &tx_hash )>;
        using SlotKeyHandler = std::function<std::string( const Subject &subject )>;

        struct QuorumTally
        {
            uint64_t total_weight    = 0;     
            uint64_t approved_weight = 0;     
            bool     has_quorum      = false; 
            // Phase 6 (D-06): populated only for bridge-mint subjects; zero for
            // non-bridge subjects (observability -- the slot-tally result).
            uint64_t qualified_sum  = 0;      
            uint64_t slot_threshold = 0;      
        };

        bool RegisterSubjectHandler( std::string_view subject_type, SubjectHandler handler );
        void UnregisterSubjectHandler( std::string_view subject_type );
        bool RegisterCertificateHandler( std::string_view subject_type, CertificateSubjectHandler handler );
        void UnregisterCertificateHandler( std::string_view subject_type );
        bool RegisterProposalCleanupHandler( std::string_view subject_type, ProposalCleanupHandler handler );
        void UnregisterProposalCleanupHandler( std::string_view subject_type );

        void SetPendingLifecycleConfig( PendingLifecycleConfig config );

        static void RegisterSlotKeyHandler( std::string_view subject_type, SlotKeyHandler handler );

        static void UnregisterSlotKeyHandler( std::string_view subject_type );

        outcome::result<void> Publish( const ConsensusMessage &message );

        outcome::result<Proposal> CreateProposal( const Subject     &subject,
                                                  const std::string &proposer_id,
                                                  const std::string &registry_cid,
                                                  uint64_t           registry_epoch );
        static outcome::result<Proposal> CreateProposal( const Subject     &subject,
                                                         const std::string &proposer_id,
                                                         const std::string &registry_cid,
                                                         uint64_t           registry_epoch,
                                                         Signer             sign );

        outcome::result<Vote> CreateVote( const std::string &proposal_id,
                                          const std::string &voter_id,
                                          bool               approve,
                                          Signer             sign );

        void SetSlotHashPopulator( SlotHashPopulator populator )
        {
            slot_hash_populator_ = std::move( populator );
        }

        outcome::result<VoteBundle> CreateVoteBundle( const std::string       &proposal_id,
                                                      const std::string       &aggregator_id,
                                                      const std::vector<Vote> &votes,
                                                      Signer                   sign );

        outcome::result<Certificate> CreateCertificate( const Proposal &proposal, const std::vector<Vote> &votes );

        outcome::result<QuorumTally> TallyVotes( const Proposal                    &proposal,
                                                 const std::vector<Vote>           &votes,
                                                 const ValidatorRegistry::Registry &registry,
                                                 const std::string                 &registry_cid ) const;
        outcome::result<QuorumTally> TallyVotes( const Proposal &proposal, const std::vector<Vote> &votes ) const;

        static bool IsBridgeMintSubject( const Proposal &proposal );

        outcome::result<QuorumTally> EvaluateQuorum( const Proposal                    &proposal,
                                                     const std::vector<Vote>           &votes,
                                                     const ValidatorRegistry::Registry &registry ) const;

        static outcome::result<std::vector<uint8_t>> ProposalSigningBytes( const Proposal &proposal );
        static outcome::result<std::vector<uint8_t>> VoteSigningBytes( const Vote &vote );
        static outcome::result<std::vector<uint8_t>> VoteBundleSigningBytes( const VoteBundle &bundle );
        static outcome::result<std::string> ComputeSubjectId( const Subject &subject );
        static outcome::result<std::string>          ComputeSubjectTypeHash( std::string_view subject_type );
        static outcome::result<NonceSubject>         DecodeNonceSubject( const Subject &subject );
        static outcome::result<TaskResultSubject>    DecodeTaskResultSubject( const Subject &subject );
        static outcome::result<RegistryBatchSubject> DecodeRegistryBatchSubject( const Subject &subject );
        static bool SubjectTypeMatches( const Subject &subject, std::string_view subject_type );
        static outcome::result<Subject> CreateNonceSubject(
            const std::string                             &account_id,
            uint64_t                                       nonce,
            const std::string                             &tx_hash,
            const EmbeddedTransaction                     &transaction,
            const std::optional<UTXOTransitionCommitment> &utxo_commitment,
            const std::optional<UTXOWitness>              &utxo_witness );
        static outcome::result<Subject> CreateTaskResultSubject( const std::string &account_id,
                                                                 const std::string &escrow_path,
                                                                 const std::string &task_result_hash,
                                                                 uint64_t           result_epoch );
        static outcome::result<Subject> CreateRegistryBatchSubject( const std::string &account_id,
                                                                    const std::string &base_registry_cid,
                                                                    uint64_t           base_registry_epoch,
                                                                    uint64_t           target_registry_epoch,
                                                                    uint32_t           certificate_count,
                                                                    const std::string &batch_root );
        static outcome::result<Subject> CreateGenericSubject( const std::string          &account_id,
                                                              std::string_view            subject_type,
                                                              const std::vector<uint8_t> &payload );
        static const std::string &BestHash( const std::string &a, const std::string &b );
        outcome::result<void> SubmitProposal( const Proposal &proposal, bool self_vote = true );
        outcome::result<void> SubmitVote( const Vote &vote, bool self_handle = true );
        outcome::result<void> SubmitCertificate( const Certificate &certificate );
        outcome::result<void> ResumeProposalHandling( const std::string &subject_hash );
        outcome::result<void> WakePendingDependency( const PendingDependencyKey &dependency );
        void ProcessCertificates();
        void ConfigureCertificateDelay( std::chrono::milliseconds delay );

        outcome::result<Certificate> GetCertificateBySubjectHash( const std::string &subject_hash ) const;
        bool CheckCertificateForSubject( const std::string &subject_hash ) const;
        bool CheckCertificateForSubject( const Subject &subject ) const;

    protected:
        void ConfigureTimestampWindow( std::chrono::milliseconds window );
        void ConfigureRoundDuration( std::chrono::milliseconds duration );
        void ConfigureRoundSkew( std::chrono::milliseconds skew );

    private:
        friend class ConsensusManagerTestAccess;
        friend class ConsensusPendingLifecycleTestAccess;
        friend class ConsensusSlotKeyTestAccess;

        explicit ConsensusManager( std::shared_ptr<ValidatorRegistry>         registry,
                                   std::shared_ptr<crdt::GlobalDB>            db,
                                   std::shared_ptr<ipfs_pubsub::GossipPubSub> pubsub,
                                   Signer                                     signer,
                                   std::string                                address,
                                   std::string                                consensus_topic );
        void StartRoundTimer();

        static constexpr std::string_view CONSENSUS_CHANNEL_PREFIX =
            "consensus-channel-"; 
        static constexpr std::string_view CERTIFICATE_BASE_PATH_KEY =
            "/cert/"; 
        static constexpr std::chrono::milliseconds DEFAULT_TIMESTAMP_WINDOW = std::chrono::minutes(
            5 ); 
        static constexpr std::chrono::milliseconds DEFAULT_ROUND_DURATION = std::chrono::milliseconds(
            500 ); 
        static constexpr std::chrono::milliseconds DEFAULT_ROUND_SKEW = std::chrono::milliseconds(
            250 ); 
        static constexpr uint64_t NO_ROUND =
            std::numeric_limits<uint64_t>::max();                             
        static constexpr std::string_view CERT_KEY_PATTERN = "^/?cert/[^/]+"; 

        struct ProposalState
        {
            Proposal                        proposal;                        
            std::vector<Vote>               votes;                           
            std::string                     slot_key;                        
            uint64_t                        total_weight    = 0;             
            uint64_t                        approved_weight = 0;             
            std::unordered_set<std::string> seen_voters;                     
            bool                            quorum_reached       = false;    
            uint64_t                        quorum_reached_ts_ms = 0;        
            uint64_t                        last_attempt_round   = NO_ROUND; 
        };

        struct SlotState
        {
            std::string best_proposal_id; 
            std::string best_tx_hash;     
            bool        voted = false;    
        };

        struct PendingProposalEntry
        {
            Proposal                                 proposal;
            std::vector<PendingDependencyKey>        dependencies;
            std::chrono::steady_clock::time_point    admitted_at;
            std::chrono::steady_clock::time_point    expires_at;
            std::chrono::steady_clock::time_point    next_retry_at;
            std::chrono::steady_clock::time_point    last_retry_at;
            std::optional<std::chrono::milliseconds> retry_after;
            std::size_t                              retained_bytes = 0;
            std::string                              proposer_id;
            std::size_t                              scheduled_retry_count = 0;
        };

        void HandleProposal( const Proposal &proposal );
        void HandleVote( const Vote &vote );
        void HandleVoteBundle( const VoteBundle &bundle );
        void HandleCertificate( const Certificate &certificate );
        void FireProposalCleanupCallbacks( const Proposal &proposal );
        static std::string GetSlotKey( const Proposal &proposal );
        bool IsBetterProposal( const Proposal &candidate, const Proposal &current ) const;
        bool IsTimestampSane( uint64_t timestamp_ms ) const;
        enum class AggregatorRole
        {
            NotInRegistry,          
            ActiveButNotAggregator, 
            CurrentAggregator,      
        };
        AggregatorRole GetAggregatorRole( const Proposal &proposal,
                                          const ValidatorRegistry::Registry &registry ) const;
        std::vector<std::string> GetOrderedActiveValidators( const ValidatorRegistry::Registry &registry ) const;
        uint64_t GetCurrentRound( uint64_t proposal_ts_ms ) const;
        outcome::result<ProposalState> FetchProposalState( const Certificate &certificate );
        ProposalState CreateProposalState( const Certificate &certificate );
        bool ValidateCertificateBestProposal( const ProposalState &state, const Certificate &certificate ) const;
        std::vector<Vote> CollectCertificateVotes( const Certificate &certificate ) const;
        void ClearProposalSlot( const Proposal &proposal );
        static outcome::result<std::string> GetSubjectHash( const Subject &subject );
        void ContinueProposalAfterSubject( const Proposal &proposal );
        bool AddPendingProposal( const Proposal                       &proposal,
                                 const std::string                    &subject_hash,
                                 const ValidationResult               &validation_result = ValidationResult::Pending(),
                                 std::size_t                           scheduled_retry_count = 0,
                                 std::chrono::steady_clock::time_point last_retry_at         = {} );
        bool RemovePendingProposal( const std::string &proposal_id, std::string_view reason );
        std::vector<Proposal> TakePendingProposals( const std::string &subject_hash );
        bool                  RemovePendingProposalLocked( const std::string &proposal_id, std::string_view reason );
        bool                  CanAdmitPendingProposalLocked( const Proposal    &proposal,
                                                             std::size_t        retained_bytes,
                                                             const std::string &proposer_id ) const;
        std::vector<PendingDependencyKey> NormalizePendingDependencies(
            const std::string      &subject_hash,
            const ValidationResult &validation_result ) const;
        std::chrono::milliseconds NextPendingRetryDelayLocked( const PendingProposalEntry &entry ) const;
        void                      RetryPendingProposal( const Proposal                       &proposal,
                                                        std::string_view                      reason,
                                                        std::size_t                           scheduled_retry_count = 0,
                                                        std::chrono::steady_clock::time_point last_retry_at = {} );
        void                      ProcessDuePendingRetries();
        void                      ExpirePendingProposals();
        void AddPendingVote( const Vote &vote );
        std::vector<Vote> TakePendingVotes( const std::string &proposal_id );
        bool RegisterCertificateFilter();
        std::optional<std::vector<crdt::pb::Element>> FilterCertificate( const crdt::pb::Element &element );
        void CertificateReceived( crdt::CRDTCallbackManager::NewDataPair new_data, const std::string &cid );
        void RecoverPendingCertificateWork();
        ConsensusManager::Check ValidateCertificate( const Certificate &certificate ) const;
        static std::string CreateProposalId( const Proposal &proposal );
        static bool SubjectHasValidTypeHash( Subject *subject );
        static bool ValidateSubject( const Subject &subject );

        void OnConsensusMessage( boost::optional<const ipfs_pubsub::GossipPubSub::Message &> message );
        void UpdateCertificatesPending();
        static bool CheckSubject( const Subject &subject );
        static bool CheckProposal( const Proposal &proposal );
        static bool CheckVote( const Vote &vote );
        static std::string                     GetPrintableSubjectHash( const Subject &subject );
        std::shared_ptr<ValidatorRegistry>     registry_; 
        std::shared_ptr<crdt::GlobalDB>        db_;       
        std::shared_ptr<crdt::CRDTWorkJournal> certificate_work_journal_; 
        std::unordered_map<std::string, SubjectHandler>
                                  subject_handlers_;       
        mutable std::shared_mutex subject_handlers_mutex_; 
        std::unordered_map<std::string, CertificateSubjectHandler>
                                  certificate_subject_handlers_; 
        mutable std::shared_mutex certificate_handlers_mutex_;   
        std::unordered_map<std::string, std::vector<ProposalCleanupHandler>>
            proposal_cleanup_handlers_; 
        static inline std::unordered_map<std::string, SlotKeyHandler>
                                  slot_key_handlers_;                 
        static inline std::shared_mutex slot_key_handlers_mutex_;     
        mutable std::shared_mutex cleanup_handlers_mutex_;            
        Signer                    signer_;                            
        SlotHashPopulator         slot_hash_populator_;               
        std::string               account_address_;                   
        std::unordered_map<std::string, ProposalState> proposals_;    
        std::unordered_map<std::string, SlotState>     slot_states_;  
        std::unordered_map<std::string, PendingProposalEntry>
            pending_entries_; 
        std::unordered_map<PendingDependencyKey, std::unordered_set<std::string>, PendingDependencyKeyHash>
            pending_by_dependency_; 
        std::unordered_map<std::string, std::size_t>
                               pending_count_by_proposer_;                   
        std::size_t            pending_retained_bytes_ = 0;                  
        PendingLifecycleConfig pending_config_;                              
        std::unordered_map<std::string, std::vector<Vote>> pending_votes_;   
        mutable std::mutex                                 proposals_mutex_; 
        std::shared_ptr<ipfs_pubsub::GossipPubSub>         pubsub_;          

        std::string consensus_messages_topic_;  
        std::string consensus_datastore_topic_; 
        std::shared_future<std::shared_ptr<ipfs_pubsub::GossipPubSub::Subscription>>
                                  consensus_subs_future_;                        
        std::chrono::milliseconds timestamp_window_{ DEFAULT_TIMESTAMP_WINDOW }; 
        std::chrono::milliseconds certificate_delay_{
            std::chrono::milliseconds( 2000 ) };                             
        std::chrono::milliseconds round_duration_{ DEFAULT_ROUND_DURATION }; 
        std::chrono::milliseconds round_skew_{ DEFAULT_ROUND_SKEW };         
        std::atomic<bool>         stop_timer_{ false };           
        std::atomic<bool>         certificates_pending_{ false }; 
        std::condition_variable   timer_cv_;                      
        std::mutex                timer_mutex_;                   
        std::thread               round_timer_;                   
    };
}

#endif // CONSENSUS_MANAGER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

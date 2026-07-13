---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/AccountMessenger.hpp
summary: Header file of the account messenger class. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/AccountMessenger.hpp



Header file of the account messenger class.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::AccountMessenger](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/)**  |
| struct | **[sgns::AccountMessenger::InterfaceMethods](/source-reference/Classes/dd/d3e/structsgns_1_1_account_messenger_1_1_interface_methods/)** <br/>Interface methods the user needs to define.  |

## Functions

|                | Name           |
| -------------- | -------------- |
| | **[OUTCOME_HPP_DECLARE_ERROR_2](/source-reference/Files/d8/d7a/_account_messenger_8hpp/#function-outcome_hpp_declare_error_2)**([sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/) , AccountMessenger::Error )<br/>Macro for declaring error handling in the AccountMessenger class.  |

## Detailed Description

Header file of the account messenger class. 

**Date**: 2025-07-21 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 

## Functions Documentation

### function OUTCOME_HPP_DECLARE_ERROR_2

```cpp
OUTCOME_HPP_DECLARE_ERROR_2(
    sgns ,
    AccountMessenger::Error 
)
```

Macro for declaring error handling in the AccountMessenger class. 



## Source code

```cpp

#ifndef ACCOUNT_MESSENGER_HPP
#define ACCOUNT_MESSENGER_HPP

#include <string>
#include <memory>
#include <functional>
#include <vector>
#include <future>
#include <condition_variable>
#include <queue>
#include <atomic>
#include <mutex>
#include <unordered_map>
#include <unordered_set>
#include <chrono>
#include <variant>
#include <optional>
#include <random>

#include <boost/optional.hpp>

#include "base/logger.hpp"
#include "ipfs_pubsub/gossip_pubsub.hpp"
#include "outcome/outcome.hpp"
#include "account/proto/SGAccountComm.pb.h"

namespace sgns
{
    class AccountMessenger : public std::enable_shared_from_this<AccountMessenger>
    {
    public:
        enum class Error
        {
            PROTO_DESERIALIZATION = 0, 
            PROTO_SERIALIZATION,       
            NONCE_REQUEST_IN_PROGRESS, 
            NONCE_GET_ERROR,           
            NO_RESPONSE_RECEIVED,      
            RESPONSE_WITHOUT_NONCE,    
            GENESIS_REQUEST_ERROR,     
            UTXO_REQUEST_ERROR,        
        };

        struct InterfaceMethods
        {
            std::function<outcome::result<std::vector<uint8_t>>( std::vector<uint8_t> data )> sign_;

            std::function<outcome::result<bool>( std::string address, std::string sig, std::vector<uint8_t> data )>
                verify_signature_;

            std::function<outcome::result<uint64_t>( std::string address )> get_local_nonce_;

            std::function<outcome::result<std::string>( uint8_t block_index, const std::string &address )>
                get_block_cid_;

            std::function<outcome::result<bool>( const std::string &cid )> has_block_cid_;

            std::function<outcome::result<std::vector<std::string>>( const std::string &address )> get_utxos_;

            std::function<outcome::result<std::optional<uint64_t>>( const std::string &address )> get_validator_weight_;

            std::function<outcome::result<std::string>( const std::string &tx_hash )> get_transaction_cid_;
        };

        // Global block response handler type
        using BlockResponseHandler =
            std::function<bool( const std::string &cid, const std::string &peer_id, const std::string &address )>;

        // Head request handler type: called when a head request is received for topics
        using HeadRequestHandler = std::function<void( const std::set<std::string> &topics )>;

        static std::shared_ptr<AccountMessenger> New( std::string                                address,
                                                      std::shared_ptr<ipfs_pubsub::GossipPubSub> pubsub,
                                                      InterfaceMethods                           methods );
        ~AccountMessenger();
        outcome::result<uint64_t> GetLatestNonce( uint64_t timeout_ms, uint64_t silent_time_ms = 150 );

        outcome::result<void> RequestGenesis( uint64_t                                            timeout_ms,
                                              std::function<void( outcome::result<std::string> )> callback = nullptr );

        outcome::result<void> RequestAccountCreation( uint64_t                                            timeout_ms,
                                                      std::function<void( outcome::result<std::string> )> callback );
        outcome::result<void> RequestValidatorRegistry( uint64_t                                            timeout_ms,
                                                        std::function<void( outcome::result<std::string> )> callback );

        outcome::result<void> RequestRegularBlock(
            uint64_t                                            timeout_ms,
            std::string                                         cid,
            std::function<void( outcome::result<std::string> )> callback = nullptr );

        outcome::result<void> RequestTransaction(
            uint64_t                                            timeout_ms,
            std::string                                         tx_hash,
            std::function<void( outcome::result<std::string> )> callback = nullptr );

        outcome::result<std::unordered_set<std::string>> RequestUTXOs( uint64_t           timeout_ms,
                                                                       const std::string &address,
                                                                       uint64_t           silent_time_ms = 150 );

        void RegisterBlockResponseHandler( BlockResponseHandler handler );

        void ClearBlockResponseHandler();

        void RegisterHeadRequestHandler( HeadRequestHandler handler );

        void ClearHeadRequestHandler();

        outcome::result<void> RequestHeads( const std::unordered_set<std::string> &topics );

    private:
        static constexpr std::string_view ACCOUNT_COMM = ".comm";
        static constexpr std::string_view REQUESTS_COMM = "SGNUS.BC.Requests.comm";

        struct BlockIndexRequest
        {
            uint8_t block_index{ 0 };
        };

        struct BlockCidRequest
        {
            std::string cid;
        };

        struct TransactionHashRequest
        {
            std::string tx_hash;
        };

        using BlockQuery = std::variant<BlockIndexRequest, BlockCidRequest, TransactionHashRequest>;

        const std::string                          address_;            
        const std::string                          account_comm_topic_; 
        const std::string                          requests_topic_;     
        std::shared_ptr<ipfs_pubsub::GossipPubSub> pubsub_;             

        std::shared_future<std::shared_ptr<ipfs_pubsub::GossipPubSub::Subscription>> subs_acc_future_;
        std::shared_future<std::shared_ptr<ipfs_pubsub::GossipPubSub::Subscription>> subs_requests_future_;

        std::unordered_map<uint64_t, std::set<uint64_t>> nonce_responses_; 
        std::unordered_map<uint64_t, std::set<std::string>>
            no_nonce_responses_; 
        std::unordered_map<uint64_t, std::chrono::steady_clock::time_point>
                   first_response_time_;   
        std::mutex nonce_responses_mutex_; 

        // Block responses storage for account/genesis requests
        std::unordered_map<uint64_t, std::set<std::string>> block_responses_; 
        std::unordered_map<uint64_t, std::chrono::steady_clock::time_point>
                   block_first_response_time_; 
        std::mutex block_responses_mutex_;     

        struct UTXOResponseData
        {
            std::string                     responder_address;
            std::unordered_set<std::string> utxos;
            bool                            has_utxos{ false };
        };

        std::unordered_map<uint64_t, std::vector<UTXOResponseData>>         utxo_responses_;
        std::unordered_map<uint64_t, std::chrono::steady_clock::time_point> utxo_first_response_time_;
        std::mutex                                                          utxo_responses_mutex_;

        InterfaceMethods methods_; 

        std::random_device rd_; 

        BlockResponseHandler global_block_handler_;
        std::mutex           global_handler_mutex_;

        HeadRequestHandler head_request_handler_;
        std::mutex         head_handler_mutex_;

        // Worker thread state
        enum class RequestType : std::uint8_t
        {
            Nonce,
            Genesis,
            AccountCreation,
            ValidatorRegistry,
            BlockByCid,
            UTXO,
            Transaction
        };

        struct RequestTask
        {
            RequestType                                                                     type;
            uint64_t                                                                        timeout_ms;
            uint64_t                                                                        silent_time_ms{ 150 };
            uint8_t                                                                         block_index{ 0 };
            std::string                                                                     cid;
            std::string                                                                     utxo_address;
            std::function<void( outcome::result<std::string> )>                             callback;
            std::shared_ptr<std::promise<outcome::result<uint64_t>>>                        nonce_promise;
            std::shared_ptr<std::promise<outcome::result<std::unordered_set<std::string>>>> utxo_promise;
        };

        std::thread             worker_thread_;
        std::mutex              queue_mutex_;
        std::condition_variable queue_cv_;
        std::queue<RequestTask> request_queue_;
        std::atomic<bool>       stop_worker_{ false };

        void                                   WorkerLoop();
        void                                   EnqueueTask( RequestTask task );
        outcome::result<uint64_t>              PerformNonceRequest( uint64_t timeout_ms, uint64_t silent_time_ms );
        outcome::result<std::set<std::string>> PerformBlockRequest( uint64_t timeout_ms, const BlockQuery &query );
        outcome::result<std::unordered_set<std::string>> PerformUTXORequest( uint64_t           timeout_ms,
                                                                             const std::string &address,
                                                                             uint64_t           silent_time_ms );

        AccountMessenger( std::string                                address,
                          std::shared_ptr<ipfs_pubsub::GossipPubSub> pubsub,
                          InterfaceMethods                           methods );
        outcome::result<void> RequestNonce( uint64_t req_id );

        outcome::result<void> RequestBlock( uint64_t req_id, uint8_t block_index );

        outcome::result<void> RequestBlockByCid( uint64_t req_id, const std::string &cid );
        outcome::result<void> RequestBlockByHash( uint64_t req_id, const std::string &tx_hash );
        outcome::result<void> RequestUTXO( uint64_t req_id, const std::string &address );

        void OnResponse( boost::optional<const ipfs_pubsub::GossipPubSub::Message &> message );
        void OnRequest( boost::optional<const ipfs_pubsub::GossipPubSub::Message &> message );
        outcome::result<void> SendAccountMessage( const accountComm::AccountMessage &msg,
                                                  const std::set<std::string>       &topics );

        void HandleNonceRequest( const accountComm::SignedNonceRequest &req );
        void HandleNonceResponse( const accountComm::SignedNonceResponse &resp );

        void HandleBlockRequest( const accountComm::SignedBlockRequest &req );
        void HandleBlockCidRequest( const accountComm::SignedBlockCidRequest &req );
        void HandleBlockResponse( const accountComm::SignedBlockResponse &resp );
        void HandleTransactionRequest( const accountComm::SignedTransactionRequest &req );
        void HandleBlockLikeRequest( const BlockQuery  &query,
                                     const std::string &requester_address,
                                     uint64_t           request_id );

        void HandleHeadRequest( const accountComm::SignedHeadRequest &req );

        void HandleUTXORequest( const accountComm::SignedUTXORequest &req );

        void HandleUTXOResponse( const accountComm::SignedUTXOResponse &resp );

        base::Logger logger_ = sgns::base::createLogger( "AccountMessenger" );
    };
}

OUTCOME_HPP_DECLARE_ERROR_2( sgns, AccountMessenger::Error );

#endif // ACCOUNT_MESSENGER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/Migration3_6_0To3_7_0.hpp
summary: Migration step that upgrades account and balance data from schema version 3.6.0 to 3.7.0. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/Migration3_6_0To3_7_0.hpp



Migration step that upgrades account and balance data from schema version 3.6.0 to 3.7.0.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::Migration3_6_0To3_7_0](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/)** <br/>Executes the 3.6.0 to 3.7.0 migration, including legacy balance recovery.  |

## Detailed Description

Migration step that upgrades account and balance data from schema version 3.6.0 to 3.7.0. 

**Date**: 2026-05-06 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef SGNS_MIGRATION_3_6_0_TO_3_7_0_HPP
#define SGNS_MIGRATION_3_6_0_TO_3_7_0_HPP

#include "IMigrationStep.hpp"
#include "base/logger.hpp"
#include "blockchain/Blockchain.hpp"
#include "crdt/globaldb/globaldb.hpp"

#include <atomic>
#include <memory>
#include <utility>
#include <vector>

namespace sgns
{
    class GeniusAccount;
    class TransactionManager;

    class Migration3_6_0To3_7_0 : public IMigrationStep, public std::enable_shared_from_this<Migration3_6_0To3_7_0>
    {
    public:
        using AddressBalance = std::pair<std::string, uint64_t>;

        Migration3_6_0To3_7_0( std::shared_ptr<boost::asio::io_context>                        ioContext,
                               std::shared_ptr<ipfs_pubsub::GossipPubSub>                      pubSub,
                               std::shared_ptr<ipfs_lite::ipfs::graphsync::Network>            graphsync,
                               std::shared_ptr<libp2p::basic::Scheduler>                       scheduler,
                               std::shared_ptr<ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator,
                               std::string                                                     writeBasePath,
                               std::string                                                     base58key,
                               std::shared_ptr<GeniusAccount>                                  account,
                               bool                                                            is_full_node );

        std::string FromVersion() const override;
        std::string ToVersion() const override;
        outcome::result<void> Init() override;
        outcome::result<void> Apply() override;
        outcome::result<void> ShutDown() override;
        outcome::result<bool> IsRequired() const override;

    private:
        enum class Status
        {
            ST_INIT = 0, 
            ST_ERROR,    
            ST_SUCCESS,  
        };

        outcome::result<std::shared_ptr<crdt::GlobalDB>> InitLegacyDb() const;
        outcome::result<std::shared_ptr<crdt::GlobalDB>> InitTargetDb() const;
        outcome::result<std::vector<AddressBalance>> ComputeLegacyBalances() const;

        base::Logger logger_ = base::createLogger( "MigrationStep" ); 

        std::shared_ptr<boost::asio::io_context>             ioContext_; 
        std::shared_ptr<ipfs_pubsub::GossipPubSub>           pubSub_;    
        std::shared_ptr<ipfs_lite::ipfs::graphsync::Network> graphsync_; 
        std::shared_ptr<libp2p::basic::Scheduler>            scheduler_; 
        std::shared_ptr<ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator_; 
        std::string writeBasePath_;                                                 
        std::string base58key_;                                                     

        std::shared_ptr<crdt::GlobalDB>     db_3_6_0_;            
        std::shared_ptr<crdt::GlobalDB>     db_3_7_0_;            
        std::shared_ptr<Blockchain>         blockchain_;          
        std::shared_ptr<TransactionManager> transaction_manager_; 
        std::shared_ptr<GeniusAccount>      account_;             
        bool                                is_full_node_ = false; 
        std::atomic<Status>                 blockchain_status_{ Status::ST_INIT }; 
    };
}

#endif // SGNS_MIGRATION_3_6_0_TO_3_7_0_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

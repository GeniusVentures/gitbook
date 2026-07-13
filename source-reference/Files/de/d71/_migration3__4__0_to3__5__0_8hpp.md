---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/Migration3_4_0To3_5_0.hpp
summary: Migration step that upgrades account data from schema version 3.4.0 to 3.5.0. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/Migration3_4_0To3_5_0.hpp



Migration step that upgrades account data from schema version 3.4.0 to 3.5.0.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::Migration3_4_0To3_5_0](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/)** <br/>Migration step for version 3.4.0 to 3.5.0. Updates persisted data required by the 3.5.0 node layout.  |

## Detailed Description

Migration step that upgrades account data from schema version 3.4.0 to 3.5.0. 

**Date**: 2025-11-11 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef SGNS_MIGRATION_3_4_0_TO_3_5_0_HPP
#define SGNS_MIGRATION_3_4_0_TO_3_5_0_HPP

#include <string>
#include <memory>
#include <atomic>

#include "IMigrationStep.hpp"
#include "blockchain/Blockchain.hpp"
#include "crdt/globaldb/globaldb.hpp"
#include "outcome/outcome.hpp"
#include "base/logger.hpp"

namespace sgns
{
    class GeniusAccount;

    class Migration3_4_0To3_5_0 : public IMigrationStep, public std::enable_shared_from_this<Migration3_4_0To3_5_0>
    {
    public:
        Migration3_4_0To3_5_0( std::shared_ptr<boost::asio::io_context>                        ioContext,
                               std::shared_ptr<ipfs_pubsub::GossipPubSub>                      pubSub,
                               std::shared_ptr<ipfs_lite::ipfs::graphsync::Network>            graphsync,
                               std::shared_ptr<libp2p::basic::Scheduler>                       scheduler,
                               std::shared_ptr<ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator,
                               std::string                                                     writeBasePath,
                               std::string                                                     base58key,
                               std::shared_ptr<GeniusAccount>                                  account );

        ~Migration3_4_0To3_5_0() override;

        std::string FromVersion() const override;

        std::string ToVersion() const override;

        outcome::result<void> Init() override;

        outcome::result<bool> IsRequired() const override;

        outcome::result<void> Apply() override;

        outcome::result<void> ShutDown() override;

    private:
        enum class Status
        {
            ST_INIT = 0, 
            ST_ERROR,    
            ST_SUCCESS,  
        };

        outcome::result<std::shared_ptr<crdt::GlobalDB>> InitLegacyDb();

        outcome::result<std::shared_ptr<crdt::GlobalDB>> InitTargetDb();

        std::shared_ptr<boost::asio::io_context>             ioContext_; 
        std::shared_ptr<ipfs_pubsub::GossipPubSub>           pubSub_;    
        std::shared_ptr<ipfs_lite::ipfs::graphsync::Network> graphsync_; 
        std::shared_ptr<libp2p::basic::Scheduler>            scheduler_; 
        std::shared_ptr<ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator_; 
        std::string                     writeBasePath_;                             
        std::string                     base58key_;                                 
        base::Logger                    logger_ = base::createLogger( "MigrationStep" ); 
        std::shared_ptr<crdt::GlobalDB> db_3_5_0_;                                       
        std::shared_ptr<crdt::GlobalDB> db_3_4_0_;                                       
        std::shared_ptr<Blockchain>     blockchain_; 
        std::shared_ptr<GeniusAccount>  account_;    
        std::atomic<Status>             blockchain_status_{ Status::ST_INIT }; 
    };

}

#endif // SGNS_MIGRATION_3_4_0_TO_3_5_0_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

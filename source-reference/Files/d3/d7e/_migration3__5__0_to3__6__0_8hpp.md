---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/Migration3_5_0To3_6_0.hpp
summary: Migration step that upgrades account data from schema version 3.5.1 to 3.6.0. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/Migration3_5_0To3_6_0.hpp



Migration step that upgrades account data from schema version 3.5.1 to 3.6.0.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::Migration3_5_0To3_6_0](/source-reference/Classes/d8/d7f/classsgns_1_1_migration3__5__0_to3__6__0/)** <br/>Executes the storage migration from database version 3.5.1 to 3.6.0.  |

## Detailed Description

Migration step that upgrades account data from schema version 3.5.1 to 3.6.0. 

**Date**: 2026-01-22 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef SGNS_MIGRATION_3_5_0_TO_3_6_0_HPP
#define SGNS_MIGRATION_3_5_0_TO_3_6_0_HPP

#include "IMigrationStep.hpp"
#include "base/logger.hpp"
#include "crdt/globaldb/globaldb.hpp"
#include <memory>

namespace sgns
{
    class Migration3_5_0To3_6_0 : public IMigrationStep, public std::enable_shared_from_this<Migration3_5_0To3_6_0>
    {
    public:
        Migration3_5_0To3_6_0( std::shared_ptr<boost::asio::io_context>                        ioContext,
                               std::shared_ptr<ipfs_pubsub::GossipPubSub>                      pubSub,
                               std::shared_ptr<ipfs_lite::ipfs::graphsync::Network>            graphsync,
                               std::shared_ptr<libp2p::basic::Scheduler>                       scheduler,
                               std::shared_ptr<ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator,
                               std::string                                                     writeBasePath,
                               std::string                                                     base58key );

        std::string FromVersion() const override;
        std::string ToVersion() const override;
        outcome::result<void> Init() override;
        outcome::result<void> Apply() override;
        outcome::result<void> ShutDown() override;
        outcome::result<bool> IsRequired() const override;

    private:
        outcome::result<std::shared_ptr<crdt::GlobalDB>> InitLegacyDb() const;
        outcome::result<std::shared_ptr<crdt::GlobalDB>> InitTargetDb() const;

        base::Logger logger_ = base::createLogger( "MigrationStep" ); 

        std::shared_ptr<boost::asio::io_context>             ioContext_; 
        std::shared_ptr<ipfs_pubsub::GossipPubSub>           pubSub_;    
        std::shared_ptr<ipfs_lite::ipfs::graphsync::Network> graphsync_; 
        std::shared_ptr<libp2p::basic::Scheduler>            scheduler_; 
        std::shared_ptr<ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator_; 
        std::string writeBasePath_;                                                 
        std::string base58key_;                                                     

        std::shared_ptr<crdt::GlobalDB> db_3_5_1_; 
        std::shared_ptr<crdt::GlobalDB> db_3_6_0_; 
    };
}

#endif // SGNS_MIGRATION_3_5_0_TO_3_6_0_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/Migration1_0_0To3_4_0.hpp
summary: Header file for Migration1_0_0To3_4_0 class. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/Migration1_0_0To3_4_0.hpp



Header file for Migration1_0_0To3_4_0 class.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::Migration1_0_0To3_4_0](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/)** <br/>Migration step for version 1.0.0 to 3.4.0. Changes the full node topic from CRDT heads.  |

## Detailed Description

Header file for Migration1_0_0To3_4_0 class. 

**Date**: 2025-10-03 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef SGNS_MIGRATION_1_0_0_TO_3_4_0_HPP
#define SGNS_MIGRATION_1_0_0_TO_3_4_0_HPP

#include <string>
#include <memory>

#include "IMigrationStep.hpp"
#include "crdt/globaldb/globaldb.hpp"
#include "outcome/outcome.hpp"
#include "base/logger.hpp"

namespace sgns
{
    class Migration1_0_0To3_4_0 : public IMigrationStep
    {
    public:
        Migration1_0_0To3_4_0( std::shared_ptr<boost::asio::io_context>                        ioContext,
                               std::shared_ptr<ipfs_pubsub::GossipPubSub>                      pubSub,
                               std::shared_ptr<ipfs_lite::ipfs::graphsync::Network>            graphsync,
                               std::shared_ptr<libp2p::basic::Scheduler>                       scheduler,
                               std::shared_ptr<ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator,
                               std::string                                                     writeBasePath,
                               std::string                                                     base58key );
        ~Migration1_0_0To3_4_0();

        std::string FromVersion() const override;

        std::string ToVersion() const override;

        outcome::result<void> Init() override;

        outcome::result<bool> IsRequired() const override;

        outcome::result<void> Apply() override;

        outcome::result<void> ShutDown() override;

    private:
        outcome::result<std::shared_ptr<crdt::GlobalDB>>                InitLegacyDb();
        outcome::result<std::shared_ptr<crdt::GlobalDB>>                InitTargetDb();
        std::shared_ptr<boost::asio::io_context>                        ioContext_; 
        std::shared_ptr<ipfs_pubsub::GossipPubSub>                      pubSub_;    
        std::shared_ptr<ipfs_lite::ipfs::graphsync::Network>            graphsync_; 
        std::shared_ptr<libp2p::basic::Scheduler>                       scheduler_; 
        std::shared_ptr<ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator_; 
        std::string                     writeBasePath_;                             
        std::string                     base58key_;                                 
        base::Logger                    logger_ = base::createLogger( "MigrationStep" ); 
        std::shared_ptr<crdt::GlobalDB> db_3_4_0_;                                       
        std::shared_ptr<crdt::GlobalDB> db_1_0_0_;                                       
    };

}

#endif // SGNS_MIGRATION_1_0_0_TO_3_4_0_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/Migration0_2_0To1_0_0.hpp
summary: Versioned migration manager and migration step interface. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/Migration0_2_0To1_0_0.hpp



Versioned migration manager and migration step interface.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::Migration0_2_0To1_0_0](/source-reference/Classes/d9/d5c/classsgns_1_1_migration0__2__0_to1__0__0/)** <br/>Migration step for version 0.2.0 to 1.0.0.  |

## Detailed Description

Versioned migration manager and migration step interface. 

**Date**: 2025-05-29 Luiz Guilherme Rizzatto Zucchi Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp


#ifndef SGNS_MIGRATION_0_2_0_TO_1_0_0_HPP
#define SGNS_MIGRATION_0_2_0_TO_1_0_0_HPP

#include <memory>
#include <string>
#include <deque>
#include <cstdint>

#include <boost/asio/io_context.hpp>
#include <ipfs_pubsub/gossip_pubsub_topic.hpp>
#include "base/logger.hpp"
#include "upnp.hpp"
#include "crdt/globaldb/globaldb.hpp"
#include "outcome/outcome.hpp"
#include <ipfs_lite/ipfs/graphsync/impl/network/network.hpp>
#include <ipfs_lite/ipfs/graphsync/impl/local_requests.hpp>
#include <libp2p/basic/scheduler/asio_scheduler_backend.hpp>

#include "IMigrationStep.hpp"

namespace sgns
{
    class Migration0_2_0To1_0_0 : public IMigrationStep
    {
    public:
        Migration0_2_0To1_0_0( std::shared_ptr<boost::asio::io_context>                        ioContext,
                               std::shared_ptr<ipfs_pubsub::GossipPubSub>                      pubSub,
                               std::shared_ptr<ipfs_lite::ipfs::graphsync::Network>            graphsync,
                               std::shared_ptr<libp2p::basic::Scheduler>                       scheduler,
                               std::shared_ptr<ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator,
                               std::string                                                     writeBasePath,
                               std::string                                                     base58key );

        std::string FromVersion() const override;

        std::string ToVersion() const override;

        outcome::result<void> Init() override;

        outcome::result<bool> IsRequired() const override;

        outcome::result<void> Apply() override;

        outcome::result<void> ShutDown() override;

    private:
        outcome::result<std::shared_ptr<crdt::GlobalDB>> InitTargetDb();

        outcome::result<std::shared_ptr<crdt::GlobalDB>> InitLegacyDb( const std::string &suffix );

        outcome::result<uint32_t> MigrateDb( const std::shared_ptr<crdt::GlobalDB> &oldDb,
                                             const std::shared_ptr<crdt::GlobalDB> &newDb );

        std::shared_ptr<crdt::GlobalDB>                                 db_1_0_0_;     
        std::shared_ptr<crdt::GlobalDB>                                 db_0_0_2_out_; 
        std::shared_ptr<crdt::GlobalDB>                                 db_0_0_2_in_;  
        std::shared_ptr<boost::asio::io_context>                        ioContext_;    
        std::shared_ptr<ipfs_pubsub::GossipPubSub>                      pubSub_;    
        std::shared_ptr<ipfs_lite::ipfs::graphsync::Network>            graphsync_; 
        std::shared_ptr<libp2p::basic::Scheduler>                       scheduler_; 
        std::shared_ptr<ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator_; 
        std::shared_ptr<crdt::AtomicTransaction> crdt_transaction_; 
        std::string                              writeBasePath_;    
        std::string                              base58key_;        
        std::unordered_set<std::string>          topics_;
        base::Logger m_logger = base::createLogger( "MigrationStep" ); 
    };
} // namespace sgns

#endif // SGNS_MIGRATION_0_2_0_TO_1_0_0_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

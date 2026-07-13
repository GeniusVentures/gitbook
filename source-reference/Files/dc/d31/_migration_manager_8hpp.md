---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/MigrationManager.hpp
summary: Versioned migration manager. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/MigrationManager.hpp



Versioned migration manager.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::MigrationManager](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/)** <br/>Executes a sequence of migration steps to update a CRDT store.  |

## Functions

|                | Name           |
| -------------- | -------------- |
| | **[OUTCOME_HPP_DECLARE_ERROR_2](/source-reference/Files/dc/d31/_migration_manager_8hpp/#function-outcome_hpp_declare_error_2)**([sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/) , MigrationManager::Error ) |

## Detailed Description

Versioned migration manager. 

**Date**: 2025-05-29 Luiz Guilherme Rizzatto Zucchi Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 

## Functions Documentation

### function OUTCOME_HPP_DECLARE_ERROR_2

```cpp
OUTCOME_HPP_DECLARE_ERROR_2(
    sgns ,
    MigrationManager::Error 
)
```




## Source code

```cpp


#ifndef SGNS_MIGRATION_MANAGER_HPP
#define SGNS_MIGRATION_MANAGER_HPP

#include <memory>
#include <deque>
#include <atomic>
#include <string>

#include <boost/asio/io_context.hpp>
#include <ipfs_pubsub/gossip_pubsub_topic.hpp>
#include "base/logger.hpp"
#include "outcome/outcome.hpp"
#include <ipfs_lite/ipfs/graphsync/impl/network/network.hpp>
#include <ipfs_lite/ipfs/graphsync/impl/local_requests.hpp>
#include <libp2p/basic/scheduler/asio_scheduler_backend.hpp>

#include "IMigrationStep.hpp"

namespace sgns
{
    class GeniusAccount;

    class MigrationManager : public std::enable_shared_from_this<MigrationManager>
    {
    public:
        enum class Error: uint8_t
        {
            BLOCKCHAIN_INIT_FAILED = 1,
        };
        static std::shared_ptr<MigrationManager> New(
            std::shared_ptr<boost::asio::io_context>                        ioContext,
            std::shared_ptr<ipfs_pubsub::GossipPubSub>                      pubSub,
            std::shared_ptr<ipfs_lite::ipfs::graphsync::Network>            graphsync,
            std::shared_ptr<libp2p::basic::Scheduler>                       scheduler,
            std::shared_ptr<ipfs_lite::ipfs::graphsync::RequestIdGenerator> generator,
            std::string                                                     writeBasePath,
            std::string                                                     base58key,
            std::shared_ptr<GeniusAccount>                                  account,
            bool                                                            is_full_node );

        void RegisterStep( std::shared_ptr<IMigrationStep> step );

        outcome::result<void> Migrate();

        size_t GetCurrentStepIndex() const
        {
            return current_step_index_.load();
        }

        size_t GetTotalSteps() const
        {
            return total_steps_;
        }

        std::string GetCurrentStepDescription() const;

        static constexpr std::string_view VERSION_INFO_KEY = "kSGNSCRDTVersion";

    private:
        MigrationManager();

        std::deque<std::shared_ptr<IMigrationStep>> steps_;               
        base::Logger m_logger = base::createLogger( "MigrationManager" ); 

        std::atomic<size_t> current_step_index_{ 0 }; 
        size_t              total_steps_{ 0 };        
    };
} // namespace sgns

OUTCOME_HPP_DECLARE_ERROR_2( sgns, MigrationManager::Error );

#endif // SGNS_MIGRATION_MANAGER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

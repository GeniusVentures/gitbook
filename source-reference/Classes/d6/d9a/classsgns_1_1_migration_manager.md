---
title: sgns::MigrationManager
summary: Executes a sequence of migration steps to update a CRDT store. 

---

# sgns::MigrationManager



Executes a sequence of migration steps to update a CRDT store. 


`#include <MigrationManager.hpp>`

Inherits from std::enable_shared_from_this< MigrationManager >

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class uint8_t | **[Error](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/#enum-error)** { BLOCKCHAIN_INIT_FAILED = 1} |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [MigrationManager](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/#function-migrationmanager) > | **[New](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/#function-new)**(std::shared_ptr< boost::asio::io_context > ioContext, std::shared_ptr< ipfs_pubsub::GossipPubSub > pubSub, std::shared_ptr< ipfs_lite::ipfs::graphsync::Network > graphsync, std::shared_ptr< libp2p::basic::Scheduler > scheduler, std::shared_ptr< ipfs_lite::ipfs::graphsync::RequestIdGenerator > generator, std::string writeBasePath, std::string base58key, std::shared_ptr< [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/) > account, bool is_full_node)<br/>Factory function to create a [MigrationManager](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/) and register all known steps.  |
| void | **[RegisterStep](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/#function-registerstep)**(std::shared_ptr< [IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/) > step)<br/>Register a migration step.  |
| outcome::result< void > | **[Migrate](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/#function-migrate)**()<br/>Perform all registered migration steps in sequence.  |
| size_t | **[GetCurrentStepIndex](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/#function-getcurrentstepindex)**() const |
| size_t | **[GetTotalSteps](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/#function-gettotalsteps)**() const |
| std::string | **[GetCurrentStepDescription](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/#function-getcurrentstepdescription)**() const |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::string_view | **[VERSION_INFO_KEY](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/#variable-version_info_key)**  |

## Public Types Documentation

### enum Error

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| BLOCKCHAIN_INIT_FAILED | 1|   |




## Public Functions Documentation

### function New

```cpp
static std::shared_ptr< MigrationManager > New(
    std::shared_ptr< boost::asio::io_context > ioContext,
    std::shared_ptr< ipfs_pubsub::GossipPubSub > pubSub,
    std::shared_ptr< ipfs_lite::ipfs::graphsync::Network > graphsync,
    std::shared_ptr< libp2p::basic::Scheduler > scheduler,
    std::shared_ptr< ipfs_lite::ipfs::graphsync::RequestIdGenerator > generator,
    std::string writeBasePath,
    std::string base58key,
    std::shared_ptr< GeniusAccount > account,
    bool is_full_node
)
```

Factory function to create a [MigrationManager](/source-reference/Classes/d6/d9a/classsgns_1_1_migration_manager/) and register all known steps. 

**Parameters**: 

  * **ioContext** Shared io_context for both legacy and new DB. 
  * **pubSub** Shared GossipPubSub instance. 
  * **graphsync** Shared GraphSync network object. 
  * **scheduler** Shared libp2p scheduler. 
  * **generator** Shared GraphSync request ID generator. 
  * **writeBasePath** Base path for writing DB files. 
  * **base58key** Key to build legacy paths. 
  * **account** [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/) used during migration (if required). 


**Return**: std::shared_ptr<MigrationManager> to the created instance. 

### function RegisterStep

```cpp
void RegisterStep(
    std::shared_ptr< IMigrationStep > step
)
```

Register a migration step. 

**Parameters**: 

  * **step** [IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/) to add. 


### function Migrate

```cpp
outcome::result< void > Migrate()
```

Perform all registered migration steps in sequence. 

**Return**: Outcome of the migration process. 

### function GetCurrentStepIndex

```cpp
inline size_t GetCurrentStepIndex() const
```


**Return**: 1-based index of the migration step currently being processed, or 0 if not started. 

### function GetTotalSteps

```cpp
inline size_t GetTotalSteps() const
```


**Return**: Total number of registered migration steps. 

### function GetCurrentStepDescription

```cpp
std::string GetCurrentStepDescription() const
```


**Return**: Human-readable description of the current migration step. 

## Public Attributes Documentation

### variable VERSION_INFO_KEY

```cpp
static std::string_view VERSION_INFO_KEY = "kSGNSCRDTVersion";
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
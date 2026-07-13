---
title: sgns::Migration3_4_0To3_5_0
summary: Migration step for version 3.4.0 to 3.5.0. Updates persisted data required by the 3.5.0 node layout. 

---

# sgns::Migration3_4_0To3_5_0



Migration step for version 3.4.0 to 3.5.0. Updates persisted data required by the 3.5.0 node layout. 


`#include <Migration3_4_0To3_5_0.hpp>`

Inherits from [sgns::IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/), std::enable_shared_from_this< Migration3_4_0To3_5_0 >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[Migration3_4_0To3_5_0](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-migration3_4_0to3_5_0)**(std::shared_ptr< boost::asio::io_context > ioContext, std::shared_ptr< ipfs_pubsub::GossipPubSub > pubSub, std::shared_ptr< ipfs_lite::ipfs::graphsync::Network > graphsync, std::shared_ptr< libp2p::basic::Scheduler > scheduler, std::shared_ptr< ipfs_lite::ipfs::graphsync::RequestIdGenerator > generator, std::string writeBasePath, std::string base58key, std::shared_ptr< [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/) > account)<br/>Constructs the migration step with the services required to read and write both database versions.  |
| | **[~Migration3_4_0To3_5_0](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-~migration3_4_0to3_5_0)**() override<br/>Destroys the migration step.  |
| virtual std::string | **[FromVersion](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-fromversion)**() const override<br/>Returns the source schema version handled by this step.  |
| virtual std::string | **[ToVersion](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-toversion)**() const override<br/>Returns the target schema version produced by this step.  |
| virtual outcome::result< void > | **[Init](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-init)**() override<br/>Initializes migration resources before the step is applied.  |
| virtual outcome::result< bool > | **[IsRequired](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-isrequired)**() const override<br/>Determines whether the 3.4.0 to 3.5.0 migration must run.  |
| virtual outcome::result< void > | **[Apply](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-apply)**() override<br/>Applies the migration and writes the upgraded transaction state.  |
| virtual outcome::result< void > | **[ShutDown](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-shutdown)**() override<br/>Releases resources allocated during migration.  |

## Additional inherited members

**Public Functions inherited from [sgns::IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-~imigrationstep)**() =default |
| std::tuple< int, int, int > | **[ParseVersion](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-parseversion)**(const std::string & version) const |
| bool | **[IsVersionLessThan](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-isversionlessthan)**(const std::string & lhs, const std::string & rhs) const |


## Public Functions Documentation

### function Migration3_4_0To3_5_0

```cpp
Migration3_4_0To3_5_0(
    std::shared_ptr< boost::asio::io_context > ioContext,
    std::shared_ptr< ipfs_pubsub::GossipPubSub > pubSub,
    std::shared_ptr< ipfs_lite::ipfs::graphsync::Network > graphsync,
    std::shared_ptr< libp2p::basic::Scheduler > scheduler,
    std::shared_ptr< ipfs_lite::ipfs::graphsync::RequestIdGenerator > generator,
    std::string writeBasePath,
    std::string base58key,
    std::shared_ptr< GeniusAccount > account
)
```

Constructs the migration step with the services required to read and write both database versions. 

**Parameters**: 

  * **ioContext** Shared IO context used by GlobalDB and migration services. 
  * **pubSub** PubSub service used by the legacy and target GlobalDB instances. 
  * **graphsync** GraphSync network used for CRDT data exchange. 
  * **scheduler** libp2p scheduler used by GraphSync. 
  * **generator** Request ID generator used by GraphSync. 
  * **writeBasePath** Base path containing versioned node database directories. 
  * **base58key** Base58 node key suffix used to locate the legacy and target databases. 
  * **account** Local account used to configure target storage and sign filler transactions. 


### function ~Migration3_4_0To3_5_0

```cpp
~Migration3_4_0To3_5_0() override
```

Destroys the migration step. 

### function FromVersion

```cpp
virtual std::string FromVersion() const override
```

Returns the source schema version handled by this step. 

**Return**: Source version string, "3.4.0". 

**Reimplements**: [sgns::IMigrationStep::FromVersion](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-fromversion)


### function ToVersion

```cpp
virtual std::string ToVersion() const override
```

Returns the target schema version produced by this step. 

**Return**: Target version string, "3.5.0". 

**Reimplements**: [sgns::IMigrationStep::ToVersion](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-toversion)


### function Init

```cpp
virtual outcome::result< void > Init() override
```

Initializes migration resources before the step is applied. 

**Return**: Success after opening the legacy database and, when present, the target database. 

**Reimplements**: [sgns::IMigrationStep::Init](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-init)


### function IsRequired

```cpp
virtual outcome::result< bool > IsRequired() const override
```

Determines whether the 3.4.0 to 3.5.0 migration must run. 

**Return**: True when the target database is older than 3.5.0 or has no version marker; false otherwise. 

**Reimplements**: [sgns::IMigrationStep::IsRequired](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-isrequired)


### function Apply

```cpp
virtual outcome::result< void > Apply() override
```

Applies the migration and writes the upgraded transaction state. 

**Return**: Success when the migration is complete or no legacy database exists; failure on database, blockchain initialization, serialization, or commit errors. 

**Reimplements**: [sgns::IMigrationStep::Apply](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-apply)


Configures account storage against the target database, starts the target blockchain, migrates transactions for all monitored networks, synthesizes zero-value mint transactions for missing local nonces, commits sync topics in batches, and records the target version on success. Transactions that cannot be fetched or validated are skipped.


### function ShutDown

```cpp
virtual outcome::result< void > ShutDown() override
```

Releases resources allocated during migration. 

**Return**: Success after deconfiguring account storage and releasing database and blockchain references. 

**Reimplements**: [sgns::IMigrationStep::ShutDown](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-shutdown)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
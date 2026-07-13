---
title: sgns::Migration3_6_0To3_7_0
summary: Executes the 3.6.0 to 3.7.0 migration, including legacy balance recovery. 

---

# sgns::Migration3_6_0To3_7_0



Executes the 3.6.0 to 3.7.0 migration, including legacy balance recovery. 


`#include <Migration3_6_0To3_7_0.hpp>`

Inherits from [sgns::IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/), std::enable_shared_from_this< Migration3_6_0To3_7_0 >

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::pair< std::string, uint64_t > | **[AddressBalance](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#using-addressbalance)** <br/>Address and balance pair recovered from the legacy database.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[Migration3_6_0To3_7_0](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-migration3_6_0to3_7_0)**(std::shared_ptr< boost::asio::io_context > ioContext, std::shared_ptr< ipfs_pubsub::GossipPubSub > pubSub, std::shared_ptr< ipfs_lite::ipfs::graphsync::Network > graphsync, std::shared_ptr< libp2p::basic::Scheduler > scheduler, std::shared_ptr< ipfs_lite::ipfs::graphsync::RequestIdGenerator > generator, std::string writeBasePath, std::string base58key, std::shared_ptr< [GeniusAccount](/source-reference/Classes/dc/d64/classsgns_1_1_genius_account/) > account, bool is_full_node)<br/>Constructs the migration step with access to legacy and target storage plus account services.  |
| virtual std::string | **[FromVersion](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-fromversion)**() const override<br/>Returns the source schema version handled by this step.  |
| virtual std::string | **[ToVersion](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-toversion)**() const override<br/>Returns the target schema version produced by this step.  |
| virtual outcome::result< void > | **[Init](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-init)**() override<br/>Initializes migration resources before applying the step.  |
| virtual outcome::result< void > | **[Apply](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-apply)**() override<br/>Applies the migration and writes the upgraded balance state.  |
| virtual outcome::result< void > | **[ShutDown](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-shutdown)**() override<br/>Releases resources allocated during migration.  |
| virtual outcome::result< bool > | **[IsRequired](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-isrequired)**() const override<br/>Determines whether the 3.6.0 to 3.7.0 migration must run.  |

## Additional inherited members

**Public Functions inherited from [sgns::IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-~imigrationstep)**() =default |
| std::tuple< int, int, int > | **[ParseVersion](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-parseversion)**(const std::string & version) const |
| bool | **[IsVersionLessThan](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-isversionlessthan)**(const std::string & lhs, const std::string & rhs) const |


## Public Types Documentation

### using AddressBalance

```cpp
using sgns::Migration3_6_0To3_7_0::AddressBalance = std::pair<std::string, uint64_t>;
```

Address and balance pair recovered from the legacy database. 

## Public Functions Documentation

### function Migration3_6_0To3_7_0

```cpp
Migration3_6_0To3_7_0(
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

Constructs the migration step with access to legacy and target storage plus account services. 

**Parameters**: 

  * **ioContext** Shared IO context used by GlobalDB and migration services. 
  * **pubSub** PubSub service used by the migrated GlobalDB instances. 
  * **graphsync** GraphSync network used for CRDT data exchange. 
  * **scheduler** libp2p scheduler used by GraphSync. 
  * **generator** Request ID generator used by GraphSync. 
  * **writeBasePath** Base path containing versioned node database directories. 
  * **base58key** Base58 node key suffix used to locate the legacy and target databases. 
  * **account** Local account used to configure storage and submit the migration claim. 
  * **is_full_node** Whether the node is running as a full node during migration. 


### function FromVersion

```cpp
virtual std::string FromVersion() const override
```

Returns the source schema version handled by this step. 

**Return**: Source version string, "3.6.0". 

**Reimplements**: [sgns::IMigrationStep::FromVersion](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-fromversion)


### function ToVersion

```cpp
virtual std::string ToVersion() const override
```

Returns the target schema version produced by this step. 

**Return**: Target version string, "3.7.0". 

**Reimplements**: [sgns::IMigrationStep::ToVersion](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-toversion)


### function Init

```cpp
virtual outcome::result< void > Init() override
```

Initializes migration resources before applying the step. 

**Return**: Success after opening the legacy database and, when present, the target database. 

**Reimplements**: [sgns::IMigrationStep::Init](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-init)


### function Apply

```cpp
virtual outcome::result< void > Apply() override
```

Applies the migration and writes the upgraded balance state. 

**Return**: Success when the migration is complete or no legacy database exists; failure on database, blockchain initialization, transaction confirmation, or serialization errors. 

**Reimplements**: [sgns::IMigrationStep::Apply](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-apply)


Migrates blockchain CIDs, computes legacy balances, persists the migration allow-list, submits a local migration claim when this account has a legacy balance, and records the target version on success.


### function ShutDown

```cpp
virtual outcome::result< void > ShutDown() override
```

Releases resources allocated during migration. 

**Return**: Success after stopping migration services and releasing database references. 

**Reimplements**: [sgns::IMigrationStep::ShutDown](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-shutdown)


### function IsRequired

```cpp
virtual outcome::result< bool > IsRequired() const override
```

Determines whether the 3.6.0 to 3.7.0 migration must run. 

**Return**: True when the target database is older than 3.7.0 or has no version marker; false otherwise. 

**Reimplements**: [sgns::IMigrationStep::IsRequired](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-isrequired)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
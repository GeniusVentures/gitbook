---
title: sgns::Migration1_0_0To3_4_0
summary: Migration step for version 1.0.0 to 3.4.0. Changes the full node topic from CRDT heads. 

---

# sgns::Migration1_0_0To3_4_0



Migration step for version 1.0.0 to 3.4.0. Changes the full node topic from CRDT heads. 


`#include <Migration1_0_0To3_4_0.hpp>`

Inherits from [sgns::IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[Migration1_0_0To3_4_0](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-migration1_0_0to3_4_0)**(std::shared_ptr< boost::asio::io_context > ioContext, std::shared_ptr< ipfs_pubsub::GossipPubSub > pubSub, std::shared_ptr< ipfs_lite::ipfs::graphsync::Network > graphsync, std::shared_ptr< libp2p::basic::Scheduler > scheduler, std::shared_ptr< ipfs_lite::ipfs::graphsync::RequestIdGenerator > generator, std::string writeBasePath, std::string base58key) |
| | **[~Migration1_0_0To3_4_0](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-~migration1_0_0to3_4_0)**() |
| virtual std::string | **[FromVersion](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-fromversion)**() const override<br/>Get the source version for this step.  |
| virtual std::string | **[ToVersion](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-toversion)**() const override<br/>Get the target version for this step.  |
| virtual outcome::result< void > | **[Init](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-init)**() override<br/>Initializes internal variables after constructor.  |
| virtual outcome::result< bool > | **[IsRequired](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-isrequired)**() const override<br/>Check if this migration should run.  |
| virtual outcome::result< void > | **[Apply](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-apply)**() override<br/>Apply the migration: initialize legacy DBs and migrate data.  |
| virtual outcome::result< void > | **[ShutDown](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-shutdown)**() override<br/>Shuts down internal variables.  |

## Additional inherited members

**Public Functions inherited from [sgns::IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-~imigrationstep)**() =default |
| std::tuple< int, int, int > | **[ParseVersion](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-parseversion)**(const std::string & version) const |
| bool | **[IsVersionLessThan](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-isversionlessthan)**(const std::string & lhs, const std::string & rhs) const |


## Public Functions Documentation

### function Migration1_0_0To3_4_0

```cpp
Migration1_0_0To3_4_0(
    std::shared_ptr< boost::asio::io_context > ioContext,
    std::shared_ptr< ipfs_pubsub::GossipPubSub > pubSub,
    std::shared_ptr< ipfs_lite::ipfs::graphsync::Network > graphsync,
    std::shared_ptr< libp2p::basic::Scheduler > scheduler,
    std::shared_ptr< ipfs_lite::ipfs::graphsync::RequestIdGenerator > generator,
    std::string writeBasePath,
    std::string base58key
)
```


### function ~Migration1_0_0To3_4_0

```cpp
~Migration1_0_0To3_4_0()
```


### function FromVersion

```cpp
virtual std::string FromVersion() const override
```

Get the source version for this step. 

**Return**: std::string "1.0.0" 

**Reimplements**: [sgns::IMigrationStep::FromVersion](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-fromversion)


### function ToVersion

```cpp
virtual std::string ToVersion() const override
```

Get the target version for this step. 

**Return**: std::string "3.4.0" 

**Reimplements**: [sgns::IMigrationStep::ToVersion](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-toversion)


### function Init

```cpp
virtual outcome::result< void > Init() override
```

Initializes internal variables after constructor. 

**Return**: Outcome of the operation 

**Reimplements**: [sgns::IMigrationStep::Init](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-init)


### function IsRequired

```cpp
virtual outcome::result< bool > IsRequired() const override
```

Check if this migration should run. 

**Return**: outcome::result<bool> true if migration should run; false to skip. On error, returns failure. 

**Reimplements**: [sgns::IMigrationStep::IsRequired](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-isrequired)


### function Apply

```cpp
virtual outcome::result< void > Apply() override
```

Apply the migration: initialize legacy DBs and migrate data. 

**Return**: outcome::result<void> success on completion; failure on error. 

**Reimplements**: [sgns::IMigrationStep::Apply](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-apply)


### function ShutDown

```cpp
virtual outcome::result< void > ShutDown() override
```

Shuts down internal variables. 

**Return**: Outcome of the operation 

**Reimplements**: [sgns::IMigrationStep::ShutDown](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-shutdown)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
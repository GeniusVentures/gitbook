---
title: sgns::IMigrationStep
summary: Interface for a migration step between two schema versions. 

---

# sgns::IMigrationStep



Interface for a migration step between two schema versions. 


`#include <IMigrationStep.hpp>`

Inherited by [sgns::Migration0_2_0To1_0_0](/source-reference/Classes/d9/d5c/classsgns_1_1_migration0__2__0_to1__0__0/), [sgns::Migration1_0_0To3_4_0](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/), [sgns::Migration3_4_0To3_5_0](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/), [sgns::Migration3_5_0To3_6_0](/source-reference/Classes/d8/d7f/classsgns_1_1_migration3__5__0_to3__6__0/), [sgns::Migration3_6_0To3_7_0](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-~imigrationstep)**() =default |
| virtual std::string | **[FromVersion](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-fromversion)**() const =0<br/>Get the version from which the migration starts.  |
| virtual std::string | **[ToVersion](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-toversion)**() const =0<br/>Get the version to which the migration applies.  |
| virtual outcome::result< void > | **[Init](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-init)**() =0<br/>Initializes internal variables after constructor.  |
| virtual outcome::result< void > | **[Apply](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-apply)**() =0<br/>Execute the migration logic.  |
| virtual outcome::result< void > | **[ShutDown](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-shutdown)**() =0<br/>Shuts down internal variables.  |
| virtual outcome::result< bool > | **[IsRequired](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-isrequired)**() const =0<br/>Check if migration is required.  |
| std::tuple< int, int, int > | **[ParseVersion](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-parseversion)**(const std::string & version) const |
| bool | **[IsVersionLessThan](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/#function-isversionlessthan)**(const std::string & lhs, const std::string & rhs) const |

## Public Functions Documentation

### function ~IMigrationStep

```cpp
virtual ~IMigrationStep() =default
```


### function FromVersion

```cpp
virtual std::string FromVersion() const =0
```

Get the version from which the migration starts. 

**Return**: The source version string. 

**Reimplemented by**: [sgns::Migration0_2_0To1_0_0::FromVersion](/source-reference/Classes/d9/d5c/classsgns_1_1_migration0__2__0_to1__0__0/#function-fromversion), [sgns::Migration1_0_0To3_4_0::FromVersion](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-fromversion), [sgns::Migration3_4_0To3_5_0::FromVersion](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-fromversion), [sgns::Migration3_5_0To3_6_0::FromVersion](/source-reference/Classes/d8/d7f/classsgns_1_1_migration3__5__0_to3__6__0/#function-fromversion), [sgns::Migration3_6_0To3_7_0::FromVersion](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-fromversion)


### function ToVersion

```cpp
virtual std::string ToVersion() const =0
```

Get the version to which the migration applies. 

**Return**: The target version string. 

**Reimplemented by**: [sgns::Migration0_2_0To1_0_0::ToVersion](/source-reference/Classes/d9/d5c/classsgns_1_1_migration0__2__0_to1__0__0/#function-toversion), [sgns::Migration1_0_0To3_4_0::ToVersion](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-toversion), [sgns::Migration3_4_0To3_5_0::ToVersion](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-toversion), [sgns::Migration3_5_0To3_6_0::ToVersion](/source-reference/Classes/d8/d7f/classsgns_1_1_migration3__5__0_to3__6__0/#function-toversion), [sgns::Migration3_6_0To3_7_0::ToVersion](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-toversion)


### function Init

```cpp
virtual outcome::result< void > Init() =0
```

Initializes internal variables after constructor. 

**Return**: Outcome of the operation 

**Reimplemented by**: [sgns::Migration0_2_0To1_0_0::Init](/source-reference/Classes/d9/d5c/classsgns_1_1_migration0__2__0_to1__0__0/#function-init), [sgns::Migration1_0_0To3_4_0::Init](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-init), [sgns::Migration3_4_0To3_5_0::Init](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-init), [sgns::Migration3_5_0To3_6_0::Init](/source-reference/Classes/d8/d7f/classsgns_1_1_migration3__5__0_to3__6__0/#function-init), [sgns::Migration3_6_0To3_7_0::Init](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-init)


### function Apply

```cpp
virtual outcome::result< void > Apply() =0
```

Execute the migration logic. 

**Return**: Outcome of the operation. 

**Reimplemented by**: [sgns::Migration0_2_0To1_0_0::Apply](/source-reference/Classes/d9/d5c/classsgns_1_1_migration0__2__0_to1__0__0/#function-apply), [sgns::Migration1_0_0To3_4_0::Apply](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-apply), [sgns::Migration3_4_0To3_5_0::Apply](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-apply), [sgns::Migration3_5_0To3_6_0::Apply](/source-reference/Classes/d8/d7f/classsgns_1_1_migration3__5__0_to3__6__0/#function-apply), [sgns::Migration3_6_0To3_7_0::Apply](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-apply)


### function ShutDown

```cpp
virtual outcome::result< void > ShutDown() =0
```

Shuts down internal variables. 

**Return**: Outcome of the operation 

**Reimplemented by**: [sgns::Migration0_2_0To1_0_0::ShutDown](/source-reference/Classes/d9/d5c/classsgns_1_1_migration0__2__0_to1__0__0/#function-shutdown), [sgns::Migration1_0_0To3_4_0::ShutDown](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-shutdown), [sgns::Migration3_4_0To3_5_0::ShutDown](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-shutdown), [sgns::Migration3_5_0To3_6_0::ShutDown](/source-reference/Classes/d8/d7f/classsgns_1_1_migration3__5__0_to3__6__0/#function-shutdown), [sgns::Migration3_6_0To3_7_0::ShutDown](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-shutdown)


### function IsRequired

```cpp
virtual outcome::result< bool > IsRequired() const =0
```

Check if migration is required. 

**Return**: outcome::result<bool> true if migration should run; false to skip. On error, returns failure. 

**Reimplemented by**: [sgns::Migration0_2_0To1_0_0::IsRequired](/source-reference/Classes/d9/d5c/classsgns_1_1_migration0__2__0_to1__0__0/#function-isrequired), [sgns::Migration1_0_0To3_4_0::IsRequired](/source-reference/Classes/d0/d09/classsgns_1_1_migration1__0__0_to3__4__0/#function-isrequired), [sgns::Migration3_4_0To3_5_0::IsRequired](/source-reference/Classes/d1/dd2/classsgns_1_1_migration3__4__0_to3__5__0/#function-isrequired), [sgns::Migration3_5_0To3_6_0::IsRequired](/source-reference/Classes/d8/d7f/classsgns_1_1_migration3__5__0_to3__6__0/#function-isrequired), [sgns::Migration3_6_0To3_7_0::IsRequired](/source-reference/Classes/db/d7d/classsgns_1_1_migration3__6__0_to3__7__0/#function-isrequired)


### function ParseVersion

```cpp
inline std::tuple< int, int, int > ParseVersion(
    const std::string & version
) const
```


### function IsVersionLessThan

```cpp
inline bool IsVersionLessThan(
    const std::string & lhs,
    const std::string & rhs
) const
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
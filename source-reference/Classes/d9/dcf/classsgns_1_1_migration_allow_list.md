---
title: sgns::MigrationAllowList
summary: Stores observed legacy balances and validates migration claim eligibility. 

---

# sgns::MigrationAllowList



Stores observed legacy balances and validates migration claim eligibility. 


`#include <MigrationAllowList.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::pair< std::string, uint64_t > | **[AddressBalance](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/#using-addressbalance)** <br/>Address and observed balance pair stored in the migration allow-list.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[MigrationAllowList](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/#function-migrationallowlist)**(std::shared_ptr< [storage::rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/) > db, std::string migration_version)<br/>Creates an allow-list view scoped to a specific migration version.  |
| outcome::result< void > | **[StoreObservedBalance](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/#function-storeobservedbalance)**(const std::string & address, uint64_t balance)<br/>Persists the observed legacy balance for a single address.  |
| outcome::result< void > | **[StoreObservedBalances](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/#function-storeobservedbalances)**(const std::vector< [AddressBalance](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/#using-addressbalance) > & balances)<br/>Persists observed legacy balances for multiple addresses.  |
| outcome::result< std::optional< uint64_t > > | **[LoadObservedBalance](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/#function-loadobservedbalance)**(const std::string & address) const<br/>Loads the observed legacy balance for a single address when present.  |
| outcome::result< bool > | **[IsEligible](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/#function-iseligible)**(const std::string & address, uint64_t claimed_balance) const<br/>Checks whether an address may claim the provided migrated balance.  |
| outcome::result< std::vector< [AddressBalance](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/#using-addressbalance) > > | **[ListObservedBalances](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/#function-listobservedbalances)**() const<br/>Lists every stored observed balance in the current migration namespace.  |
| std::string | **[BuildPrefix](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/#function-buildprefix)**(std::string_view migration_version)<br/>Builds the RocksDB key prefix used for a migration version namespace.  |
| std::string | **[BuildKey](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/#function-buildkey)**(std::string_view migration_version, std::string_view address)<br/>Builds the RocksDB key used for a specific address inside a migration namespace.  |

## Friends

|                | Name           |
| -------------- | -------------- |
| class | **[::MigrationParamTest](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/#friend-migrationparamtest)**  |

## Public Types Documentation

### using AddressBalance

```cpp
using sgns::MigrationAllowList::AddressBalance = std::pair<std::string, uint64_t>;
```

Address and observed balance pair stored in the migration allow-list. 

## Public Functions Documentation

### function MigrationAllowList

```cpp
MigrationAllowList(
    std::shared_ptr< storage::rocksdb > db,
    std::string migration_version
)
```

Creates an allow-list view scoped to a specific migration version. 

**Parameters**: 

  * **db** RocksDB instance used to persist and query observed balances. 
  * **migration_version** Source migration version namespace, for example "3.6.0". 


### function StoreObservedBalance

```cpp
outcome::result< void > StoreObservedBalance(
    const std::string & address,
    uint64_t balance
)
```

Persists the observed legacy balance for a single address. 

**Parameters**: 

  * **address** Legacy source address whose balance was observed. 
  * **balance** Observed balance for `address`. 


**Return**: Success when the balance is written, or a database error on failure. 

### function StoreObservedBalances

```cpp
outcome::result< void > StoreObservedBalances(
    const std::vector< AddressBalance > & balances
)
```

Persists observed legacy balances for multiple addresses. 

**Parameters**: 

  * **balances** Address and balance pairs to persist. 


**Return**: Success when every balance is written, or the first write error encountered. 

### function LoadObservedBalance

```cpp
outcome::result< std::optional< uint64_t > > LoadObservedBalance(
    const std::string & address
) const
```

Loads the observed legacy balance for a single address when present. 

**Parameters**: 

  * **address** Legacy source address to look up. 


**Return**: Optional observed balance; empty when no allow-list entry exists for `address`. 

### function IsEligible

```cpp
outcome::result< bool > IsEligible(
    const std::string & address,
    uint64_t claimed_balance
) const
```

Checks whether an address may claim the provided migrated balance. 

**Parameters**: 

  * **address** Legacy source address making the migration claim. 
  * **claimed_balance** Balance claimed by the migration transaction. 


**Return**: True when `address` exists in the allow-list and `claimed_balance` is no more than twice the observed balance. 

**Note**: The maximum allowed claim saturates at `std::numeric_limits<uint64_t>::max()` to avoid overflow. 

### function ListObservedBalances

```cpp
outcome::result< std::vector< AddressBalance > > ListObservedBalances() const
```

Lists every stored observed balance in the current migration namespace. 

**Return**: Address and balance pairs sorted by address. 

### function BuildPrefix

```cpp
static std::string BuildPrefix(
    std::string_view migration_version
)
```

Builds the RocksDB key prefix used for a migration version namespace. 

**Parameters**: 

  * **migration_version** Source migration version namespace. 


**Return**: Key prefix for all allow-list entries under `migration_version`. 

### function BuildKey

```cpp
static std::string BuildKey(
    std::string_view migration_version,
    std::string_view address
)
```

Builds the RocksDB key used for a specific address inside a migration namespace. 

**Parameters**: 

  * **migration_version** Source migration version namespace. 
  * **address** Legacy source address. 


**Return**: Full allow-list key for `address` under `migration_version`. 

## Friends

### friend ::MigrationParamTest

```cpp
friend class ::MigrationParamTest(
    ::MigrationParamTest 
);
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
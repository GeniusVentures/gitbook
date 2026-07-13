---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/MigrationAllowList.hpp
summary: Persistent allow-list used to track balances eligible for migration claims. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/MigrationAllowList.hpp



Persistent allow-list used to track balances eligible for migration claims.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::MigrationAllowList](/source-reference/Classes/d9/dcf/classsgns_1_1_migration_allow_list/)** <br/>Stores observed legacy balances and validates migration claim eligibility.  |

## Detailed Description

Persistent allow-list used to track balances eligible for migration claims. 

**Date**: 2026-05-01 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef SGNS_MIGRATION_ALLOW_LIST_HPP
#define SGNS_MIGRATION_ALLOW_LIST_HPP

#include "base/buffer.hpp"
#include "base/logger.hpp"
#include "outcome/outcome.hpp"
#include "storage/rocksdb/rocksdb.hpp"

#include <cstdint>
#include <memory>
#include <optional>
#include <string>
#include <utility>
#include <vector>

class MigrationParamTest;

namespace sgns
{
    class MigrationAllowList
    {
    public:
        using AddressBalance = std::pair<std::string, uint64_t>;

        MigrationAllowList( std::shared_ptr<storage::rocksdb> db, std::string migration_version );

        outcome::result<void>                    StoreObservedBalance( const std::string &address, uint64_t balance );

        outcome::result<void>                    StoreObservedBalances( const std::vector<AddressBalance> &balances );

        outcome::result<std::optional<uint64_t>> LoadObservedBalance( const std::string &address ) const;

        outcome::result<bool>                    IsEligible( const std::string &address, uint64_t claimed_balance ) const;

        outcome::result<std::vector<AddressBalance>> ListObservedBalances() const;

        static std::string BuildPrefix( std::string_view migration_version );

        static std::string BuildKey( std::string_view migration_version, std::string_view address );

    private:
        friend class ::MigrationParamTest;

        static void SetEligibilityCheckEnabledForTests( bool enabled );

        static bool IsEligibilityCheckEnabledForTests();

        static outcome::result<uint64_t> DecodeBalance( const base::Buffer &buffer );

        std::shared_ptr<storage::rocksdb> db_;                 
        std::string                       migration_version_;  
        std::string                       prefix_;             
        base::Logger                      logger_ = base::createLogger( "MigrationAllowList" ); 
    };
}

#endif // SGNS_MIGRATION_ALLOW_LIST_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

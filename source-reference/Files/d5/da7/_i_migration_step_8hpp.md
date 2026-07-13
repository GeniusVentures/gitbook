---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/IMigrationStep.hpp
summary: Versioned migration manager and migration step interface. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/IMigrationStep.hpp



Versioned migration manager and migration step interface.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::IMigrationStep](/source-reference/Classes/d5/d0d/classsgns_1_1_i_migration_step/)** <br/>Interface for a migration step between two schema versions.  |

## Detailed Description

Versioned migration manager and migration step interface. 

**Date**: 2025-05-29 Luiz Guilherme Rizzatto Zucchi Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp


#ifndef SGNS_IMIGRATION_STEP_HPP
#define SGNS_IMIGRATION_STEP_HPP

#include <string>
#include <tuple>
#include <sstream>
#include "outcome/outcome.hpp"

namespace sgns
{
    class IMigrationStep
    {
    public:
        virtual ~IMigrationStep() = default;

        virtual std::string FromVersion() const = 0;

        virtual std::string ToVersion() const = 0;

        virtual outcome::result<void> Init() = 0;
        virtual outcome::result<void> Apply() = 0;

        virtual outcome::result<void> ShutDown() = 0;

        virtual outcome::result<bool> IsRequired() const = 0;

        std::tuple<int, int, int> ParseVersion( const std::string &version ) const
        {
            int                major = 0, minor = 0, patch = 0;
            char               dot;
            std::istringstream iss( version );
            iss >> major >> dot >> minor >> dot >> patch;
            return { major, minor, patch };
        }

        bool IsVersionLessThan( const std::string &lhs, const std::string &rhs ) const
        {
            auto [lhs_major, lhs_minor, lhs_patch] = ParseVersion( lhs );
            auto [rhs_major, rhs_minor, rhs_patch] = ParseVersion( rhs );
            if ( lhs_major != rhs_major )
            {
                return lhs_major < rhs_major;
            }
            if ( lhs_minor != rhs_minor )
            {
                return lhs_minor < rhs_minor;
            }
            return lhs_patch < rhs_patch;
        }
    };
} // namespace sgns

#endif // SGNS_IMIGRATION_STEP_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

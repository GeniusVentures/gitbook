---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/MigrationInputValidator.hpp
summary: Input validation strategy for one-time migration claims. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/MigrationInputValidator.hpp



Input validation strategy for one-time migration claims.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::MigrationInputValidator](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/)** <br/>Implements the InputValidator for a Migration type.  |

## Attributes

|                | Name           |
| -------------- | -------------- |
| bool | **[kMigrationValidatorRegistered](/source-reference/Files/d2/d7f/_migration_input_validator_8hpp/#variable-kmigrationvalidatorregistered)** <br/>Static instance to trigger registration of the [MigrationInputValidator](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/) before main() starts.  |

## Detailed Description

Input validation strategy for one-time migration claims. 

**Date**: 2026-06-12 


## Attributes Documentation

### variable kMigrationValidatorRegistered

```cpp
static bool kMigrationValidatorRegistered = MigrationInputValidator::Register();
```

Static instance to trigger registration of the [MigrationInputValidator](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/) before main() starts. 


## Source code

```cpp

#ifndef SGNS_MIGRATION_INPUT_VALIDATOR_HPP
#define SGNS_MIGRATION_INPUT_VALIDATOR_HPP

#include "account/InputValidators.hpp"

namespace sgns
{
    class MigrationInputValidator final : public IInputValidator
    {
    public:
        bool ValidateUTXOParameters( const UTXOTxParameters &params,
                                     const std::string      &address,
                                     const UTXOManager      &utxo_manager ) const override;

        bool ValidateWitness( const ConsensusSubject                   &subject,
                              const std::shared_ptr<GeniusTransaction> &tx,
                              const UTXOTxParameters                   &params,
                              const std::shared_ptr<Blockchain>        &blockchain ) const override;

        bool RequiresConsensusUTXOData() const override
        {
            return false;
        }

        static bool Register()
        {
            static MigrationInputValidator instance;
            IInputValidator::Register( "migration", &instance );
            return true;
        }
    };

    static inline bool kMigrationValidatorRegistered = MigrationInputValidator::Register();
} // namespace sgns

#endif // SGNS_MIGRATION_INPUT_VALIDATOR_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

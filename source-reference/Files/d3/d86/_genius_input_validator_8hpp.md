---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/GeniusInputValidator.hpp
summary: Input validation strategy for native Genius-chain transactions. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/GeniusInputValidator.hpp



Input validation strategy for native Genius-chain transactions.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::GeniusInputValidator](/source-reference/Classes/dd/d55/classsgns_1_1_genius_input_validator/)** <br/>Validator for native Genius-chain transactions.  |

## Attributes

|                | Name           |
| -------------- | -------------- |
| bool | **[kGeniusValidatorRegistered](/source-reference/Files/d3/d86/_genius_input_validator_8hpp/#variable-kgeniusvalidatorregistered)**  |

## Detailed Description

Input validation strategy for native Genius-chain transactions. 

**Date**: 2026-06-02 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 


## Attributes Documentation

### variable kGeniusValidatorRegistered

```cpp
static bool kGeniusValidatorRegistered = GeniusInputValidator::Register();
```



## Source code

```cpp

#ifndef SGNS_GENIUS_INPUT_VALIDATOR_HPP
#define SGNS_GENIUS_INPUT_VALIDATOR_HPP

#include <memory>

#include "account/InputValidators.hpp"

namespace sgns
{
    class GeniusInputValidator final : public IInputValidator
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
            return true;
        }

        static bool Register()
        {
            static GeniusInputValidator instance;
            IInputValidator::Register( "supergenius", &instance );
            IInputValidator::Register( "supergenius_chain", &instance );
            IInputValidator::Register( "", &instance );
            return true;
        }
    };

    static inline bool kGeniusValidatorRegistered = GeniusInputValidator::Register();
} // namespace sgns

#endif // SGNS_GENIUS_INPUT_VALIDATOR_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

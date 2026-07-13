---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/hasher/hasher_impl.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/hasher/hasher_impl.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crypto](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crypto::HasherImpl](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/)**  |




## Source code

```cpp
#ifndef SUPERGENIUS_SRC_CRYPTO_HASHER_HASHER_IMPL_HPP_
#define SUPERGENIUS_SRC_CRYPTO_HASHER_HASHER_IMPL_HPP_

#include "crypto/hasher.hpp"

namespace sgns::crypto
{
    class HasherImpl : public Hasher
    {
    public:
        using Hasher::sha2_256;

        ~HasherImpl() override = default;

        [[nodiscard]] Hash64 twox_64( gsl::span<const uint8_t> buffer ) const override;

        [[nodiscard]] Hash128 twox_128( gsl::span<const uint8_t> buffer ) const override;

        [[nodiscard]] Hash128 blake2b_128( gsl::span<const uint8_t> buffer ) const override;

        [[nodiscard]] Hash256 twox_256( gsl::span<const uint8_t> buffer ) const override;

        [[nodiscard]] Hash256 blake2b_256( gsl::span<const uint8_t> buffer ) const override;

        [[nodiscard]] Hash256 keccak_256( gsl::span<const uint8_t> buffer ) const override;

        [[nodiscard]] Hash256 blake2s_256( gsl::span<const uint8_t> buffer ) const override;

        [[nodiscard]] Hash256 sha2_256( gsl::span<const uint8_t> buffer ) const override;

        std::string GetName() override
        {
            return "HasherImpl";
        }
    };
}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

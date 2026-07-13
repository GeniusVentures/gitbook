---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/hasher.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/hasher.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crypto](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crypto::Hasher](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/)**  |




## Source code

```cpp
#ifndef SUPERGENIUS_SRC_HASHER_HASHER_HPP_
#define SUPERGENIUS_SRC_HASHER_HASHER_HPP_

#include <cstddef>

#include <gsl/span>

#include "base/blob.hpp"
#include "singleton/IComponent.hpp"

namespace sgns::crypto {
  class Hasher : public IComponent {
   protected:
    using Hash64 = base::Hash64;
    using Hash128 = base::Hash128;
    using Hash256 = base::Hash256;

   public:
       ~Hasher() override = default;

       //------------ by ruymaster ----//
       [[nodiscard]] virtual Hash64 twox_64( gsl::span<const uint8_t> buffer ) const = 0;

       //------------ by ruymaster ----//
       [[nodiscard]] virtual Hash128 twox_128( gsl::span<const uint8_t> buffer ) const = 0;

       [[nodiscard]] virtual Hash128 blake2b_128( gsl::span<const uint8_t> buffer ) const = 0;

       //---------------------
       [[nodiscard]] virtual Hash256 twox_256( gsl::span<const uint8_t> buffer ) const = 0;

       [[nodiscard]] virtual Hash256 blake2b_256( gsl::span<const uint8_t> buffer ) const = 0;

       [[nodiscard]] virtual Hash256 keccak_256( gsl::span<const uint8_t> buffer ) const = 0;

       [[nodiscard]] virtual Hash256 blake2s_256( gsl::span<const uint8_t> buffer ) const = 0;

       [[nodiscard]] virtual Hash256 sha2_256( gsl::span<const uint8_t> buffer ) const = 0;

       [[nodiscard]] Hash256 sha2_256( const void *data, size_t size ) const
       {
           return sha2_256(
               gsl::span<const uint8_t>( reinterpret_cast<const uint8_t *>( data ), size ) );
       }
  };
}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

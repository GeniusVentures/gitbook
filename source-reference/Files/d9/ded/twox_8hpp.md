---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/twox/twox.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/twox/twox.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crypto](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| base::Hash64 | **[make_twox64](/source-reference/Files/d9/ded/twox_8hpp/#function-make_twox64)**(gsl::span< const uint8_t > buf) |
| base::Hash128 | **[make_twox128](/source-reference/Files/d9/ded/twox_8hpp/#function-make_twox128)**(gsl::span< const uint8_t > buf) |
| base::Hash256 | **[make_twox256](/source-reference/Files/d9/ded/twox_8hpp/#function-make_twox256)**(gsl::span< const uint8_t > buf) |


## Functions Documentation

### function make_twox64

```cpp
base::Hash64 make_twox64(
    gsl::span< const uint8_t > buf
)
```


### function make_twox128

```cpp
base::Hash128 make_twox128(
    gsl::span< const uint8_t > buf
)
```


### function make_twox256

```cpp
base::Hash256 make_twox256(
    gsl::span< const uint8_t > buf
)
```




## Source code

```cpp
#ifndef SUPERGENIUS_CRYPTO_TWOX_HPP
#define SUPERGENIUS_CRYPTO_TWOX_HPP

#include "base/blob.hpp"

namespace sgns::crypto
{
    base::Hash64 make_twox64( gsl::span<const uint8_t> buf );

    base::Hash128 make_twox128( gsl::span<const uint8_t> buf );

    base::Hash256 make_twox256( gsl::span<const uint8_t> buf );
}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

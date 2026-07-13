---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/hasher/hasher_impl.cpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/hasher/hasher_impl.cpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crypto](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/)**  |

## Types

|                | Name           |
| -------------- | -------------- |
| using Blob< 16 > | **[Hash128](/source-reference/Files/d3/d84/hasher__impl_8cpp/#using-hash128)**  |
| using Blob< 32 > | **[Hash256](/source-reference/Files/d3/d84/hasher__impl_8cpp/#using-hash256)**  |
| using Blob< 8 > | **[Hash64](/source-reference/Files/d3/d84/hasher__impl_8cpp/#using-hash64)**  |

## Types Documentation

### using Hash128

```cpp
using sgns::base::Hash128 = Blob<16>;
```


### using Hash256

```cpp
using sgns::base::Hash256 = Blob<32>;
```


### using Hash64

```cpp
using sgns::base::Hash64 = Blob<8>;
```





## Source code

```cpp
#include "crypto/hasher/hasher_impl.hpp"

#include <gsl/span>

#include <crypto/blake2/blake2b.h>
#include <crypto/blake2/blake2s.h>
#include "crypto/keccak/keccak.h"
#include "crypto/sha/sha256.hpp"
//-------------------
#include "crypto/twox/twox.hpp"

namespace sgns::crypto {
  using base::Hash128;
  using base::Hash256;
  using base::Hash64;

//-----------------------------
  Hash64 HasherImpl::twox_64(gsl::span<const uint8_t> buffer) const {
    return make_twox64(buffer);
  }

  Hash128 HasherImpl::twox_128(gsl::span<const uint8_t> buffer) const {
    return make_twox128(buffer);
  }

  Hash128 HasherImpl::blake2b_128(gsl::span<const uint8_t> buffer) const {
    Hash128 out;
    sgns_blake2b(out.data(), 16, nullptr, 0, buffer.data(), buffer.size());
    return out;
  }

//----------------------------
  Hash256 HasherImpl::twox_256(gsl::span<const uint8_t> buffer) const {
    return make_twox256(buffer);
  }

  Hash256 HasherImpl::blake2b_256(gsl::span<const uint8_t> buffer) const {
    Hash256 out;
    sgns_blake2b(out.data(), 32, nullptr, 0, buffer.data(), buffer.size());
    return out;
  }

  Hash256 HasherImpl::keccak_256(gsl::span<const uint8_t> buffer) const {
    Hash256 out;
    sha3_HashBuffer(256,
                    SHA3_FLAGS::SHA3_FLAGS_KECCAK,
                    buffer.data(),
                    buffer.size(),
                    out.data(),
                    32);
    return out;
  }

  Hash256 HasherImpl::blake2s_256(gsl::span<const uint8_t> buffer) const {
    Hash256 out;
    blake2s(out.data(), 32, nullptr, 0, buffer.data(), buffer.size());
    return out;
  }

  Hash256 HasherImpl::sha2_256(gsl::span<const uint8_t> buffer) const {
    return crypto::sha256(buffer);
  }
}  // namespace sgns::crypto
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

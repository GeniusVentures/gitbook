---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/twox/twox.cpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/twox/twox.cpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crypto](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| void | **[make_twox64](/source-reference/Files/d8/d88/twox_8cpp/#function-make_twox64)**(const uint8_t * in, uint32_t len, uint8_t * out) |
| base::Hash64 | **[make_twox64](/source-reference/Files/d8/d88/twox_8cpp/#function-make_twox64)**(gsl::span< const uint8_t > buf) |
| void | **[make_twox128](/source-reference/Files/d8/d88/twox_8cpp/#function-make_twox128)**(const uint8_t * in, uint32_t len, uint8_t * out) |
| base::Hash128 | **[make_twox128](/source-reference/Files/d8/d88/twox_8cpp/#function-make_twox128)**(gsl::span< const uint8_t > buf) |
| void | **[make_twox256](/source-reference/Files/d8/d88/twox_8cpp/#function-make_twox256)**(const uint8_t * in, uint32_t len, uint8_t * out) |
| base::Hash256 | **[make_twox256](/source-reference/Files/d8/d88/twox_8cpp/#function-make_twox256)**(gsl::span< const uint8_t > buf) |


## Functions Documentation

### function make_twox64

```cpp
void make_twox64(
    const uint8_t * in,
    uint32_t len,
    uint8_t * out
)
```


### function make_twox64

```cpp
base::Hash64 make_twox64(
    gsl::span< const uint8_t > buf
)
```


### function make_twox128

```cpp
void make_twox128(
    const uint8_t * in,
    uint32_t len,
    uint8_t * out
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
void make_twox256(
    const uint8_t * in,
    uint32_t len,
    uint8_t * out
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
#include "crypto/twox/twox.hpp"

#include <xxhash.h>

namespace sgns::crypto {
  void make_twox64(const uint8_t *in, uint32_t len, uint8_t *out) {
    auto *ptr = reinterpret_cast<uint64_t *>(out);
    ptr[0] = XXH64(in, len, 0);
  }

  base::Hash64 make_twox64(gsl::span<const uint8_t> buf) {
    base::Hash64 hash{};
    make_twox64(buf.data(), buf.size(), hash.data());
    return hash;
  }

  void make_twox128(const uint8_t *in, uint32_t len, uint8_t *out) {
    auto *ptr = reinterpret_cast<uint64_t *>(out);
    ptr[0] = XXH64(in, len, 0);
    ptr[1] = XXH64(in, len, 1);
  }

  base::Hash128 make_twox128(gsl::span<const uint8_t> buf) {
    base::Hash128 hash{};
    make_twox128(buf.data(), buf.size(), hash.data());
    return hash;
  }

  void make_twox256(const uint8_t *in, uint32_t len, uint8_t *out) {
    auto *ptr = reinterpret_cast<uint64_t *>(out);
    ptr[0] = XXH64(in, len, 0);
    ptr[1] = XXH64(in, len, 1);
    ptr[2] = XXH64(in, len, 2);
    ptr[3] = XXH64(in, len, 3);
  }

  base::Hash256 make_twox256(gsl::span<const uint8_t> buf) {
    base::Hash256 hash{};
    make_twox256(buf.data(), buf.size(), hash.data());
    return hash;
  }
}
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

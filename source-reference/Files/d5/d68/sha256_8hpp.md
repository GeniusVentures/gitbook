---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/sha/sha256.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/sha/sha256.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crypto](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| base::Hash256 | **[sha256](/source-reference/Files/d5/d68/sha256_8hpp/#function-sha256)**(std::string_view input) |
| base::Hash256 | **[sha256](/source-reference/Files/d5/d68/sha256_8hpp/#function-sha256)**(gsl::span< const uint8_t > input) |
| std::vector< uint8_t > | **[sha256](/source-reference/Files/d5/d68/sha256_8hpp/#function-sha256)**(const void * data, size_t dataSize) |


## Functions Documentation

### function sha256

```cpp
base::Hash256 sha256(
    std::string_view input
)
```


**Parameters**: 

  * **input** to be hashed 


**Return**: hashed bytes 

Take a SHA-256 hash from string 


### function sha256

```cpp
base::Hash256 sha256(
    gsl::span< const uint8_t > input
)
```


**Parameters**: 

  * **input** to be hashed 


**Return**: hashed bytes 

Take a SHA-256 hash from bytes 


### function sha256

```cpp
std::vector< uint8_t > sha256(
    const void * data,
    size_t dataSize
)
```




## Source code

```cpp
#ifndef SUPERGENIUS_SHA256_HPP
#define SUPERGENIUS_SHA256_HPP

#include <string_view>

#include <gsl/span>
#include "base/blob.hpp"

namespace sgns::crypto {
  base::Hash256 sha256(std::string_view input);

  base::Hash256 sha256(gsl::span<const uint8_t> input);

  std::vector<uint8_t> sha256(const void* data, size_t dataSize);
}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

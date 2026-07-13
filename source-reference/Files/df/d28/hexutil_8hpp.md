---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/hexutil.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/hexutil.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/)**  |

## Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[UnhexError](/source-reference/Files/df/d28/hexutil_8hpp/#enum-unhexerror)** { NOT_ENOUGH_INPUT = 1, NON_HEX_INPUT, VALUE_OUT_OF_RANGE, MISSING_0X_PREFIX, UNKNOWN}<br/>error codes for exceptions that may occur during unhexing  |

## Functions

|                | Name           |
| -------------- | -------------- |
| std::string | **[hex_upper](/source-reference/Files/df/d28/hexutil_8hpp/#function-hex_upper)**(gsl::span< const uint8_t > bytes)<br/>Converts bytes to uppercase hex representation.  |
| std::string | **[hex_lower](/source-reference/Files/df/d28/hexutil_8hpp/#function-hex_lower)**(gsl::span< const uint8_t > bytes)<br/>Converts bytes to hex representation.  |
| outcome::result< std::vector< uint8_t > > | **[unhex](/source-reference/Files/df/d28/hexutil_8hpp/#function-unhex)**(std::string_view hex)<br/>Converts hex representation to bytes.  |
| outcome::result< std::vector< uint8_t > > | **[unhexWith0x](/source-reference/Files/df/d28/hexutil_8hpp/#function-unhexwith0x)**(std::string_view hex)<br/>Unhex hex-string with 0x in the begining.  |
| | **[OUTCOME_HPP_DECLARE_ERROR_2](/source-reference/Files/df/d28/hexutil_8hpp/#function-outcome_hpp_declare_error_2)**([sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/) , UnhexError ) |

## Types Documentation

### enum UnhexError

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| NOT_ENOUGH_INPUT | 1|   |
| NON_HEX_INPUT | |   |
| VALUE_OUT_OF_RANGE | |   |
| MISSING_0X_PREFIX | |   |
| UNKNOWN | |   |



error codes for exceptions that may occur during unhexing 


## Functions Documentation

### function hex_upper

```cpp
std::string hex_upper(
    gsl::span< const uint8_t > bytes
)
```

Converts bytes to uppercase hex representation. 

**Parameters**: 

  * **bytes** input bytes 


**Return**: hexstring 

### function hex_lower

```cpp
std::string hex_lower(
    gsl::span< const uint8_t > bytes
)
```

Converts bytes to hex representation. 

**Parameters**: 

  * **bytes** input bytes 


**Return**: hexstring 

### function unhex

```cpp
outcome::result< std::vector< uint8_t > > unhex(
    std::string_view hex
)
```

Converts hex representation to bytes. 

**Parameters**: 

  * **hex** hex string input 


**See**: [https://www.boost.org/doc/libs/1_51_0/libs/algorithm/doc/html/the_boost_algorithm_library/Misc/hex.html](https://www.boost.org/doc/libs/1_51_0/libs/algorithm/doc/html/the_boost_algorithm_library/Misc/hex.html)

**Return**: result containing array of bytes if input string is hex encoded and has even length

**Note**: reads both uppercase and lowercase hexstrings

### function unhexWith0x

```cpp
outcome::result< std::vector< uint8_t > > unhexWith0x(
    std::string_view hex
)
```

Unhex hex-string with 0x in the begining. 

**Parameters**: 

  * **hex** hex string with 0x in the beginning 


**Return**: unhexed buffer 

### function OUTCOME_HPP_DECLARE_ERROR_2

```cpp
OUTCOME_HPP_DECLARE_ERROR_2(
    sgns::base ,
    UnhexError 
)
```




## Source code

```cpp
#ifndef SUPERGENIUS_HEXUTIL_HPP
#define SUPERGENIUS_HEXUTIL_HPP

#include <string_view>
#include <vector>

#include <gsl/span>
#include "outcome/outcome.hpp"

namespace sgns::base {

  enum class UnhexError {
    NOT_ENOUGH_INPUT = 1,
    NON_HEX_INPUT,
    VALUE_OUT_OF_RANGE,
    MISSING_0X_PREFIX,
    UNKNOWN
  };

  std::string hex_upper(gsl::span<const uint8_t> bytes) noexcept;

  std::string hex_lower(gsl::span<const uint8_t> bytes) noexcept;

  outcome::result<std::vector<uint8_t>> unhex(std::string_view hex);

  outcome::result<std::vector<uint8_t>> unhexWith0x(std::string_view hex);
}

OUTCOME_HPP_DECLARE_ERROR_2(sgns::base, UnhexError);

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

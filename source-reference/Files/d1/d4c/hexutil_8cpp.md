---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/hexutil.cpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/hexutil.cpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| | **[OUTCOME_CPP_DEFINE_CATEGORY_3](/source-reference/Files/d1/d4c/hexutil_8cpp/#function-outcome_cpp_define_category_3)**([sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/) , UnhexError , e ) |
| std::string | **[hex_upper](/source-reference/Files/d1/d4c/hexutil_8cpp/#function-hex_upper)**(gsl::span< const uint8_t > bytes)<br/>Converts bytes to uppercase hex representation.  |
| std::string | **[hex_lower](/source-reference/Files/d1/d4c/hexutil_8cpp/#function-hex_lower)**(gsl::span< const uint8_t > bytes)<br/>Converts bytes to hex representation.  |
| outcome::result< std::vector< uint8_t > > | **[unhex](/source-reference/Files/d1/d4c/hexutil_8cpp/#function-unhex)**(std::string_view hex)<br/>Converts hex representation to bytes.  |
| outcome::result< std::vector< uint8_t > > | **[unhexWith0x](/source-reference/Files/d1/d4c/hexutil_8cpp/#function-unhexwith0x)**(std::string_view hex)<br/>Unhex hex-string with 0x in the begining.  |


## Functions Documentation

### function OUTCOME_CPP_DEFINE_CATEGORY_3

```cpp
OUTCOME_CPP_DEFINE_CATEGORY_3(
    sgns::base ,
    UnhexError ,
    e 
)
```


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



## Source code

```cpp
#include "base/hexutil.hpp"

#include <boost/algorithm/hex.hpp>
#include <gsl/span>

OUTCOME_CPP_DEFINE_CATEGORY_3(sgns::base, UnhexError, e) {
  using sgns::base::UnhexError;
  switch (e) {
    case UnhexError::NON_HEX_INPUT:
      return "Input contains non-hex characters";
    case UnhexError::NOT_ENOUGH_INPUT:
      return "Input contains odd number of characters";
    case UnhexError::VALUE_OUT_OF_RANGE:
      return "Decoded value is out of range of requested type";
    case UnhexError::MISSING_0X_PREFIX:
      return "Missing expected 0x prefix";
    case UnhexError::UNKNOWN:
      return "Unknown error";
  }
  return "Unknown error (error id not listed)";
}

namespace sgns::base {
  std::string hex_upper(const gsl::span<const uint8_t> bytes) noexcept {
    std::string res(bytes.size() * 2, '\x00');
    boost::algorithm::hex(bytes.begin(), bytes.end(), res.begin());
    return res;
  }

  std::string hex_lower(const gsl::span<const uint8_t> bytes) noexcept {
    std::string res(bytes.size() * 2, '\x00');
    boost::algorithm::hex_lower(bytes.begin(), bytes.end(), res.begin());
    return res;
  }

  outcome::result<std::vector<uint8_t>> unhex(std::string_view hex) {
    std::vector<uint8_t> blob;
    blob.reserve((hex.size() + 1) / 2);

    if ( hex.size() >= 2 && hex[0] == '0' && hex[1] == 'x' )
    {
        hex = std::string_view( &hex[2], hex.length() - 2 );
    }

    try {
        boost::algorithm::unhex( hex, std::back_inserter( blob ) );
        return blob;
    } catch (const boost::algorithm::not_enough_input &e) {
      return UnhexError::NOT_ENOUGH_INPUT;

    } catch (const boost::algorithm::non_hex_input &e) {
      return UnhexError::NON_HEX_INPUT;

    } catch (const std::exception &e) {
      return UnhexError::UNKNOWN;
    }
  }

  outcome::result<std::vector<uint8_t>> unhexWith0x(
      std::string_view hex_with_prefix) {
    const static std::string leading_chrs = "0x";

    if (hex_with_prefix.substr(0, leading_chrs.size()) != leading_chrs) {
      return UnhexError::MISSING_0X_PREFIX;
    }

    auto without_prefix = hex_with_prefix.substr(leading_chrs.size());

    return base::unhex(without_prefix);
  }
}
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

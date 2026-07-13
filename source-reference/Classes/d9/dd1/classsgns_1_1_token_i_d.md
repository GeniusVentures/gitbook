---
title: sgns::TokenID
summary: Represents a 32-byte token identifier while preserving legacy GNUS semantics. 

---

# sgns::TokenID



Represents a 32-byte token identifier while preserving legacy GNUS semantics. 


`#include <TokenID.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[Endianness](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#enum-endianness)** { HOST, BIG, LITTLE}<br/>Byte order used when converting integer token identifiers.  |
| using std::array< uint8_t, 32 > | **[ByteArray](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#using-bytearray)** <br/>Fixed-size byte storage used for token identifiers.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| constexpr | **[TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid)**()<br/>Constructs an invalid or legacy-default token identifier.  |
| | **[TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid)**(const TokenID & other) =default<br/>Copy-constructs a token identifier.  |
| | **[TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid)**(TokenID && other) =default<br/>Move-constructs a token identifier.  |
| [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid) & | **[operator=](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-operator=)**(const [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid) & other) =default<br/>Copy-assigns a token identifier.  |
| [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid) & | **[operator=](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-operator=)**([TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid) && other) =default<br/>Move-assigns a token identifier.  |
| const [ByteArray](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#using-bytearray) & | **[bytes](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-bytes)**() const<br/>Returns the raw 32-byte storage buffer.  |
| size_t | **[size](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-size)**() const<br/>Returns 32 for valid token identifiers or 0 for legacy-invalid ones.  |
| bool | **[operator==](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-operator==)**(const [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid) & other) const<br/>Tests exact equality including validity state.  |
| bool | **[operator!=](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-operator!=)**(const [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid) & other) const<br/>Tests exact inequality including validity state.  |
| bool | **[operator<](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-operator<)**(const [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid) & other) const<br/>Orders token identifiers by raw byte value.  |
| std::string | **[ToHex](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tohex)**() const<br/>Converts the token identifier to a lowercase hexadecimal string.  |
| bool | **[IsGNUS](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-isgnus)**() const<br/>Returns true when this identifier refers to the default GNUS token.  |
| bool | **[Equals](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-equals)**(const [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid) & other) const<br/>Compares token identifiers while treating all GNUS representations as equivalent.  |
| [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid) | **[FromBytes](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-frombytes)**(std::initializer_list< uint8_t > list)<br/>Builds a token identifier from a byte initializer list.  |
| [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid) | **[FromBytes](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-frombytes)**(const void * data, size_t size)<br/>Builds a token identifier from up to 32 bytes, left-padding shorter inputs.  |
| template <typename Uint256 \> <br/>[TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-tokenid) | **[FromUint256](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-fromuint256)**(const Uint256 & value, [Endianness](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#enum-endianness) endianness =[Endianness::HOST](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#enumvalue-host))<br/>Builds a token identifier from a 256-bit integer value.  |

## Public Types Documentation

### enum Endianness

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| HOST | |   |
| BIG | |   |
| LITTLE | |   |



Byte order used when converting integer token identifiers. 

### using ByteArray

```cpp
using sgns::TokenID::ByteArray = std::array<uint8_t, 32>;
```

Fixed-size byte storage used for token identifiers. 

## Public Functions Documentation

### function TokenID

```cpp
inline constexpr TokenID()
```

Constructs an invalid or legacy-default token identifier. 

### function TokenID

```cpp
TokenID(
    const TokenID & other
) =default
```

Copy-constructs a token identifier. 

**Parameters**: 

  * **other** Token identifier to copy. 


### function TokenID

```cpp
TokenID(
    TokenID && other
) =default
```

Move-constructs a token identifier. 

**Parameters**: 

  * **other** Token identifier to move from. 


### function operator=

```cpp
TokenID & operator=(
    const TokenID & other
) =default
```

Copy-assigns a token identifier. 

**Parameters**: 

  * **other** Token identifier to copy. 


**Return**: Reference to this token identifier. 

### function operator=

```cpp
TokenID & operator=(
    TokenID && other
) =default
```

Move-assigns a token identifier. 

**Parameters**: 

  * **other** Token identifier to move from. 


**Return**: Reference to this token identifier. 

### function bytes

```cpp
inline const ByteArray & bytes() const
```

Returns the raw 32-byte storage buffer. 

**Return**: Const reference to the internal 32-byte array. 

### function size

```cpp
inline size_t size() const
```

Returns 32 for valid token identifiers or 0 for legacy-invalid ones. 

**Return**: Serialized byte size of this identifier. 

### function operator==

```cpp
inline bool operator==(
    const TokenID & other
) const
```

Tests exact equality including validity state. 

**Parameters**: 

  * **other** Token identifier to compare against. 


**Return**: True when both identifiers have the same validity state and bytes. 

### function operator!=

```cpp
inline bool operator!=(
    const TokenID & other
) const
```

Tests exact inequality including validity state. 

**Parameters**: 

  * **other** Token identifier to compare against. 


**Return**: True when `other` is not exactly equal to this identifier. 

### function operator<

```cpp
inline bool operator<(
    const TokenID & other
) const
```

Orders token identifiers by raw byte value. 

**Parameters**: 

  * **other** Token identifier to compare against. 


**Return**: True when this identifier's bytes compare lexicographically before `other`. 

### function ToHex

```cpp
inline std::string ToHex() const
```

Converts the token identifier to a lowercase hexadecimal string. 

**Return**: Lowercase hexadecimal representation of the 32-byte storage buffer. 

### function IsGNUS

```cpp
inline bool IsGNUS() const
```

Returns true when this identifier refers to the default GNUS token. 

**Return**: True when the identifier is invalid or all bytes are zero. 

### function Equals

```cpp
inline bool Equals(
    const TokenID & other
) const
```

Compares token identifiers while treating all GNUS representations as equivalent. 

**Parameters**: 

  * **other** Token identifier to compare against. 


**Return**: True when the identifiers are exactly equal or both represent the GNUS token. 

### function FromBytes

```cpp
static inline TokenID FromBytes(
    std::initializer_list< uint8_t > list
)
```

Builds a token identifier from a byte initializer list. 

**Parameters**: 

  * **list** Bytes used to build the identifier. 


**Return**: Token identifier containing `list`, left-padded to 32 bytes when shorter. 

### function FromBytes

```cpp
static inline TokenID FromBytes(
    const void * data,
    size_t size
)
```

Builds a token identifier from up to 32 bytes, left-padding shorter inputs. 

**Parameters**: 

  * **data** Pointer to the source bytes. 
  * **[size](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/#function-size)** Number of bytes available at `data`. 


**Return**: Valid token identifier when `data` is non-null and `size` is 1 to 32; otherwise an invalid identifier. 

### function FromUint256

```cpp
template <typename Uint256 >
static inline TokenID FromUint256(
    const Uint256 & value,
    Endianness endianness =Endianness::HOST
)
```

Builds a token identifier from a 256-bit integer value. 

**Parameters**: 

  * **value** Integer value to convert. 
  * **endianness** Byte order to use for the resulting token bytes. 


**Template Parameters**: 

  * **Uint256** 256-bit unsigned integer type with 64-bit word access. 


**Return**: Valid token identifier containing the 32-byte representation of `value`. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: sgns::base::Blob

---

# sgns::base::Blob



 [More...](#detailed-description)


`#include <blob.hpp>`

Inherits from std::array< uint8_t, size_ >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-blob)**() |
| constexpr | **[Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-blob)**(const std::array< uint8_t, size_ > & l)<br/>constructor enabling initializer list  |
| std::string | **[toString](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-tostring)**() const |
| std::string | **[toReadableString](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-toreadablestring)**() const |
| std::string | **[toHex](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-tohex)**() const |
| std::vector< uint8_t > | **[ToVec](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-tovec)**() const |
| size_t | **[size](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-size)**() |
| outcome::result< [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-blob)< size_ > > | **[fromString](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-fromstring)**(std::string_view data) |
| outcome::result< [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-blob)< size_ > > | **[fromReadableString](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-fromreadablestring)**(std::string_view data) |
| outcome::result< [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-blob)< size_ > > | **[fromHex](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-fromhex)**(std::string_view hex) |
| outcome::result< [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-blob)< size_ > > | **[fromHexWithPrefix](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-fromhexwithprefix)**(std::string_view hex) |
| outcome::result< [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-blob)< size_ > > | **[fromSpan](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/#function-fromspan)**(gsl::span< uint8_t > span) |

## Detailed Description

```cpp
template <size_t size_>
class sgns::base::Blob;
```


Base type which represents blob of fixed size.

std::string is convenient to use but it is not safe. We can not specify the fixed length for string.

For std::array it is possible, so we prefer it over std::string. 

## Public Functions Documentation

### function Blob

```cpp
inline Blob()
```


Initialize blob value 


### function Blob

```cpp
inline explicit constexpr Blob(
    const std::array< uint8_t, size_ > & l
)
```

constructor enabling initializer list 

**Parameters**: 

  * **l** initializer list 


### function toString

```cpp
inline std::string toString() const
```


Converts current blob to std::string 


### function toReadableString

```cpp
inline std::string toReadableString() const
```


Converts current blob to a readable std::string 


### function toHex

```cpp
inline std::string toHex() const
```


Converts current blob to hex string. 


### function ToVec

```cpp
inline std::vector< uint8_t > ToVec() const
```


### function size

```cpp
static inline size_t size()
```


In compile-time returns size of current blob. 


### function fromString

```cpp
static inline outcome::result< Blob< size_ > > fromString(
    std::string_view data
)
```


**Parameters**: 

  * **data** arbitrary string containing 


**Return**: result containing [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/) object if string has proper size 

Create [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/) from arbitrary string, putting its bytes into the blob 


### function fromReadableString

```cpp
static inline outcome::result< Blob< size_ > > fromReadableString(
    std::string_view data
)
```


### function fromHex

```cpp
static inline outcome::result< Blob< size_ > > fromHex(
    std::string_view hex
)
```


**Parameters**: 

  * **hex** hex string 


**Return**: result containing [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/) object if hex string has proper size and is in hex format 

Create [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/) from hex string 


### function fromHexWithPrefix

```cpp
static inline outcome::result< Blob< size_ > > fromHexWithPrefix(
    std::string_view hex
)
```


**Parameters**: 

  * **hex** hex string 


**Return**: result containing [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/) object if hex string has proper size and is in hex format 

Create [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/) from hex string prefixed with 0x 


### function fromSpan

```cpp
static inline outcome::result< Blob< size_ > > fromSpan(
    gsl::span< uint8_t > span
)
```


**Parameters**: 

  * **span** input byte span 


**Return**: result containing [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/) object if span has proper size 

Create [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/) from span of uint8_t 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
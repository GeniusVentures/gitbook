---
title: sgns::base

---

# sgns::base





## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::base::Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/)**  |
| class | **[sgns::base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/)** <br/>Class represents arbitrary (including empty) byte buffer.  |
| struct | **[sgns::base::Wrapper](/source-reference/Classes/df/d5a/structsgns_1_1base_1_1_wrapper/)** <br/>Make strongly typed structures from different concepts of the equal types. E.g. block height and round number are both uint64_t, but better to be different types. Or, ID and Signature both vectors.  |

## Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[BlobError](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#enum-bloberror)** { INCORRECT_LENGTH = 1} |
| enum class| **[UnhexError](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#enum-unhexerror)** { NOT_ENOUGH_INPUT = 1, NON_HEX_INPUT, VALUE_OUT_OF_RANGE, MISSING_0X_PREFIX, UNKNOWN}<br/>error codes for exceptions that may occur during unhexing  |
| using [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/)< 8 > | **[Hash64](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash64)**  |
| using [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/)< 16 > | **[Hash128](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash128)**  |
| using [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/)< 32 > | **[Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256)**  |
| using [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/)< 64 > | **[Hash512](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash512)**  |
| using std::shared_ptr< spdlog::logger > | **[Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| template <class Stream ,size_t size,typename  =std::enable_if_t<Stream::is_encoder_stream>\> <br/>Stream & | **[operator<<](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-operator<<)**(Stream & s, const [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/)< size > & blob)<br/>scale-encodes blob instance to stream  |
| template <class Stream ,size_t size,typename  =std::enable_if_t<Stream::is_decoder_stream>\> <br/>Stream & | **[operator>>](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-operator>>)**(Stream & s, [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/)< size > & blob)<br/>decodes blob instance from stream  |
| template <size_t N\> <br/>std::ostream & | **[operator<<](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-operator<<)**(std::ostream & os, const [Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/)< N > & blob) |
| std::ostream & | **[operator<<](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-operator<<)**(std::ostream & os, const [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & buffer) |
| template <class Stream ,typename  =std::enable_if_t<Stream::is_encoder_stream>\> <br/>Stream & | **[operator<<](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-operator<<)**(Stream & s, const [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & buffer)<br/>override operator<< for all streams except std::ostream  |
| template <class Stream ,typename  =std::enable_if_t<Stream::is_decoder_stream>\> <br/>Stream & | **[operator>>](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-operator>>)**(Stream & s, [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & buffer)<br/>decodes buffer object from stream  |
| std::string | **[hex_upper](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-hex_upper)**(gsl::span< const uint8_t > bytes)<br/>Converts bytes to uppercase hex representation.  |
| std::string | **[hex_lower](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-hex_lower)**(gsl::span< const uint8_t > bytes)<br/>Converts bytes to hex representation.  |
| outcome::result< std::vector< uint8_t > > | **[unhex](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-unhex)**(std::string_view hex)<br/>Converts hex representation to bytes.  |
| outcome::result< std::vector< uint8_t > > | **[unhexWith0x](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-unhexwith0x)**(std::string_view hex)<br/>Unhex hex-string with 0x in the begining.  |
| [Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) | **[createLogger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-createlogger)**(const std::string & tag, const std::string & basepath ="")<br/>Create a logger instance.  |
| template <typename T ,typename  =std::enable_if_t<std::is_enum_v<T>>\> <br/>void | **[raise](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-raise)**(T t)<br/>throws outcome::result error as boost exception  |
| template <typename T ,typename  =std::enable_if_t<!std::is_enum_v<T>>\> <br/>void | **[raise](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-raise)**(const T & t)<br/>throws outcome::result error made of error as boost exception  |
| template <typename T ,typename Tag ,typename  =std::enable_if_t<std::is_arithmetic_v<T>>\> <br/>bool | **[operator<](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#function-operator<)**(const [Wrapper](/source-reference/Classes/df/d5a/structsgns_1_1base_1_1_wrapper/)< T, Tag > & a, const [Wrapper](/source-reference/Classes/df/d5a/structsgns_1_1base_1_1_wrapper/)< T, Tag > & b) |

## Types Documentation

### enum BlobError

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| INCORRECT_LENGTH | 1|   |




Error codes for exceptions that may occur during blob initialization 


### enum UnhexError

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| NOT_ENOUGH_INPUT | 1|   |
| NON_HEX_INPUT | |   |
| VALUE_OUT_OF_RANGE | |   |
| MISSING_0X_PREFIX | |   |
| UNKNOWN | |   |



error codes for exceptions that may occur during unhexing 

### using Hash64

```cpp
using sgns::base::Hash64 = Blob<8>;
```


### using Hash128

```cpp
using sgns::base::Hash128 = Blob<16>;
```


### using Hash256

```cpp
using sgns::base::Hash256 = Blob<32>;
```


### using Hash512

```cpp
using sgns::base::Hash512 = Blob<64>;
```


### using Logger

```cpp
using sgns::base::Logger = std::shared_ptr<spdlog::logger>;
```



## Functions Documentation

### function operator<<

```cpp
template <class Stream ,
size_t size,
typename  =std::enable_if_t<Stream::is_encoder_stream>>
Stream & operator<<(
    Stream & s,
    const Blob< size > & blob
)
```

scale-encodes blob instance to stream 

**Parameters**: 

  * **s** output stream reference 
  * **blob** value to encode 


**Template Parameters**: 

  * **Stream** output stream type 
  * **size** blob size 


**Return**: reference to stream 

### function operator>>

```cpp
template <class Stream ,
size_t size,
typename  =std::enable_if_t<Stream::is_decoder_stream>>
Stream & operator>>(
    Stream & s,
    Blob< size > & blob
)
```

decodes blob instance from stream 

**Parameters**: 

  * **s** input stream reference 
  * **blob** value to encode 


**Template Parameters**: 

  * **Stream** output stream type 
  * **size** blob size 


**Return**: reference to stream 

### function operator<<

```cpp
template <size_t N>
inline std::ostream & operator<<(
    std::ostream & os,
    const Blob< N > & blob
)
```


### function operator<<

```cpp
std::ostream & operator<<(
    std::ostream & os,
    const Buffer & buffer
)
```


### function operator<<

```cpp
template <class Stream ,
typename  =std::enable_if_t<Stream::is_encoder_stream>>
Stream & operator<<(
    Stream & s,
    const Buffer & buffer
)
```

override operator<< for all streams except std::ostream 

**Parameters**: 

  * **s** stream reference 
  * **buffer** value to encode 


**Template Parameters**: 

  * **Stream** stream type 


**Return**: reference to stream 

### function operator>>

```cpp
template <class Stream ,
typename  =std::enable_if_t<Stream::is_decoder_stream>>
Stream & operator>>(
    Stream & s,
    Buffer & buffer
)
```

decodes buffer object from stream 

**Parameters**: 

  * **s** stream reference 
  * **buffer** value to decode 


**Template Parameters**: 

  * **Stream** input stream type 


**Return**: reference to stream 

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

### function createLogger

```cpp
Logger createLogger(
    const std::string & tag,
    const std::string & basepath =""
)
```

Create a logger instance. 

**Parameters**: 

  * **tag** Tagging name for identifying logger. 
  * **basepath** Optional base path for log output (platform dependent). 


**Return**: [Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) object. 

### function raise

```cpp
template <typename T ,
typename  =std::enable_if_t<std::is_enum_v<T>>>
void raise(
    T t
)
```

throws outcome::result error as boost exception 

**Parameters**: 

  * **t** error value 


**Template Parameters**: 

  * **T** enum error type, only outcome::result enums are allowed 


### function raise

```cpp
template <typename T ,
typename  =std::enable_if_t<!std::is_enum_v<T>>>
void raise(
    const T & t
)
```

throws outcome::result error made of error as boost exception 

**Parameters**: 

  * **t** outcome error value 


**Template Parameters**: 

  * **T** outcome error type 


### function operator<

```cpp
template <typename T ,
typename Tag ,
typename  =std::enable_if_t<std::is_arithmetic_v<T>>>
bool operator<(
    const Wrapper< T, Tag > & a,
    const Wrapper< T, Tag > & b
)
```






-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
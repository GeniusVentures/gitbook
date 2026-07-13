---
title: sgns::crypto

---

# sgns::crypto





## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crypto::Hasher](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/)**  |
| class | **[sgns::crypto::HasherImpl](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/)**  |

## Types

|                | Name           |
| -------------- | -------------- |
| using Blob< 16 > | **[Hash128](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/#using-hash128)**  |
| using Blob< 32 > | **[Hash256](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/#using-hash256)**  |
| using Blob< 8 > | **[Hash64](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/#using-hash64)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[sha256](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/#function-sha256)**(std::string_view input) |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[sha256](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/#function-sha256)**(gsl::span< const uint8_t > input) |
| std::vector< uint8_t > | **[sha256](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/#function-sha256)**(const void * data, size_t dataSize) |
| void | **[make_twox64](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/#function-make_twox64)**(const uint8_t * in, uint32_t len, uint8_t * out) |
| [base::Hash64](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash64) | **[make_twox64](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/#function-make_twox64)**(gsl::span< const uint8_t > buf) |
| void | **[make_twox128](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/#function-make_twox128)**(const uint8_t * in, uint32_t len, uint8_t * out) |
| [base::Hash128](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash128) | **[make_twox128](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/#function-make_twox128)**(gsl::span< const uint8_t > buf) |
| void | **[make_twox256](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/#function-make_twox256)**(const uint8_t * in, uint32_t len, uint8_t * out) |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[make_twox256](/source-reference/Namespaces/df/d6e/namespacesgns_1_1crypto/#function-make_twox256)**(gsl::span< const uint8_t > buf) |

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






-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
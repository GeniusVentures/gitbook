---
title: sgns::crypto::HasherImpl

---

# sgns::crypto::HasherImpl






`#include <hasher_impl.hpp>`

Inherits from [sgns::crypto::Hasher](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/), [IComponent](/source-reference/Classes/d1/dbf/class_i_component/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[~HasherImpl](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/#function-~hasherimpl)**() override =default |
| virtual [Hash64](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#using-hash64) | **[twox_64](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/#function-twox_64)**(gsl::span< const uint8_t > buffer) const override<br/>twox_128 calculates 16-byte twox hash  |
| virtual [Hash128](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#using-hash128) | **[twox_128](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/#function-twox_128)**(gsl::span< const uint8_t > buffer) const override<br/>twox_128 calculates 16-byte twox hash  |
| virtual [Hash128](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#using-hash128) | **[blake2b_128](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/#function-blake2b_128)**(gsl::span< const uint8_t > buffer) const override<br/>blake2b_128 function calculates 16-byte blake2b hash  |
| virtual [Hash256](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#using-hash256) | **[twox_256](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/#function-twox_256)**(gsl::span< const uint8_t > buffer) const override<br/>twox_256 calculates 32-byte twox hash  |
| virtual [Hash256](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#using-hash256) | **[blake2b_256](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/#function-blake2b_256)**(gsl::span< const uint8_t > buffer) const override<br/>blake2b_256 function calculates 32-byte blake2b hash  |
| virtual [Hash256](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#using-hash256) | **[keccak_256](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/#function-keccak_256)**(gsl::span< const uint8_t > buffer) const override<br/>keccak_256 function calculates 32-byte keccak hash  |
| virtual [Hash256](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#using-hash256) | **[blake2s_256](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/#function-blake2s_256)**(gsl::span< const uint8_t > buffer) const override<br/>blake2s_256 function calculates 32-byte blake2s hash  |
| virtual [Hash256](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#using-hash256) | **[sha2_256](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/#function-sha2_256)**(gsl::span< const uint8_t > buffer) const override<br/>sha2_256 function calculates 32-byte sha2-256 hash  |
| virtual std::string | **[GetName](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/#function-getname)**() override |
| [Hash256](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#using-hash256) | **[sha2_256](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/#function-sha2_256)**(const void * data, size_t size) const<br/>sha2_256 helper for raw memory buffers  |

## Additional inherited members

**Protected Types inherited from [sgns::crypto::Hasher](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/)**

|                | Name           |
| -------------- | -------------- |
| using [base::Hash64](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash64) | **[Hash64](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#using-hash64)**  |
| using [base::Hash128](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash128) | **[Hash128](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#using-hash128)**  |
| using [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[Hash256](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#using-hash256)**  |

**Public Functions inherited from [sgns::crypto::Hasher](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/)**

|                | Name           |
| -------------- | -------------- |
| | **[~Hasher](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#function-~hasher)**() override =default |

**Public Functions inherited from [IComponent](/source-reference/Classes/d1/dbf/class_i_component/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IComponent](/source-reference/Classes/d1/dbf/class_i_component/#function-~icomponent)**() =default |


## Public Functions Documentation

### function ~HasherImpl

```cpp
~HasherImpl() override =default
```


### function twox_64

```cpp
virtual Hash64 twox_64(
    gsl::span< const uint8_t > buffer
) const override
```

twox_128 calculates 16-byte twox hash 

**Parameters**: 

  * **buffer** source buffer 


**Return**: 128-bit hash value 

**Reimplements**: [sgns::crypto::Hasher::twox_64](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#function-twox_64)


### function twox_128

```cpp
virtual Hash128 twox_128(
    gsl::span< const uint8_t > buffer
) const override
```

twox_128 calculates 16-byte twox hash 

**Parameters**: 

  * **buffer** source buffer 


**Return**: 128-bit hash value 

**Reimplements**: [sgns::crypto::Hasher::twox_128](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#function-twox_128)


### function blake2b_128

```cpp
virtual Hash128 blake2b_128(
    gsl::span< const uint8_t > buffer
) const override
```

blake2b_128 function calculates 16-byte blake2b hash 

**Parameters**: 

  * **buffer** source value 


**Return**: 128-bit hash value 

**Reimplements**: [sgns::crypto::Hasher::blake2b_128](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#function-blake2b_128)


### function twox_256

```cpp
virtual Hash256 twox_256(
    gsl::span< const uint8_t > buffer
) const override
```

twox_256 calculates 32-byte twox hash 

**Parameters**: 

  * **buffer** source buffer 


**Return**: 256-bit hash value 

**Reimplements**: [sgns::crypto::Hasher::twox_256](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#function-twox_256)


### function blake2b_256

```cpp
virtual Hash256 blake2b_256(
    gsl::span< const uint8_t > buffer
) const override
```

blake2b_256 function calculates 32-byte blake2b hash 

**Parameters**: 

  * **buffer** source value 


**Return**: 256-bit hash value 

**Reimplements**: [sgns::crypto::Hasher::blake2b_256](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#function-blake2b_256)


### function keccak_256

```cpp
virtual Hash256 keccak_256(
    gsl::span< const uint8_t > buffer
) const override
```

keccak_256 function calculates 32-byte keccak hash 

**Parameters**: 

  * **buffer** source value 


**Return**: 256-bit hash value 

**Reimplements**: [sgns::crypto::Hasher::keccak_256](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#function-keccak_256)


### function blake2s_256

```cpp
virtual Hash256 blake2s_256(
    gsl::span< const uint8_t > buffer
) const override
```

blake2s_256 function calculates 32-byte blake2s hash 

**Parameters**: 

  * **buffer** source value 


**Return**: 256-bit hash value 

**Reimplements**: [sgns::crypto::Hasher::blake2s_256](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#function-blake2s_256)


### function sha2_256

```cpp
virtual Hash256 sha2_256(
    gsl::span< const uint8_t > buffer
) const override
```

sha2_256 function calculates 32-byte sha2-256 hash 

**Parameters**: 

  * **buffer** source value 


**Return**: 256-bit hash value 

**Reimplements**: [sgns::crypto::Hasher::sha2_256](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/#function-sha2_256)


### function GetName

```cpp
inline virtual std::string GetName() override
```


**Reimplements**: [IComponent::GetName](/source-reference/Classes/d1/dbf/class_i_component/#function-getname)


### function sha2_256

```cpp
inline Hash256 sha2_256(
    const void * data,
    size_t size
) const
```

sha2_256 helper for raw memory buffers 

**Parameters**: 

  * **data** pointer to source bytes 
  * **size** source byte size 


**Return**: 256-bit hash value 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
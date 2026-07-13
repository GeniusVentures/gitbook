---
title: sgns::base::Wrapper
summary: Make strongly typed structures from different concepts of the equal types. E.g. block height and round number are both uint64_t, but better to be different types. Or, ID and Signature both vectors. 

---

# sgns::base::Wrapper



Make strongly typed structures from different concepts of the equal types. E.g. block height and round number are both uint64_t, but better to be different types. Or, ID and Signature both vectors.  [More...](#detailed-description)


`#include <wrapper.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[Wrapper](/source-reference/Classes/df/d5a/structsgns_1_1base_1_1_wrapper/#function-wrapper)**(T && t) |
| T | **[unwrap](/source-reference/Classes/df/d5a/structsgns_1_1base_1_1_wrapper/#function-unwrap)**() |
| const T & | **[unwrap](/source-reference/Classes/df/d5a/structsgns_1_1base_1_1_wrapper/#function-unwrap)**() const |
| T & | **[unwrap_mutable](/source-reference/Classes/df/d5a/structsgns_1_1base_1_1_wrapper/#function-unwrap_mutable)**() |
| bool | **[operator==](/source-reference/Classes/df/d5a/structsgns_1_1base_1_1_wrapper/#function-operator==)**(const [Wrapper](/source-reference/Classes/df/d5a/structsgns_1_1base_1_1_wrapper/#function-wrapper)< T, Tag > & other) const |

## Detailed Description

```cpp
template <typename T ,
typename Tag >
struct sgns::base::Wrapper;
```

Make strongly typed structures from different concepts of the equal types. E.g. block height and round number are both uint64_t, but better to be different types. Or, ID and Signature both vectors. 

**Template Parameters**: 

  * **T** wrapped type 
  * **Tag** unique tag 

## Public Functions Documentation

### function Wrapper

```cpp
inline explicit Wrapper(
    T && t
)
```


### function unwrap

```cpp
inline T unwrap()
```


### function unwrap

```cpp
inline const T & unwrap() const
```


### function unwrap_mutable

```cpp
inline T & unwrap_mutable()
```


### function operator==

```cpp
inline bool operator==(
    const Wrapper< T, Tag > & other
) const
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
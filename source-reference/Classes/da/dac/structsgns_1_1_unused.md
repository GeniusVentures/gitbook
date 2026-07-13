---
title: sgns::Unused

---

# sgns::Unused



 [More...](#detailed-description)


`#include <unused.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[operator==](/source-reference/Classes/da/dac/structsgns_1_1_unused/#function-operator==)**(const [Unused](/source-reference/Classes/da/dac/structsgns_1_1_unused/) & ) const |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| size_t | **[index](/source-reference/Classes/da/dac/structsgns_1_1_unused/#variable-index)**  |

## Detailed Description

```cpp
template <size_t N>
struct sgns::Unused;
```


Special zero-size-type for some things (e.g., unsupported and experimental). 

## Public Functions Documentation

### function operator==

```cpp
inline bool operator==(
    const Unused & 
) const
```


## Public Attributes Documentation

### variable index

```cpp
static size_t index = N;
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
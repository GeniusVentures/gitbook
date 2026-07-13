---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/unused.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/unused.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::Unused](/source-reference/Classes/da/dac/structsgns_1_1_unused/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| template <size_t N,class Stream \> <br/>Stream & | **[operator<<](/source-reference/Files/dd/d26/unused_8hpp/#function-operator<<)**(Stream & s, const Unused< N > & ) |
| template <size_t N,class Stream \> <br/>Stream & | **[operator>>](/source-reference/Files/dd/d26/unused_8hpp/#function-operator>>)**(Stream & s, Unused< N > & ) |


## Functions Documentation

### function operator<<

```cpp
template <size_t N,
class Stream >
Stream & operator<<(
    Stream & s,
    const Unused< N > & 
)
```


### function operator>>

```cpp
template <size_t N,
class Stream >
Stream & operator>>(
    Stream & s,
    Unused< N > & 
)
```




## Source code

```cpp
#ifndef SUPERGENIUS_UNUSED
#define SUPERGENIUS_UNUSED

#include <cstddef>

namespace sgns {

  template <size_t N>
  struct Unused {
    inline static constexpr size_t index = N;

    bool operator==(const Unused &) const {
      return true;
    }
  };

  template <size_t N, class Stream>
  Stream &operator<<(Stream &s, const Unused<N> &) {
    return s;
  }

  template <size_t N, class Stream>
  Stream &operator>>(Stream &s, Unused<N> &) {
    return s;
  }

}  // namespace sgns

#endif  // SUPERGENIUS_UNUSED
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

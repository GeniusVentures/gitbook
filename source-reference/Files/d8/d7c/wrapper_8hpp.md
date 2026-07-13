---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/wrapper.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/wrapper.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::base::Wrapper](/source-reference/Classes/df/d5a/structsgns_1_1base_1_1_wrapper/)** <br/>Make strongly typed structures from different concepts of the equal types. E.g. block height and round number are both uint64_t, but better to be different types. Or, ID and Signature both vectors.  |
| struct | **[std::hash< sgns::base::Wrapper< T, Tag > >](/source-reference/Classes/d4/d33/structstd_1_1hash_3_01sgns_1_1base_1_1_wrapper_3_01_t_00_01_tag_01_4_01_4/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| template <typename T ,typename Tag ,typename  =std::enable_if_t<std::is_arithmetic_v<T>>\> <br/>bool | **[operator<](/source-reference/Files/d8/d7c/wrapper_8hpp/#function-operator<)**(const Wrapper< T, Tag > & a, const Wrapper< T, Tag > & b) |


## Functions Documentation

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




## Source code

```cpp
#ifndef SUPERGENIUS_SRC_COMMON_WRAPPER_HPP
#define SUPERGENIUS_SRC_COMMON_WRAPPER_HPP

#include <type_traits>

#include <boost/operators.hpp>

namespace sgns::base {

  template <typename T, typename Tag>
  struct Wrapper {
    explicit Wrapper(T &&t) : data_(std::forward<T>(t)) {}

    T unwrap() {
      return data_;
    }

    const T &unwrap() const {
      return data_;
    }

    T &unwrap_mutable() {
      return data_;
    }

    bool operator==(const Wrapper<T, Tag> &other) const {
      return data_ == other.data_;
    }

   private:
    T data_;
  };

  template <typename T, typename Tag, typename = std::enable_if_t<std::is_arithmetic_v<T>>>
  bool operator<( const Wrapper<T, Tag> &a, const Wrapper<T, Tag> &b )
  {
      return a.unwrap() < b.unwrap();
  }

}  // namespace sgns::base

template <typename T, typename Tag>
struct std::hash<sgns::base::Wrapper<T, Tag>> {
  std::size_t operator()(const sgns::base::Wrapper<T, Tag> &w) {
    return std::hash<T>()(w.unwrap());
  }
};

#endif  // SUPERGENIUS_SRC_COMMON_WRAPPER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

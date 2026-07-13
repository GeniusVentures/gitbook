---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/outcome_throw.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/outcome_throw.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| template <typename T ,typename  =std::enable_if_t<std::is_enum_v<T>>\> <br/>void | **[raise](/source-reference/Files/d6/d8d/outcome__throw_8hpp/#function-raise)**(T t)<br/>throws outcome::result error as boost exception  |
| template <typename T ,typename  =std::enable_if_t<!std::is_enum_v<T>>\> <br/>void | **[raise](/source-reference/Files/d6/d8d/outcome__throw_8hpp/#function-raise)**(const T & t)<br/>throws outcome::result error made of error as boost exception  |


## Functions Documentation

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




## Source code

```cpp
#ifndef SUPERGENIUS_SRC_COMMON_OUTCOME_THROW_HPP
#define SUPERGENIUS_SRC_COMMON_OUTCOME_THROW_HPP

#include <boost/system/system_error.hpp>
#include <boost/throw_exception.hpp>

namespace sgns::base {
  template <typename T, typename = std::enable_if_t<std::is_enum_v<T>>>
  void raise(T t) {
    std::error_code ec = make_error_code(t);
    boost::throw_exception(std::system_error(ec));
  }

  template <typename T, typename = std::enable_if_t<!std::is_enum_v<T>>>
  void raise(const T &t) {
    boost::throw_exception(std::system_error(t.value(), t.category()));
  }
}  // namespace sgns::base

#endif  // SUPERGENIUS_SRC_COMMON_OUTCOME_THROW_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

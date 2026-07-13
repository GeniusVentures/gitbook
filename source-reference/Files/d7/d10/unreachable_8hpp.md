---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/macro/unreachable.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/macro/unreachable.hpp





## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[Unreachable_At_Line](/source-reference/Classes/d5/d2f/class_unreachable___at___line/)** <br/>This file declares UNREACHABLE macro. Use it to prevent compiler warnings.  |

## Defines

|                | Name           |
| -------------- | -------------- |
|  | **[UNREACHABLE](/source-reference/Files/d7/d10/unreachable_8hpp/#define-unreachable)**  |




## Macros Documentation

### define UNREACHABLE

```cpp
#define UNREACHABLE throw Unreachable_At_Line<__LINE__>();
```


## Source code

```cpp
#ifndef SUPERGENIUS_UNREACHABLE_HPP
#define SUPERGENIUS_UNREACHABLE_HPP


#if defined(__GNUC__)
#define UNREACHABLE __builtin_unreachable();
#elif defined(_MSC_VER)
#define UNREACHABLE __assume(false);
#else
template <unsigned int LINE>
class Unreachable_At_Line {};
#define UNREACHABLE throw Unreachable_At_Line<__LINE__>();  // NOLINT
#endif

#undef GCC_VERSION

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

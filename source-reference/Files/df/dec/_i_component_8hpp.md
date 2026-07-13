---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/singleton/IComponent.hpp
summary: Component interface class. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/singleton/IComponent.hpp



Component interface class.  [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[IComponent](/source-reference/Classes/d1/dbf/class_i_component/)**  |

## Detailed Description

Component interface class. 

**Date**: 2024-02-23 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef _ICOMPONENT_HPP_
#define _ICOMPONENT_HPP_
#include <string>

class IComponent
{
public:
    virtual ~IComponent()         = default;
    virtual std::string GetName() = 0;

};

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

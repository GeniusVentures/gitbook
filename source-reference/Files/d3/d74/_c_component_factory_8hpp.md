---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/singleton/CComponentFactory.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/singleton/CComponentFactory.hpp



 [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[CComponentFactory](/source-reference/Classes/df/d07/class_c_component_factory/)**  |

## Detailed Description


**Date**: 2024-02-23 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef _CCOMPONENT_FACTORY_HPP_
#define _CCOMPONENT_FACTORY_HPP_

#include <unordered_map>
#include "singleton/IComponentFactory.hpp"
#include "singleton/Singleton.hpp"

class CComponentFactory : public IComponentFactory
{
    SINGLETON( CComponentFactory );

private:
    std::unordered_map<std::string, std::shared_ptr<IComponent>> ComponentTable;

public:
    void Register( std::shared_ptr<IComponent>         component,
                   const std::string                  &type,
                   const boost::optional<std::string> &variant = boost::none ) override;

    outcome::result<std::shared_ptr<IComponent>> GetComponent(
        const std::string &type, const boost::optional<std::string> &variant = boost::none ) override;
};

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

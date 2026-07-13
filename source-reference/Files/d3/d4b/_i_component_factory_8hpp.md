---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/singleton/IComponentFactory.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/singleton/IComponentFactory.hpp



 [More...](#detailed-description)

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[IComponentFactory](/source-reference/Classes/d0/d47/class_i_component_factory/)**  |

## Detailed Description


**Date**: 2024-02-23 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#include <memory>
#include <boost/optional.hpp>
#include "singleton/IComponent.hpp"
#include "outcome/outcome.hpp"

class IComponentFactory
{
public:
    virtual ~IComponentFactory() = default;

    virtual void Register( std::shared_ptr<IComponent>               component,
                           const std::string                        &type,
                           const boost::optional<std::string> &variant ) = 0;

    virtual outcome::result<std::shared_ptr<IComponent>> GetComponent(
        const std::string &type, const boost::optional<std::string> &variant ) = 0;
};
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

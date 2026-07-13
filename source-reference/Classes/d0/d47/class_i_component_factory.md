---
title: IComponentFactory

---

# IComponentFactory






`#include <IComponentFactory.hpp>`

Inherited by [CComponentFactory](/source-reference/Classes/df/d07/class_c_component_factory/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IComponentFactory](/source-reference/Classes/d0/d47/class_i_component_factory/#function-~icomponentfactory)**() =default |
| virtual void | **[Register](/source-reference/Classes/d0/d47/class_i_component_factory/#function-register)**(std::shared_ptr< [IComponent](/source-reference/Classes/d1/dbf/class_i_component/) > component, const std::string & type, const boost::optional< std::string > & variant) =0 |
| virtual outcome::result< std::shared_ptr< [IComponent](/source-reference/Classes/d1/dbf/class_i_component/) > > | **[GetComponent](/source-reference/Classes/d0/d47/class_i_component_factory/#function-getcomponent)**(const std::string & type, const boost::optional< std::string > & variant) =0 |

## Public Functions Documentation

### function ~IComponentFactory

```cpp
virtual ~IComponentFactory() =default
```


### function Register

```cpp
virtual void Register(
    std::shared_ptr< IComponent > component,
    const std::string & type,
    const boost::optional< std::string > & variant
) =0
```


**Reimplemented by**: [CComponentFactory::Register](/source-reference/Classes/df/d07/class_c_component_factory/#function-register)


### function GetComponent

```cpp
virtual outcome::result< std::shared_ptr< IComponent > > GetComponent(
    const std::string & type,
    const boost::optional< std::string > & variant
) =0
```


**Reimplemented by**: [CComponentFactory::GetComponent](/source-reference/Classes/df/d07/class_c_component_factory/#function-getcomponent)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
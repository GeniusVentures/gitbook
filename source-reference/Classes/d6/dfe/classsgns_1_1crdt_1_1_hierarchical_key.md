---
title: sgns::crdt::HierarchicalKey
summary: A Key represents the unique identifier of an object, inspired by file systems and Google App Engine key model. Keys are meant to be unique across a system. Keys are hierarchical, incorporating more and more specific namespaces. Thus keys can be deemed 'children' or 'ancestors' of other keys:: Key("/Comedy") Key("/Comedy/MontyPython") Also, every namespace can be parametrized to embed relevant object information. For example, the Key name (most specific namespace) could include the object type:: Key("/Comedy/MontyPython/Actor:JohnCleese") Key("/Comedy/MontyPython/Sketch:CheeseShop") Key("/Comedy/MontyPython/Sketch:CheeseShop/Character:Mousebender"). 

---

# sgns::crdt::HierarchicalKey



A Key represents the unique identifier of an object, inspired by file systems and Google App Engine key model. Keys are meant to be unique across a system. Keys are hierarchical, incorporating more and more specific namespaces. Thus keys can be deemed 'children' or 'ancestors' of other keys:: Key("/Comedy") Key("/Comedy/MontyPython") Also, every namespace can be parametrized to embed relevant object information. For example, the Key `name` (most specific namespace) could include the object type:: Key("/Comedy/MontyPython/Actor:JohnCleese") Key("/Comedy/MontyPython/Sketch:CheeseShop") Key("/Comedy/MontyPython/Sketch:CheeseShop/Character:Mousebender"). 


`#include <hierarchical_key.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/#function-hierarchicalkey)**() =default |
| | **[HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/#function-hierarchicalkey)**(std::string key) |
| void | **[SetKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/#function-setkey)**(const std::string & aKey) |
| std::string | **[GetKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/#function-getkey)**() const |
| [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/#function-hierarchicalkey) | **[ChildString](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/#function-childstring)**(std::string_view s) const<br/>Appends `s` to the key.  |
| std::vector< std::string > | **[GetList](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/#function-getlist)**() const |
| bool | **[IsTopLevel](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/#function-istoplevel)**() const |
| bool | **[operator==](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/#function-operator==)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/#function-hierarchicalkey) & rhs) const |
| bool | **[operator!=](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/#function-operator!=)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/#function-hierarchicalkey) & rhs) const |

## Public Functions Documentation

### function HierarchicalKey

```cpp
HierarchicalKey() =default
```


### function HierarchicalKey

```cpp
HierarchicalKey(
    std::string key
)
```


**Parameters**: 

  * **key** Key string 


Constructs a key from a string. 


### function SetKey

```cpp
inline void SetKey(
    const std::string & aKey
)
```


### function GetKey

```cpp
inline std::string GetKey() const
```


### function ChildString

```cpp
HierarchicalKey ChildString(
    std::string_view s
) const
```

Appends `s` to the key. 

**Parameters**: 

  * **s** String to be appended



NewKey("/Comedy/MontyPython").ChildString("Actor:JohnCleese") NewKey("/Comedy/MontyPython/Actor:JohnCleese") 


### function GetList

```cpp
std::vector< std::string > GetList() const
```


List returns the `list` representation of this Key. NewKey("/Comedy/MontyPython/Actor:JohnCleese").List() ["Comedy", "MontyPythong", "Actor:JohnCleese"] 


### function IsTopLevel

```cpp
bool IsTopLevel() const
```


### function operator==

```cpp
inline bool operator==(
    const HierarchicalKey & rhs
) const
```


### function operator!=

```cpp
inline bool operator!=(
    const HierarchicalKey & rhs
) const
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
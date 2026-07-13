---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/hierarchical_key.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/hierarchical_key.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/)** <br/>A Key represents the unique identifier of an object, inspired by file systems and Google App Engine key model. Keys are meant to be unique across a system. Keys are hierarchical, incorporating more and more specific namespaces. Thus keys can be deemed 'children' or 'ancestors' of other keys:: Key("/Comedy") Key("/Comedy/MontyPython") Also, every namespace can be parametrized to embed relevant object information. For example, the Key `name` (most specific namespace) could include the object type:: Key("/Comedy/MontyPython/Actor:JohnCleese") Key("/Comedy/MontyPython/Sketch:CheeseShop") Key("/Comedy/MontyPython/Sketch:CheeseShop/Character:Mousebender").  |




## Source code

```cpp
#ifndef SUPERGENIUS_HIERARCHICAL_KEY_HPP
#define SUPERGENIUS_HIERARCHICAL_KEY_HPP

#include <string>
#include <vector>

namespace sgns::crdt
{
  class HierarchicalKey
  {
  public:

    HierarchicalKey() = default;

    HierarchicalKey( std::string key );

    void SetKey(const std::string& aKey ) { key_ = aKey; };

    std::string GetKey() const { return key_; };

    HierarchicalKey ChildString( std::string_view s ) const;

    std::vector<std::string> GetList() const;

    bool IsTopLevel() const;

    bool operator==( const HierarchicalKey &rhs ) const
    {
      return key_ == rhs.key_;
    }

    bool operator!=( const HierarchicalKey &rhs ) const
    {
      return !operator==(rhs);
    }

  private:

    std::string key_;
  };
} // namespace sgns::crdt

#endif //SUPERGENIUS_HIERARCHICAL_KEY_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

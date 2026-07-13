---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/generic_iterator.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/generic_iterator.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::face](/source-reference/Namespaces/d0/d0d/namespacesgns_1_1face/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::face::GenericIterator](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/)**  |




## Source code

```cpp
#ifndef SUPERGENIUS_GENERIC_ITERATOR_HPP
#define SUPERGENIUS_GENERIC_ITERATOR_HPP

#include <memory>

namespace sgns::face {

  template <typename Container>
  class GenericIterator {
   public:
    using value_type = typename Container::value_type;

    virtual ~GenericIterator() = default;

    // needed as there's no simple way to copy an object by a pointer to its
    // abstract interface
    virtual std::unique_ptr<GenericIterator> clone() const = 0;

    virtual value_type *get() = 0;
    virtual value_type const *get() const = 0;

    virtual value_type &operator*() = 0;
    virtual value_type const &operator*() const = 0;

    virtual GenericIterator<Container> &operator++() = 0;

    value_type &operator->() {
      return **this;
    }

    virtual bool operator!=(const GenericIterator<Container> &other) const {
      return get() != other.get();
    }

    bool operator==(const GenericIterator<Container> &other) {
      return get() == other.get();
    }
  };

}  // namespace sgns::face

#endif  // SUPERGENIUS_GENERIC_ITERATOR_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

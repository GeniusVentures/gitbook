---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/generic_list.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/face/generic_list.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::face](/source-reference/Namespaces/d0/d0d/namespacesgns_1_1face/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::face::GenericList](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/)** <br/>An interface for a generic list.  |
| class | **[sgns::face::ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/)**  |




## Source code

```cpp
#ifndef SUPERGENIUS_GENERIC_LIST_HPP
#define SUPERGENIUS_GENERIC_LIST_HPP

#include <cstddef>
#include <memory>

#include "storage/face/generic_iterator.hpp"

namespace sgns::face {

  template <typename T>
  class ForwardIterator;

  template <typename T>
  class GenericList {
   public:
    using size_type = size_t;
    using value_type = T;
    using iterator = ForwardIterator<GenericList<T>>;

    virtual ~GenericList() = default;

    virtual void push_back(value_type &&t) = 0;
    virtual void push_back(const value_type &t) = 0;

    virtual void push_front(value_type &&t) = 0;
    virtual void push_front(const value_type &t) = 0;

    virtual value_type pop_back() = 0;

    virtual value_type pop_front() = 0;

    virtual void erase(const iterator &begin, const iterator &end) = 0;

    /*
     * Obtain an iterator to the list
     */
    virtual iterator begin() = 0;
    virtual iterator end() = 0;

    virtual bool empty() const = 0;

    virtual size_type size() const = 0;
  };

  template <typename Container>
  class ForwardIterator {
   public:
    using iterator_category = std::forward_iterator_tag;
    using pointer = typename Container::value_type *;
    using const_pointer = const typename Container::value_type *;
    using reference = typename Container::value_type &;
    using const_reference = const typename Container::value_type &;
    using value_type = typename Container::value_type;

    ForwardIterator(std::unique_ptr<GenericIterator<Container>> it)
        : it_{std::move(it)} {}

    ForwardIterator(ForwardIterator &&it) noexcept : it_{std::move(it.it_)} {}
    ForwardIterator(ForwardIterator const &it) : it_{it.it_->clone()} {}

    ~ForwardIterator() = default;

    GenericIterator<Container> &get_iterator() {
      return *it_;
    }

    GenericIterator<Container> const &get_iterator() const {
      return *it_;
    }

    ForwardIterator &operator=(const ForwardIterator &it) {
      it_ = it.it_->clone();
      return *this;
    }

    ForwardIterator &operator=(ForwardIterator &&it) noexcept {
      it_ = it.it_->clone();
      return *this;
    }

    bool operator!=(const ForwardIterator &other) {
      return *it_ != *other.it_;
    }

    bool operator==(const ForwardIterator &other) {
      return *it_ == *other.it_;
    }

    reference operator*() const {
      return **it_;
    }

    pointer operator->() {
      return it_->get();
    }

    ForwardIterator &operator++() {
      ++(*it_);
      return *this;
    }

   private:
    std::unique_ptr<GenericIterator<Container>> it_;
  };

}  // namespace sgns::face

#endif  // SUPERGENIUS_GENERIC_LIST_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

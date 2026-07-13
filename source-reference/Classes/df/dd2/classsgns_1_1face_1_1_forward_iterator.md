---
title: sgns::face::ForwardIterator

---

# sgns::face::ForwardIterator



 [More...](#detailed-description)


`#include <generic_list.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::forward_iterator_tag | **[iterator_category](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#using-iterator_category)**  |
| using typename Container::value_type * | **[pointer](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#using-pointer)**  |
| using const typename Container::value_type * | **[const_pointer](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#using-const_pointer)**  |
| using typename Container::value_type & | **[reference](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#using-reference)**  |
| using const typename Container::value_type & | **[const_reference](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#using-const_reference)**  |
| using typename Container::value_type | **[value_type](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#using-value_type)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-forwarditerator)**(std::unique_ptr< [GenericIterator](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/)< Container > > it) |
| | **[ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-forwarditerator)**(ForwardIterator && it) |
| | **[ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-forwarditerator)**(ForwardIterator const & it) |
| | **[~ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-~forwarditerator)**() =default |
| [GenericIterator](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/)< Container > & | **[get_iterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-get_iterator)**() |
| [GenericIterator](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/)< Container > const & | **[get_iterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-get_iterator)**() const |
| [ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-forwarditerator) & | **[operator=](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-operator=)**(const [ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-forwarditerator) & it) |
| [ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-forwarditerator) & | **[operator=](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-operator=)**([ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-forwarditerator) && it) |
| bool | **[operator!=](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-operator!=)**(const [ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-forwarditerator) & other) |
| bool | **[operator==](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-operator==)**(const [ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-forwarditerator) & other) |
| [reference](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#using-reference) | **[operator*](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-operator*)**() const |
| [pointer](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#using-pointer) | **[operator->](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-operator->)**() |
| [ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-forwarditerator) & | **[operator++](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/#function-operator++)**() |

## Detailed Description

```cpp
template <typename Container >
class sgns::face::ForwardIterator;
```


**Template Parameters**: 

  * **Container** over which the iterator would iterate 


As [GenericIterator](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/) is abstract and cannot be instantiated, there is a concrete object that wraps a pointer to a generic iterator 

## Public Types Documentation

### using iterator_category

```cpp
using sgns::face::ForwardIterator< Container >::iterator_category = std::forward_iterator_tag;
```


### using pointer

```cpp
using sgns::face::ForwardIterator< Container >::pointer = typename Container::value_type *;
```


### using const_pointer

```cpp
using sgns::face::ForwardIterator< Container >::const_pointer = const typename Container::value_type *;
```


### using reference

```cpp
using sgns::face::ForwardIterator< Container >::reference = typename Container::value_type &;
```


### using const_reference

```cpp
using sgns::face::ForwardIterator< Container >::const_reference = const typename Container::value_type &;
```


### using value_type

```cpp
using sgns::face::ForwardIterator< Container >::value_type = typename Container::value_type;
```


## Public Functions Documentation

### function ForwardIterator

```cpp
inline ForwardIterator(
    std::unique_ptr< GenericIterator< Container > > it
)
```


### function ForwardIterator

```cpp
inline ForwardIterator(
    ForwardIterator && it
)
```


### function ForwardIterator

```cpp
inline ForwardIterator(
    ForwardIterator const & it
)
```


### function ~ForwardIterator

```cpp
~ForwardIterator() =default
```


### function get_iterator

```cpp
inline GenericIterator< Container > & get_iterator()
```


### function get_iterator

```cpp
inline GenericIterator< Container > const & get_iterator() const
```


### function operator=

```cpp
inline ForwardIterator & operator=(
    const ForwardIterator & it
)
```


### function operator=

```cpp
inline ForwardIterator & operator=(
    ForwardIterator && it
)
```


### function operator!=

```cpp
inline bool operator!=(
    const ForwardIterator & other
)
```


### function operator==

```cpp
inline bool operator==(
    const ForwardIterator & other
)
```


### function operator*

```cpp
inline reference operator*() const
```


### function operator->

```cpp
inline pointer operator->()
```


### function operator++

```cpp
inline ForwardIterator & operator++()
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
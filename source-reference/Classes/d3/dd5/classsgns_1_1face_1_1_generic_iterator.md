---
title: sgns::face::GenericIterator

---

# sgns::face::GenericIterator



 [More...](#detailed-description)


`#include <generic_iterator.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| using typename Container::value_type | **[value_type](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#using-value_type)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~GenericIterator](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#function-~genericiterator)**() =default |
| virtual std::unique_ptr< [GenericIterator](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/) > | **[clone](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#function-clone)**() const =0 |
| virtual [value_type](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#using-value_type) * | **[get](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#function-get)**() =0 |
| virtual [value_type](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#using-value_type) const * | **[get](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#function-get)**() const =0 |
| virtual [value_type](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#using-value_type) & | **[operator*](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#function-operator*)**() =0 |
| virtual [value_type](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#using-value_type) const & | **[operator*](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#function-operator*)**() const =0 |
| virtual [GenericIterator](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/)< Container > & | **[operator++](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#function-operator++)**() =0 |
| [value_type](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#using-value_type) & | **[operator->](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#function-operator->)**() |
| virtual bool | **[operator!=](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#function-operator!=)**(const [GenericIterator](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/)< Container > & other) const |
| bool | **[operator==](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/#function-operator==)**(const [GenericIterator](/source-reference/Classes/d3/dd5/classsgns_1_1face_1_1_generic_iterator/)< Container > & other) |

## Detailed Description

```cpp
template <typename Container >
class sgns::face::GenericIterator;
```


**Template Parameters**: 

  * **Container** over which the iterator would iterate 


An interface for an iterator 

## Public Types Documentation

### using value_type

```cpp
using sgns::face::GenericIterator< Container >::value_type = typename Container::value_type;
```


## Public Functions Documentation

### function ~GenericIterator

```cpp
virtual ~GenericIterator() =default
```


### function clone

```cpp
virtual std::unique_ptr< GenericIterator > clone() const =0
```


### function get

```cpp
virtual value_type * get() =0
```


### function get

```cpp
virtual value_type const * get() const =0
```


### function operator*

```cpp
virtual value_type & operator*() =0
```


### function operator*

```cpp
virtual value_type const & operator*() const =0
```


### function operator++

```cpp
virtual GenericIterator< Container > & operator++() =0
```


### function operator->

```cpp
inline value_type & operator->()
```


### function operator!=

```cpp
inline virtual bool operator!=(
    const GenericIterator< Container > & other
) const
```


### function operator==

```cpp
inline bool operator==(
    const GenericIterator< Container > & other
)
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
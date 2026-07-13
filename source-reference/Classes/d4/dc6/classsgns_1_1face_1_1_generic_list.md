---
title: sgns::face::GenericList
summary: An interface for a generic list. 

---

# sgns::face::GenericList



An interface for a generic list.  [More...](#detailed-description)


`#include <generic_list.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| using size_t | **[size_type](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-size_type)**  |
| using T | **[value_type](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-value_type)**  |
| using [ForwardIterator](/source-reference/Classes/df/dd2/classsgns_1_1face_1_1_forward_iterator/)< [GenericList](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/)< T > > | **[iterator](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-iterator)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~GenericList](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#function-~genericlist)**() =default |
| virtual void | **[push_back](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#function-push_back)**([value_type](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-value_type) && t) =0 |
| virtual void | **[push_back](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#function-push_back)**(const [value_type](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-value_type) & t) =0 |
| virtual void | **[push_front](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#function-push_front)**([value_type](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-value_type) && t) =0 |
| virtual void | **[push_front](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#function-push_front)**(const [value_type](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-value_type) & t) =0 |
| virtual [value_type](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-value_type) | **[pop_back](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#function-pop_back)**() =0 |
| virtual [value_type](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-value_type) | **[pop_front](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#function-pop_front)**() =0 |
| virtual void | **[erase](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#function-erase)**(const [iterator](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-iterator) & begin, const [iterator](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-iterator) & end) =0 |
| virtual [iterator](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-iterator) | **[begin](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#function-begin)**() =0 |
| virtual [iterator](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-iterator) | **[end](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#function-end)**() =0 |
| virtual bool | **[empty](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#function-empty)**() const =0 |
| virtual [size_type](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#using-size_type) | **[size](/source-reference/Classes/d4/dc6/classsgns_1_1face_1_1_generic_list/#function-size)**() const =0 |

## Detailed Description

```cpp
template <typename T >
class sgns::face::GenericList;
```

An interface for a generic list. 
## Public Types Documentation

### using size_type

```cpp
using sgns::face::GenericList< T >::size_type = size_t;
```


### using value_type

```cpp
using sgns::face::GenericList< T >::value_type = T;
```


### using iterator

```cpp
using sgns::face::GenericList< T >::iterator = ForwardIterator<GenericList<T>>;
```


## Public Functions Documentation

### function ~GenericList

```cpp
virtual ~GenericList() =default
```


### function push_back

```cpp
virtual void push_back(
    value_type && t
) =0
```


Put an element to the back of the list 


### function push_back

```cpp
virtual void push_back(
    const value_type & t
) =0
```


### function push_front

```cpp
virtual void push_front(
    value_type && t
) =0
```


Put an element to the front of the list 


### function push_front

```cpp
virtual void push_front(
    const value_type & t
) =0
```


### function pop_back

```cpp
virtual value_type pop_back() =0
```


Get the back of the list and then remove it 


### function pop_front

```cpp
virtual value_type pop_front() =0
```


Get the front of the list and then remove it 


### function erase

```cpp
virtual void erase(
    const iterator & begin,
    const iterator & end
) =0
```


Erase a range of elements 


### function begin

```cpp
virtual iterator begin() =0
```


### function end

```cpp
virtual iterator end() =0
```


### function empty

```cpp
virtual bool empty() const =0
```


Tell whether list is empty 


### function size

```cpp
virtual size_type size() const =0
```


Obtain the size of the list 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
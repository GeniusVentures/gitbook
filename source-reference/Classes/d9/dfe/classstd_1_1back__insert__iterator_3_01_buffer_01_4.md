---
title: std::back_insert_iterator< Buffer >

---

# std::back_insert_iterator< Buffer >






`#include <buffer_back_insert_iterator.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| using [Buffer::value_type](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/#using-value_type) | **[value_type](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#using-value_type)**  |
| using typename std::vector< uint8_t >::difference_type | **[difference_type](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#using-difference_type)**  |
| using [Buffer::pointer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/#using-pointer) | **[pointer](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#using-pointer)**  |
| using typename std::vector< uint8_t >::reference | **[reference](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#using-reference)**  |
| using std::random_access_iterator_tag | **[iterator_category](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#using-iterator_category)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| constexpr | **[back_insert_iterator](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-back_insert_iterator)**([Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & c) |
| | **[back_insert_iterator](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-back_insert_iterator)**(const back_insert_iterator< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > & a) |
| [back_insert_iterator](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-back_insert_iterator)< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > & | **[operator=](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-operator=)**(const [back_insert_iterator](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-back_insert_iterator)< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > & a) |
| [back_insert_iterator](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-back_insert_iterator)< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > & | **[operator=](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-operator=)**(uint8_t value) |
| [back_insert_iterator](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-back_insert_iterator)< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > & | **[operator=](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-operator=)**(uint32_t value) |
| [back_insert_iterator](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-back_insert_iterator)< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > & | **[operator=](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-operator=)**(std::string_view value) |
| [back_insert_iterator](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-back_insert_iterator)< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > & | **[operator=](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-operator=)**(gsl::span< const uint8_t > s) |
| [back_insert_iterator](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-back_insert_iterator)< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > & | **[operator=](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-operator=)**(const std::vector< uint8_t > & v) |
| [back_insert_iterator](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-back_insert_iterator) & | **[operator*](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-operator*)**() |
| [back_insert_iterator](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-back_insert_iterator) & | **[operator++](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-operator++)**() |
| [back_insert_iterator](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-back_insert_iterator) & | **[operator++](/source-reference/Classes/d9/dfe/classstd_1_1back__insert__iterator_3_01_buffer_01_4/#function-operator++)**(int ) |

## Public Types Documentation

### using value_type

```cpp
using std::back_insert_iterator< Buffer >::value_type = Buffer::value_type;
```


### using difference_type

```cpp
using std::back_insert_iterator< Buffer >::difference_type = typename std::vector<uint8_t>::difference_type;
```


### using pointer

```cpp
using std::back_insert_iterator< Buffer >::pointer = Buffer::pointer;
```


### using reference

```cpp
using std::back_insert_iterator< Buffer >::reference = typename std::vector<uint8_t>::reference;
```


### using iterator_category

```cpp
using std::back_insert_iterator< Buffer >::iterator_category = std::random_access_iterator_tag;
```


## Public Functions Documentation

### function back_insert_iterator

```cpp
inline explicit constexpr back_insert_iterator(
    Buffer & c
)
```


### function back_insert_iterator

```cpp
inline back_insert_iterator(
    const back_insert_iterator< Buffer > & a
)
```


### function operator=

```cpp
inline back_insert_iterator< Buffer > & operator=(
    const back_insert_iterator< Buffer > & a
)
```


### function operator=

```cpp
inline back_insert_iterator< Buffer > & operator=(
    uint8_t value
)
```


### function operator=

```cpp
inline back_insert_iterator< Buffer > & operator=(
    uint32_t value
)
```


### function operator=

```cpp
inline back_insert_iterator< Buffer > & operator=(
    std::string_view value
)
```


### function operator=

```cpp
inline back_insert_iterator< Buffer > & operator=(
    gsl::span< const uint8_t > s
)
```


### function operator=

```cpp
inline back_insert_iterator< Buffer > & operator=(
    const std::vector< uint8_t > & v
)
```


### function operator*

```cpp
inline back_insert_iterator & operator*()
```


### function operator++

```cpp
inline back_insert_iterator & operator++()
```


### function operator++

```cpp
inline back_insert_iterator & operator++(
    int 
)
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
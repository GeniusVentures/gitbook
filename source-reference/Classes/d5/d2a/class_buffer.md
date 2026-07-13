---
title: Buffer
summary: Class represents arbitrary (including empty) byte buffer. 

---

# Buffer



Class represents arbitrary (including empty) byte buffer. 


`#include <buffer.hpp>`

Inherits from boost::equality_comparable< Buffer >, boost::equality_comparable< gsl::span< uint8_t > >, boost::equality_comparable< std::vector< uint8_t > >

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::vector< uint8_t >::iterator | **[iterator](/source-reference/Classes/d5/d2a/class_buffer/#using-iterator)**  |
| using std::vector< uint8_t >::reverse_iterator | **[reverse_iterator](/source-reference/Classes/d5/d2a/class_buffer/#using-reverse_iterator)**  |
| using std::vector< uint8_t >::const_reverse_iterator | **[const_reverse_iterator](/source-reference/Classes/d5/d2a/class_buffer/#using-const_reverse_iterator)**  |
| using std::vector< uint8_t >::const_iterator | **[const_iterator](/source-reference/Classes/d5/d2a/class_buffer/#using-const_iterator)**  |
| using uint8_t | **[value_type](/source-reference/Classes/d5/d2a/class_buffer/#using-value_type)**  |
| using typename std::vector< uint8_t >::pointer | **[pointer](/source-reference/Classes/d5/d2a/class_buffer/#using-pointer)**  |
| using typename std::vector< uint8_t >::const_pointer | **[const_pointer](/source-reference/Classes/d5/d2a/class_buffer/#using-const_pointer)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[Buffer](/source-reference/Classes/d5/d2a/class_buffer/#function-buffer)**(size_t size, uint8_t byte)<br/>Allocates a buffer of the given size, filled with a byte value.  |
| | **[Buffer](/source-reference/Classes/d5/d2a/class_buffer/#function-buffer)**(std::vector< uint8_t > v)<br/>lvalue construct buffer from a byte vector  |
| | **[Buffer](/source-reference/Classes/d5/d2a/class_buffer/#function-buffer)**(gsl::span< const uint8_t > s) |
| | **[Buffer](/source-reference/Classes/d5/d2a/class_buffer/#function-buffer)**(const uint8_t * begin, const uint8_t * end) |
| | **[Buffer](/source-reference/Classes/d5/d2a/class_buffer/#function-buffer)**() =default |
| | **[Buffer](/source-reference/Classes/d5/d2a/class_buffer/#function-buffer)**(const [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & b) =default |
| | **[Buffer](/source-reference/Classes/d5/d2a/class_buffer/#function-buffer)**([Buffer](/source-reference/Classes/d5/d2a/class_buffer/) && b) =default |
| | **[Buffer](/source-reference/Classes/d5/d2a/class_buffer/#function-buffer)**(std::initializer_list< uint8_t > b) |
| | **[~Buffer](/source-reference/Classes/d5/d2a/class_buffer/#function-~buffer)**() =default |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[reserve](/source-reference/Classes/d5/d2a/class_buffer/#function-reserve)**(size_t size) |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[resize](/source-reference/Classes/d5/d2a/class_buffer/#function-resize)**(size_t size) |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[operator=](/source-reference/Classes/d5/d2a/class_buffer/#function-operator=)**(const [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & other) =default |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[operator=](/source-reference/Classes/d5/d2a/class_buffer/#function-operator=)**([Buffer](/source-reference/Classes/d5/d2a/class_buffer/) && other) =default |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[operator+=](/source-reference/Classes/d5/d2a/class_buffer/#function-operator+=)**(const [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & other) |
| uint8_t | **[operator[]](/source-reference/Classes/d5/d2a/class_buffer/#function-operator[])**(size_t index) const<br/>Accessor of byte elements given an index in the byte array.  |
| uint8_t & | **[operator[]](/source-reference/Classes/d5/d2a/class_buffer/#function-operator[])**(size_t index)<br/>Accessor of byte elements given an index in the byte array.  |
| bool | **[operator==](/source-reference/Classes/d5/d2a/class_buffer/#function-operator==)**(const [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & b) const<br/>Lexicographical comparison of two buffers.  |
| bool | **[operator==](/source-reference/Classes/d5/d2a/class_buffer/#function-operator==)**(const std::vector< uint8_t > & b) const<br/>Lexicographical comparison of buffer and vector of bytes.  |
| bool | **[operator==](/source-reference/Classes/d5/d2a/class_buffer/#function-operator==)**(gsl::span< const uint8_t > s) const<br/>Lexicographical comparison of buffer and vector of bytes.  |
| bool | **[operator<](/source-reference/Classes/d5/d2a/class_buffer/#function-operator<)**(const [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & b) const<br/>Lexicographical comparison of two buffers.  |
| [iterator](/source-reference/Classes/d5/d2a/class_buffer/#using-iterator) | **[begin](/source-reference/Classes/d5/d2a/class_buffer/#function-begin)**()<br/>Iterator, which points to begin of this buffer.  |
| [const_iterator](/source-reference/Classes/d5/d2a/class_buffer/#using-const_iterator) | **[begin](/source-reference/Classes/d5/d2a/class_buffer/#function-begin)**() const<br/>Iterator, which points to begin of this buffer.  |
| [iterator](/source-reference/Classes/d5/d2a/class_buffer/#using-iterator) | **[end](/source-reference/Classes/d5/d2a/class_buffer/#function-end)**()<br/>Iterator, which points to the element next to the last in this buffer.  |
| [const_iterator](/source-reference/Classes/d5/d2a/class_buffer/#using-const_iterator) | **[end](/source-reference/Classes/d5/d2a/class_buffer/#function-end)**() const<br/>Iterator, which points to the element next to the last in this buffer.  |
| [reverse_iterator](/source-reference/Classes/d5/d2a/class_buffer/#using-reverse_iterator) | **[rbegin](/source-reference/Classes/d5/d2a/class_buffer/#function-rbegin)**()<br/>Iterator, which points to last of this buffer.  |
| [const_reverse_iterator](/source-reference/Classes/d5/d2a/class_buffer/#using-const_reverse_iterator) | **[rbegin](/source-reference/Classes/d5/d2a/class_buffer/#function-rbegin)**() const<br/>Iterator, which points to last of this buffer.  |
| [reverse_iterator](/source-reference/Classes/d5/d2a/class_buffer/#using-reverse_iterator) | **[rend](/source-reference/Classes/d5/d2a/class_buffer/#function-rend)**()<br/>Iterator, which points to the element previous to first in this buffer.  |
| [const_reverse_iterator](/source-reference/Classes/d5/d2a/class_buffer/#using-const_reverse_iterator) | **[rend](/source-reference/Classes/d5/d2a/class_buffer/#function-rend)**() const<br/>Iterator, which points to the element previous to first in this buffer.  |
| size_t | **[size](/source-reference/Classes/d5/d2a/class_buffer/#function-size)**() const<br/>Getter for size of this buffer.  |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[putUint8](/source-reference/Classes/d5/d2a/class_buffer/#function-putuint8)**(uint8_t n)<br/>Put an 8-bit value into this buffer.  |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[putUint32](/source-reference/Classes/d5/d2a/class_buffer/#function-putuint32)**(uint32_t n)<br/>Put a 32-bit value into this buffer.  |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[putUint64](/source-reference/Classes/d5/d2a/class_buffer/#function-putuint64)**(uint64_t n)<br/>Put a 64-bit value into this buffer.  |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[put](/source-reference/Classes/d5/d2a/class_buffer/#function-put)**(std::string_view str)<br/>Put a string into the byte buffer.  |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[put](/source-reference/Classes/d5/d2a/class_buffer/#function-put)**(const std::vector< uint8_t > & v)<br/>Put a vector of bytes into the byte buffer.  |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[put](/source-reference/Classes/d5/d2a/class_buffer/#function-put)**(gsl::span< const uint8_t > s)<br/>Put a sequence of bytes into the byte buffer.  |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[putBytes](/source-reference/Classes/d5/d2a/class_buffer/#function-putbytes)**(const uint8_t * begin, const uint8_t * end)<br/>Put an array of bytes bounded by pointers into the byte buffer.  |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & | **[putBuffer](/source-reference/Classes/d5/d2a/class_buffer/#function-putbuffer)**(const [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & buf)<br/>Put another buffer content at the end of current one.  |
| void | **[clear](/source-reference/Classes/d5/d2a/class_buffer/#function-clear)**() |
| const uint8_t * | **[data](/source-reference/Classes/d5/d2a/class_buffer/#function-data)**() const<br/>getter for raw array of bytes  |
| uint8_t * | **[data](/source-reference/Classes/d5/d2a/class_buffer/#function-data)**() |
| const std::vector< uint8_t > & | **[toVector](/source-reference/Classes/d5/d2a/class_buffer/#function-tovector)**() const<br/>getter for vector of bytes  |
| std::vector< uint8_t > & | **[toVector](/source-reference/Classes/d5/d2a/class_buffer/#function-tovector)**() |
| [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) | **[subbuffer](/source-reference/Classes/d5/d2a/class_buffer/#function-subbuffer)**(size_t offset =0, size_t length =-1) const |
| std::string | **[toHex](/source-reference/Classes/d5/d2a/class_buffer/#function-tohex)**() const<br/>encode bytearray as hex  |
| bool | **[empty](/source-reference/Classes/d5/d2a/class_buffer/#function-empty)**() const |
| std::string_view | **[toString](/source-reference/Classes/d5/d2a/class_buffer/#function-tostring)**() const<br/>return content of bytearray as string  |
| outcome::result< [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) > | **[fromHex](/source-reference/Classes/d5/d2a/class_buffer/#function-fromhex)**(std::string_view hex)<br/>Construct [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) from hex string.  |

## Public Types Documentation

### using iterator

```cpp
using sgns::base::Buffer::iterator = std::vector<uint8_t>::iterator;
```


### using reverse_iterator

```cpp
using sgns::base::Buffer::reverse_iterator = std::vector<uint8_t>::reverse_iterator;
```


### using const_reverse_iterator

```cpp
using sgns::base::Buffer::const_reverse_iterator = std::vector<uint8_t>::const_reverse_iterator;
```


### using const_iterator

```cpp
using sgns::base::Buffer::const_iterator = std::vector<uint8_t>::const_iterator;
```


### using value_type

```cpp
using sgns::base::Buffer::value_type = uint8_t;
```


### using pointer

```cpp
using sgns::base::Buffer::pointer = typename std::vector<uint8_t>::pointer;
```


### using const_pointer

```cpp
using sgns::base::Buffer::const_pointer = typename std::vector<uint8_t>::const_pointer;
```


## Public Functions Documentation

### function Buffer

```cpp
Buffer(
    size_t size,
    uint8_t byte
)
```

Allocates a buffer of the given size, filled with a byte value. 

**Parameters**: 

  * **[size](/source-reference/Classes/d5/d2a/class_buffer/#function-size)** [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) size in bytes. 
  * **byte** Fill value for all bytes. 


### function Buffer

```cpp
explicit Buffer(
    std::vector< uint8_t > v
)
```

lvalue construct buffer from a byte vector 

### function Buffer

```cpp
explicit Buffer(
    gsl::span< const uint8_t > s
)
```


### function Buffer

```cpp
Buffer(
    const uint8_t * begin,
    const uint8_t * end
)
```


### function Buffer

```cpp
Buffer() =default
```


### function Buffer

```cpp
Buffer(
    const Buffer & b
) =default
```


### function Buffer

```cpp
Buffer(
    Buffer && b
) =default
```


### function Buffer

```cpp
Buffer(
    std::initializer_list< uint8_t > b
)
```


### function ~Buffer

```cpp
~Buffer() =default
```


### function reserve

```cpp
Buffer & reserve(
    size_t size
)
```


### function resize

```cpp
Buffer & resize(
    size_t size
)
```


### function operator=

```cpp
Buffer & operator=(
    const Buffer & other
) =default
```


### function operator=

```cpp
Buffer & operator=(
    Buffer && other
) =default
```


### function operator+=

```cpp
Buffer & operator+=(
    const Buffer & other
)
```


### function operator[]

```cpp
uint8_t operator[](
    size_t index
) const
```

Accessor of byte elements given an index in the byte array. 

**Parameters**: 

  * **index** Element index. 


### function operator[]

```cpp
uint8_t & operator[](
    size_t index
)
```

Accessor of byte elements given an index in the byte array. 

**Parameters**: 

  * **index** Element index. 


### function operator==

```cpp
bool operator==(
    const Buffer & b
) const
```

Lexicographical comparison of two buffers. 

### function operator==

```cpp
bool operator==(
    const std::vector< uint8_t > & b
) const
```

Lexicographical comparison of buffer and vector of bytes. 

### function operator==

```cpp
bool operator==(
    gsl::span< const uint8_t > s
) const
```

Lexicographical comparison of buffer and vector of bytes. 

### function operator<

```cpp
bool operator<(
    const Buffer & b
) const
```

Lexicographical comparison of two buffers. 

### function begin

```cpp
iterator begin()
```

Iterator, which points to begin of this buffer. 

### function begin

```cpp
const_iterator begin() const
```

Iterator, which points to begin of this buffer. 

### function end

```cpp
iterator end()
```

Iterator, which points to the element next to the last in this buffer. 

### function end

```cpp
const_iterator end() const
```

Iterator, which points to the element next to the last in this buffer. 

### function rbegin

```cpp
reverse_iterator rbegin()
```

Iterator, which points to last of this buffer. 

### function rbegin

```cpp
const_reverse_iterator rbegin() const
```

Iterator, which points to last of this buffer. 

### function rend

```cpp
reverse_iterator rend()
```

Iterator, which points to the element previous to first in this buffer. 

### function rend

```cpp
const_reverse_iterator rend() const
```

Iterator, which points to the element previous to first in this buffer. 

### function size

```cpp
size_t size() const
```

Getter for size of this buffer. 

### function putUint8

```cpp
Buffer & putUint8(
    uint8_t n
)
```

Put an 8-bit value into this buffer. 

**Parameters**: 

  * **n** Value to append. 


**Return**: This buffer, suitable for chaining. 

### function putUint32

```cpp
Buffer & putUint32(
    uint32_t n
)
```

Put a 32-bit value into this buffer. 

**Parameters**: 

  * **n** Value to append (serialized as big-endian). 


**Return**: This buffer, suitable for chaining. 

### function putUint64

```cpp
Buffer & putUint64(
    uint64_t n
)
```

Put a 64-bit value into this buffer. 

**Parameters**: 

  * **n** Value to append (serialized as big-endian). 


**Return**: This buffer, suitable for chaining. 

### function put

```cpp
Buffer & put(
    std::string_view str
)
```

Put a string into the byte buffer. 

**Parameters**: 

  * **str** Arbitrary string. 


**Return**: This buffer, suitable for chaining. 

### function put

```cpp
Buffer & put(
    const std::vector< uint8_t > & v
)
```

Put a vector of bytes into the byte buffer. 

**Parameters**: 

  * **v** Arbitrary vector of bytes. 


**Return**: This buffer, suitable for chaining. 

### function put

```cpp
Buffer & put(
    gsl::span< const uint8_t > s
)
```

Put a sequence of bytes into the byte buffer. 

**Parameters**: 

  * **s** Arbitrary span of bytes. 


**Return**: This buffer, suitable for chaining. 

### function putBytes

```cpp
Buffer & putBytes(
    const uint8_t * begin,
    const uint8_t * end
)
```

Put an array of bytes bounded by pointers into the byte buffer. 

**Parameters**: 

  * **[begin](/source-reference/Classes/d5/d2a/class_buffer/#function-begin)** Pointer to the array start. 
  * **[end](/source-reference/Classes/d5/d2a/class_buffer/#function-end)** Pointer to the address after the last element. 


**Return**: This buffer, suitable for chaining. 

### function putBuffer

```cpp
Buffer & putBuffer(
    const Buffer & buf
)
```

Put another buffer content at the end of current one. 

**Parameters**: 

  * **buf** another buffer 


**Return**: this buffer suitable for chaining. 

### function clear

```cpp
void clear()
```


Clear the contents of the [Buffer](/source-reference/Classes/d5/d2a/class_buffer/)


### function data

```cpp
const uint8_t * data() const
```

getter for raw array of bytes 

### function data

```cpp
uint8_t * data()
```


### function toVector

```cpp
const std::vector< uint8_t > & toVector() const
```

getter for vector of bytes 

### function toVector

```cpp
std::vector< uint8_t > & toVector()
```


### function subbuffer

```cpp
Buffer subbuffer(
    size_t offset =0,
    size_t length =-1
) const
```


Returns a copy of a part of the buffer Works alike subspan() of gsl::span 


### function toHex

```cpp
std::string toHex() const
```

encode bytearray as hex 

**Return**: hex-encoded string 

### function empty

```cpp
bool empty() const
```


**Return**: true, if buffer is empty, false otherwise 

Check if this buffer is empty 


### function toString

```cpp
std::string_view toString() const
```

return content of bytearray as string 

**Return**: string 

**Note**: Does not ensure correct encoding 

### function fromHex

```cpp
static outcome::result< Buffer > fromHex(
    std::string_view hex
)
```

Construct [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) from hex string. 

**Parameters**: 

  * **hex** hex-encoded string 


**Return**: result containing constructed buffer if input string is hex-encoded string. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/buffer.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/buffer.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/)**  |
| **[std](/source-reference/Namespaces/d8/dcc/namespacestd/)** <br/>STL namespace.  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/)** <br/>Class represents arbitrary (including empty) byte buffer.  |
| struct | **[std::hash< sgns::base::Buffer >](/source-reference/Classes/d0/dcb/structstd_1_1hash_3_01sgns_1_1base_1_1_buffer_01_4/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| template <class Stream ,typename  =std::enable_if_t<Stream::is_encoder_stream>\> <br/>Stream & | **[operator<<](/source-reference/Files/da/d1d/buffer_8hpp/#function-operator<<)**(Stream & s, const [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & buffer)<br/>override operator<< for all streams except std::ostream  |
| template <class Stream ,typename  =std::enable_if_t<Stream::is_decoder_stream>\> <br/>Stream & | **[operator>>](/source-reference/Files/da/d1d/buffer_8hpp/#function-operator>>)**(Stream & s, [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & buffer)<br/>decodes buffer object from stream  |
| std::ostream & | **[operator<<](/source-reference/Files/da/d1d/buffer_8hpp/#function-operator<<)**(std::ostream & os, const [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) & buffer) |


## Functions Documentation

### function operator<<

```cpp
template <class Stream ,
typename  =std::enable_if_t<Stream::is_encoder_stream>>
Stream & operator<<(
    Stream & s,
    const Buffer & buffer
)
```

override operator<< for all streams except std::ostream 

**Parameters**: 

  * **s** stream reference 
  * **buffer** value to encode 


**Template Parameters**: 

  * **Stream** stream type 


**Return**: reference to stream 

### function operator>>

```cpp
template <class Stream ,
typename  =std::enable_if_t<Stream::is_decoder_stream>>
Stream & operator>>(
    Stream & s,
    Buffer & buffer
)
```

decodes buffer object from stream 

**Parameters**: 

  * **s** stream reference 
  * **buffer** value to decode 


**Template Parameters**: 

  * **Stream** input stream type 


**Return**: reference to stream 

### function operator<<

```cpp
std::ostream & operator<<(
    std::ostream & os,
    const Buffer & buffer
)
```




## Source code

```cpp
#ifndef SUPERGENIUS_BUFFER_HPP
#define SUPERGENIUS_BUFFER_HPP

#include <string_view>
#include <vector>

#include <boost/container_hash/hash.hpp>
#include <boost/operators.hpp>
#include <gsl/span>
#include "outcome/outcome.hpp"

namespace sgns::base {

  class Buffer : public boost::equality_comparable<Buffer>,
                 public boost::equality_comparable<gsl::span<uint8_t>>,
                 public boost::equality_comparable<std::vector<uint8_t>> {
   public:
    using iterator = std::vector<uint8_t>::iterator;
    using reverse_iterator = std::vector<uint8_t>::reverse_iterator;
    using const_reverse_iterator = std::vector<uint8_t>::const_reverse_iterator;
    using const_iterator = std::vector<uint8_t>::const_iterator;
    using value_type = uint8_t;
    // with this gsl::span can be built from Buffer
    using pointer = typename std::vector<uint8_t>::pointer;
    using const_pointer = typename std::vector<uint8_t>::const_pointer;

    Buffer(size_t size, uint8_t byte);

    ~Buffer() = default;

    explicit Buffer(std::vector<uint8_t> v);
    explicit Buffer(gsl::span<const uint8_t> s);

    Buffer(const uint8_t *begin, const uint8_t *end);

    Buffer() = default;
    Buffer(const Buffer &b) = default;
    Buffer(Buffer &&b) noexcept = default;
    Buffer(std::initializer_list<uint8_t> b);

    Buffer &reserve(size_t size);
    Buffer &resize(size_t size);

    Buffer &operator=(const Buffer &other) = default;
    Buffer &operator=(Buffer &&other) noexcept = default;

    Buffer &operator+=(const Buffer &other) noexcept;

    uint8_t operator[](size_t index) const;

    uint8_t &operator[](size_t index);

    bool operator==(const Buffer &b) const noexcept;

    bool operator==(const std::vector<uint8_t> &b) const noexcept;

    bool operator==(gsl::span<const uint8_t> s) const noexcept;

    bool operator<(const Buffer &b) const noexcept;

    iterator begin();

    iterator end();
    reverse_iterator rbegin();

    reverse_iterator rend();
    [[nodiscard]] const_reverse_iterator rbegin() const;

    [[nodiscard]] const_reverse_iterator rend() const;

    [[nodiscard]] const_iterator begin() const;

    [[nodiscard]] const_iterator end() const;

    [[nodiscard]] size_t size() const;

    Buffer &putUint8(uint8_t n);

    Buffer &putUint32(uint32_t n);

    Buffer &putUint64(uint64_t n);

    Buffer &put(std::string_view str);

    Buffer &put(const std::vector<uint8_t> &v);

    Buffer &put(gsl::span<const uint8_t> s);

    Buffer &putBytes(const uint8_t *begin, const uint8_t *end);

    Buffer &putBuffer(const Buffer &buf);

    void clear();

    const uint8_t *data() const;
    uint8_t *data();

    const std::vector<uint8_t> &toVector() const;

    std::vector<uint8_t> &toVector();

    Buffer subbuffer(size_t offset = 0, size_t length = -1) const;

    std::string toHex() const;

    bool empty() const;

    static outcome::result<Buffer> fromHex(std::string_view hex);

    std::string_view toString() const;

private:
    std::vector<uint8_t> data_;

    template <typename T>
    Buffer &putRange(const T &begin, const T &end);
  };

  template <class Stream,
            typename = std::enable_if_t<Stream::is_encoder_stream>>
  Stream &operator<<(Stream &s, const Buffer &buffer) {
    return s << buffer.toVector();
  }

  template <class Stream,
            typename = std::enable_if_t<Stream::is_decoder_stream>>
  Stream &operator>>(Stream &s, Buffer &buffer) {
    std::vector<uint8_t> data;
    s >> data;
    buffer.put(data);
    return s;
  }

  std::ostream &operator<<(std::ostream &os, const Buffer &buffer);

}  // namespace sgns::base

namespace std {
  template <>
  struct hash<sgns::base::Buffer> {
    size_t operator()(const sgns::base::Buffer &x) const {
      return boost::hash_range(x.begin(), x.end());
    }
  };
}  // namespace std

#endif  // SUPERGENIUS_BUFFER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

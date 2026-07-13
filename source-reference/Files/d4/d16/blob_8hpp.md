---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/blob.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/blob.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::base::Blob](/source-reference/Classes/d4/dc6/classsgns_1_1base_1_1_blob/)**  |
| struct | **[std::hash< sgns::base::Blob< N > >](/source-reference/Classes/d9/d75/structstd_1_1hash_3_01sgns_1_1base_1_1_blob_3_01_n_01_4_01_4/)**  |

## Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[BlobError](/source-reference/Files/d4/d16/blob_8hpp/#enum-bloberror)** { INCORRECT_LENGTH = 1} |
| using Blob< 8 > | **[Hash64](/source-reference/Files/d4/d16/blob_8hpp/#using-hash64)**  |
| using Blob< 16 > | **[Hash128](/source-reference/Files/d4/d16/blob_8hpp/#using-hash128)**  |
| using Blob< 32 > | **[Hash256](/source-reference/Files/d4/d16/blob_8hpp/#using-hash256)**  |
| using Blob< 64 > | **[Hash512](/source-reference/Files/d4/d16/blob_8hpp/#using-hash512)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| template <class Stream ,size_t size,typename  =std::enable_if_t<Stream::is_encoder_stream>\> <br/>Stream & | **[operator<<](/source-reference/Files/d4/d16/blob_8hpp/#function-operator<<)**(Stream & s, const Blob< size > & blob)<br/>scale-encodes blob instance to stream  |
| template <class Stream ,size_t size,typename  =std::enable_if_t<Stream::is_decoder_stream>\> <br/>Stream & | **[operator>>](/source-reference/Files/d4/d16/blob_8hpp/#function-operator>>)**(Stream & s, Blob< size > & blob)<br/>decodes blob instance from stream  |
| template <size_t N\> <br/>std::ostream & | **[operator<<](/source-reference/Files/d4/d16/blob_8hpp/#function-operator<<)**(std::ostream & os, const Blob< N > & blob) |
| | **[OUTCOME_HPP_DECLARE_ERROR_2](/source-reference/Files/d4/d16/blob_8hpp/#function-outcome_hpp_declare_error_2)**([sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/) , BlobError ) |

## Types Documentation

### enum BlobError

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| INCORRECT_LENGTH | 1|   |




Error codes for exceptions that may occur during blob initialization 


### using Hash64

```cpp
using sgns::base::Hash64 = Blob<8>;
```


### using Hash128

```cpp
using sgns::base::Hash128 = Blob<16>;
```


### using Hash256

```cpp
using sgns::base::Hash256 = Blob<32>;
```


### using Hash512

```cpp
using sgns::base::Hash512 = Blob<64>;
```



## Functions Documentation

### function operator<<

```cpp
template <class Stream ,
size_t size,
typename  =std::enable_if_t<Stream::is_encoder_stream>>
Stream & operator<<(
    Stream & s,
    const Blob< size > & blob
)
```

scale-encodes blob instance to stream 

**Parameters**: 

  * **s** output stream reference 
  * **blob** value to encode 


**Template Parameters**: 

  * **Stream** output stream type 
  * **size** blob size 


**Return**: reference to stream 

### function operator>>

```cpp
template <class Stream ,
size_t size,
typename  =std::enable_if_t<Stream::is_decoder_stream>>
Stream & operator>>(
    Stream & s,
    Blob< size > & blob
)
```

decodes blob instance from stream 

**Parameters**: 

  * **s** input stream reference 
  * **blob** value to encode 


**Template Parameters**: 

  * **Stream** output stream type 
  * **size** blob size 


**Return**: reference to stream 

### function operator<<

```cpp
template <size_t N>
inline std::ostream & operator<<(
    std::ostream & os,
    const Blob< N > & blob
)
```


### function OUTCOME_HPP_DECLARE_ERROR_2

```cpp
OUTCOME_HPP_DECLARE_ERROR_2(
    sgns::base ,
    BlobError 
)
```




## Source code

```cpp
#ifndef SUPERGENIUS_BLOB_HPP
#define SUPERGENIUS_BLOB_HPP

#include <cstddef>
#include <array>

#include <boost/functional/hash.hpp>
#include "base/hexutil.hpp"
#include <iostream>

namespace sgns::base {

  enum class BlobError { INCORRECT_LENGTH = 1 };

  template <size_t size_>
  class Blob : public std::array<uint8_t, size_> {
   public:
    Blob() {
      this->fill(0);
    }

    explicit constexpr Blob( const std::array<uint8_t, size_> &l )
    {
        std::copy( l.begin(), l.end(), this->begin() );
    }

    constexpr static size_t size() {
      return size_;
    }

    [[nodiscard]] std::string toString() const noexcept
    {
        return std::string{ this->begin(), this->end() };
    }

    [[nodiscard]] std::string toReadableString() const noexcept
    {
        std::string out_str;
        char        temp_buf[3];

        for ( auto it = this->begin(); it != this->end(); ++it )
        {
            snprintf( temp_buf, sizeof( temp_buf ), "%02x", *it );
            out_str.append( temp_buf, sizeof( temp_buf ) - 1 );
        }

        return out_str;
    }

    [[nodiscard]] std::string toHex() const noexcept
    {
        // return hex_lower({this->begin(), this->end()});
        return hex_lower( gsl::make_span( *this ) );
    }

    static outcome::result<Blob<size_>> fromString(std::string_view data) {
      if (data.size() != size_) {
        return BlobError::INCORRECT_LENGTH;
      }

      Blob<size_> b;
      std::copy(data.begin(), data.end(), b.begin());

      return b;
    }


    static outcome::result<Blob<size_>> fromReadableString(std::string_view data) {
      if (data.size()/2 != size_) {
        return BlobError::INCORRECT_LENGTH;
      }
      Blob<size_> b;

      for ( std::size_t i = 0; i < data.size(); i+=2 )
      {
          std::string byteString = std::string(data).substr(i, 2);
          char byte = static_cast<char>(std::stoul(byteString, nullptr, 16));
          b[i/2] = static_cast<uint8_t>(byte);
      }


      return b;
    }

    static outcome::result<Blob<size_>> fromHex(std::string_view hex) {
      BOOST_OUTCOME_TRY( auto res, unhex(hex));
      return fromSpan(res);
    }

    static outcome::result<Blob<size_>> fromHexWithPrefix(
        std::string_view hex) {
      BOOST_OUTCOME_TRY( auto res, unhexWith0x(hex));
      return fromSpan(res);
    }

    static outcome::result<Blob<size_>> fromSpan(
        gsl::span<uint8_t> span) {
      if (span.size() != size_) {
        return BlobError::INCORRECT_LENGTH;
      }

      Blob<size_> blob;
      std::copy(span.begin(), span.end(), blob.begin());
      return blob;
    }

    [[nodiscard]] std::vector<uint8_t> ToVec() const
    {
        return { this->begin(), this->end() };
    }
  };

  // extern specification of the most frequently instantiated blob
  // specializations, used mostly for Hash instantiation
  extern template class Blob<8ul>;
  extern template class Blob<16ul>;
  extern template class Blob<32ul>;
  extern template class Blob<64ul>;

  // Hash specializations
  using Hash64 = Blob<8>;
  using Hash128 = Blob<16>;
  using Hash256 = Blob<32>;
  using Hash512 = Blob<64>;

  template <class Stream,
            size_t size,
            typename = std::enable_if_t<Stream::is_encoder_stream>>
  Stream &operator<<(Stream &s, const Blob<size> &blob) {
    for (auto &&it = blob.begin(), end = blob.end(); it != end; ++it) {
      s << *it;
    }
    return s;
  }

  template <class Stream,
            size_t size,
            typename = std::enable_if_t<Stream::is_decoder_stream>>
  Stream &operator>>(Stream &s, Blob<size> &blob) {
    for (auto &&it = blob.begin(), end = blob.end(); it != end; ++it) {
      s >> *it;
    }
    return s;
  }

  template <size_t N>
  inline std::ostream &operator<<(std::ostream &os, const Blob<N> &blob) {
    return os << blob.toHex();
  }

}  // namespace sgns::base

template <size_t N>
struct std::hash<sgns::base::Blob<N>> {
  auto operator()(const sgns::base::Blob<N> &blob) const {
    return boost::hash_range(blob.data(), blob.data() + N);  // NOLINT
  }
};

OUTCOME_HPP_DECLARE_ERROR_2(sgns::base, BlobError);

#endif  // SUPERGENIUS_BLOB_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

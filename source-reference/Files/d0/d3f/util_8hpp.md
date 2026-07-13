---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/util.hpp
summary: Utilities functions header file. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/util.hpp



Utilities functions header file.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| std::string | **[to_string](/source-reference/Files/d0/d3f/util_8hpp/#function-to_string)**(const std::vector< unsigned char > & bytes)<br/>Convert a byte array to a hexadecimal string.  |
| bool | **[isLittleEndian](/source-reference/Files/d0/d3f/util_8hpp/#function-islittleendian)**()<br/>Checks if the architecture is little endian.  |
| template <typename T \> <br/>T | **[Vector2Num](/source-reference/Files/d0/d3f/util_8hpp/#function-vector2num)**(const std::vector< uint8_t > & bytes)<br/>Converts a little-endian byte vector into a number.  |
| uint128_t | **[Vector2Num](/source-reference/Files/d0/d3f/util_8hpp/#function-vector2num)**(const std::vector< uint8_t > & bytes) |
| uint256_t | **[Vector2Num](/source-reference/Files/d0/d3f/util_8hpp/#function-vector2num)**(const std::vector< uint8_t > & bytes) |
| template <typename T \> <br/>std::vector< uint8_t > | **[Num2Vector](/source-reference/Files/d0/d3f/util_8hpp/#function-num2vector)**(const T & num, std::size_t num_bytes_resolution =sizeof(T))<br/>Converts a number into a byte vector (little-endian).  |
| template <typename T \> <br/>T | **[HexASCII2Num](/source-reference/Files/d0/d3f/util_8hpp/#function-hexascii2num)**(const char * p_char, std::size_t num_nibbles_resolution =sizeof(T) *2)<br/>Converts a hexadecimal ASCII char array into a number.  |
| template <typename T \> <br/>std::vector< T > | **[HexASCII2NumStr](/source-reference/Files/d0/d3f/util_8hpp/#function-hexascii2numstr)**(const char * p_char, std::size_t char_ptr_size)<br/>Converts a hexadecimal ASCII char array into a vector of numbers.  |
| template <typename T \> <br/>std::enable_if_t< std::is_same_v< typename T::value_type, uint8_t > > | **[AdjustEndianess](/source-reference/Files/d0/d3f/util_8hpp/#function-adjustendianess)**(T & data, std::optional< typename T::iterator > start =std::nullopt, std::optional< typename T::iterator > finish =std::nullopt)<br/>Adjust endianess if needed.  |
| std::string | **[Uint256ToString](/source-reference/Files/d0/d3f/util_8hpp/#function-uint256tostring)**(const uint256_t & value) |
| template <typename Condition \> <br/>bool | **[waitForCondition](/source-reference/Files/d0/d3f/util_8hpp/#function-waitforcondition)**(Condition condition, std::chrono::milliseconds timeout, std::chrono::milliseconds * actualDuration =nullptr, std::chrono::milliseconds check_interval =std::chrono::milliseconds(10)) |

## Detailed Description

Utilities functions header file. 

**Date**: 2024-01-12 Super Genius ([ken@gnus.ai](mailto:ken@gnus.ai)) Henrique A. Klein ([henryaklein@gmail.com](mailto:henryaklein@gmail.com)) 

## Functions Documentation

### function to_string

```cpp
static std::string to_string(
    const std::vector< unsigned char > & bytes
)
```

Convert a byte array to a hexadecimal string. 

**Parameters**: 

  * **bytes** A vector of bytes to be converted. 


**Return**: A hexadecimal string representation of the bytes. 

### function isLittleEndian

```cpp
static bool isLittleEndian()
```

Checks if the architecture is little endian. 

**Return**: true if little endian, false otherwise 

### function Vector2Num

```cpp
template <typename T >
static T Vector2Num(
    const std::vector< uint8_t > & bytes
)
```

Converts a little-endian byte vector into a number. 

**Parameters**: 

  * **bytes** Byte vector to convert. 


**Template Parameters**: 

  * **T** uint8_t, uint16_t, uint32_t, uint64_t, or supported multiprecision integer types. 


**Return**: The converted number. 

### function Vector2Num

```cpp
uint128_t Vector2Num(
    const std::vector< uint8_t > & bytes
)
```


### function Vector2Num

```cpp
uint256_t Vector2Num(
    const std::vector< uint8_t > & bytes
)
```


### function Num2Vector

```cpp
template <typename T >
static std::vector< uint8_t > Num2Vector(
    const T & num,
    std::size_t num_bytes_resolution =sizeof(T)
)
```

Converts a number into a byte vector (little-endian). 

**Parameters**: 

  * **num** Number to convert. 
  * **num_bytes_resolution** Optional byte resolution (defaults to sizeof(T)). 


**Template Parameters**: 

  * **T** uint8_t, uint16_t, uint32_t or uint64_t 


**Return**: The converted byte vector. 

### function HexASCII2Num

```cpp
template <typename T >
static T HexASCII2Num(
    const char * p_char,
    std::size_t num_nibbles_resolution =sizeof(T) *2
)
```

Converts a hexadecimal ASCII char array into a number. 

**Parameters**: 

  * **p_char** Hexadecimal ASCII char array 
  * **num_nibbles_resolution** How many nibbles will constitute a number 


**Template Parameters**: 

  * **T** uint8_t, uint16_t, uint32_t or uint64_t 


**Return**: The converted number (8-64 bit variable) 

### function HexASCII2NumStr

```cpp
template <typename T >
static std::vector< T > HexASCII2NumStr(
    const char * p_char,
    std::size_t char_ptr_size
)
```

Converts a hexadecimal ASCII char array into a vector of numbers. 

**Parameters**: 

  * **p_char** Hexadecimal ASCII char array 
  * **char_ptr_size** Size of the char array 


**Template Parameters**: 

  * **T** uint8_t, uint16_t, uint32_t or uint64_t 


**Return**: The vector of converted numbers 

### function AdjustEndianess

```cpp
template <typename T >
static std::enable_if_t< std::is_same_v< typename T::value_type, uint8_t > > AdjustEndianess(
    T & data,
    std::optional< typename T::iterator > start =std::nullopt,
    std::optional< typename T::iterator > finish =std::nullopt
)
```

Adjust endianess if needed. 

**Parameters**: 

  * **data** The container of data (vector/array) 
  * **start** Optional beginning of the valid data 
  * **finish** Optional ending of the valid data 


**Template Parameters**: 

  * **T** std::vector<uint8_t> or std::array<uint8_t,N> 


### function Uint256ToString

```cpp
static std::string Uint256ToString(
    const uint256_t & value
)
```


### function waitForCondition

```cpp
template <typename Condition >
bool waitForCondition(
    Condition condition,
    std::chrono::milliseconds timeout,
    std::chrono::milliseconds * actualDuration =nullptr,
    std::chrono::milliseconds check_interval =std::chrono::milliseconds(10)
)
```


**Parameters**: 

  * **condition** a callable that returns bool, true when condition is met 
  * **timeout** maximum time to wait 
  * **actualDuration** optional pointer to store the actual wait duration 
  * **check_interval** time to wait between condition checks 


**Return**: true if condition became true before timeout, false if timeout occurred 

Wait for a condition to become true with timeout 




## Source code

```cpp


#ifndef _UTIL_HPP
#define _UTIL_HPP

#include <string>
#include <vector>
#include <type_traits>
#include <optional>
#include <algorithm>
#include <cmath>
#include <charconv>
#include <boost/random.hpp>
#include <boost/random/mersenne_twister.hpp>
#include <boost/random/uniform_int_distribution.hpp>
#include <boost/multiprecision/cpp_int.hpp>
#include "outcome/outcome.hpp"

namespace sgns
{
    using namespace boost::multiprecision;
    namespace br = boost::random;

    static std::string to_string( const std::vector<unsigned char> &bytes )
    {
        std::string out_str;
        char        temp_buf[3];
        for ( auto it = bytes.rbegin(); it != bytes.rend(); ++it )
        {
            snprintf( temp_buf, sizeof( temp_buf ), "%02x", *it );
            out_str.append( temp_buf, sizeof( temp_buf ) - 1 );
        }
        return out_str;
    }

    static bool isLittleEndian()
    {
        std::uint32_t num     = 1;
        auto         *bytePtr = reinterpret_cast<std::uint8_t *>( &num );

        return *bytePtr == 1;
    }


    template <typename T>
    static T Vector2Num( const std::vector<uint8_t> &bytes )
    {
        static_assert(
            std::is_integral_v<T> || std::is_same_v<T, boost::multiprecision::uint128_t> ||
                std::is_same_v<T, boost::multiprecision::uint256_t>,
            "T must be an integral type or boost::multiprecision::uint128_t or boost::multiprecision::uint256_t" );
        if ( bytes.size() > sizeof( T ) )
        {
            throw std::invalid_argument( "Byte vector too large for conversion" );
        }

        T value = 0;
        for ( size_t i = 0; i < bytes.size(); ++i )
        {
            value |= static_cast<T>( bytes[i] ) << ( i * 8 );
        }
        return value;
    }

    template <>
    uint128_t Vector2Num( const std::vector<uint8_t> &bytes )
    {
        if ( bytes.size() > 16 )
        {
            throw std::invalid_argument( "Byte vector too large for conversion" );
        }

        uint128_t value = 0;
        for ( size_t i = 0; i < bytes.size(); ++i )
        {
            value |= static_cast<uint128_t>( bytes[i] ) << ( i * 8 );
        }
        return value;
    }

    template <>
    uint256_t Vector2Num( const std::vector<uint8_t> &bytes )
    {
        if ( bytes.size() > 32 )
        {
            throw std::invalid_argument( "Byte vector too large for conversion" );
        }

        uint256_t value = 0;
        for ( size_t i = 0; i < bytes.size(); ++i )
        {
            value |= static_cast<uint256_t>( bytes[i] ) << ( i * 8 );
        }
        return value;
    }

    template <typename T>
    static std::vector<uint8_t> Num2Vector( const T &num, std::size_t num_bytes_resolution = sizeof( T ) )
    {
        const auto *bytesPtr = reinterpret_cast<const uint8_t *>( &num );
        return std::vector<uint8_t>( bytesPtr, bytesPtr + sizeof( T ) );
    }

    template <typename T>
    static T HexASCII2Num( const char *p_char, std::size_t num_nibbles_resolution = sizeof( T ) * 2 )
    {
        T sum = 0;

        for ( std::size_t i = 0; i < num_nibbles_resolution; ++i )
        {
            if ( std::isdigit( p_char[i] ) )
            {
                sum += ( ( p_char[i] - '0' ) << ( 4 * ( num_nibbles_resolution - i - 1 ) ) );
            }
            else
            {
                sum += ( ( std::toupper( p_char[i] ) - 'A' + 10 ) << ( 4 * ( num_nibbles_resolution - i - 1 ) ) );
            }
        }

        return sum;
    }

    template <typename T>
    static std::vector<T> HexASCII2NumStr( const char *p_char, std::size_t char_ptr_size )
    {
        static_assert( std::is_same_v<T, uint8_t> || std::is_same_v<T, uint16_t> || std::is_same_v<T, uint32_t> ||
                       std::is_same_v<T, uint64_t> );
        std::vector<T> out_vect;
        std::size_t    num_nibbles_resolution = ( sizeof( T ) * 2 );
        auto           point_of_insertion     = [&]()
        {
            if ( isLittleEndian() )
            {
                return out_vect.begin();
            }

            return out_vect.end();
        };

        for ( std::size_t i = 0; i < char_ptr_size; i += num_nibbles_resolution )
        {
            out_vect.insert( point_of_insertion(), static_cast<T>( HexASCII2Num<T>( &p_char[i] ) ) );
        }
        return out_vect;
    }

    template <typename T>
    static std::enable_if_t<std::is_same_v<typename T::value_type, uint8_t>> AdjustEndianess(
        T                                  &data,
        std::optional<typename T::iterator> start  = std::nullopt,
        std::optional<typename T::iterator> finish = std::nullopt )
    {
        if ( !start )
        {
            start = data.begin();
        }
        if ( !finish )
        {
            finish = data.end();
        }
        if ( !isLittleEndian() )
        {
            std::reverse( start.value(), finish.value() );
        }
    }

    static std::string Uint256ToString( const uint256_t &value )
    {
        std::ostringstream oss;
        oss << "0x";
        oss << std::hex << std::setw( 64 ) << std::setfill( '0' ) << value;
        return oss.str();
    }
}

template <typename Condition>
bool waitForCondition(Condition condition,
                     std::chrono::milliseconds timeout,
                     std::chrono::milliseconds* actualDuration = nullptr,
                     std::chrono::milliseconds check_interval = std::chrono::milliseconds(10)) {
    auto startTime = std::chrono::steady_clock::now();
    while (!condition()) {
        if (std::chrono::steady_clock::now() - startTime > timeout) {
            if (actualDuration) {
                *actualDuration = std::chrono::duration_cast<std::chrono::milliseconds>(
                    std::chrono::steady_clock::now() - startTime);
            }
            return false; // Timeout occurred
        }
        std::this_thread::sleep_for(check_interval);
    }

    if (actualDuration) {
        *actualDuration = std::chrono::duration_cast<std::chrono::milliseconds>(
            std::chrono::steady_clock::now() - startTime);
    }
    return true; // Condition met within timeout
}


#endif //_UTIL_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

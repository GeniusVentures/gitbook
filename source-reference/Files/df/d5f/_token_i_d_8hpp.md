---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/TokenID.hpp
summary: Fixed-size token identifier wrapper with GNUS compatibility helpers. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/TokenID.hpp



Fixed-size token identifier wrapper with GNUS compatibility helpers.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/)** <br/>Represents a 32-byte token identifier while preserving legacy GNUS semantics.  |

## Functions

|                | Name           |
| -------------- | -------------- |
| std::ostream & | **[operator<<](/source-reference/Files/df/d5f/_token_i_d_8hpp/#function-operator<<)**(std::ostream & os, const [sgns::TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) & id)<br/>Streams a token identifier as hexadecimal text.  |

## Detailed Description

Fixed-size token identifier wrapper with GNUS compatibility helpers. 

**Date**: 2025-06-19 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 

## Functions Documentation

### function operator<<

```cpp
inline std::ostream & operator<<(
    std::ostream & os,
    const sgns::TokenID & id
)
```

Streams a token identifier as hexadecimal text. 

**Parameters**: 

  * **os** Output stream to write to. 
  * **id** Token identifier to stream. 


**Return**: Reference to `os` after writing the token identifier. 



## Source code

```cpp

#ifndef SGNS_TOKEN_ID_HPP
#define SGNS_TOKEN_ID_HPP

#include <array>
#include <algorithm>
#include <cstdint>
#include <cstring>
#include <iomanip>
#include <string>
#include <sstream>

namespace sgns
{
    class TokenID
    {
    public:
        using ByteArray = std::array<uint8_t, 32>;

        enum class Endianness
        {
            HOST,
            BIG,
            LITTLE
        };

        constexpr TokenID() : data_{}, valid_( false ) {}

        TokenID( const TokenID &other ) = default;

        TokenID( TokenID &&other ) = default;

        TokenID &operator=( const TokenID &other ) = default;

        TokenID &operator=( TokenID &&other ) = default;

        static TokenID FromBytes( std::initializer_list<uint8_t> list )
        {
            return FromBytes( list.begin(), list.size() );
        }

        static TokenID FromBytes( const void *data, size_t size )
        {
            TokenID id;
            if ( !data || size == 0 )
            {
                // legacy/invalid case
                return id;
            }

            if ( size <= 32 )
            {
                // size 1–32: left-pad into the 32-byte buffer
                size_t copy_size = std::min( size, id.data_.size() );
                std::memcpy( id.data_.data() + ( id.data_.size() - copy_size ), data, copy_size );
                id.valid_ = true;
            }

            return id;
        }

        template <typename Uint256>
        static TokenID FromUint256( const Uint256 &value, Endianness endianness = Endianness::HOST )
        {
            static_assert( Uint256::num_bits == 256, "FromUint256 requires a 256-bit unsigned integer type" );

            const Endianness resolved_endianness = ResolveEndianness( endianness );

            TokenID id;
            for ( size_t i = 0; i < id.data_.size(); ++i )
            {
                const size_t byte_index = resolved_endianness == Endianness::BIG ? id.data_.size() - 1 - i : i;
                id.data_[i]             = static_cast<uint8_t>( ( value >> ( byte_index * 8 ) ) & 0xFF );
            }

            id.valid_ = true;
            return id;
        }

        const ByteArray &bytes() const
        {
            return data_;
        }

        size_t size() const
        {
            return valid_ ? 32 : 0;
        }

        bool operator==( const TokenID &other ) const
        {
            return valid_ == other.valid_ && data_ == other.data_;
        }

        bool operator!=( const TokenID &other ) const
        {
            return !( *this == other );
        }

        bool operator<( const TokenID &other ) const
        {
            return data_ < other.data_; // lexicographic comparison
        }

        std::string ToHex() const
        {
            std::ostringstream oss;
            for ( uint8_t byte : data_ )
            {
                oss << std::hex << std::setw( 2 ) << std::setfill( '0' ) << (int) byte;
            }
            return oss.str();
        }

        bool IsGNUS() const
        {
            return !valid_ || std::all_of( data_.begin(), data_.end(), []( uint8_t b ) { return b == 0; } );
        }

        bool Equals( const TokenID &other ) const
        {
            if ( *this == other )
            {
                return true;
            }
            return this->IsGNUS() && other.IsGNUS();
        }

    private:
        static Endianness ResolveEndianness( Endianness endianness )
        {
            if ( endianness != Endianness::HOST )
            {
                return endianness;
            }

            const uint16_t value = 0x0001;
            return *reinterpret_cast<const uint8_t *>( &value ) == 0x01 ? Endianness::LITTLE : Endianness::BIG;
        }

        ByteArray data_;  
        bool      valid_; 
    };
}

inline std::ostream &operator<<( std::ostream &os, const sgns::TokenID &id )
{
    return os << id.ToHex();
}

#endif // SGNS_TOKEN_ID_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

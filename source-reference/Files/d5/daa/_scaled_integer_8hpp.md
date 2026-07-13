---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/ScaledInteger.hpp
summary: Utilities for decimal arithmetic using scaled integers. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/ScaledInteger.hpp



Utilities for decimal arithmetic using scaled integers.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/)** <br/>Represents a decimal value using an integer scaled by 10^precision.  |

## Detailed Description

Utilities for decimal arithmetic using scaled integers. 

**Version**: 1.1 

**Date**: 2025-06-10 

**Copyright**: Copyright (c) 2025 

Luiz Guilherme Rizzatto Zucchi ([luizgrz@gmail.com](mailto:luizgrz@gmail.com)) 




## Source code

```cpp


#ifndef SGNS_SCALED_INTEGER_HPP
#define SGNS_SCALED_INTEGER_HPP

#include <string>
#include <memory>
#include <boost/multiprecision/cpp_int.hpp>
#include "outcome/outcome.hpp"

namespace sgns
{
    class ScaledInteger
    {
    public:
        enum class ParseMode
        {
            Strict,   
            Truncate, 
        };

        static outcome::result<std::shared_ptr<ScaledInteger>> New( uint64_t raw_value, uint64_t precision );

        static outcome::result<std::shared_ptr<ScaledInteger>> New( double value, uint64_t precision );

        static outcome::result<std::shared_ptr<ScaledInteger>> New( const std::string &str,
                                                                    uint64_t           precision,
                                                                    ParseMode          mode = ParseMode::Strict );

        static outcome::result<std::shared_ptr<ScaledInteger>> New( const std::string &str );

        static constexpr uint64_t ScaleFactor( uint64_t precision );

        static outcome::result<uint64_t> FromString( const std::string &str,
                                                     uint64_t           precision,
                                                     ParseMode          mode = ParseMode::Strict );

        static std::string ToString( uint64_t value, uint64_t precision );

        static outcome::result<uint64_t> FromDouble( double value, uint64_t precision );

        static outcome::result<uint64_t> Multiply( uint64_t a, uint64_t b, uint64_t precision );

        static outcome::result<uint64_t> Divide( uint64_t a, uint64_t b, uint64_t precision );

        static outcome::result<uint64_t> ConvertPrecision( uint64_t value, uint64_t from, uint64_t to );

        uint64_t Value() const noexcept;

        uint64_t Precision() const noexcept;

        std::string ToString( bool fixedDecimals = true ) const;

        outcome::result<ScaledInteger> Add( const ScaledInteger &other ) const;

        outcome::result<ScaledInteger> Subtract( const ScaledInteger &other ) const;

        outcome::result<ScaledInteger> Multiply( const ScaledInteger &other ) const;

        outcome::result<ScaledInteger> Divide( const ScaledInteger &other ) const;

        outcome::result<ScaledInteger> ConvertPrecision( uint64_t to ) const;

    private:
        explicit ScaledInteger( uint64_t value, uint64_t precision );

        uint64_t value_;
        uint64_t precision_;
    };

} // namespace sgns

#endif // SGNS_SCALED_INTEGER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

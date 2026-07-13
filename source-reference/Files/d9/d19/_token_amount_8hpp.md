---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/TokenAmount.hpp
summary: Fixed-precision (6 decimals) token amount type with arithmetic helpers. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/TokenAmount.hpp



Fixed-precision (6 decimals) token amount type with arithmetic helpers.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/)** <br/>Utility for GNUS token fixed-point parsing, formatting and cost calculation.  |

## Detailed Description

Fixed-precision (6 decimals) token amount type with arithmetic helpers. 

**Copyright**: 2025 



## Source code

```cpp


#ifndef SGNS_TOKEN_AMOUNT_HPP
#define SGNS_TOKEN_AMOUNT_HPP

#include <string>
#include <memory>
#include "outcome/outcome.hpp"

namespace sgns
{
    class TokenAmount
    {
    public:
        static constexpr uint64_t PRECISION = 6;

        static constexpr uint64_t PRICE_PER_FLOP = 500;

        static constexpr uint64_t PRICE_PER_FLOP_FRACTIONAL_DIGITS = 15;

        static constexpr uint64_t FLOPS_PER_BYTE = 20;

        static constexpr uint64_t MIN_MINION_UNITS = 1;

        static outcome::result<std::shared_ptr<TokenAmount>> New( uint64_t raw_minions );

        static outcome::result<std::shared_ptr<TokenAmount>> New( double value );

        static outcome::result<std::shared_ptr<TokenAmount>> New( const std::string &str );

        outcome::result<TokenAmount> Multiply( const TokenAmount &other ) const;

        outcome::result<TokenAmount> Divide( const TokenAmount &other ) const;

        uint64_t Value() const;

        static outcome::result<uint64_t> ParseMinions( const std::string &str );

        static std::string FormatMinions( uint64_t minions );

        static outcome::result<uint64_t> CalculateCostMinions( uint64_t total_bytes, double price_usd_per_genius );

        static outcome::result<std::string> ConvertToChildToken( uint64_t in, std::string ratio );
        static outcome::result<uint64_t>    ConvertFromChildToken( std::string in, std::string ratio );

    private:
        uint64_t minions_;

        TokenAmount( uint64_t minion_units );
    };

} // namespace sgns

#endif // SGNS_TOKEN_AMOUNT_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: sgns::TokenAmount
summary: Utility for GNUS token fixed-point parsing, formatting and cost calculation. 

---

# sgns::TokenAmount



Utility for GNUS token fixed-point parsing, formatting and cost calculation. 


`#include <TokenAmount.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| outcome::result< std::shared_ptr< [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-tokenamount) > > | **[New](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-new)**(uint64_t raw_minions)<br/>Creates a [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) from already-scaled minion units.  |
| outcome::result< std::shared_ptr< [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-tokenamount) > > | **[New](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-new)**(double value)<br/>Creates a [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) from a floating point value. The value is rounded to 6 decimal digits internally.  |
| outcome::result< std::shared_ptr< [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-tokenamount) > > | **[New](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-new)**(const std::string & str)<br/>Creates a [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) from a decimal string.  |
| outcome::result< uint64_t > | **[ParseMinions](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-parseminions)**(const std::string & str)<br/>Parses a token amount string into raw minion units.  |
| std::string | **[FormatMinions](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-formatminions)**(uint64_t minions)<br/>Converts raw minion units to a token string.  |
| outcome::result< uint64_t > | **[CalculateCostMinions](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-calculatecostminions)**(uint64_t total_bytes, double price_usd_per_genius)<br/>Calculates token cost for a given byte size and USD price.  |
| outcome::result< std::string > | **[ConvertToChildToken](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-converttochildtoken)**(uint64_t in, std::string ratio) |
| outcome::result< uint64_t > | **[ConvertFromChildToken](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-convertfromchildtoken)**(std::string in, std::string ratio) |
| outcome::result< [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-tokenamount) > | **[Multiply](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-multiply)**(const [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-tokenamount) & other) const<br/>Multiplies this [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) by another.  |
| outcome::result< [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-tokenamount) > | **[Divide](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-divide)**(const [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-tokenamount) & other) const<br/>Divides this [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) by another.  |
| uint64_t | **[Value](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#function-value)**() const<br/>Returns the raw scaled integer (minion) value.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| uint64_t | **[PRECISION](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#variable-precision)** <br/>Fixed-point precision (1 minion = 10^-6 GNUS).  |
| uint64_t | **[PRICE_PER_FLOP](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#variable-price_per_flop)** <br/>USD per FLOP rate scaled by 10^15.  |
| uint64_t | **[PRICE_PER_FLOP_FRACTIONAL_DIGITS](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#variable-price_per_flop_fractional_digits)** <br/>Fractional digits used in USD/FLOP rate.  |
| uint64_t | **[FLOPS_PER_BYTE](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#variable-flops_per_byte)** <br/>Estimated number of FLOPs required per byte.  |
| uint64_t | **[MIN_MINION_UNITS](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/#variable-min_minion_units)** <br/>Minimum representable non-zero minion units.  |

## Public Functions Documentation

### function New

```cpp
static outcome::result< std::shared_ptr< TokenAmount > > New(
    uint64_t raw_minions
)
```

Creates a [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) from already-scaled minion units. 

**Parameters**: 

  * **raw_minions** Value in 10^6-scaled integer units. 


**Return**: A shared pointer to a [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) instance or error code. 

### function New

```cpp
static outcome::result< std::shared_ptr< TokenAmount > > New(
    double value
)
```

Creates a [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) from a floating point value. The value is rounded to 6 decimal digits internally. 

**Parameters**: 

  * **value** Floating point value representing token amount. 


**Return**: A shared pointer to a [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) instance or error code. 

### function New

```cpp
static outcome::result< std::shared_ptr< TokenAmount > > New(
    const std::string & str
)
```

Creates a [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) from a decimal string. 

**Parameters**: 

  * **str** String representation of the token amount. 


**Return**: A shared pointer to a [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) instance or error code. 

### function ParseMinions

```cpp
static outcome::result< uint64_t > ParseMinions(
    const std::string & str
)
```

Parses a token amount string into raw minion units. 

**Parameters**: 

  * **str** Decimal string representation (e.g., "0.001000"). 


**Return**: Parsed minion value or error. 

### function FormatMinions

```cpp
static std::string FormatMinions(
    uint64_t minions
)
```

Converts raw minion units to a token string. 

**Parameters**: 

  * **minions** Raw integer minion units. 


**Return**: Formatted string with fixed-point representation. 

Ensures exactly 6 digits of precision in the result.


### function CalculateCostMinions

```cpp
static outcome::result< uint64_t > CalculateCostMinions(
    uint64_t total_bytes,
    double price_usd_per_genius
)
```

Calculates token cost for a given byte size and USD price. 

**Parameters**: 

  * **total_bytes** Total number of bytes processed. 
  * **price_usd_per_genius** GNUS token price in USD. 


**Return**: Total cost in minion units, or error on overflow/underflow. 

Internally estimates FLOPs based on bytes, applies the FLOP pricing and converts to GNUS token units using the provided USD price.


### function ConvertToChildToken

```cpp
static outcome::result< std::string > ConvertToChildToken(
    uint64_t in,
    std::string ratio
)
```


### function ConvertFromChildToken

```cpp
static outcome::result< uint64_t > ConvertFromChildToken(
    std::string in,
    std::string ratio
)
```


### function Multiply

```cpp
outcome::result< TokenAmount > Multiply(
    const TokenAmount & other
) const
```

Multiplies this [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) by another. 

**Parameters**: 

  * **other** Another [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) instance. 


**Return**: Result of the multiplication or error. 

Result is rounded back to fixed 6-digit precision.


### function Divide

```cpp
outcome::result< TokenAmount > Divide(
    const TokenAmount & other
) const
```

Divides this [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) by another. 

**Parameters**: 

  * **other** Another [TokenAmount](/source-reference/Classes/dd/dd7/classsgns_1_1_token_amount/) instance. 


**Return**: Result of the division or error. 

### function Value

```cpp
uint64_t Value() const
```

Returns the raw scaled integer (minion) value. 

**Return**: Value in raw minion units (10^6 scaled). 

## Public Attributes Documentation

### variable PRECISION

```cpp
static uint64_t PRECISION = 6;
```

Fixed-point precision (1 minion = 10^-6 GNUS). 

### variable PRICE_PER_FLOP

```cpp
static uint64_t PRICE_PER_FLOP = 500;
```

USD per FLOP rate scaled by 10^15. 

### variable PRICE_PER_FLOP_FRACTIONAL_DIGITS

```cpp
static uint64_t PRICE_PER_FLOP_FRACTIONAL_DIGITS = 15;
```

Fractional digits used in USD/FLOP rate. 

### variable FLOPS_PER_BYTE

```cpp
static uint64_t FLOPS_PER_BYTE = 20;
```

Estimated number of FLOPs required per byte. 

### variable MIN_MINION_UNITS

```cpp
static uint64_t MIN_MINION_UNITS = 1;
```

Minimum representable non-zero minion units. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
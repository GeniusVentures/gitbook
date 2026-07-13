---
title: sgns::ScaledInteger
summary: Represents a decimal value using an integer scaled by 10^precision. 

---

# sgns::ScaledInteger



Represents a decimal value using an integer scaled by 10^precision.  [More...](#detailed-description)


`#include <ScaledInteger.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[ParseMode](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#enum-parsemode)** { Strict, Truncate}<br/>Controls handling of extra fractional digits when parsing.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| outcome::result< std::shared_ptr< [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) > > | **[New](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-new)**(uint64_t raw_value, uint64_t precision)<br/>Create a [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) from a raw integer and precision.  |
| outcome::result< std::shared_ptr< [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) > > | **[New](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-new)**(double value, uint64_t precision)<br/>Create a [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) from a double and precision.  |
| outcome::result< std::shared_ptr< [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) > > | **[New](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-new)**(const std::string & str, uint64_t precision, [ParseMode](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#enum-parsemode) mode =[ParseMode::Strict](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#enumvalue-strict))<br/>Create a [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) from a string and precision.  |
| outcome::result< std::shared_ptr< [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) > > | **[New](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-new)**(const std::string & str)<br/>Create a [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) from a decimal string by inferring precision.  |
| uint64_t | **[ScaleFactor](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scalefactor)**(uint64_t precision)<br/>Compute 10^precision as the scale factor.  |
| outcome::result< uint64_t > | **[FromString](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-fromstring)**(const std::string & str, uint64_t precision, [ParseMode](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#enum-parsemode) mode =[ParseMode::Strict](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#enumvalue-strict))<br/>Convert a numeric string to a raw scaled integer.  |
| std::string | **[ToString](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-tostring)**(uint64_t value, uint64_t precision)<br/>Convert a scaled integer to a string representation.  |
| outcome::result< uint64_t > | **[FromDouble](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-fromdouble)**(double value, uint64_t precision)<br/>Convert a double to a raw scaled integer.  |
| outcome::result< uint64_t > | **[Multiply](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-multiply)**(uint64_t a, uint64_t b, uint64_t precision)<br/>Multiply two raw scaled integers.  |
| outcome::result< uint64_t > | **[Divide](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-divide)**(uint64_t a, uint64_t b, uint64_t precision)<br/>Divide two raw scaled integers.  |
| outcome::result< uint64_t > | **[ConvertPrecision](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-convertprecision)**(uint64_t value, uint64_t from, uint64_t to)<br/>Change the precision of a raw scaled integer.  |
| uint64_t | **[Value](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-value)**() const<br/>Get the raw scaled integer value.  |
| uint64_t | **[Precision](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-precision)**() const<br/>Get the precision (number of decimal places).  |
| std::string | **[ToString](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-tostring)**(bool fixedDecimals =true) const<br/>Return this value as a string.  |
| outcome::result< [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) > | **[Add](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-add)**(const [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) & other) const<br/>Add another [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) with matching precision.  |
| outcome::result< [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) > | **[Subtract](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-subtract)**(const [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) & other) const<br/>Subtract another [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) with matching precision.  |
| outcome::result< [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) > | **[Multiply](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-multiply)**(const [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) & other) const<br/>Multiply by another [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) with matching precision.  |
| outcome::result< [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) > | **[Divide](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-divide)**(const [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) & other) const<br/>Divide by another [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) with matching precision.  |
| outcome::result< [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-scaledinteger) > | **[ConvertPrecision](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/#function-convertprecision)**(uint64_t to) const<br/>Convert this [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) to a different precision.  |

## Detailed Description

```cpp
class sgns::ScaledInteger;
```

Represents a decimal value using an integer scaled by 10^precision. 

Internally stores the decimal as an integer multiplied by 10^precision. Example: raw_value = 12345, precision = 2 => decimal value 123.45 

## Public Types Documentation

### enum ParseMode

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| Strict | | Fail if input has more fractional digits than precision.   |
| Truncate | | Drop any extra fractional digits.   |



Controls handling of extra fractional digits when parsing. 

## Public Functions Documentation

### function New

```cpp
static outcome::result< std::shared_ptr< ScaledInteger > > New(
    uint64_t raw_value,
    uint64_t precision
)
```

Create a [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) from a raw integer and precision. 

**Parameters**: 

  * **raw_value** Integer representation scaled by 10^precision. 
  * **precision** Number of decimal places (scale factor). 


**Return**: Outcome containing shared_ptr to [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) or error. 

### function New

```cpp
static outcome::result< std::shared_ptr< ScaledInteger > > New(
    double value,
    uint64_t precision
)
```

Create a [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) from a double and precision. 

**Parameters**: 

  * **value** Double value to convert. 
  * **precision** Number of decimal places (scale factor). 


**Return**: Outcome containing shared_ptr to [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) or error. 

### function New

```cpp
static outcome::result< std::shared_ptr< ScaledInteger > > New(
    const std::string & str,
    uint64_t precision,
    ParseMode mode =ParseMode::Strict
)
```

Create a [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) from a string and precision. 

**Parameters**: 

  * **str** String representation of the decimal value. 
  * **precision** Number of decimal places (scale factor). 
  * **mode** Mode for handling extra fractional digits. 


**Return**: Outcome containing shared_ptr to [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) or error. 

### function New

```cpp
static outcome::result< std::shared_ptr< ScaledInteger > > New(
    const std::string & str
)
```

Create a [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) from a decimal string by inferring precision. 

**Parameters**: 

  * **str** String representation of the decimal value (e.g., "123.45"). In Strict mode, will fail if more than inferred precision. 


**Return**: Outcome containing shared_ptr to [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) or error. 

### function ScaleFactor

```cpp
static uint64_t ScaleFactor(
    uint64_t precision
)
```

Compute 10^precision as the scale factor. 

**Parameters**: 

  * **precision** Number of decimal places. 


**Return**: Scale factor (10^precision). 

### function FromString

```cpp
static outcome::result< uint64_t > FromString(
    const std::string & str,
    uint64_t precision,
    ParseMode mode =ParseMode::Strict
)
```

Convert a numeric string to a raw scaled integer. 

**Parameters**: 

  * **str** Numeric string with integer and fractional parts. 
  * **precision** Number of decimal places. 
  * **mode** Mode for handling extra fractional digits. 


**Return**: Outcome containing raw scaled integer or error. 

### function ToString

```cpp
static std::string ToString(
    uint64_t value,
    uint64_t precision
)
```

Convert a scaled integer to a string representation. 

**Parameters**: 

  * **value** Raw scaled integer. 
  * **precision** Number of decimal places. 


**Return**: String representation of the decimal value. 

### function FromDouble

```cpp
static outcome::result< uint64_t > FromDouble(
    double value,
    uint64_t precision
)
```

Convert a double to a raw scaled integer. 

**Parameters**: 

  * **value** Double value to convert. 
  * **precision** Number of decimal places. 


**Return**: Outcome containing raw scaled integer or error. 

### function Multiply

```cpp
static outcome::result< uint64_t > Multiply(
    uint64_t a,
    uint64_t b,
    uint64_t precision
)
```

Multiply two raw scaled integers. 

**Parameters**: 

  * **a** First raw scaled integer. 
  * **b** Second raw scaled integer. 
  * **precision** Number of decimal places. 


**Return**: Outcome containing raw scaled integer product or error. 

### function Divide

```cpp
static outcome::result< uint64_t > Divide(
    uint64_t a,
    uint64_t b,
    uint64_t precision
)
```

Divide two raw scaled integers. 

**Parameters**: 

  * **a** Dividend as raw scaled integer. 
  * **b** Divisor as raw scaled integer. 
  * **precision** Number of decimal places. 


**Return**: Outcome containing raw scaled integer quotient or error. 

### function ConvertPrecision

```cpp
static outcome::result< uint64_t > ConvertPrecision(
    uint64_t value,
    uint64_t from,
    uint64_t to
)
```

Change the precision of a raw scaled integer. 

**Parameters**: 

  * **value** Raw scaled integer at original precision. 
  * **from** Original number of decimal places. 
  * **to** Target number of decimal places. 


**Return**: Outcome containing raw scaled integer at new precision or error. 

### function Value

```cpp
uint64_t Value() const
```

Get the raw scaled integer value. 

**Return**: Raw scaled integer. 

### function Precision

```cpp
uint64_t Precision() const
```

Get the precision (number of decimal places). 

**Return**: Number of decimal places. 

### function ToString

```cpp
std::string ToString(
    bool fixedDecimals =true
) const
```

Return this value as a string. 

**Parameters**: 

  * **fixedDecimals** 

* true: always show all fractional digits (pad with zeros up to precision)
* false: trim trailing '0's in the fractional part (and drop the '.' if no fraction remains) 


**Return**: formatted string 

### function Add

```cpp
outcome::result< ScaledInteger > Add(
    const ScaledInteger & other
) const
```

Add another [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) with matching precision. 

**Parameters**: 

  * **other** [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) to add. 


**Return**: Outcome containing sum [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) or error. 

### function Subtract

```cpp
outcome::result< ScaledInteger > Subtract(
    const ScaledInteger & other
) const
```

Subtract another [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) with matching precision. 

**Parameters**: 

  * **other** [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) to subtract. 


**Return**: Outcome containing difference [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) or error. 

### function Multiply

```cpp
outcome::result< ScaledInteger > Multiply(
    const ScaledInteger & other
) const
```

Multiply by another [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) with matching precision. 

**Parameters**: 

  * **other** [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) to multiply. 


**Return**: Outcome containing product [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) or error. 

### function Divide

```cpp
outcome::result< ScaledInteger > Divide(
    const ScaledInteger & other
) const
```

Divide by another [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) with matching precision. 

**Parameters**: 

  * **other** [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) to divide by. 


**Return**: Outcome containing quotient [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) or error. 

### function ConvertPrecision

```cpp
outcome::result< ScaledInteger > ConvertPrecision(
    uint64_t to
) const
```

Convert this [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) to a different precision. 

**Parameters**: 

  * **to** Target number of decimal places. 


**Return**: Outcome containing new [ScaledInteger](/source-reference/Classes/d3/d10/classsgns_1_1_scaled_integer/) or error. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
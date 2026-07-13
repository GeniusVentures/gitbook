---
title: sgns::CoinGeckoPriceRetriever

---

# sgns::CoinGeckoPriceRetriever






`#include <coinprices.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[PriceError](/source-reference/Classes/d9/da9/classsgns_1_1_coin_gecko_price_retriever/#enum-priceerror)** { EmptyInput = 1, NetworkError, JsonParseError, NoDataFound, RateLimitExceeded, DateTooOld} |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CoinGeckoPriceRetriever](/source-reference/Classes/d9/da9/classsgns_1_1_coin_gecko_price_retriever/#function-coingeckopriceretriever)**() |
| std::string | **[formatDate](/source-reference/Classes/d9/da9/classsgns_1_1_coin_gecko_price_retriever/#function-formatdate)**(int64_t timestamp, bool includeTime =false) |
| outcome::result< std::map< std::string, double > > | **[getCurrentPrices](/source-reference/Classes/d9/da9/classsgns_1_1_coin_gecko_price_retriever/#function-getcurrentprices)**(const std::vector< std::string > & tokenIds) |
| outcome::result< std::map< std::string, std::map< int64_t, double > > > | **[getHistoricalPrices](/source-reference/Classes/d9/da9/classsgns_1_1_coin_gecko_price_retriever/#function-gethistoricalprices)**(const std::vector< std::string > & tokenIds, const std::vector< int64_t > & timestamps) |
| outcome::result< std::map< std::string, std::map< int64_t, double > > > | **[getHistoricalPriceRange](/source-reference/Classes/d9/da9/classsgns_1_1_coin_gecko_price_retriever/#function-gethistoricalpricerange)**(const std::vector< std::string > & tokenIds, int64_t from, int64_t to) |

## Public Types Documentation

### enum PriceError

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| EmptyInput | 1|   |
| NetworkError | |   |
| JsonParseError | |   |
| NoDataFound | |   |
| RateLimitExceeded | |   |
| DateTooOld | |   |




## Public Functions Documentation

### function CoinGeckoPriceRetriever

```cpp
CoinGeckoPriceRetriever()
```


### function formatDate

```cpp
std::string formatDate(
    int64_t timestamp,
    bool includeTime =false
)
```


### function getCurrentPrices

```cpp
outcome::result< std::map< std::string, double > > getCurrentPrices(
    const std::vector< std::string > & tokenIds
)
```


### function getHistoricalPrices

```cpp
outcome::result< std::map< std::string, std::map< int64_t, double > > > getHistoricalPrices(
    const std::vector< std::string > & tokenIds,
    const std::vector< int64_t > & timestamps
)
```


### function getHistoricalPriceRange

```cpp
outcome::result< std::map< std::string, std::map< int64_t, double > > > getHistoricalPriceRange(
    const std::vector< std::string > & tokenIds,
    int64_t from,
    int64_t to
)
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
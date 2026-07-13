---
title: sgns::BurnEventParams
summary: Parsed burn event parameters shared between real-time watch (OnWatchEvent) and startup catch-up scan (PerformStartupCatchupScan). 

---

# sgns::BurnEventParams



Parsed burn event parameters shared between real-time watch (OnWatchEvent) and startup catch-up scan (PerformStartupCatchupScan). 


`#include <BridgeEventTypes.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) | **[token_id](/source-reference/Classes/da/d8d/structsgns_1_1_burn_event_params/#variable-token_id)** <br/>Token identifier from event [1].  |
| uint64_t | **[amount](/source-reference/Classes/da/d8d/structsgns_1_1_burn_event_params/#variable-amount)** <br/>Burn amount from event [2].  |
| std::string | **[destination](/source-reference/Classes/da/d8d/structsgns_1_1_burn_event_params/#variable-destination)** <br/>128-char hex recipient from event [5] (decompressed if v2)  |

## Public Attributes Documentation

### variable token_id

```cpp
TokenID token_id;
```

Token identifier from event [1]. 

### variable amount

```cpp
uint64_t amount;
```

Burn amount from event [2]. 

### variable destination

```cpp
std::string destination;
```

128-char hex recipient from event [5] (decompressed if v2) 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
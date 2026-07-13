---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/BridgeEventTypes.hpp
summary: Lightweight bridge event types and signature constants. No heavy dependencies — safe to include from tests and watchers. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/BridgeEventTypes.hpp



Lightweight bridge event types and signature constants. No heavy dependencies — safe to include from tests and watchers.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::BurnEventParams](/source-reference/Classes/da/d8d/structsgns_1_1_burn_event_params/)** <br/>Parsed burn event parameters shared between real-time watch (OnWatchEvent) and startup catch-up scan (PerformStartupCatchupScan).  |

## Attributes

|                | Name           |
| -------------- | -------------- |
| std::string_view | **[kBridgeSourceBurnedSig](/source-reference/Files/d6/de2/_bridge_event_types_8hpp/#variable-kbridgesourceburnedsig)** <br/>Canonical Solidity event signatures for bridge events. Single source of truth — shared by watch registration, catch-up scan, and RPC endpoint validation.  |
| std::string_view | **[kBridgeOutInitiatedSig](/source-reference/Files/d6/de2/_bridge_event_types_8hpp/#variable-kbridgeoutinitiatedsig)**  |

## Detailed Description

Lightweight bridge event types and signature constants. No heavy dependencies — safe to include from tests and watchers. 

**Date**: 2026-06-22 


## Attributes Documentation

### variable kBridgeSourceBurnedSig

```cpp
std::string_view kBridgeSourceBurnedSig                                                      =
"BridgeSourceBurned(address,uint256,uint256,uint256,uint256,bytes)";
```

Canonical Solidity event signatures for bridge events. Single source of truth — shared by watch registration, catch-up scan, and RPC endpoint validation. 

**Note**: The old signature with 5 parameters it not supported as it was wrong. 

### variable kBridgeOutInitiatedSig

```cpp
std::string_view kBridgeOutInitiatedSig                                                      =
"BridgeOutInitiated(address,uint256,uint256,uint256,uint256,bytes32,bool)";
```



## Source code

```cpp

#ifndef SGNS_BRIDGE_EVENT_TYPES_HPP
#define SGNS_BRIDGE_EVENT_TYPES_HPP

#include <cstdint>
#include <string>
#include <string_view>

#include "account/TokenID.hpp"

namespace sgns
{
    struct BurnEventParams
    {
        TokenID     token_id;     
        uint64_t    amount;       
        std::string destination;  
    };

    inline constexpr std::string_view kBridgeSourceBurnedSig =
        "BridgeSourceBurned(address,uint256,uint256,uint256,uint256,bytes)";
    inline constexpr std::string_view kBridgeOutInitiatedSig =
        "BridgeOutInitiated(address,uint256,uint256,uint256,uint256,bytes32,bool)";

} // namespace sgns

#endif // SGNS_BRIDGE_EVENT_TYPES_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

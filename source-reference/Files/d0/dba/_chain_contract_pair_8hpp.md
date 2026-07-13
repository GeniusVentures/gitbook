---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/ChainContractPair.hpp
summary: Shared struct linking a chain name to its bridge contract address and numeric chain ID. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/ChainContractPair.hpp



Shared struct linking a chain name to its bridge contract address and numeric chain ID.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::ChainContractPair](/source-reference/Classes/d5/d01/structsgns_1_1_chain_contract_pair/)** <br/>Represents a chain name and its GNUS bridge contract address.  |

## Detailed Description

Shared struct linking a chain name to its bridge contract address and numeric chain ID. 

**Date**: 2025-06-17 SuperGenius


This is the shared leaf type consumed by ChainRpcEndpointProvider (as observer payload) and by BridgeRelayer (as a Start() parameter). Extracting it into its own header breaks the include cycle that would otherwise exist between those two headers when BridgeRelayer inherits IBridgeInitObserver from the provider header. 




## Source code

```cpp

#ifndef _CHAIN_CONTRACT_PAIR_HPP_
#define _CHAIN_CONTRACT_PAIR_HPP_

#include <cstdint>
#include <string>

namespace sgns
{
    struct ChainContractPair
    {
        std::string chain_name;
        std::string contract_address;
        uint64_t    chain_id = 0;
    };
} // namespace sgns

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

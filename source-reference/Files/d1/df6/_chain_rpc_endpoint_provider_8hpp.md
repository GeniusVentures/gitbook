---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/ChainRpcEndpointProvider.hpp
summary: Loads RPC endpoints from the evmrelay ChainList provider and wires them into PublicChainInputValidator with weighted consensus support. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/ChainRpcEndpointProvider.hpp



Loads RPC endpoints from the evmrelay ChainList provider and wires them into PublicChainInputValidator with weighted consensus support.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/)** <br/>Observer interface notified when RPC endpoints have been loaded and wired.  |
| class | **[sgns::ChainRpcEndpointProvider](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/)** <br/>Encapsulates ChainList RPC endpoint loading and validator wiring.  |

## Types

|                | Name           |
| -------------- | -------------- |
| using std::function< std::optional< std::string >()> | **[ChainlistFetcher](/source-reference/Files/d1/df6/_chain_rpc_endpoint_provider_8hpp/#using-chainlistfetcher)** <br/>Fetches the chainlist dataset (JSON text) used to discover public RPC URLs at startup.  |

## Detailed Description

Loads RPC endpoints from the evmrelay ChainList provider and wires them into PublicChainInputValidator with weighted consensus support. 

**Date**: 2026-05-27 SuperGenius 
## Types Documentation

### using ChainlistFetcher

```cpp
using sgns::ChainlistFetcher = std::function<std::optional<std::string>()>;
```

Fetches the chainlist dataset (JSON text) used to discover public RPC URLs at startup. 

**Return**: The chainlist JSON text, or std::nullopt on fetch failure. 

Production default: HTTPS GET of [https://chainid.network/chains.json](https://chainid.network/chains.json). Tests inject a callable returning canned JSON (no network).





## Source code

```cpp

#ifndef _CHAIN_RPC_ENDPOINT_PROVIDER_HPP_
#define _CHAIN_RPC_ENDPOINT_PROVIDER_HPP_

#include <cstdint>
#include <filesystem>
#include <functional>
#include <optional>
#include <string>
#include <unordered_map>
#include <vector>

#include "account/ChainContractPair.hpp"
#include "account/PublicChainInputValidator.hpp"

namespace sgns
{
    class IBridgeInitObserver
    {
    public:
        virtual void OnRpcEndpointsReady( std::vector<ChainContractPair> chains ) = 0;

        virtual ~IBridgeInitObserver() = default;
    };

    using ChainlistFetcher = std::function<std::optional<std::string>()>;

    class ChainRpcEndpointProvider
    {
    public:
        ChainRpcEndpointProvider() = default;

        void AddObserver( IBridgeInitObserver &observer );

        void SetChainlistFetcher( ChainlistFetcher fetcher )
        {
            chainlist_fetcher_ = std::move( fetcher );
        }

        using CancelChecker = std::function<bool()>;

        bool Initialize( const std::filesystem::path    &bridge_chains_config_path,
                         PublicChainInputValidator       &validator,
                         CancelChecker                   is_cancelled = {} );

    private:
        std::vector<IBridgeInitObserver *> observers_;
        ChainlistFetcher                   chainlist_fetcher_;
    };
} // namespace sgns

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/watcher/impl/bridge_rpc_watcher.hpp
summary: Header file for the bridge RPC watcher. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/watcher/impl/bridge_rpc_watcher.hpp



Header file for the bridge RPC watcher.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::evmwatcher](/source-reference/Namespaces/df/d85/namespacesgns_1_1evmwatcher/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::evmwatcher::BridgeRpcWatcher](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/)** <br/>RPC-based bridge event watcher that polls eth_getLogs, verifies receipts, and produces normalized BridgeEventClaim objects.  |
| struct | **[sgns::evmwatcher::BridgeRpcWatcher::Config](/source-reference/Classes/d3/d68/structsgns_1_1evmwatcher_1_1_bridge_rpc_watcher_1_1_config/)** <br/>Configuration structure for [BridgeRpcWatcher](/source-reference/Classes/d1/d21/classsgns_1_1evmwatcher_1_1_bridge_rpc_watcher/).  |

## Detailed Description

Header file for the bridge RPC watcher. 

**Date**: 2026-06-03 SuperGenius ([ken@gnus.ai](mailto:ken@gnus.ai)) Copyright 2026 Genius Ventures, Inc. SPDX-License-Identifier: MIT 



## Source code

```cpp


#ifndef BRIDGE_RPC_WATCHER_HPP
#define BRIDGE_RPC_WATCHER_HPP

#include <watcher/messaging_watcher.hpp>

#include <eth/bridge_event.hpp>
#include <eth/rpc_http_transport.hpp>

#include <chrono>
#include <cstdint>
#include <functional>
#include <string>
#include <vector>

namespace sgns::evmwatcher
{

    class BridgeRpcWatcher final : public watcher::MessagingWatcher
    {
    public:
        using BridgeClaimCallback = std::function<void( const eth::BridgeEventClaim & )>;

        struct Config
        {
            std::string rpc_url;                 
            uint64_t    chain_id      = 0;       
            uint64_t    dest_chain_id = 0;       
            std::string contract_address;        
            std::string event_signature;         
            uint64_t    confirmation_depth = 12; 
            std::chrono::seconds poll_interval{ 4 };   
            uint64_t             max_log_range = 1000; 
        };

        BridgeRpcWatcher( const Config &config, MessageCallback message_callback, BridgeClaimCallback claim_callback );

        void startWatching() override;
        void stopWatching() override;

        [[nodiscard]] const Config &GetConfig() const noexcept
        {
            return config_;
        }

        [[nodiscard]] uint64_t GetLastProcessedBlock() const noexcept
        {
            return last_block_;
        }

    protected:
        void watch() override;

    private:
        void poll_once();

        Config                     config_;         
        BridgeClaimCallback        claim_callback_; 
        eth::rpc::RpcHttpTransport transport_;      
        uint64_t                   last_block_ = 0; 
    };

} // namespace sgns::evmwatcher

#endif // BRIDGE_RPC_WATCHER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

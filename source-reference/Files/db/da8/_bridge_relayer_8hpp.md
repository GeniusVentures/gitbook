---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/BridgeRelayer.hpp
summary: Wires evmrelay burn events to MintFunds via shared EthWatchService. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/BridgeRelayer.hpp



Wires evmrelay burn events to MintFunds via shared EthWatchService.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::BridgeRelayer](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/)** <br/>Registers both BridgeSourceBurned (v1) and BridgeOutInitiated (v2) watches on a shared EthWatchService across multiple chains and calls MintFunds when burns are detected. OnWatchEvent dispatches on the variant type of values[5] to handle both event formats (D-06).  |

## Detailed Description

Wires evmrelay burn events to MintFunds via shared EthWatchService. 

**Date**: 2026-05-30 



## Source code

```cpp

#ifndef SGNS_BRIDGE_RELAYER_HPP
#define SGNS_BRIDGE_RELAYER_HPP

#include <memory>
#include <string>
#include <unordered_map>
#include <vector>

#include "account/BridgeEventTypes.hpp"
#include "account/ChainContractPair.hpp"
#include "account/ChainRpcEndpointProvider.hpp"
#include "account/TransactionManager.hpp"
#include "base/logger.hpp"
#include "eth/eth_watch_service.hpp"
#include "outcome/outcome.hpp"

class BridgeRelayerTestAccess;

namespace sgns
{
    class BridgeRelayer : public IBridgeInitObserver,
                          public std::enable_shared_from_this<BridgeRelayer>
    {
    public:
        static std::shared_ptr<BridgeRelayer> Create( std::weak_ptr<TransactionManager>     tx_manager,
                                                       std::shared_ptr<eth::EthWatchService> watch_service );

        static outcome::result<BurnEventParams> ParseBurnEventValues(
            const std::vector<eth::abi::AbiValue>& values );

        void Start( std::vector<ChainContractPair> chains );

        void OnRpcEndpointsReady( std::vector<ChainContractPair> chains ) override;

        void Stop();

    private:
        friend class ::BridgeRelayerTestAccess;
        explicit BridgeRelayer( std::weak_ptr<TransactionManager>     tx_manager,
                                std::shared_ptr<eth::EthWatchService> watch_service,
                                base::Logger                          logger = nullptr );
        void OnWatchEvent( const eth::WatchEventNotification &notification, const std::string &chain_name );

        std::weak_ptr<TransactionManager> tx_manager_; 
        std::shared_ptr<eth::EthWatchService> watch_service_; 
        base::Logger                          logger_;        
        std::unordered_map<std::string, std::pair<eth::EventWatchId, eth::EventWatchId>> chain_watches_;
    };
} // namespace sgns

#endif // SGNS_BRIDGE_RELAYER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

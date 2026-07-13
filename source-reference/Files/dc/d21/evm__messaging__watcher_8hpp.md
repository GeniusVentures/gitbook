---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/watcher/impl/evm_messaging_watcher.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/watcher/impl/evm_messaging_watcher.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::evmwatcher](/source-reference/Namespaces/df/d85/namespacesgns_1_1evmwatcher/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::evmwatcher::EvmMessagingWatcher](/source-reference/Classes/d6/d4c/classsgns_1_1evmwatcher_1_1_evm_messaging_watcher/)**  |
| struct | **[sgns::evmwatcher::EvmMessagingWatcher::ChainConfig](/source-reference/Classes/d7/d91/structsgns_1_1evmwatcher_1_1_evm_messaging_watcher_1_1_chain_config/)**  |




## Source code

```cpp
#ifndef EVM_MESSAGING_WATCHER_HPP
#define EVM_MESSAGING_WATCHER_HPP

#include <rapidjson/document.h>
#include <string>
#include <vector>
#include "watcher/messaging_watcher.hpp"
#include "api/transport/impl/ws/ws_client_impl.hpp"

namespace sgns::evmwatcher {

class EvmMessagingWatcher : public watcher::MessagingWatcher {
    public:
        // Type alias for context from the WebSocket implementation
        using Context = api::WsClientImpl::Context;

        using TopicFilter = struct {
            std::string topic_hash;
        };

        struct ChainConfig {
            std::string rpc_url;
            std::string chain_id;
            std::string chain_name;
            std::string ws_url;
        };

        EvmMessagingWatcher(const rapidjson::Document &config, MessageCallback callback,
                            const std::string &contract_address, const std::vector<TopicFilter> &topic_filters);

        [[nodiscard]] std::string getContractAddress() const;
        void setContractAddress(const std::string &contract_address);

        [[nodiscard]] std::vector<TopicFilter> getTopicFilters() const;
        void setTopicFilters(const std::vector<TopicFilter> &topic_filters);

        void setupWebSocketListener(const ChainConfig &chainConfig);

        [[nodiscard]] ChainConfig getChain() const;
        void startWatching() override;
        void stopWatching() override;

    private:
        void parseConfig(const rapidjson::Document &config);  // Override with the updated signature
        std::string contract_address;
        std::vector<TopicFilter> topic_filters;
        std::shared_ptr<api::WsClientImpl> ws_client;
        api::WsClientImpl::Context ws_context;
        ChainConfig chain;  // Add chains vector to store chain configurations
    };

}  // namespace sgns::evmwatcher

#endif  // EVM_MESSAGING_WATCHER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

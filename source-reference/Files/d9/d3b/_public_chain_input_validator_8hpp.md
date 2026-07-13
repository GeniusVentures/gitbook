---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/PublicChainInputValidator.hpp
summary: Input validation strategy for public-chain source proofs. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/PublicChainInputValidator.hpp



Input validation strategy for public-chain source proofs.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[eth](/source-reference/Namespaces/da/ddf/namespaceeth/)**  |
| **[eth::rpc](/source-reference/Namespaces/d8/d41/namespaceeth_1_1rpc/)**  |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::WeightedRpcEndpoint](/source-reference/Classes/d4/d8c/structsgns_1_1_weighted_rpc_endpoint/)** <br/>Weighted RPC endpoint used for multi-provider consensus verification.  |
| class | **[sgns::PublicChainInputValidator](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/)** <br/>Validator for transactions that reference external public-chain proofs.  |

## Types

|                | Name           |
| -------------- | -------------- |
| using std::function< std::unique_ptr< eth::rpc::JsonRpcTransport >(const std::string &url, std::chrono::seconds timeout)> | **[TransportFactory](/source-reference/Files/d9/d3b/_public_chain_input_validator_8hpp/#using-transportfactory)** <br/>Factory callable that produces a JsonRpcTransport from a URL and timeout.  |

## Detailed Description

Input validation strategy for public-chain source proofs. 

**Date**: 2026-06-02 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 
## Types Documentation

### using TransportFactory

```cpp
using sgns::TransportFactory = std::function<std::unique_ptr<eth::rpc::JsonRpcTransport>( const std::string   &url,
                                                                                       std::chrono::seconds timeout )>;
```

Factory callable that produces a JsonRpcTransport from a URL and timeout. 

**Parameters**: 

  * **url** RPC endpoint URL. 
  * **timeout** Transport operation timeout. 


**Return**: Unique ownership of a transport implementing JsonRpcTransport. 

Injected via SetTransportFactory(). When not set, the default factory creates real RpcHttpTransport instances (production path per D-16). Tests inject a factory that returns MockRpcTransport instances (D-07, D-14).





## Source code

```cpp

#ifndef SGNS_PUBLIC_CHAIN_INPUT_VALIDATOR_HPP
#define SGNS_PUBLIC_CHAIN_INPUT_VALIDATOR_HPP

#include <chrono>
#include <cstdint>
#include <functional>
#include <memory>
#include <string>
#include <unordered_map>
#include <vector>

#include "account/InputValidators.hpp"

namespace eth::rpc
{
    class JsonRpcTransport;
} // namespace eth::rpc

class PublicChainInputValidatorTestAccess;

namespace sgns
{
    struct WeightedRpcEndpoint
    {
        std::string url;
        uint8_t     consensus_weight = 25;
        std::string bridge_contract_address; 
        std::vector<std::string> accepted_topic0_hashes;
    };

    using TransportFactory = std::function<std::unique_ptr<eth::rpc::JsonRpcTransport>( const std::string   &url,
                                                                                        std::chrono::seconds timeout )>;

    class PublicChainInputValidator final : public IInputValidator
    {
    public:
        void RegisterForChain( const std::string &chain_id )
        {
            IInputValidator::Register( chain_id, this );
            registered_chain_ids_.push_back( chain_id );
        }

        ~PublicChainInputValidator() override
        {
            for ( const auto &chain_id : registered_chain_ids_ )
            {
                IInputValidator::UnregisterIf( chain_id, this );
            }
        }

        void SetRpcEndpoints( const std::string &chain_id, std::vector<WeightedRpcEndpoint> endpoints );

        void AddRpcEndpoints( const std::string &chain_id, std::vector<WeightedRpcEndpoint> endpoints );

        bool ValidateUTXOParameters( const UTXOTxParameters &params,
                                     const std::string      &address,
                                     const UTXOManager      &utxo_manager ) const override;

        bool ValidateWitness( const ConsensusSubject                   &subject,
                              const std::shared_ptr<GeniusTransaction> &tx,
                              const UTXOTxParameters                   &params,
                              const std::shared_ptr<Blockchain>        &blockchain ) const override;

        bool RequiresConsensusUTXOData() const override
        {
            return false;
        }

        void SetTransportFactory( TransportFactory factory )
        {
            transport_factory_ = std::move( factory );
        }

        [[nodiscard]] std::optional<std::string> GetFirstRpcUrl( const std::string &chain_id ) const
        {
            auto it = rpc_endpoints_.find( chain_id );
            if ( it != rpc_endpoints_.end() && !it->second.empty() )
            {
                return it->second.front().url;
            }
            return std::nullopt;
        }

        [[nodiscard]] std::vector<uint8_t> GetSlotHash( size_t           slot_index,
                                                        const std::string &chain_id ) const noexcept;

        [[nodiscard]] std::optional<std::string> GetFirstConfiguredChainId() const noexcept
        {
            if ( rpc_endpoints_.empty() )
            {
                return std::nullopt;
            }
            // unordered_map iteration is not order-stable across runs, but for
            // single-chain deployments (the Phase 6 target) there is exactly one
            // entry. Multi-chain resolution will read chain_id from the proposal
            // subject instead.
            return rpc_endpoints_.begin()->first;
        }

    private:
        friend class ::PublicChainInputValidatorTestAccess;

        bool VerifyPublicChainSmartContract( const std::shared_ptr<GeniusTransaction> &tx,
                                             const std::string                        &source_reference ) const;

        std::unordered_map<std::string, std::vector<WeightedRpcEndpoint>> rpc_endpoints_;

        std::vector<std::string> registered_chain_ids_;

        mutable TransportFactory transport_factory_;
    };
} // namespace sgns

#endif // SGNS_PUBLIC_CHAIN_INPUT_VALIDATOR_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: sgns::ChainRpcEndpointProvider
summary: Encapsulates ChainList RPC endpoint loading and validator wiring. 

---

# sgns::ChainRpcEndpointProvider



Encapsulates ChainList RPC endpoint loading and validator wiring.  [More...](#detailed-description)


`#include <ChainRpcEndpointProvider.hpp>`

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::function< bool()> | **[CancelChecker](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/#using-cancelchecker)** <br/>Loads RPC endpoints from bridge_chains_config.json + a runtime chainlist fetch, wires them into the validator, then calls [IInputValidator::Register](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-register) per chain.  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[ChainRpcEndpointProvider](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/#function-chainrpcendpointprovider)**() =default |
| void | **[AddObserver](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/#function-addobserver)**([IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/) & observer)<br/>Registers an observer to receive the chain/contract list on Init success.  |
| void | **[SetChainlistFetcher](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/#function-setchainlistfetcher)**([ChainlistFetcher](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-chainlistfetcher) fetcher)<br/>Overrides the chainlist dataset fetcher (for tests; no network).  |
| bool | **[Initialize](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/#function-initialize)**(const std::filesystem::path & bridge_chains_config_path, [PublicChainInputValidator](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/) & validator, [CancelChecker](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/#using-cancelchecker) is_cancelled ={}) |

## Detailed Description

```cpp
class sgns::ChainRpcEndpointProvider;
```

Encapsulates ChainList RPC endpoint loading and validator wiring. 

Reads bridge_chains_config.json at the path provided, extracts chain_id and bridge_contract_address for each chain entry, runtime-fetches public RPC URLs from the chainid.network chainlist dataset (filter: bridge_contract_address + topic0 attached per chain), wires them into [PublicChainInputValidator](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/) with consensus weights, calls [IInputValidator::Register](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-register) per chain, and notifies [IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/) subscribers on success. 

## Public Types Documentation

### using CancelChecker

```cpp
using sgns::ChainRpcEndpointProvider::CancelChecker = std::function<bool()>;
```

Loads RPC endpoints from bridge_chains_config.json + a runtime chainlist fetch, wires them into the validator, then calls [IInputValidator::Register](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-register) per chain. 

**Parameters**: 

  * **bridge_chains_config_path** Path to bridge_chains_config.json. 
  * **validator** [PublicChainInputValidator](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/) to configure. 
  * **is_cancelled** Optional cancellation predicate, checked after the blocking chainlist fetch and BEFORE publishing (validator registration + observer notification). Used by [GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/) to abort a stale init whose account was switched mid-fetch, so it never publishes raw validator pointers / notifies freed observers. 


**Return**: True when at least one chain entry was accepted (had chain_id + bridge_contract_address). 

Each fetched public RPC URL contributes 25% consensus weight (≥3 reach the 75-weight quorum). A chainlist fetch failure leaves a chain with no endpoints — it still registers for relayer watch, but receipt verification and catch-up scan fail closed.


## Public Functions Documentation

### function ChainRpcEndpointProvider

```cpp
ChainRpcEndpointProvider() =default
```


### function AddObserver

```cpp
void AddObserver(
    IBridgeInitObserver & observer
)
```

Registers an observer to receive the chain/contract list on Init success. 

**Parameters**: 

  * **observer** Non-owning reference to an [IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/).



Subscription must occur before [Initialize()](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/#function-initialize) is posted to the io_context so the callback fires inside that same [Initialize()](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/#function-initialize) invocation. 


### function SetChainlistFetcher

```cpp
inline void SetChainlistFetcher(
    ChainlistFetcher fetcher
)
```

Overrides the chainlist dataset fetcher (for tests; no network). 

**Parameters**: 

  * **fetcher** Callable returning the chainlist JSON text (or nullopt). 


Must be called before [Initialize()](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/#function-initialize). When unset, [Initialize()](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/#function-initialize) performs a real HTTPS GET of [https://chainid.network/chains.json](https://chainid.network/chains.json).


### function Initialize

```cpp
bool Initialize(
    const std::filesystem::path & bridge_chains_config_path,
    PublicChainInputValidator & validator,
    CancelChecker is_cancelled ={}
)
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
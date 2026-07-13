---
title: sgns::IBridgeInitObserver
summary: Observer interface notified when RPC endpoints have been loaded and wired. 

---

# sgns::IBridgeInitObserver



Observer interface notified when RPC endpoints have been loaded and wired.  [More...](#detailed-description)


`#include <ChainRpcEndpointProvider.hpp>`

Inherited by [sgns::BridgeRelayer](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/), [sgns::GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual void | **[OnRpcEndpointsReady](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/#function-onrpcendpointsready)**(std::vector< [ChainContractPair](/source-reference/Classes/d5/d01/structsgns_1_1_chain_contract_pair/) > chains) =0<br/>Called when RPC endpoint initialization completes successfully.  |
| virtual | **[~IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/#function-~ibridgeinitobserver)**() =default |

## Detailed Description

```cpp
class sgns::IBridgeInitObserver;
```

Observer interface notified when RPC endpoints have been loaded and wired. 

Subscribers (e.g. [BridgeRelayer](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/)) implement this interface and call [ChainRpcEndpointProvider::AddObserver()](/source-reference/Classes/d9/dab/classsgns_1_1_chain_rpc_endpoint_provider/#function-addobserver) before Initialize() is posted to the io_context. The callback fires synchronously inside Initialize() after all endpoints are wired and [IInputValidator::Register](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-register) has been called for each discovered chain. 

## Public Functions Documentation

### function OnRpcEndpointsReady

```cpp
virtual void OnRpcEndpointsReady(
    std::vector< ChainContractPair > chains
) =0
```

Called when RPC endpoint initialization completes successfully. 

**Parameters**: 

  * **chains** List of (chain_name, contract_address, chain_id) pairs discovered. 


**Reimplemented by**: [sgns::BridgeRelayer::OnRpcEndpointsReady](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/#function-onrpcendpointsready), [sgns::GeniusNode::OnRpcEndpointsReady](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-onrpcendpointsready)


### function ~IBridgeInitObserver

```cpp
virtual ~IBridgeInitObserver() =default
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
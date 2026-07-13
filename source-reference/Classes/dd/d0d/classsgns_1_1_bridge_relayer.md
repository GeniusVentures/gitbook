---
title: sgns::BridgeRelayer
summary: Registers both BridgeSourceBurned (v1) and BridgeOutInitiated (v2) watches on a shared EthWatchService across multiple chains and calls MintFunds when burns are detected. OnWatchEvent dispatches on the variant type of values[5] to handle both event formats (D-06). 

---

# sgns::BridgeRelayer



Registers both BridgeSourceBurned (v1) and BridgeOutInitiated (v2) watches on a shared EthWatchService across multiple chains and calls MintFunds when burns are detected. OnWatchEvent dispatches on the variant type of values[5] to handle both event formats (D-06). 


`#include <BridgeRelayer.hpp>`

Inherits from [sgns::IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/), std::enable_shared_from_this< BridgeRelayer >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [BridgeRelayer](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/#function-bridgerelayer) > | **[Create](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/#function-create)**(std::weak_ptr< [TransactionManager](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/) > tx_manager, std::shared_ptr< eth::EthWatchService > watch_service)<br/>Factory method to create a [BridgeRelayer](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/) instance with weak [TransactionManager](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/) reference.  |
| outcome::result< [BurnEventParams](/source-reference/Classes/da/d8d/structsgns_1_1_burn_event_params/) > | **[ParseBurnEventValues](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/#function-parseburneventvalues)**(const std::vector< eth::abi::AbiValue > & values)<br/>Parse decoded ABI values into [BurnEventParams](/source-reference/Classes/da/d8d/structsgns_1_1_burn_event_params/) for bridging.  |
| void | **[Start](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/#function-start)**(std::vector< [ChainContractPair](/source-reference/Classes/d5/d01/structsgns_1_1_chain_contract_pair/) > chains)<br/>Register both v1 (BridgeSourceBurned) and v2 (BridgeOutInitiated) watches on all provided chains.  |
| virtual void | **[OnRpcEndpointsReady](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/#function-onrpcendpointsready)**(std::vector< [ChainContractPair](/source-reference/Classes/d5/d01/structsgns_1_1_chain_contract_pair/) > chains) override<br/>[IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/) callback — self-starts when the provider signals readiness.  |
| void | **[Stop](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/#function-stop)**()<br/>Stop watching (currently a no-op — EthWatchService lifecycle is external).  |

## Friends

|                | Name           |
| -------------- | -------------- |
| class | **[::BridgeRelayerTestAccess](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/#friend-bridgerelayertestaccess)** <br/>Friend accessor for unit testing OnWatchEvent and chain_watches_.  |

## Additional inherited members

**Public Functions inherited from [sgns::IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/#function-~ibridgeinitobserver)**() =default |


## Public Functions Documentation

### function Create

```cpp
static std::shared_ptr< BridgeRelayer > Create(
    std::weak_ptr< TransactionManager > tx_manager,
    std::shared_ptr< eth::EthWatchService > watch_service
)
```

Factory method to create a [BridgeRelayer](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/) instance with weak [TransactionManager](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/) reference. 

**Parameters**: 

  * **tx_manager** Weak pointer to the [TransactionManager](/source-reference/Classes/d2/d58/classsgns_1_1_transaction_manager/) to call MintFunds on. 
  * **watch_service** Shared EthWatchService for event detection. 


**Return**: If successful, a shared pointer to the created [BridgeRelayer](/source-reference/Classes/dd/d0d/classsgns_1_1_bridge_relayer/); otherwise, a nullptr 

### function ParseBurnEventValues

```cpp
static outcome::result< BurnEventParams > ParseBurnEventValues(
    const std::vector< eth::abi::AbiValue > & values
)
```

Parse decoded ABI values into [BurnEventParams](/source-reference/Classes/da/d8d/structsgns_1_1_burn_event_params/) for bridging. 

**Parameters**: 

  * **values** Decoded ABI values in declaration order. 


**Return**: Parsed parameters on success, or error if values are malformed. 

Works for both OnWatchEvent (decoded via decode_log) and catch-up scan (decoded via decode_log). values layout: [0] sender (address, indexed) [3] srcChainID (uint256) [1] id (uint256) [4] destChainID (uint256) [2] amount (uint256) [5] sgnsDestination (bytes/bytes32) [6] destinationYOdd (bool, v2 only)


### function Start

```cpp
void Start(
    std::vector< ChainContractPair > chains
)
```

Register both v1 (BridgeSourceBurned) and v2 (BridgeOutInitiated) watches on all provided chains. 

**Parameters**: 

  * **chains** Vector of (chain_name, contract_address) pairs. Chains without a valid contract address are skipped with a warning. Best-effort: if one event/chain fails, others still register (D-21). 


### function OnRpcEndpointsReady

```cpp
virtual void OnRpcEndpointsReady(
    std::vector< ChainContractPair > chains
) override
```

[IBridgeInitObserver](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/) callback — self-starts when the provider signals readiness. 

**Parameters**: 

  * **chains** List of (chain_name, contract_address, chain_id) pairs. 


**Reimplements**: [sgns::IBridgeInitObserver::OnRpcEndpointsReady](/source-reference/Classes/d7/db1/classsgns_1_1_i_bridge_init_observer/#function-onrpcendpointsready)


### function Stop

```cpp
void Stop()
```

Stop watching (currently a no-op — EthWatchService lifecycle is external). 

## Friends

### friend ::BridgeRelayerTestAccess

```cpp
friend class ::BridgeRelayerTestAccess(
    ::BridgeRelayerTestAccess 
);
```

Friend accessor for unit testing OnWatchEvent and chain_watches_. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
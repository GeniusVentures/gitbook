---
title: sgns::WeightedRpcEndpoint
summary: Weighted RPC endpoint used for multi-provider consensus verification. 

---

# sgns::WeightedRpcEndpoint



Weighted RPC endpoint used for multi-provider consensus verification.  [More...](#detailed-description)


`#include <PublicChainInputValidator.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::string | **[url](/source-reference/Classes/d4/d8c/structsgns_1_1_weighted_rpc_endpoint/#variable-url)**  |
| uint8_t | **[consensus_weight](/source-reference/Classes/d4/d8c/structsgns_1_1_weighted_rpc_endpoint/#variable-consensus_weight)**  |
| std::string | **[bridge_contract_address](/source-reference/Classes/d4/d8c/structsgns_1_1_weighted_rpc_endpoint/#variable-bridge_contract_address)**  |
| std::vector< std::string > | **[accepted_topic0_hashes](/source-reference/Classes/d4/d8c/structsgns_1_1_weighted_rpc_endpoint/#variable-accepted_topic0_hashes)**  |

## Detailed Description

```cpp
struct sgns::WeightedRpcEndpoint;
```

Weighted RPC endpoint used for multi-provider consensus verification. 

Direct (api-key) endpoints contribute 50% weight. Public endpoints from ChainList contribute 25% weight. Verification requires >= 75% weighted consensus across queried endpoints. 

## Public Attributes Documentation

### variable url

```cpp
std::string url;
```


### variable consensus_weight

```cpp
uint8_t consensus_weight = 25;
```


### variable bridge_contract_address

```cpp
std::string bridge_contract_address;
```


Expected bridge contract (hex, "0x...") 


### variable accepted_topic0_hashes

```cpp
std::vector< std::string > accepted_topic0_hashes;
```


Accepted bridge event topic0 hashes (hex, "0x..."). Carries BOTH the v1 BridgeSourceBurned and v2 BridgeOutInitiated topic0 so witness validation accepts mints created from either event version. 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
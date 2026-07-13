---
title: sgns::PublicChainInputValidator
summary: Validator for transactions that reference external public-chain proofs. 

---

# sgns::PublicChainInputValidator



Validator for transactions that reference external public-chain proofs. 


`#include <PublicChainInputValidator.hpp>`

Inherits from [sgns::IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| void | **[RegisterForChain](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-registerforchain)**(const std::string & chain_id)<br/>Registers this validator for `chain_id` in the global registry and records it for self-removal on destruction (compare-and- remove), so the registry never holds a dangling pointer after this validator (and its owning transaction manager) is destroyed.  |
| | **[~PublicChainInputValidator](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-~publicchaininputvalidator)**() override |
| void | **[SetRpcEndpoints](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-setrpcendpoints)**(const std::string & chain_id, std::vector< [WeightedRpcEndpoint](/source-reference/Classes/d4/d8c/structsgns_1_1_weighted_rpc_endpoint/) > endpoints)<br/>Configure weighted RPC endpoints for a source chain.  |
| void | **[AddRpcEndpoints](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-addrpcendpoints)**(const std::string & chain_id, std::vector< [WeightedRpcEndpoint](/source-reference/Classes/d4/d8c/structsgns_1_1_weighted_rpc_endpoint/) > endpoints)<br/>Merge weighted RPC endpoints into a source chain's existing list.  |
| virtual bool | **[ValidateUTXOParameters](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-validateutxoparameters)**(const [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) & params, const std::string & address, const [UTXOManager](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/) & utxo_manager) const override<br/>Validates local UTXO structure for externally sourced claims.  |
| virtual bool | **[ValidateWitness](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-validatewitness)**(const ConsensusSubject & subject, const std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > & tx, const [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) & params, const std::shared_ptr< [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) > & blockchain) const override<br/>Validates the external witness data supplied by consensus.  |
| virtual bool | **[RequiresConsensusUTXOData](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-requiresconsensusutxodata)**() const override<br/>Public-chain validation does not require local UTXO witness data.  |
| void | **[SetTransportFactory](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-settransportfactory)**([TransportFactory](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-transportfactory) factory)<br/>Inject a custom transport factory for DI-based mock support.  |
| std::optional< std::string > | **[GetFirstRpcUrl](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-getfirstrpcurl)**(const std::string & chain_id) const<br/>Returns the first RPC endpoint URL for a given chain ID, if any exist.  |
| std::vector< uint8_t > | **[GetSlotHash](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-getslothash)**(size_t slot_index, const std::string & chain_id) const<br/>Returns the SHA-256 hash of an endpoint URL for a vote slot (Phase 6, D-01).  |
| std::optional< std::string > | **[GetFirstConfiguredChainId](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-getfirstconfiguredchainid)**() const<br/>Returns the first configured chain id, if any (Phase 6, D-01).  |

## Friends

|                | Name           |
| -------------- | -------------- |
| class | **[::PublicChainInputValidatorTestAccess](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#friend-publicchaininputvalidatortestaccess)** <br/>Friend accessor for unit testing VerifyPublicChainSmartContract and the wired rpc_endpoints_ (mirrors BridgeRelayerTestAccess).  |

## Additional inherited members

**Public Types inherited from [sgns::IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/)**

|                | Name           |
| -------------- | -------------- |
| using const [IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/) * | **[ValidatorPtr](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#using-validatorptr)**  |

**Public Functions inherited from [sgns::IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-~iinputvalidator)**() =default<br/>Destroys the input validator.  |
| void | **[Register](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-register)**(const std::string & chain_id, [ValidatorPtr](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#using-validatorptr) validator) |
| void | **[UnregisterIf](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-unregisterif)**(const std::string & chain_id, [ValidatorPtr](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#using-validatorptr) expected)<br/>Remove a chain's registration only if it currently points to `expected` (compare-and-remove). Prevents a stale validator from clobbering a newer account's registration when it is destroyed, and lets a validator self-clean on destruction so the registry never holds a dangling pointer.  |
| [ValidatorPtr](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#using-validatorptr) | **[Get](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-get)**(const std::string & chain_id) |


## Public Functions Documentation

### function RegisterForChain

```cpp
inline void RegisterForChain(
    const std::string & chain_id
)
```

Registers this validator for `chain_id` in the global registry and records it for self-removal on destruction (compare-and- remove), so the registry never holds a dangling pointer after this validator (and its owning transaction manager) is destroyed. 

### function ~PublicChainInputValidator

```cpp
inline ~PublicChainInputValidator() override
```


### function SetRpcEndpoints

```cpp
void SetRpcEndpoints(
    const std::string & chain_id,
    std::vector< WeightedRpcEndpoint > endpoints
)
```

Configure weighted RPC endpoints for a source chain. 

**Parameters**: 

  * **chain_id** Source chain identifier (e.g. "1" for Ethereum). 
  * **endpoints** Weighted RPC endpoint URLs for verifying burn receipts. 


### function AddRpcEndpoints

```cpp
void AddRpcEndpoints(
    const std::string & chain_id,
    std::vector< WeightedRpcEndpoint > endpoints
)
```

Merge weighted RPC endpoints into a source chain's existing list. 

**Parameters**: 

  * **chain_id** Source chain identifier (e.g. "1" for Ethereum). 
  * **endpoints** Weighted RPC endpoints to merge (URL-deduped). 


Unlike SetRpcEndpoints (wholesale replace), this preserves endpoints already configured for the chain (e.g. operator-supplied private/API-key endpoints from [GeniusNode::ConfigureRpcEndpoint](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-configurerpcendpoint)) and appends the new ones, deduplicating by URL. Used by the chainlist runtime fetch so an async non-empty fetch never drops higher-weight private endpoints.


### function ValidateUTXOParameters

```cpp
virtual bool ValidateUTXOParameters(
    const UTXOTxParameters & params,
    const std::string & address,
    const UTXOManager & utxo_manager
) const override
```

Validates local UTXO structure for externally sourced claims. 

**Parameters**: 

  * **params** UTXO inputs and outputs carried by the transaction. 
  * **address** Source address; ignored for public-chain validation. 
  * **utxo_manager** Local UTXO manager; ignored for public-chain validation. 


**Return**: True when both input and output lists are non-empty. 

**Reimplements**: [sgns::IInputValidator::ValidateUTXOParameters](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-validateutxoparameters)


### function ValidateWitness

```cpp
virtual bool ValidateWitness(
    const ConsensusSubject & subject,
    const std::shared_ptr< GeniusTransaction > & tx,
    const UTXOTxParameters & params,
    const std::shared_ptr< Blockchain > & blockchain
) const override
```

Validates the external witness data supplied by consensus. 

**Parameters**: 

  * **subject** Consensus subject carrying UTXO commitment data. 
  * **tx** Transaction that references the public-chain source event. 
  * **params** UTXO inputs and outputs carrying the source reference and minted outputs. 
  * **blockchain** [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) service; currently unused by public-chain validation. 


**Return**: True when `tx` is present, `params` are non-empty, and the source reference verification succeeds. 

**Reimplements**: [sgns::IInputValidator::ValidateWitness](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-validatewitness)


### function RequiresConsensusUTXOData

```cpp
inline virtual bool RequiresConsensusUTXOData() const override
```

Public-chain validation does not require local UTXO witness data. 

**Return**: Always false. 

**Reimplements**: [sgns::IInputValidator::RequiresConsensusUTXOData](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-requiresconsensusutxodata)


Bridge mints use the EVM transaction hash as input, not a local UTXO. Receipt verification is handled via RPC in VerifyPublicChainSmartContract.


### function SetTransportFactory

```cpp
inline void SetTransportFactory(
    TransportFactory factory
)
```

Inject a custom transport factory for DI-based mock support. 

**Parameters**: 

  * **factory** Callable taking (url, timeout) → unique_ptr<JsonRpcTransport>. 


When set, every call to [VerifyPublicChainSmartContract()](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-verifypublicchainsmartcontract) will use this factory to create transport instances instead of the default RpcHttpTransport factory. Not called in production (D-16).


### function GetFirstRpcUrl

```cpp
inline std::optional< std::string > GetFirstRpcUrl(
    const std::string & chain_id
) const
```

Returns the first RPC endpoint URL for a given chain ID, if any exist. 

**Parameters**: 

  * **chain_id** Numeric chain ID as a string (e.g. "1" for Ethereum). 


**Return**: The first endpoint URL if one exists, std::nullopt otherwise. 

Used by the startup catch-up scan to obtain an RPC URL for eth_getLogs queries without needing to re-parse the ChainList provider data.


### function GetSlotHash

```cpp
std::vector< uint8_t > GetSlotHash(
    size_t slot_index,
    const std::string & chain_id
) const
```

Returns the SHA-256 hash of an endpoint URL for a vote slot (Phase 6, D-01). 

**Parameters**: 

  * **slot_index** Vote slot (0, 1, or 2). 
  * **chain_id** Source chain identifier. 


**Return**: 32-byte SHA-256 of the qualifying endpoint URL, or an empty vector when no qualifying endpoint exists or the slot/chain is unknown. 

Slot semantics (per the slot-based RPC-hash voting model):

* slot 0: first DIRECT_API endpoint (consensus_weight >= 50, D-02).
* slot 1: first PUBLIC endpoint (consensus_weight < 50).
* slot 2: second PUBLIC endpoint (consensus_weight < 50).

The hash is over the endpoint's raw `url` string (UTF-8), NOT the resolved URL nor the bridge_contract_address/event_topic0 fields, so the hash is stable across config reloads and deterministic across peers that share config (T-06-03). An empty vector signals abstention (D-05).


### function GetFirstConfiguredChainId

```cpp
inline std::optional< std::string > GetFirstConfiguredChainId() const
```

Returns the first configured chain id, if any (Phase 6, D-01). 

**Return**: First configured chain id, or std::nullopt when none configured. 

Used by [GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/)'s slot-hash populator lambda to resolve a chain context for single-chain deployments (multi-chain resolution is a future enhancement). Read-only and additive (D-10: Tier 1 untouched).


## Friends

### friend ::PublicChainInputValidatorTestAccess

```cpp
friend class ::PublicChainInputValidatorTestAccess(
    ::PublicChainInputValidatorTestAccess 
);
```

Friend accessor for unit testing VerifyPublicChainSmartContract and the wired rpc_endpoints_ (mirrors BridgeRelayerTestAccess). 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
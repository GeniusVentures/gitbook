---
title: sgns::IInputValidator
summary: Strategy interface for validating transaction inputs and their witness data. 

---

# sgns::IInputValidator



Strategy interface for validating transaction inputs and their witness data. 


`#include <InputValidators.hpp>`

Inherited by [sgns::GeniusInputValidator](/source-reference/Classes/dd/d55/classsgns_1_1_genius_input_validator/), [sgns::MigrationInputValidator](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/), [sgns::PublicChainInputValidator](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/)

## Public Types

|                | Name           |
| -------------- | -------------- |
| using const [IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/) * | **[ValidatorPtr](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#using-validatorptr)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-~iinputvalidator)**() =default<br/>Destroys the input validator.  |
| virtual bool | **[ValidateUTXOParameters](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-validateutxoparameters)**(const [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) & params, const std::string & address, const [UTXOManager](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/) & utxo_manager) const =0<br/>Validates ownership and structure of the supplied UTXO parameters.  |
| virtual bool | **[ValidateWitness](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-validatewitness)**(const ConsensusSubject & subject, const std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > & tx, const [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) & params, const std::shared_ptr< [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) > & blockchain) const =0<br/>Validates the chain-specific witness data associated with a transaction input set.  |
| virtual bool | **[RequiresConsensusUTXOData](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-requiresconsensusutxodata)**() const =0<br/>Indicates whether this validator requires consensus-provided UTXO data.  |
| void | **[Register](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-register)**(const std::string & chain_id, [ValidatorPtr](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#using-validatorptr) validator) |
| void | **[UnregisterIf](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-unregisterif)**(const std::string & chain_id, [ValidatorPtr](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#using-validatorptr) expected)<br/>Remove a chain's registration only if it currently points to `expected` (compare-and-remove). Prevents a stale validator from clobbering a newer account's registration when it is destroyed, and lets a validator self-clean on destruction so the registry never holds a dangling pointer.  |
| [ValidatorPtr](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#using-validatorptr) | **[Get](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-get)**(const std::string & chain_id) |

## Public Types Documentation

### using ValidatorPtr

```cpp
using sgns::IInputValidator::ValidatorPtr = const IInputValidator *;
```


## Public Functions Documentation

### function ~IInputValidator

```cpp
virtual ~IInputValidator() =default
```

Destroys the input validator. 

### function ValidateUTXOParameters

```cpp
virtual bool ValidateUTXOParameters(
    const UTXOTxParameters & params,
    const std::string & address,
    const UTXOManager & utxo_manager
) const =0
```

Validates ownership and structure of the supplied UTXO parameters. 

**Parameters**: 

  * **params** UTXO inputs and outputs carried by the transaction. 
  * **address** Source address expected to own or authorize the inputs. 
  * **utxo_manager** Local UTXO manager used for ownership and signature checks when required. 


**Return**: True when the parameters are structurally valid for this source chain. 

**Reimplemented by**: [sgns::GeniusInputValidator::ValidateUTXOParameters](/source-reference/Classes/dd/d55/classsgns_1_1_genius_input_validator/#function-validateutxoparameters), [sgns::MigrationInputValidator::ValidateUTXOParameters](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/#function-validateutxoparameters), [sgns::PublicChainInputValidator::ValidateUTXOParameters](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-validateutxoparameters)


### function ValidateWitness

```cpp
virtual bool ValidateWitness(
    const ConsensusSubject & subject,
    const std::shared_ptr< GeniusTransaction > & tx,
    const UTXOTxParameters & params,
    const std::shared_ptr< Blockchain > & blockchain
) const =0
```

Validates the chain-specific witness data associated with a transaction input set. 

**Parameters**: 

  * **subject** Consensus subject that carries nonce, witness, and UTXO commitment data. 
  * **tx** Transaction whose inputs and outputs are being validated. 
  * **params** UTXO inputs and outputs carried by `tx`. 
  * **blockchain** [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) service used to resolve producer certificates when required. 


**Return**: True when the witness proves that `params` are valid for `tx`. 

**Reimplemented by**: [sgns::GeniusInputValidator::ValidateWitness](/source-reference/Classes/dd/d55/classsgns_1_1_genius_input_validator/#function-validatewitness), [sgns::MigrationInputValidator::ValidateWitness](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/#function-validatewitness), [sgns::PublicChainInputValidator::ValidateWitness](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-validatewitness)


### function RequiresConsensusUTXOData

```cpp
virtual bool RequiresConsensusUTXOData() const =0
```

Indicates whether this validator requires consensus-provided UTXO data. 

**Return**: True when the validator needs UTXO witness and commitment data from consensus. 

**Reimplemented by**: [sgns::GeniusInputValidator::RequiresConsensusUTXOData](/source-reference/Classes/dd/d55/classsgns_1_1_genius_input_validator/#function-requiresconsensusutxodata), [sgns::MigrationInputValidator::RequiresConsensusUTXOData](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/#function-requiresconsensusutxodata), [sgns::PublicChainInputValidator::RequiresConsensusUTXOData](/source-reference/Classes/d5/d75/classsgns_1_1_public_chain_input_validator/#function-requiresconsensusutxodata)


### function Register

```cpp
static inline void Register(
    const std::string & chain_id,
    ValidatorPtr validator
)
```


### function UnregisterIf

```cpp
static inline void UnregisterIf(
    const std::string & chain_id,
    ValidatorPtr expected
)
```

Remove a chain's registration only if it currently points to `expected` (compare-and-remove). Prevents a stale validator from clobbering a newer account's registration when it is destroyed, and lets a validator self-clean on destruction so the registry never holds a dangling pointer. 

### function Get

```cpp
static inline ValidatorPtr Get(
    const std::string & chain_id
)
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
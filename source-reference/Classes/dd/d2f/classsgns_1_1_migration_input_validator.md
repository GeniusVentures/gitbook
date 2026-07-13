---
title: sgns::MigrationInputValidator
summary: Implements the InputValidator for a Migration type. 

---

# sgns::MigrationInputValidator



Implements the InputValidator for a Migration type. 


`#include <MigrationInputValidator.hpp>`

Inherits from [sgns::IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual bool | **[ValidateUTXOParameters](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/#function-validateutxoparameters)**(const [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) & params, const std::string & address, const [UTXOManager](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/) & utxo_manager) const override<br/>Validates ownership and structure of the supplied UTXO parameters.  |
| virtual bool | **[ValidateWitness](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/#function-validatewitness)**(const ConsensusSubject & subject, const std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > & tx, const [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) & params, const std::shared_ptr< [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) > & blockchain) const override<br/>Validates the chain-specific witness data associated with a transaction input set.  |
| virtual bool | **[RequiresConsensusUTXOData](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/#function-requiresconsensusutxodata)**() const override<br/>Indicates whether this validator requires consensus-provided UTXO data.  |
| bool | **[Register](/source-reference/Classes/dd/d2f/classsgns_1_1_migration_input_validator/#function-register)**()<br/>Registers this validator in the global registry for the "migration" chain ID.  |

## Additional inherited members

**Public Types inherited from [sgns::IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/)**

|                | Name           |
| -------------- | -------------- |
| using const [IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/) * | **[ValidatorPtr](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#using-validatorptr)**  |

**Public Functions inherited from [sgns::IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-~iinputvalidator)**() =default<br/>Destroys the input validator.  |
| void | **[UnregisterIf](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-unregisterif)**(const std::string & chain_id, [ValidatorPtr](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#using-validatorptr) expected)<br/>Remove a chain's registration only if it currently points to `expected` (compare-and-remove). Prevents a stale validator from clobbering a newer account's registration when it is destroyed, and lets a validator self-clean on destruction so the registry never holds a dangling pointer.  |
| [ValidatorPtr](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#using-validatorptr) | **[Get](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-get)**(const std::string & chain_id) |


## Public Functions Documentation

### function ValidateUTXOParameters

```cpp
virtual bool ValidateUTXOParameters(
    const UTXOTxParameters & params,
    const std::string & address,
    const UTXOManager & utxo_manager
) const override
```

Validates ownership and structure of the supplied UTXO parameters. 

**Parameters**: 

  * **params** UTXO inputs and outputs carried by the transaction. 
  * **address** Source address expected to own or authorize the inputs. 
  * **utxo_manager** Local UTXO manager used for ownership and signature checks when required. 


**Return**: True when the parameters are structurally valid for this source chain. 

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

Validates the chain-specific witness data associated with a transaction input set. 

**Parameters**: 

  * **subject** Consensus subject that carries nonce, witness, and UTXO commitment data. 
  * **tx** Transaction whose inputs and outputs are being validated. 
  * **params** UTXO inputs and outputs carried by `tx`. 
  * **blockchain** [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) service used to resolve producer certificates when required. 


**Return**: True when the witness proves that `params` are valid for `tx`. 

**Reimplements**: [sgns::IInputValidator::ValidateWitness](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-validatewitness)


### function RequiresConsensusUTXOData

```cpp
inline virtual bool RequiresConsensusUTXOData() const override
```

Indicates whether this validator requires consensus-provided UTXO data. 

**Return**: True when the validator needs UTXO witness and commitment data from consensus. 

**Reimplements**: [sgns::IInputValidator::RequiresConsensusUTXOData](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-requiresconsensusutxodata)


### function Register

```cpp
static inline bool Register()
```

Registers this validator in the global registry for the "migration" chain ID. 

**Return**: true when the registration is done. This is used to ensure that the static instance is initialized and registered before main() starts. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
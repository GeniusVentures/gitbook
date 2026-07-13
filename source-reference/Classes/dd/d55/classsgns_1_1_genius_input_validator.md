---
title: sgns::GeniusInputValidator
summary: Validator for native Genius-chain transactions. 

---

# sgns::GeniusInputValidator



Validator for native Genius-chain transactions. 


`#include <GeniusInputValidator.hpp>`

Inherits from [sgns::IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual bool | **[ValidateUTXOParameters](/source-reference/Classes/dd/d55/classsgns_1_1_genius_input_validator/#function-validateutxoparameters)**(const [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) & params, const std::string & address, const [UTXOManager](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/) & utxo_manager) const override<br/>Validates UTXO ownership and signatures for Genius-native inputs.  |
| virtual bool | **[ValidateWitness](/source-reference/Classes/dd/d55/classsgns_1_1_genius_input_validator/#function-validatewitness)**(const ConsensusSubject & subject, const std::shared_ptr< [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/) > & tx, const [UTXOTxParameters](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-utxotxparameters) & params, const std::shared_ptr< [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) > & blockchain) const override<br/>Validates witness data against Genius-chain consensus state.  |
| virtual bool | **[RequiresConsensusUTXOData](/source-reference/Classes/dd/d55/classsgns_1_1_genius_input_validator/#function-requiresconsensusutxodata)**() const override<br/>Genius-native validation requires consensus UTXO context.  |
| bool | **[Register](/source-reference/Classes/dd/d55/classsgns_1_1_genius_input_validator/#function-register)**() |

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

Validates UTXO ownership and signatures for Genius-native inputs. 

**Parameters**: 

  * **params** UTXO inputs and outputs carried by the transaction. 
  * **address** Source address expected to own or authorize the inputs. 
  * **utxo_manager** Local UTXO manager used to verify the inputs. 


**Return**: True when both input and output lists are non-empty and `utxo_manager` accepts the parameters. 

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

Validates witness data against Genius-chain consensus state. 

**Parameters**: 

  * **subject** Consensus subject containing the UTXO witness and commitment. 
  * **tx** Genius-chain transaction being validated. 
  * **params** UTXO inputs and outputs carried by `tx`. 
  * **blockchain** [Blockchain](/source-reference/Classes/de/da2/classsgns_1_1_blockchain/) service used to resolve producer certificates. 


**Return**: True when the witness and transaction UTXO parameters are consistent. 

**Reimplements**: [sgns::IInputValidator::ValidateWitness](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-validatewitness)


Checks the transaction hash, UTXO commitment roots, consumed input proofs, input signatures, ownership, duplicate inputs, registered token identifiers, and raw-value input/output balance.


### function RequiresConsensusUTXOData

```cpp
inline virtual bool RequiresConsensusUTXOData() const override
```

Genius-native validation requires consensus UTXO context. 

**Return**: Always true. 

**Reimplements**: [sgns::IInputValidator::RequiresConsensusUTXOData](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/#function-requiresconsensusutxodata)


### function Register

```cpp
static inline bool Register()
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: sgns::InputUTXOInfo
summary: Raw UTXO input data included in a spend request. 

---

# sgns::InputUTXOInfo



Raw UTXO input data included in a spend request. 


`#include <UTXOStructs.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::vector< uint8_t > | **[SerializeForSigning](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/#function-serializeforsigning)**() const<br/>Serializes the input fields that must be signed by the owner.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[txid_hash_](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/#variable-txid_hash_)** <br/>Hash of the transaction that created the output.  |
| uint32_t | **[output_idx_](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/#variable-output_idx_)** <br/>Zero-based output index within the originating transaction.  |
| std::vector< uint8_t > | **[signature_](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/#variable-signature_)** <br/>Signature authorizing the spend of this outpoint.  |

## Public Functions Documentation

### function SerializeForSigning

```cpp
std::vector< uint8_t > SerializeForSigning() const
```

Serializes the input fields that must be signed by the owner. 

## Public Attributes Documentation

### variable txid_hash_

```cpp
base::Hash256 txid_hash_;
```

Hash of the transaction that created the output. 

### variable output_idx_

```cpp
uint32_t output_idx_;
```

Zero-based output index within the originating transaction. 

### variable signature_

```cpp
std::vector< uint8_t > signature_;
```

Signature authorizing the spend of this outpoint. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
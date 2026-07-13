---
title: sgns::OutPoint
summary: Unique identifier for a transaction output. 

---

# sgns::OutPoint



Unique identifier for a transaction output. 


`#include <GeniusUTXO.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[operator==](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/#function-operator==)**(const [OutPoint](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/) & other) const<br/>Compares two outpoints for exact transaction-and-index equality.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[txid_hash_](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/#variable-txid_hash_)** <br/>Hash of the transaction that produced the output.  |
| uint32_t | **[output_idx_](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/#variable-output_idx_)** <br/>Output index within the producing transaction.  |

## Public Functions Documentation

### function operator==

```cpp
inline bool operator==(
    const OutPoint & other
) const
```

Compares two outpoints for exact transaction-and-index equality. 

**Parameters**: 

  * **other** Outpoint to compare against. 


**Return**: True when both the transaction hash and output index match. 

## Public Attributes Documentation

### variable txid_hash_

```cpp
base::Hash256 txid_hash_;
```

Hash of the transaction that produced the output. 

### variable output_idx_

```cpp
uint32_t output_idx_ { 0 };
```

Output index within the producing transaction. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
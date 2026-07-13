---
title: sgns::OutputDestInfo
summary: Single UTXO output destination entry. 

---

# sgns::OutputDestInfo



Single UTXO output destination entry. 


`#include <UTXOStructs.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| uint64_t | **[encrypted_amount](/source-reference/Classes/dc/dfd/structsgns_1_1_output_dest_info/#variable-encrypted_amount)** <br/>El Gamal encrypted amount.  |
| std::string | **[dest_address](/source-reference/Classes/dc/dfd/structsgns_1_1_output_dest_info/#variable-dest_address)** <br/>Destination node address.  |
| [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) | **[token_id](/source-reference/Classes/dc/dfd/structsgns_1_1_output_dest_info/#variable-token_id)** <br/>Token identifier.  |

## Public Attributes Documentation

### variable encrypted_amount

```cpp
uint64_t encrypted_amount;
```

El Gamal encrypted amount. 

### variable dest_address

```cpp
std::string dest_address;
```

Destination node address. 

### variable token_id

```cpp
TokenID token_id;
```

Token identifier. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
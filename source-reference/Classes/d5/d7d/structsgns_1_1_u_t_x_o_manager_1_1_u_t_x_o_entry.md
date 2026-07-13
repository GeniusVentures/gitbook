---
title: sgns::UTXOManager::UTXOEntry
summary: Metadata tracked for each outpoint in the local registry. 

---

# sgns::UTXOManager::UTXOEntry



Metadata tracked for each outpoint in the local registry. 


`#include <UTXOManager.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [UTXOState](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enum-utxostate) | **[state](/source-reference/Classes/d5/d7d/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_entry/#variable-state)** <br/>Current lifecycle state of the UTXO.  |
| [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) | **[utxo](/source-reference/Classes/d5/d7d/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_entry/#variable-utxo)** <br/>The actual UTXO data.  |
| uint64_t | **[created_epoch](/source-reference/Classes/d5/d7d/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_entry/#variable-created_epoch)** <br/>Epoch when the UTXO was created.  |
| std::optional< uint64_t > | **[spent_epoch](/source-reference/Classes/d5/d7d/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_entry/#variable-spent_epoch)** <br/>Epoch when the UTXO was consumed, if applicable.  |
| std::optional< [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) > | **[spent_by_txid](/source-reference/Classes/d5/d7d/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_entry/#variable-spent_by_txid)** <br/>Transaction ID that consumed this UTXO, if applicable.  |
| [UTXOType](/source-reference/Classes/d0/dac/classsgns_1_1_u_t_x_o_manager/#enum-utxotype) | **[type](/source-reference/Classes/d5/d7d/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_entry/#variable-type)** <br/>Type classification for the UTXO.  |

## Public Attributes Documentation

### variable state

```cpp
UTXOState state { UTXOState::UTXO_READY };
```

Current lifecycle state of the UTXO. 

### variable utxo

```cpp
GeniusUTXO utxo;
```

The actual UTXO data. 

### variable created_epoch

```cpp
uint64_t created_epoch { 0 };
```

Epoch when the UTXO was created. 

### variable spent_epoch

```cpp
std::optional< uint64_t > spent_epoch;
```

Epoch when the UTXO was consumed, if applicable. 

### variable spent_by_txid

```cpp
std::optional< base::Hash256 > spent_by_txid;
```

Transaction ID that consumed this UTXO, if applicable. 

### variable type

```cpp
UTXOType type { UTXOType::UTXO_NORMAL };
```

Type classification for the UTXO. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
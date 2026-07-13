---
title: sgns::UTXOManager::UTXOCheckpoint
summary: Persisted checkpoint snapshot used to audit finalized UTXO state at a given epoch. 

---

# sgns::UTXOManager::UTXOCheckpoint



Persisted checkpoint snapshot used to audit finalized UTXO state at a given epoch. 


`#include <UTXOManager.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::string | **[owner_address](/source-reference/Classes/dc/d6b/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_checkpoint/#variable-owner_address)** <br/>Owner address associated with this checkpoint.  |
| uint64_t | **[epoch](/source-reference/Classes/dc/d6b/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_checkpoint/#variable-epoch)** <br/>Epoch number when the checkpoint was created.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[last_finalized_tx](/source-reference/Classes/dc/d6b/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_checkpoint/#variable-last_finalized_tx)** <br/>Transaction ID of the last finalized transaction at the time of checkpointing.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[registry_hash](/source-reference/Classes/dc/d6b/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_checkpoint/#variable-registry_hash)** <br/>Hash of the full UTXO registry state at the time of checkpointing.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[utxo_merkle_root](/source-reference/Classes/dc/d6b/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_checkpoint/#variable-utxo_merkle_root)** <br/>Merkle root of the unspent UTXOs at the time of checkpointing.  |
| uint64_t | **[utxo_count](/source-reference/Classes/dc/d6b/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_checkpoint/#variable-utxo_count)** <br/>Total number of UTXOs included in the checkpoint.  |
| uint64_t | **[created_at_ms](/source-reference/Classes/dc/d6b/structsgns_1_1_u_t_x_o_manager_1_1_u_t_x_o_checkpoint/#variable-created_at_ms)** <br/>Timestamp in milliseconds when the checkpoint was created.  |

## Public Attributes Documentation

### variable owner_address

```cpp
std::string owner_address;
```

Owner address associated with this checkpoint. 

### variable epoch

```cpp
uint64_t epoch { 0 };
```

Epoch number when the checkpoint was created. 

### variable last_finalized_tx

```cpp
base::Hash256 last_finalized_tx {};
```

Transaction ID of the last finalized transaction at the time of checkpointing. 

### variable registry_hash

```cpp
base::Hash256 registry_hash {};
```

Hash of the full UTXO registry state at the time of checkpointing. 

### variable utxo_merkle_root

```cpp
base::Hash256 utxo_merkle_root {};
```

Merkle root of the unspent UTXOs at the time of checkpointing. 

### variable utxo_count

```cpp
uint64_t utxo_count { 0 };
```

Total number of UTXOs included in the checkpoint. 

### variable created_at_ms

```cpp
uint64_t created_at_ms { 0 };
```

Timestamp in milliseconds when the checkpoint was created. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
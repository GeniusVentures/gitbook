---
title: sgns::AccountMessenger::InterfaceMethods
summary: Interface methods the user needs to define. 

---

# sgns::AccountMessenger::InterfaceMethods



Interface methods the user needs to define. 


`#include <AccountMessenger.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::function< outcome::result< std::vector< uint8_t > >(std::vector< uint8_t > data)> | **[sign_](/source-reference/Classes/dd/d3e/structsgns_1_1_account_messenger_1_1_interface_methods/#variable-sign_)** <br/>Signing method.  |
| std::function< outcome::result< bool >(std::string address, std::string sig, std::vector< uint8_t > data)> | **[verify_signature_](/source-reference/Classes/dd/d3e/structsgns_1_1_account_messenger_1_1_interface_methods/#variable-verify_signature_)** <br/>Verify signature method.  |
| std::function< outcome::result< uint64_t >(std::string address)> | **[get_local_nonce_](/source-reference/Classes/dd/d3e/structsgns_1_1_account_messenger_1_1_interface_methods/#variable-get_local_nonce_)** <br/>Get local nonce method.  |
| std::function< outcome::result< std::string >(uint8_t block_index, const std::string &address)> | **[get_block_cid_](/source-reference/Classes/dd/d3e/structsgns_1_1_account_messenger_1_1_interface_methods/#variable-get_block_cid_)** <br/>Get local genesis block method.  |
| std::function< outcome::result< bool >(const std::string &cid)> | **[has_block_cid_](/source-reference/Classes/dd/d3e/structsgns_1_1_account_messenger_1_1_interface_methods/#variable-has_block_cid_)** <br/>Check if a CID is locally available.  |
| std::function< outcome::result< std::vector< std::string > >(const std::string &address)> | **[get_utxos_](/source-reference/Classes/dd/d3e/structsgns_1_1_account_messenger_1_1_interface_methods/#variable-get_utxos_)** <br/>Get local UTXOs as a list of strings for a given address.  |
| std::function< outcome::result< std::optional< uint64_t > >(const std::string &address)> | **[get_validator_weight_](/source-reference/Classes/dd/d3e/structsgns_1_1_account_messenger_1_1_interface_methods/#variable-get_validator_weight_)** <br/>Get validator weight for an address (empty if not a validator).  |
| std::function< outcome::result< std::string >(const std::string &tx_hash)> | **[get_transaction_cid_](/source-reference/Classes/dd/d3e/structsgns_1_1_account_messenger_1_1_interface_methods/#variable-get_transaction_cid_)** <br/>Get transaction CID by hash.  |

## Public Attributes Documentation

### variable sign_

```cpp
std::function< outcome::result< std::vector< uint8_t > >(std::vector< uint8_t > data)> sign_;
```

Signing method. 

### variable verify_signature_

```cpp
std::function< outcome::result< bool >(std::string address, std::string sig, std::vector< uint8_t > data)> verify_signature_;
```

Verify signature method. 

### variable get_local_nonce_

```cpp
std::function< outcome::result< uint64_t >(std::string address)> get_local_nonce_;
```

Get local nonce method. 

### variable get_block_cid_

```cpp
std::function< outcome::result< std::string >(uint8_t block_index, const std::string &address)> get_block_cid_;
```

Get local genesis block method. 

### variable has_block_cid_

```cpp
std::function< outcome::result< bool >(const std::string &cid)> has_block_cid_;
```

Check if a CID is locally available. 

### variable get_utxos_

```cpp
std::function< outcome::result< std::vector< std::string > >(const std::string &address)> get_utxos_;
```

Get local UTXOs as a list of strings for a given address. 

### variable get_validator_weight_

```cpp
std::function< outcome::result< std::optional< uint64_t > >(const std::string &address)> get_validator_weight_;
```

Get validator weight for an address (empty if not a validator). 

### variable get_transaction_cid_

```cpp
std::function< outcome::result< std::string >(const std::string &tx_hash)> get_transaction_cid_;
```

Get transaction CID by hash. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
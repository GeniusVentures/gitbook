---
title: sgns::AccountMessenger::RequestTask

---

# sgns::AccountMessenger::RequestTask





## Public Attributes

|                | Name           |
| -------------- | -------------- |
| [RequestType](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#enum-requesttype) | **[type](/source-reference/Classes/dc/d28/structsgns_1_1_account_messenger_1_1_request_task/#variable-type)**  |
| uint64_t | **[timeout_ms](/source-reference/Classes/dc/d28/structsgns_1_1_account_messenger_1_1_request_task/#variable-timeout_ms)**  |
| uint64_t | **[silent_time_ms](/source-reference/Classes/dc/d28/structsgns_1_1_account_messenger_1_1_request_task/#variable-silent_time_ms)**  |
| uint8_t | **[block_index](/source-reference/Classes/dc/d28/structsgns_1_1_account_messenger_1_1_request_task/#variable-block_index)**  |
| std::string | **[cid](/source-reference/Classes/dc/d28/structsgns_1_1_account_messenger_1_1_request_task/#variable-cid)**  |
| std::string | **[utxo_address](/source-reference/Classes/dc/d28/structsgns_1_1_account_messenger_1_1_request_task/#variable-utxo_address)**  |
| std::function< void(outcome::result< std::string >)> | **[callback](/source-reference/Classes/dc/d28/structsgns_1_1_account_messenger_1_1_request_task/#variable-callback)**  |
| std::shared_ptr< std::promise< outcome::result< uint64_t > > > | **[nonce_promise](/source-reference/Classes/dc/d28/structsgns_1_1_account_messenger_1_1_request_task/#variable-nonce_promise)**  |
| std::shared_ptr< std::promise< outcome::result< std::unordered_set< std::string > > > > | **[utxo_promise](/source-reference/Classes/dc/d28/structsgns_1_1_account_messenger_1_1_request_task/#variable-utxo_promise)**  |

## Public Attributes Documentation

### variable type

```cpp
RequestType type;
```


### variable timeout_ms

```cpp
uint64_t timeout_ms;
```


### variable silent_time_ms

```cpp
uint64_t silent_time_ms { 150 };
```


### variable block_index

```cpp
uint8_t block_index { 0 };
```


### variable cid

```cpp
std::string cid;
```


### variable utxo_address

```cpp
std::string utxo_address;
```


### variable callback

```cpp
std::function< void(outcome::result< std::string >)> callback;
```


### variable nonce_promise

```cpp
std::shared_ptr< std::promise< outcome::result< uint64_t > > > nonce_promise;
```


### variable utxo_promise

```cpp
std::shared_ptr< std::promise< outcome::result< std::unordered_set< std::string > > > > utxo_promise;
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
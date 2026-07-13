---
title: sgns::AccountMessenger

---

# sgns::AccountMessenger






`#include <AccountMessenger.hpp>`

Inherits from std::enable_shared_from_this< AccountMessenger >

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[InterfaceMethods](/source-reference/Classes/dd/d3e/structsgns_1_1_account_messenger_1_1_interface_methods/)** <br/>Interface methods the user needs to define.  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[Error](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#enum-error)** { PROTO_DESERIALIZATION = 0, PROTO_SERIALIZATION, NONCE_REQUEST_IN_PROGRESS, NONCE_GET_ERROR, NO_RESPONSE_RECEIVED, RESPONSE_WITHOUT_NONCE, GENESIS_REQUEST_ERROR, UTXO_REQUEST_ERROR}<br/>Account Messenger errors.  |
| using std::function< bool(const std::string &cid, const std::string &peer_id, const std::string &address)> | **[BlockResponseHandler](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#using-blockresponsehandler)**  |
| using std::function< void(const std::set< std::string > &topics)> | **[HeadRequestHandler](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#using-headrequesthandler)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [AccountMessenger](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-accountmessenger) > | **[New](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-new)**(std::string address, std::shared_ptr< ipfs_pubsub::GossipPubSub > pubsub, [InterfaceMethods](/source-reference/Classes/dd/d3e/structsgns_1_1_account_messenger_1_1_interface_methods/) methods)<br/>Factory constructor of new [AccountMessenger](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/).  |
| | **[~AccountMessenger](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-~accountmessenger)**()<br/>Destroy the Account Messenger object.  |
| outcome::result< uint64_t > | **[GetLatestNonce](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-getlatestnonce)**(uint64_t timeout_ms, uint64_t silent_time_ms =150)<br/>Get the Latest Nonce from the network.  |
| outcome::result< void > | **[RequestGenesis](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-requestgenesis)**(uint64_t timeout_ms, std::function< void(outcome::result< std::string >)> callback =nullptr)<br/>Request genesis block from the network (retries until timeout).  |
| outcome::result< void > | **[RequestAccountCreation](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-requestaccountcreation)**(uint64_t timeout_ms, std::function< void(outcome::result< std::string >)> callback)<br/>Request account creation from the network and invoke callback with found CIDs.  |
| outcome::result< void > | **[RequestValidatorRegistry](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-requestvalidatorregistry)**(uint64_t timeout_ms, std::function< void(outcome::result< std::string >)> callback) |
| outcome::result< void > | **[RequestRegularBlock](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-requestregularblock)**(uint64_t timeout_ms, std::string cid, std::function< void(outcome::result< std::string >)> callback =nullptr)<br/>Request a block by CID from the network (retries until timeout).  |
| outcome::result< void > | **[RequestTransaction](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-requesttransaction)**(uint64_t timeout_ms, std::string tx_hash, std::function< void(outcome::result< std::string >)> callback =nullptr)<br/>Request a transaction by hash from the network (retries until timeout).  |
| outcome::result< std::unordered_set< std::string > > | **[RequestUTXOs](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-requestutxos)**(uint64_t timeout_ms, const std::string & address, uint64_t silent_time_ms =150)<br/>Request UTXOs for a specific address and return the selected response.  |
| void | **[RegisterBlockResponseHandler](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-registerblockresponsehandler)**([BlockResponseHandler](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#using-blockresponsehandler) handler)<br/>Register global block response handler.  |
| void | **[ClearBlockResponseHandler](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-clearblockresponsehandler)**()<br/>Clears the block response handler.  |
| void | **[RegisterHeadRequestHandler](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-registerheadrequesthandler)**([HeadRequestHandler](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#using-headrequesthandler) handler)<br/>Register handler for incoming head requests.  |
| void | **[ClearHeadRequestHandler](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-clearheadrequesthandler)**()<br/>Clears the head request handler.  |
| outcome::result< void > | **[RequestHeads](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#function-requestheads)**(const std::unordered_set< std::string > & topics)<br/>Request heads broadcast for specific topics.  |

## Public Types Documentation

### enum Error

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| PROTO_DESERIALIZATION | 0| [Error](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#enum-error) in protobuf data deserialization.   |
| PROTO_SERIALIZATION | | [Error](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/#enum-error) in protobuf data serialization.   |
| NONCE_REQUEST_IN_PROGRESS | | Nonce request already in progress.   |
| NONCE_GET_ERROR | | Nonce couldn't be fetched.   |
| NO_RESPONSE_RECEIVED | | No response received from network.   |
| RESPONSE_WITHOUT_NONCE | | Response received but without nonce data.   |
| GENESIS_REQUEST_ERROR | | Genesis request failed.   |
| UTXO_REQUEST_ERROR | | UTXO request failed.   |



Account Messenger errors. 

### using BlockResponseHandler

```cpp
using sgns::AccountMessenger::BlockResponseHandler = 
std::function<bool( const std::string &cid, const std::string &peer_id, const std::string &address )>;
```


### using HeadRequestHandler

```cpp
using sgns::AccountMessenger::HeadRequestHandler = std::function<void( const std::set<std::string> &topics )>;
```


## Public Functions Documentation

### function New

```cpp
static std::shared_ptr< AccountMessenger > New(
    std::string address,
    std::shared_ptr< ipfs_pubsub::GossipPubSub > pubsub,
    InterfaceMethods methods
)
```

Factory constructor of new [AccountMessenger](/source-reference/Classes/d5/d74/classsgns_1_1_account_messenger/). 

**Parameters**: 

  * **address** Own address 
  * **pubsub** pubsub instance 
  * **methods** interface methods [InterfaceMethods](/source-reference/Classes/dd/d3e/structsgns_1_1_account_messenger_1_1_interface_methods/)


**Return**: Valid pointer if succeeds, nullptr otherwise 

### function ~AccountMessenger

```cpp
~AccountMessenger()
```

Destroy the Account Messenger object. 

### function GetLatestNonce

```cpp
outcome::result< uint64_t > GetLatestNonce(
    uint64_t timeout_ms,
    uint64_t silent_time_ms =150
)
```

Get the Latest Nonce from the network. 

**Parameters**: 

  * **timeout_ms** Timeout in miliseconds to get the latest nonce 
  * **silent_time_ms** Time tyo wait for subsequential nonce responses after first was received 


**Return**: Nonce value if success, error otherwise 

### function RequestGenesis

```cpp
outcome::result< void > RequestGenesis(
    uint64_t timeout_ms,
    std::function< void(outcome::result< std::string >)> callback =nullptr
)
```

Request genesis block from the network (retries until timeout). 

**Parameters**: 

  * **timeout_ms** Total timeout in milliseconds to wait for responses 
  * **callback** Function to be called for each CID found (empty string if none) 


**Return**: success if at least one response arrives before timeout, error otherwise 

### function RequestAccountCreation

```cpp
outcome::result< void > RequestAccountCreation(
    uint64_t timeout_ms,
    std::function< void(outcome::result< std::string >)> callback
)
```

Request account creation from the network and invoke callback with found CIDs. 

**Parameters**: 

  * **timeout_ms** Total timeout in milliseconds to wait for responses 
  * **callback** Function to be called for each CID found (signature: void(std::string)) 


**Return**: success on scheduled request, error otherwise 

### function RequestValidatorRegistry

```cpp
outcome::result< void > RequestValidatorRegistry(
    uint64_t timeout_ms,
    std::function< void(outcome::result< std::string >)> callback
)
```


### function RequestRegularBlock

```cpp
outcome::result< void > RequestRegularBlock(
    uint64_t timeout_ms,
    std::string cid,
    std::function< void(outcome::result< std::string >)> callback =nullptr
)
```

Request a block by CID from the network (retries until timeout). 

**Parameters**: 

  * **timeout_ms** Total timeout in milliseconds to wait for responses 
  * **cid** CID to request 
  * **callback** Callback invoked with the CID result (or error) 


**Return**: success on scheduled request, error otherwise 

### function RequestTransaction

```cpp
outcome::result< void > RequestTransaction(
    uint64_t timeout_ms,
    std::string tx_hash,
    std::function< void(outcome::result< std::string >)> callback =nullptr
)
```

Request a transaction by hash from the network (retries until timeout). 

**Parameters**: 

  * **timeout_ms** Total timeout in milliseconds to wait for responses 
  * **tx_hash** Transaction hash to request 
  * **callback** Callback invoked with the CID result (or error) 


**Return**: success on scheduled request, error otherwise 

### function RequestUTXOs

```cpp
outcome::result< std::unordered_set< std::string > > RequestUTXOs(
    uint64_t timeout_ms,
    const std::string & address,
    uint64_t silent_time_ms =150
)
```

Request UTXOs for a specific address and return the selected response. 

**Parameters**: 

  * **timeout_ms** Total timeout in milliseconds to wait for responses 
  * **address** Address to request UTXOs for 
  * **silent_time_ms** Time to wait for subsequent responses after first one 


**Return**: Set of UTXO strings based on selection criteria, or error otherwise 

### function RegisterBlockResponseHandler

```cpp
void RegisterBlockResponseHandler(
    BlockResponseHandler handler
)
```

Register global block response handler. 

**Parameters**: 

  * **handler** Function to call for all block responses 


### function ClearBlockResponseHandler

```cpp
void ClearBlockResponseHandler()
```

Clears the block response handler. 

### function RegisterHeadRequestHandler

```cpp
void RegisterHeadRequestHandler(
    HeadRequestHandler handler
)
```

Register handler for incoming head requests. 

**Parameters**: 

  * **handler** Function to call when head request is received with topic list 


### function ClearHeadRequestHandler

```cpp
void ClearHeadRequestHandler()
```

Clears the head request handler. 

### function RequestHeads

```cpp
outcome::result< void > RequestHeads(
    const std::unordered_set< std::string > & topics
)
```

Request heads broadcast for specific topics. 

**Parameters**: 

  * **topics** Vector of topic names to request heads for 


**Return**: outcome::success if request was sent, error otherwise 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
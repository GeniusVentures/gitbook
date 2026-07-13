---
title: sgns::crdt::KeyPairFileStorage

---

# sgns::crdt::KeyPairFileStorage






`#include <keypair_file_storage.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[KeyPairFileStorage](/source-reference/Classes/d6/d1e/classsgns_1_1crdt_1_1_key_pair_file_storage/#function-keypairfilestorage)**(boost::filesystem::path keyPath) |
| outcome::result< libp2p::crypto::KeyPair > | **[GetKeyPair](/source-reference/Classes/d6/d1e/classsgns_1_1crdt_1_1_key_pair_file_storage/#function-getkeypair)**() const |

## Public Functions Documentation

### function KeyPairFileStorage

```cpp
KeyPairFileStorage(
    boost::filesystem::path keyPath
)
```


### function GetKeyPair

```cpp
outcome::result< libp2p::crypto::KeyPair > GetKeyPair() const
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
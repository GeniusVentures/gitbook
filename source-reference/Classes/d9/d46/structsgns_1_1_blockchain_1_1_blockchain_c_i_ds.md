---
title: sgns::Blockchain::BlockchainCIDs

---

# sgns::Blockchain::BlockchainCIDs





## Public Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[hasGenesis](/source-reference/Classes/d9/d46/structsgns_1_1_blockchain_1_1_blockchain_c_i_ds/#function-hasgenesis)**() const<br/>Checks whether a genesis CID is available.  |
| bool | **[hasAccount](/source-reference/Classes/d9/d46/structsgns_1_1_blockchain_1_1_blockchain_c_i_ds/#function-hasaccount)**(const std::string & address) const<br/>Checks whether an address has account-creation CID.  |
| bool | **[hasAnyAccount](/source-reference/Classes/d9/d46/structsgns_1_1_blockchain_1_1_blockchain_c_i_ds/#function-hasanyaccount)**() const<br/>Checks whether any account-creation CID exists.  |
| bool | **[isCompleteFor](/source-reference/Classes/d9/d46/structsgns_1_1_blockchain_1_1_blockchain_c_i_ds/#function-iscompletefor)**(const std::string & address) const<br/>Checks whether both genesis and account CID exist for address.  |

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::optional< std::string > | **[genesis_](/source-reference/Classes/d9/d46/structsgns_1_1_blockchain_1_1_blockchain_c_i_ds/#variable-genesis_)** <br/>Selected genesis CID.  |
| std::unordered_map< std::string, std::string > | **[account_creation_](/source-reference/Classes/d9/d46/structsgns_1_1_blockchain_1_1_blockchain_c_i_ds/#variable-account_creation_)** <br/>Selected account-creation CIDs keyed by address.  |

## Public Functions Documentation

### function hasGenesis

```cpp
inline bool hasGenesis() const
```

Checks whether a genesis CID is available. 

**Return**: `true` when genesis CID exists. 

### function hasAccount

```cpp
inline bool hasAccount(
    const std::string & address
) const
```

Checks whether an address has account-creation CID. 

**Parameters**: 

  * **address** Account address key. 


**Return**: `true` when address entry exists. 

### function hasAnyAccount

```cpp
inline bool hasAnyAccount() const
```

Checks whether any account-creation CID exists. 

**Return**: `true` when at least one account entry exists. 

### function isCompleteFor

```cpp
inline bool isCompleteFor(
    const std::string & address
) const
```

Checks whether both genesis and account CID exist for address. 

**Parameters**: 

  * **address** Account address key. 


**Return**: `true` when both required CIDs are present. 

## Public Attributes Documentation

### variable genesis_

```cpp
std::optional< std::string > genesis_;
```

Selected genesis CID. 

### variable account_creation_

```cpp
std::unordered_map< std::string, std::string > account_creation_;
```

Selected account-creation CIDs keyed by address. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
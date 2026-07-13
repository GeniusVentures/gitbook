---
title: sgns::utxo_address

---

# sgns::utxo_address





## Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[IsEscrowLockAddress](/source-reference/Namespaces/dd/de2/namespacesgns_1_1utxo__address/#function-isescrowlockaddress)**(std::string_view address)<br/>Checks if the address is a valid escrow lock address (0x-prefixed 64 hex chars).  |
| bool | **[IsAccountPublicKeyAddress](/source-reference/Namespaces/dd/de2/namespacesgns_1_1utxo__address/#function-isaccountpublickeyaddress)**(std::string_view address)<br/>Checks if the address is a public key.  |


## Functions Documentation

### function IsEscrowLockAddress

```cpp
bool IsEscrowLockAddress(
    std::string_view address
)
```

Checks if the address is a valid escrow lock address (0x-prefixed 64 hex chars). 

**Parameters**: 

  * **address** The address to check 


**Return**: true if the address is a valid escrow lock address, false otherwise 

### function IsAccountPublicKeyAddress

```cpp
bool IsAccountPublicKeyAddress(
    std::string_view address
)
```

Checks if the address is a public key. 

**Parameters**: 

  * **address** The address to check 


**Return**: true if the address is a public key address, false otherwise 





-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/UTXOStructs.hpp
summary: Shared UTXO transaction input and output data structures. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/UTXOStructs.hpp



Shared UTXO transaction input and output data structures.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::utxo_address](/source-reference/Namespaces/dd/de2/namespacesgns_1_1utxo__address/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::InputUTXOInfo](/source-reference/Classes/d3/dbc/structsgns_1_1_input_u_t_x_o_info/)** <br/>Raw UTXO input data included in a spend request.  |
| struct | **[sgns::OutputDestInfo](/source-reference/Classes/dc/dfd/structsgns_1_1_output_dest_info/)** <br/>Single UTXO output destination entry.  |

## Types

|                | Name           |
| -------------- | -------------- |
| using std::pair< std::vector< InputUTXOInfo >, std::vector< OutputDestInfo > > | **[UTXOTxParameters](/source-reference/Files/d1/dd1/_u_t_x_o_structs_8hpp/#using-utxotxparameters)** <br/>Pair of signed inputs and destination outputs that make up a UTXO transaction payload.  |

## Functions

|                | Name           |
| -------------- | -------------- |
| bool | **[IsEscrowLockAddress](/source-reference/Files/d1/dd1/_u_t_x_o_structs_8hpp/#function-isescrowlockaddress)**(std::string_view address)<br/>Checks if the address is a valid escrow lock address (0x-prefixed 64 hex chars).  |
| bool | **[IsAccountPublicKeyAddress](/source-reference/Files/d1/dd1/_u_t_x_o_structs_8hpp/#function-isaccountpublickeyaddress)**(std::string_view address)<br/>Checks if the address is a public key.  |

## Detailed Description

Shared UTXO transaction input and output data structures. 

**Date**: 2026-01-20 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 
## Types Documentation

### using UTXOTxParameters

```cpp
using sgns::UTXOTxParameters = std::pair<std::vector<InputUTXOInfo>, std::vector<OutputDestInfo>>;
```

Pair of signed inputs and destination outputs that make up a UTXO transaction payload. 


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



## Source code

```cpp

#ifndef SGNS_UTXO_STRUCTS_HPP
#define SGNS_UTXO_STRUCTS_HPP

#include "base/blob.hpp"
#include "TokenID.hpp"

namespace sgns
{
    namespace utxo_address
    {
        bool IsEscrowLockAddress( std::string_view address );

        bool IsAccountPublicKeyAddress( std::string_view address );
    } // namespace utxo_address

    struct InputUTXOInfo
    {
        std::vector<uint8_t> SerializeForSigning() const;

        base::Hash256        txid_hash_;  
        uint32_t             output_idx_; 
        std::vector<uint8_t> signature_;  
    };

    struct OutputDestInfo
    {
        uint64_t    encrypted_amount; 
        std::string dest_address;     
        TokenID     token_id;         
    };

    using UTXOTxParameters = std::pair<std::vector<InputUTXOInfo>, std::vector<OutputDestInfo>>;
}

#endif // SGNS_UTXO_STRUCTS_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

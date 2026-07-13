---
title: sgns::GeniusUTXO
summary: Immutable-style UTXO value object containing ownership, token, amount, and outpoint metadata. 

---

# sgns::GeniusUTXO



Immutable-style UTXO value object containing ownership, token, amount, and outpoint metadata. 


`#include <GeniusUTXO.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/#function-geniusutxo)**()<br/>Constructs an empty UTXO placeholder.  |
| | **[GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/#function-geniusutxo)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & hash, uint32_t previous_index, uint64_t amount, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id)<br/>Constructs a UTXO without an owner address.  |
| | **[GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/#function-geniusutxo)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & hash, uint32_t previous_index, uint64_t amount, [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) token_id, std::string owner_address)<br/>Constructs a fully specified UTXO.  |
| void | **[SetOwnerAddress](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/#function-setowneraddress)**(std::string owner_address)<br/>Sets the owner address associated with this UTXO.  |
| const std::string & | **[GetOwnerAddress](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/#function-getowneraddress)**() const<br/>Returns the owner address associated with this UTXO.  |
| [OutPoint](/source-reference/Classes/d6/dfe/structsgns_1_1_out_point/) | **[GetOutPoint](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/#function-getoutpoint)**() const<br/>Returns the full outpoint descriptor.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[GetTxID](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/#function-gettxid)**() const<br/>Returns the originating transaction id.  |
| uint32_t | **[GetOutputIdx](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/#function-getoutputidx)**() const<br/>Returns the output index within the originating transaction.  |
| uint64_t | **[GetAmount](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/#function-getamount)**() const<br/>Returns the unencrypted amount represented by the UTXO.  |
| [TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) | **[GetTokenID](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/#function-gettokenid)**() const<br/>Returns the token identifier associated with the UTXO.  |

## Public Functions Documentation

### function GeniusUTXO

```cpp
inline GeniusUTXO()
```

Constructs an empty UTXO placeholder. 

The placeholder has a default outpoint, zero amount, default token identifier, and no owner address. 


### function GeniusUTXO

```cpp
inline GeniusUTXO(
    const base::Hash256 & hash,
    uint32_t previous_index,
    uint64_t amount,
    TokenID token_id
)
```

Constructs a UTXO without an owner address. 

**Parameters**: 

  * **hash** Hash of the transaction that produced this output. 
  * **previous_index** Output index within the producing transaction. 
  * **amount** Amount carried by the output. 
  * **token_id** Token identifier carried by the output. 


### function GeniusUTXO

```cpp
inline GeniusUTXO(
    const base::Hash256 & hash,
    uint32_t previous_index,
    uint64_t amount,
    TokenID token_id,
    std::string owner_address
)
```

Constructs a fully specified UTXO. 

**Parameters**: 

  * **hash** Hash of the transaction that produced this output. 
  * **previous_index** Output index within the producing transaction. 
  * **amount** Amount carried by the output. 
  * **token_id** Token identifier carried by the output. 
  * **owner_address** Address that owns or can spend the output. 


### function SetOwnerAddress

```cpp
inline void SetOwnerAddress(
    std::string owner_address
)
```

Sets the owner address associated with this UTXO. 

**Parameters**: 

  * **owner_address** Address that owns or can spend the output. 


### function GetOwnerAddress

```cpp
inline const std::string & GetOwnerAddress() const
```

Returns the owner address associated with this UTXO. 

**Return**: Address that owns or can spend the output; empty when not set. 

### function GetOutPoint

```cpp
inline OutPoint GetOutPoint() const
```

Returns the full outpoint descriptor. 

**Return**: Outpoint containing the producing transaction hash and output index. 

### function GetTxID

```cpp
inline base::Hash256 GetTxID() const
```

Returns the originating transaction id. 

**Return**: Hash of the transaction that produced this output. 

### function GetOutputIdx

```cpp
inline uint32_t GetOutputIdx() const
```

Returns the output index within the originating transaction. 

**Return**: Output index within the producing transaction. 

### function GetAmount

```cpp
inline uint64_t GetAmount() const
```

Returns the unencrypted amount represented by the UTXO. 

**Return**: Amount carried by the output. 

### function GetTokenID

```cpp
inline TokenID GetTokenID() const
```

Returns the token identifier associated with the UTXO. 

**Return**: Token identifier carried by the output. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
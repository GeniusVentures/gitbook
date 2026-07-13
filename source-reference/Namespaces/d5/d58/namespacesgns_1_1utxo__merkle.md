---
title: sgns::utxo_merkle
summary: Utilities for building deterministic Merkle roots over ordered UTXO payloads. 

---

# sgns::utxo_merkle



Utilities for building deterministic Merkle roots over ordered UTXO payloads. 

## Functions

|                | Name           |
| -------------- | -------------- |
| void | **[AppendUInt32BE](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#function-appenduint32be)**(std::vector< uint8_t > & out, uint32_t value)<br/>Appends a 32-bit unsigned integer in big-endian order.  |
| void | **[AppendUInt64BE](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#function-appenduint64be)**(std::vector< uint8_t > & out, uint64_t value)<br/>Appends a 64-bit unsigned integer in big-endian order.  |
| uint32_t | **[ReadUInt32BE](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#function-readuint32be)**(const uint8_t * data)<br/>Reads a 32-bit unsigned integer from big-endian bytes.  |
| uint64_t | **[ReadUInt64BE](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#function-readuint64be)**(const uint8_t * data)<br/>Reads a 64-bit unsigned integer from big-endian bytes.  |
| std::string | **[OutPointKey](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#function-outpointkey)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & txid, uint32_t idx)<br/>Generates a canonical key for a UTXO outpoint, used for deterministic ordering in Merkle tree construction.  |
| std::vector< uint8_t > | **[SerializeUTXOLeafPayload](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#function-serializeutxoleafpayload)**(const [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) & utxo)<br/>Serializes a UTXO into the canonical leaf payload used for Merkle hashing.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[HashLeaf](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#function-hashleaf)**(const std::vector< uint8_t > & payload)<br/>Hashes a serialized UTXO leaf payload with the leaf domain separator.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[HashNode](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#function-hashnode)**(const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & left, const [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) & right)<br/>Hashes two child nodes with the internal-node domain separator.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[EmptyUTXOMerkleRoot](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#function-emptyutxomerkleroot)**()<br/>Returns the canonical root used for an empty UTXO set.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[ComputeMerkleRootFromLeafHashes](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#function-computemerklerootfromleafhashes)**(std::vector< [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) > level_hashes)<br/>Reduces a list of leaf hashes into a single Merkle root.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[ComputeMerkleRootFromPayloads](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#function-computemerklerootfrompayloads)**(std::vector< std::vector< uint8_t > > payloads)<br/>Sorts canonical payloads, hashes them as leaves, and computes the Merkle root.  |
| [base::Hash256](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-hash256) | **[ComputeMerkleRootFromUTXOs](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#function-computemerklerootfromutxos)**(const std::vector< [GeniusUTXO](/source-reference/Classes/da/da7/classsgns_1_1_genius_u_t_x_o/) > & utxos)<br/>Computes the Merkle root for a given set of UTXOs by serializing them into canonical payloads and hashing them.  |

## Attributes

|                | Name           |
| -------------- | -------------- |
| uint8_t | **[kLeafPrefix](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#variable-kleafprefix)** <br/>Domain separator prefix used for hashed leaf payloads.  |
| uint8_t | **[kNodePrefix](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/#variable-knodeprefix)** <br/>Domain separator prefix used for hashed internal nodes.  |


## Functions Documentation

### function AppendUInt32BE

```cpp
inline void AppendUInt32BE(
    std::vector< uint8_t > & out,
    uint32_t value
)
```

Appends a 32-bit unsigned integer in big-endian order. 

**Parameters**: 

  * **out** The vector to append to 
  * **value** the value to append 


### function AppendUInt64BE

```cpp
inline void AppendUInt64BE(
    std::vector< uint8_t > & out,
    uint64_t value
)
```

Appends a 64-bit unsigned integer in big-endian order. 

**Parameters**: 

  * **out** The vector to append to 
  * **value** the value to append 


### function ReadUInt32BE

```cpp
inline uint32_t ReadUInt32BE(
    const uint8_t * data
)
```

Reads a 32-bit unsigned integer from big-endian bytes. 

**Parameters**: 

  * **data** A pointer to the byte array 


**Return**: the 32 bit unsigned integer represented by the bytes 

### function ReadUInt64BE

```cpp
inline uint64_t ReadUInt64BE(
    const uint8_t * data
)
```

Reads a 64-bit unsigned integer from big-endian bytes. 

**Parameters**: 

  * **data** A pointer to the byte array 


**Return**: the 64 bit unsigned integer represented by the bytes 

### function OutPointKey

```cpp
inline std::string OutPointKey(
    const base::Hash256 & txid,
    uint32_t idx
)
```

Generates a canonical key for a UTXO outpoint, used for deterministic ordering in Merkle tree construction. 

**Parameters**: 

  * **txid** The transaction hash that created the UTXO 
  * **idx** The output index of the UTXO within the transaction 


**Return**: Canonical string key in the format "txid:idx" where txid is the readable hex representation of the transaction hash 

### function SerializeUTXOLeafPayload

```cpp
inline std::vector< uint8_t > SerializeUTXOLeafPayload(
    const GeniusUTXO & utxo
)
```

Serializes a UTXO into the canonical leaf payload used for Merkle hashing. 

**Parameters**: 

  * **utxo** The UTXO to serialize 


**Return**: The serialized leaf payload 

### function HashLeaf

```cpp
inline base::Hash256 HashLeaf(
    const std::vector< uint8_t > & payload
)
```

Hashes a serialized UTXO leaf payload with the leaf domain separator. 

**Parameters**: 

  * **payload** The payload to hash 


**Return**: The hash of the payload as a leaf node in the Merkle tree 

### function HashNode

```cpp
inline base::Hash256 HashNode(
    const base::Hash256 & left,
    const base::Hash256 & right
)
```

Hashes two child nodes with the internal-node domain separator. 

**Parameters**: 

  * **left** The hash of the left child node 
  * **right** The hash of the right child node 


**Return**: The hash of the parent node 

### function EmptyUTXOMerkleRoot

```cpp
inline base::Hash256 EmptyUTXOMerkleRoot()
```

Returns the canonical root used for an empty UTXO set. 

**Return**: The canonical root for an empty UTXO set 

### function ComputeMerkleRootFromLeafHashes

```cpp
inline base::Hash256 ComputeMerkleRootFromLeafHashes(
    std::vector< base::Hash256 > level_hashes
)
```

Reduces a list of leaf hashes into a single Merkle root. 

**Parameters**: 

  * **level_hashes** The list of leaf hashes 


**Return**: The computed Merkle root 

### function ComputeMerkleRootFromPayloads

```cpp
inline base::Hash256 ComputeMerkleRootFromPayloads(
    std::vector< std::vector< uint8_t > > payloads
)
```

Sorts canonical payloads, hashes them as leaves, and computes the Merkle root. 

**Parameters**: 

  * **payloads** The list of serialized UTXO payloads to include in the Merkle tree 


**Return**: The computed Merkle root of the payloads 

### function ComputeMerkleRootFromUTXOs

```cpp
inline base::Hash256 ComputeMerkleRootFromUTXOs(
    const std::vector< GeniusUTXO > & utxos
)
```

Computes the Merkle root for a given set of UTXOs by serializing them into canonical payloads and hashing them. 

**Parameters**: 

  * **utxos** The list of UTXOs to include in the Merkle tree 


**Return**: The computed Merkle root of the UTXOs 


## Attributes Documentation

### variable kLeafPrefix

```cpp
uint8_t kLeafPrefix = 0x00;
```

Domain separator prefix used for hashed leaf payloads. 

### variable kNodePrefix

```cpp
uint8_t kNodePrefix = 0x01;
```

Domain separator prefix used for hashed internal nodes. 




-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
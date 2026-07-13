---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/UTXOMerkle.hpp
summary: Helpers for deterministic serialization and Merkle hashing of UTXO snapshots. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/UTXOMerkle.hpp



Helpers for deterministic serialization and Merkle hashing of UTXO snapshots.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::utxo_merkle](/source-reference/Namespaces/d5/d58/namespacesgns_1_1utxo__merkle/)** <br/>Utilities for building deterministic Merkle roots over ordered UTXO payloads.  |

## Functions

|                | Name           |
| -------------- | -------------- |
| void | **[AppendUInt32BE](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#function-appenduint32be)**(std::vector< uint8_t > & out, uint32_t value)<br/>Appends a 32-bit unsigned integer in big-endian order.  |
| void | **[AppendUInt64BE](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#function-appenduint64be)**(std::vector< uint8_t > & out, uint64_t value)<br/>Appends a 64-bit unsigned integer in big-endian order.  |
| uint32_t | **[ReadUInt32BE](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#function-readuint32be)**(const uint8_t * data)<br/>Reads a 32-bit unsigned integer from big-endian bytes.  |
| uint64_t | **[ReadUInt64BE](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#function-readuint64be)**(const uint8_t * data)<br/>Reads a 64-bit unsigned integer from big-endian bytes.  |
| std::string | **[OutPointKey](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#function-outpointkey)**(const base::Hash256 & txid, uint32_t idx)<br/>Generates a canonical key for a UTXO outpoint, used for deterministic ordering in Merkle tree construction.  |
| std::vector< uint8_t > | **[SerializeUTXOLeafPayload](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#function-serializeutxoleafpayload)**(const GeniusUTXO & utxo)<br/>Serializes a UTXO into the canonical leaf payload used for Merkle hashing.  |
| base::Hash256 | **[HashLeaf](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#function-hashleaf)**(const std::vector< uint8_t > & payload)<br/>Hashes a serialized UTXO leaf payload with the leaf domain separator.  |
| base::Hash256 | **[HashNode](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#function-hashnode)**(const base::Hash256 & left, const base::Hash256 & right)<br/>Hashes two child nodes with the internal-node domain separator.  |
| base::Hash256 | **[EmptyUTXOMerkleRoot](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#function-emptyutxomerkleroot)**()<br/>Returns the canonical root used for an empty UTXO set.  |
| base::Hash256 | **[ComputeMerkleRootFromLeafHashes](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#function-computemerklerootfromleafhashes)**(std::vector< base::Hash256 > level_hashes)<br/>Reduces a list of leaf hashes into a single Merkle root.  |
| base::Hash256 | **[ComputeMerkleRootFromPayloads](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#function-computemerklerootfrompayloads)**(std::vector< std::vector< uint8_t > > payloads)<br/>Sorts canonical payloads, hashes them as leaves, and computes the Merkle root.  |
| base::Hash256 | **[ComputeMerkleRootFromUTXOs](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#function-computemerklerootfromutxos)**(const std::vector< GeniusUTXO > & utxos)<br/>Computes the Merkle root for a given set of UTXOs by serializing them into canonical payloads and hashing them.  |

## Attributes

|                | Name           |
| -------------- | -------------- |
| uint8_t | **[kLeafPrefix](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#variable-kleafprefix)** <br/>Domain separator prefix used for hashed leaf payloads.  |
| uint8_t | **[kNodePrefix](/source-reference/Files/d6/d16/_u_t_x_o_merkle_8hpp/#variable-knodeprefix)** <br/>Domain separator prefix used for hashed internal nodes.  |

## Detailed Description

Helpers for deterministic serialization and Merkle hashing of UTXO snapshots. 

**Date**: 2026-03-18 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 

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


## Source code

```cpp

#ifndef SGNS_UTXO_MERKLE_HPP
#define SGNS_UTXO_MERKLE_HPP

#include "account/GeniusUTXO.hpp"
#include "crypto/sha/sha256.hpp"

#include <algorithm>
#include <string>
#include <vector>

namespace sgns::utxo_merkle
{
    constexpr uint8_t kLeafPrefix = 0x00;
    constexpr uint8_t kNodePrefix = 0x01;

    inline void AppendUInt32BE( std::vector<uint8_t> &out, uint32_t value )
    {
        out.push_back( static_cast<uint8_t>( ( value >> 24 ) & 0xFF ) );
        out.push_back( static_cast<uint8_t>( ( value >> 16 ) & 0xFF ) );
        out.push_back( static_cast<uint8_t>( ( value >> 8 ) & 0xFF ) );
        out.push_back( static_cast<uint8_t>( value & 0xFF ) );
    }

    inline void AppendUInt64BE( std::vector<uint8_t> &out, uint64_t value )
    {
        out.push_back( static_cast<uint8_t>( ( value >> 56 ) & 0xFF ) );
        out.push_back( static_cast<uint8_t>( ( value >> 48 ) & 0xFF ) );
        out.push_back( static_cast<uint8_t>( ( value >> 40 ) & 0xFF ) );
        out.push_back( static_cast<uint8_t>( ( value >> 32 ) & 0xFF ) );
        out.push_back( static_cast<uint8_t>( ( value >> 24 ) & 0xFF ) );
        out.push_back( static_cast<uint8_t>( ( value >> 16 ) & 0xFF ) );
        out.push_back( static_cast<uint8_t>( ( value >> 8 ) & 0xFF ) );
        out.push_back( static_cast<uint8_t>( value & 0xFF ) );
    }

    inline uint32_t ReadUInt32BE( const uint8_t *data )
    {
        return ( static_cast<uint32_t>( data[0] ) << 24 ) | ( static_cast<uint32_t>( data[1] ) << 16 ) |
               ( static_cast<uint32_t>( data[2] ) << 8 ) | static_cast<uint32_t>( data[3] );
    }

    inline uint64_t ReadUInt64BE( const uint8_t *data )
    {
        return ( static_cast<uint64_t>( data[0] ) << 56 ) | ( static_cast<uint64_t>( data[1] ) << 48 ) |
               ( static_cast<uint64_t>( data[2] ) << 40 ) | ( static_cast<uint64_t>( data[3] ) << 32 ) |
               ( static_cast<uint64_t>( data[4] ) << 24 ) | ( static_cast<uint64_t>( data[5] ) << 16 ) |
               ( static_cast<uint64_t>( data[6] ) << 8 ) | static_cast<uint64_t>( data[7] );
    }

    inline std::string OutPointKey( const base::Hash256 &txid, uint32_t idx )
    {
        return txid.toReadableString() + ":" + std::to_string( idx );
    }

    inline std::vector<uint8_t> SerializeUTXOLeafPayload( const GeniusUTXO &utxo )
    {
        std::vector<uint8_t> payload;
        const auto          &owner_address = utxo.GetOwnerAddress();
        const auto           txid          = utxo.GetTxID();
        const auto           token_id      = utxo.GetTokenID();
        const auto          &token_bytes   = token_id.bytes();
        payload.reserve( 32 + 4 + 4 + owner_address.size() + token_bytes.size() + 8 );

        payload.insert( payload.end(), txid.begin(), txid.end() );
        AppendUInt32BE( payload, utxo.GetOutputIdx() );
        AppendUInt32BE( payload, static_cast<uint32_t>( owner_address.size() ) );
        payload.insert( payload.end(), owner_address.begin(), owner_address.end() );
        payload.insert( payload.end(), token_bytes.begin(), token_bytes.end() );
        AppendUInt64BE( payload, utxo.GetAmount() );
        return payload;
    }

    inline base::Hash256 HashLeaf( const std::vector<uint8_t> &payload )
    {
        std::vector<uint8_t> bytes;
        bytes.reserve( payload.size() + 1 );
        bytes.push_back( kLeafPrefix );
        bytes.insert( bytes.end(), payload.begin(), payload.end() );
        return crypto::sha256( gsl::span<const uint8_t>( bytes.data(), bytes.size() ) );
    }

    inline base::Hash256 HashNode( const base::Hash256 &left, const base::Hash256 &right )
    {
        std::vector<uint8_t> bytes;
        bytes.reserve( 1 + left.size() + right.size() );
        bytes.push_back( kNodePrefix );
        bytes.insert( bytes.end(), left.begin(), left.end() );
        bytes.insert( bytes.end(), right.begin(), right.end() );
        return crypto::sha256( gsl::span<const uint8_t>( bytes.data(), bytes.size() ) );
    }

    inline base::Hash256 EmptyUTXOMerkleRoot()
    {
        static const base::Hash256 empty_root = crypto::sha256( std::string_view( "UTXO_EMPTY_V1" ) );
        return empty_root;
    }

    inline base::Hash256 ComputeMerkleRootFromLeafHashes( std::vector<base::Hash256> level_hashes )
    {
        if ( level_hashes.empty() )
        {
            return EmptyUTXOMerkleRoot();
        }

        while ( level_hashes.size() > 1 )
        {
            if ( ( level_hashes.size() % 2 ) != 0 )
            {
                level_hashes.push_back( level_hashes.back() );
            }

            std::vector<base::Hash256> next_level;
            next_level.reserve( level_hashes.size() / 2 );
            for ( size_t i = 0; i < level_hashes.size(); i += 2 )
            {
                next_level.push_back( HashNode( level_hashes[i], level_hashes[i + 1] ) );
            }
            level_hashes = std::move( next_level );
        }

        return level_hashes.front();
    }

    inline base::Hash256 ComputeMerkleRootFromPayloads( std::vector<std::vector<uint8_t>> payloads )
    {
        if ( payloads.empty() )
        {
            return EmptyUTXOMerkleRoot();
        }

        std::sort( payloads.begin(), payloads.end() );

        std::vector<base::Hash256> leaf_hashes;
        leaf_hashes.reserve( payloads.size() );
        for ( const auto &payload : payloads )
        {
            leaf_hashes.push_back( HashLeaf( payload ) );
        }

        return ComputeMerkleRootFromLeafHashes( std::move( leaf_hashes ) );
    }

    inline base::Hash256 ComputeMerkleRootFromUTXOs( const std::vector<GeniusUTXO> &utxos )
    {
        if ( utxos.empty() )
        {
            return EmptyUTXOMerkleRoot();
        }
        std::vector<std::vector<uint8_t>> payloads;
        payloads.reserve( utxos.size() );
        for ( const auto &utxo : utxos )
        {
            payloads.push_back( SerializeUTXOLeafPayload( utxo ) );
        }
        return ComputeMerkleRootFromPayloads( std::move( payloads ) );
    }
}
#endif // SGNS_UTXO_MERKLE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

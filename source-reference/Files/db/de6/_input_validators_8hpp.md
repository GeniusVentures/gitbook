---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/InputValidators.hpp
summary: Input validation strategy interface for transaction inputs. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/InputValidators.hpp



Input validation strategy interface for transaction inputs.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::input_validator_constants](/source-reference/Namespaces/d1/dec/namespacesgns_1_1input__validator__constants/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::IInputValidator](/source-reference/Classes/de/d6f/classsgns_1_1_i_input_validator/)** <br/>Strategy interface for validating transaction inputs and their witness data.  |

## Attributes

|                | Name           |
| -------------- | -------------- |
| size_t | **[HASH256_BYTES](/source-reference/Files/db/de6/_input_validators_8hpp/#variable-hash256_bytes)**  |
| size_t | **[SERIALIZED_UINT32_BYTES](/source-reference/Files/db/de6/_input_validators_8hpp/#variable-serialized_uint32_bytes)**  |
| size_t | **[SERIALIZED_UINT64_BYTES](/source-reference/Files/db/de6/_input_validators_8hpp/#variable-serialized_uint64_bytes)**  |
| size_t | **[OUTPUT_INDEX_OFFSET](/source-reference/Files/db/de6/_input_validators_8hpp/#variable-output_index_offset)**  |
| size_t | **[OWNER_ADDRESS_LENGTH_OFFSET](/source-reference/Files/db/de6/_input_validators_8hpp/#variable-owner_address_length_offset)**  |
| size_t | **[OWNER_ADDRESS_OFFSET](/source-reference/Files/db/de6/_input_validators_8hpp/#variable-owner_address_offset)**  |
| size_t | **[TOKEN_ID_BYTES_IN_PAYLOAD](/source-reference/Files/db/de6/_input_validators_8hpp/#variable-token_id_bytes_in_payload)**  |
| size_t | **[AMOUNT_BYTES_IN_PAYLOAD](/source-reference/Files/db/de6/_input_validators_8hpp/#variable-amount_bytes_in_payload)**  |
| uint32_t | **[ESCROW_LOCK_OUTPUT_INDEX](/source-reference/Files/db/de6/_input_validators_8hpp/#variable-escrow_lock_output_index)**  |
| std::string_view | **[TRANSFER_TX_TYPE](/source-reference/Files/db/de6/_input_validators_8hpp/#variable-transfer_tx_type)**  |

## Detailed Description

Input validation strategy interface for transaction inputs. 

**Date**: 2026-03-23 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 


## Attributes Documentation

### variable HASH256_BYTES

```cpp
size_t HASH256_BYTES = base::Hash256::size();
```


### variable SERIALIZED_UINT32_BYTES

```cpp
size_t SERIALIZED_UINT32_BYTES = sizeof( uint32_t );
```


### variable SERIALIZED_UINT64_BYTES

```cpp
size_t SERIALIZED_UINT64_BYTES = sizeof( uint64_t );
```


### variable OUTPUT_INDEX_OFFSET

```cpp
size_t OUTPUT_INDEX_OFFSET = HASH256_BYTES;
```


### variable OWNER_ADDRESS_LENGTH_OFFSET

```cpp
size_t OWNER_ADDRESS_LENGTH_OFFSET = OUTPUT_INDEX_OFFSET + SERIALIZED_UINT32_BYTES;
```


### variable OWNER_ADDRESS_OFFSET

```cpp
size_t OWNER_ADDRESS_OFFSET = OWNER_ADDRESS_LENGTH_OFFSET + SERIALIZED_UINT32_BYTES;
```


### variable TOKEN_ID_BYTES_IN_PAYLOAD

```cpp
size_t TOKEN_ID_BYTES_IN_PAYLOAD = HASH256_BYTES;
```


### variable AMOUNT_BYTES_IN_PAYLOAD

```cpp
size_t AMOUNT_BYTES_IN_PAYLOAD = SERIALIZED_UINT64_BYTES;
```


### variable ESCROW_LOCK_OUTPUT_INDEX

```cpp
uint32_t ESCROW_LOCK_OUTPUT_INDEX = 0;
```


### variable TRANSFER_TX_TYPE

```cpp
std::string_view TRANSFER_TX_TYPE = "transfer";
```



## Source code

```cpp

#ifndef SGNS_INPUT_VALIDATORS_HPP
#define SGNS_INPUT_VALIDATORS_HPP

#include <cstddef>
#include <cstdint>
#include <memory>
#include <string>
#include <string_view>
#include <unordered_map>
#include <vector>

#include "account/UTXOStructs.hpp"
#include "base/blob.hpp"

namespace sgns
{
    namespace input_validator_constants
    {
        constexpr size_t HASH256_BYTES               = base::Hash256::size();
        constexpr size_t SERIALIZED_UINT32_BYTES     = sizeof( uint32_t );
        constexpr size_t SERIALIZED_UINT64_BYTES     = sizeof( uint64_t );
        constexpr size_t OUTPUT_INDEX_OFFSET         = HASH256_BYTES;
        constexpr size_t OWNER_ADDRESS_LENGTH_OFFSET = OUTPUT_INDEX_OFFSET + SERIALIZED_UINT32_BYTES;
        constexpr size_t OWNER_ADDRESS_OFFSET        = OWNER_ADDRESS_LENGTH_OFFSET + SERIALIZED_UINT32_BYTES;
        constexpr size_t TOKEN_ID_BYTES_IN_PAYLOAD   = HASH256_BYTES;
        constexpr size_t AMOUNT_BYTES_IN_PAYLOAD     = SERIALIZED_UINT64_BYTES;

        constexpr uint32_t         ESCROW_LOCK_OUTPUT_INDEX = 0;
        constexpr std::string_view TRANSFER_TX_TYPE         = "transfer";
    } // namespace input_validator_constants

    class Blockchain;
    class ConsensusSubject;
    class GeniusTransaction;
    class UTXOManager;

    class IInputValidator
    {
    public:
        virtual ~IInputValidator() = default;

        virtual bool ValidateUTXOParameters( const UTXOTxParameters &params,
                                             const std::string      &address,
                                             const UTXOManager      &utxo_manager ) const = 0;

        virtual bool ValidateWitness( const ConsensusSubject                     &subject,
                                      const std::shared_ptr<GeniusTransaction> &tx,
                                      const UTXOTxParameters                     &params,
                                      const std::shared_ptr<Blockchain>          &blockchain ) const = 0;

        virtual bool RequiresConsensusUTXOData() const = 0;

        using ValidatorPtr = const IInputValidator *;

        static void Register( const std::string &chain_id, ValidatorPtr validator )
        {
            registry()[chain_id] = validator;
        }

        static void UnregisterIf( const std::string &chain_id, ValidatorPtr expected )
        {
            auto it = registry().find( chain_id );
            if ( it != registry().end() && it->second == expected )
            {
                registry().erase( it );
            }
        }

        static ValidatorPtr Get( const std::string &chain_id )
        {
            auto it = registry().find( chain_id );
            return it != registry().end() ? it->second : nullptr;
        }

    private:
        static std::unordered_map<std::string, ValidatorPtr> &registry()
        {
            static std::unordered_map<std::string, ValidatorPtr> map;
            return map;
        }
    };
} // namespace sgns

#endif // SGNS_INPUT_VALIDATORS_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: sgns::input_validator_constants

---

# sgns::input_validator_constants





## Attributes

|                | Name           |
| -------------- | -------------- |
| size_t | **[HASH256_BYTES](/source-reference/Namespaces/d1/dec/namespacesgns_1_1input__validator__constants/#variable-hash256_bytes)**  |
| size_t | **[SERIALIZED_UINT32_BYTES](/source-reference/Namespaces/d1/dec/namespacesgns_1_1input__validator__constants/#variable-serialized_uint32_bytes)**  |
| size_t | **[SERIALIZED_UINT64_BYTES](/source-reference/Namespaces/d1/dec/namespacesgns_1_1input__validator__constants/#variable-serialized_uint64_bytes)**  |
| size_t | **[OUTPUT_INDEX_OFFSET](/source-reference/Namespaces/d1/dec/namespacesgns_1_1input__validator__constants/#variable-output_index_offset)**  |
| size_t | **[OWNER_ADDRESS_LENGTH_OFFSET](/source-reference/Namespaces/d1/dec/namespacesgns_1_1input__validator__constants/#variable-owner_address_length_offset)**  |
| size_t | **[OWNER_ADDRESS_OFFSET](/source-reference/Namespaces/d1/dec/namespacesgns_1_1input__validator__constants/#variable-owner_address_offset)**  |
| size_t | **[TOKEN_ID_BYTES_IN_PAYLOAD](/source-reference/Namespaces/d1/dec/namespacesgns_1_1input__validator__constants/#variable-token_id_bytes_in_payload)**  |
| size_t | **[AMOUNT_BYTES_IN_PAYLOAD](/source-reference/Namespaces/d1/dec/namespacesgns_1_1input__validator__constants/#variable-amount_bytes_in_payload)**  |
| uint32_t | **[ESCROW_LOCK_OUTPUT_INDEX](/source-reference/Namespaces/d1/dec/namespacesgns_1_1input__validator__constants/#variable-escrow_lock_output_index)**  |
| std::string_view | **[TRANSFER_TX_TYPE](/source-reference/Namespaces/d1/dec/namespacesgns_1_1input__validator__constants/#variable-transfer_tx_type)**  |



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





-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/keccak/keccak.h

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crypto/keccak/keccak.h





## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sha3_context_](/source-reference/Classes/d0/d9a/structsha3__context__/)**  |
| union | **[sha3_context_.__unnamed0__](/source-reference/Classes/d4/d0b/unionsha3__context___8____unnamed0____/)**  |

## Types

|                | Name           |
| -------------- | -------------- |
| enum| **[SHA3_FLAGS](/source-reference/Files/d6/dd8/keccak_8h/#enum-sha3_flags)** { SHA3_FLAGS_NONE = 0, SHA3_FLAGS_KECCAK = 1} |
| enum| **[SHA3_RETURN](/source-reference/Files/d6/dd8/keccak_8h/#enum-sha3_return)** { SHA3_RETURN_OK = 0, SHA3_RETURN_BAD_PARAMS = 1} |
| typedef struct [sha3_context_](/source-reference/Classes/d0/d9a/structsha3__context__/) | **[sha3_context](/source-reference/Files/d6/dd8/keccak_8h/#typedef-sha3_context)**  |
| typedef enum [SHA3_RETURN](/source-reference/Files/d6/dd8/keccak_8h/#enum-sha3_return) | **[sha3_return_t](/source-reference/Files/d6/dd8/keccak_8h/#typedef-sha3_return_t)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| [sha3_return_t](/source-reference/Files/d6/dd8/keccak_8h/#typedef-sha3_return_t) | **[sha3_Init](/source-reference/Files/d6/dd8/keccak_8h/#function-sha3_init)**(void * priv, unsigned bitSize) |
| void | **[sha3_Init256](/source-reference/Files/d6/dd8/keccak_8h/#function-sha3_init256)**(void * priv) |
| void | **[sha3_Init384](/source-reference/Files/d6/dd8/keccak_8h/#function-sha3_init384)**(void * priv) |
| void | **[sha3_Init512](/source-reference/Files/d6/dd8/keccak_8h/#function-sha3_init512)**(void * priv) |
| enum [SHA3_FLAGS](/source-reference/Files/d6/dd8/keccak_8h/#enum-sha3_flags) | **[sha3_SetFlags](/source-reference/Files/d6/dd8/keccak_8h/#function-sha3_setflags)**(void * priv, enum SHA3_FLAGS) |
| void | **[sgns_sha3_Update](/source-reference/Files/d6/dd8/keccak_8h/#function-sgns_sha3_update)**(void * priv, void const * bufIn, size_t len) |
| void const * | **[sha3_Finalize](/source-reference/Files/d6/dd8/keccak_8h/#function-sha3_finalize)**(void * priv) |
| [sha3_return_t](/source-reference/Files/d6/dd8/keccak_8h/#typedef-sha3_return_t) | **[sha3_HashBuffer](/source-reference/Files/d6/dd8/keccak_8h/#function-sha3_hashbuffer)**(unsigned bitSize, enum [SHA3_FLAGS](/source-reference/Files/d6/dd8/keccak_8h/#enum-sha3_flags) flags, const void * in, unsigned inBytes, void * out, unsigned outBytes) |

## Defines

|                | Name           |
| -------------- | -------------- |
|  | **[SHA3_KECCAK_SPONGE_WORDS](/source-reference/Files/d6/dd8/keccak_8h/#define-sha3_keccak_sponge_words)**  |

## Types Documentation

### enum SHA3_FLAGS

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| SHA3_FLAGS_NONE | 0|   |
| SHA3_FLAGS_KECCAK | 1|   |




### enum SHA3_RETURN

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| SHA3_RETURN_OK | 0|   |
| SHA3_RETURN_BAD_PARAMS | 1|   |




### typedef sha3_context

```cpp
typedef struct sha3_context_ sha3_context;
```


### typedef sha3_return_t

```cpp
typedef enum SHA3_RETURN sha3_return_t;
```



## Functions Documentation

### function sha3_Init

```cpp
sha3_return_t sha3_Init(
    void * priv,
    unsigned bitSize
)
```


### function sha3_Init256

```cpp
void sha3_Init256(
    void * priv
)
```


### function sha3_Init384

```cpp
void sha3_Init384(
    void * priv
)
```


### function sha3_Init512

```cpp
void sha3_Init512(
    void * priv
)
```


### function sha3_SetFlags

```cpp
enum SHA3_FLAGS sha3_SetFlags(
    void * priv,
    enum SHA3_FLAGS
)
```


### function sgns_sha3_Update

```cpp
void sgns_sha3_Update(
    void * priv,
    void const * bufIn,
    size_t len
)
```


### function sha3_Finalize

```cpp
void const * sha3_Finalize(
    void * priv
)
```


### function sha3_HashBuffer

```cpp
sha3_return_t sha3_HashBuffer(
    unsigned bitSize,
    enum SHA3_FLAGS flags,
    const void * in,
    unsigned inBytes,
    void * out,
    unsigned outBytes
)
```




## Macros Documentation

### define SHA3_KECCAK_SPONGE_WORDS

```cpp
#define SHA3_KECCAK_SPONGE_WORDS (((1600) / 8 /*bits to byte*/) / sizeof(uint64_t))
```


## Source code

```cpp


#ifndef SRC_KECCAK_H
#define SRC_KECCAK_H

#if defined(__cplusplus)
extern "C" {
#endif

/* 'Words' here refers to uint64_t */
#define SHA3_KECCAK_SPONGE_WORDS \
  (((1600) / 8 /*bits to byte*/) / sizeof(uint64_t))
typedef struct sha3_context_ {
  uint64_t saved; /* the portion of the input message that we
                   * didn't consume yet */
  union {         /* Keccak's state */
    uint64_t s[SHA3_KECCAK_SPONGE_WORDS];
    uint8_t sb[SHA3_KECCAK_SPONGE_WORDS * 8];
  };
  unsigned byteIndex;     /* 0..7--the next byte after the set one
                           * (starts from 0; 0--none are buffered) */
  unsigned wordIndex;     /* 0..24--the next word to integrate input
                           * (starts from 0) */
  unsigned capacityWords; /* the double size of the hash output in
                           * words (e.g. 16 for Keccak 512) */
} sha3_context;

enum SHA3_FLAGS { SHA3_FLAGS_NONE = 0, SHA3_FLAGS_KECCAK = 1 };

enum SHA3_RETURN { SHA3_RETURN_OK = 0, SHA3_RETURN_BAD_PARAMS = 1 };
typedef enum SHA3_RETURN sha3_return_t;

/* For Init or Reset call these: */
sha3_return_t sha3_Init(void *priv, unsigned bitSize);

void sha3_Init256(void *priv);
void sha3_Init384(void *priv);
void sha3_Init512(void *priv);

enum SHA3_FLAGS sha3_SetFlags(void *priv, enum SHA3_FLAGS);

void sgns_sha3_Update(void *priv, void const *bufIn, size_t len);

void const *sha3_Finalize(void *priv);

/* Single-call hashing */
sha3_return_t sha3_HashBuffer(
    unsigned bitSize,      /* 256, 384, 512 */
    enum SHA3_FLAGS flags, /* SHA3_FLAGS_NONE or SHA3_FLAGS_KECCAK */
    const void *in,
    unsigned inBytes,
    void *out,
    unsigned outBytes); /* up to bitSize/8; truncation OK */

#if defined(__cplusplus)
}
#endif

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

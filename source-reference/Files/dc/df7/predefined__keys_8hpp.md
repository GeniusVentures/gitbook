---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/predefined_keys.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/storage/predefined_keys.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| const std::string & | **[GetAuthoritySetKey](/source-reference/Files/dc/df7/predefined__keys_8hpp/#function-getauthoritysetkey)**() |
| const std::string & | **[GetSetStateKey](/source-reference/Files/dc/df7/predefined__keys_8hpp/#function-getsetstatekey)**() |
| const std::string & | **[GetGenesisBlockHashLookupKey](/source-reference/Files/dc/df7/predefined__keys_8hpp/#function-getgenesisblockhashlookupkey)**() |
| const std::string & | **[GetLastFinalizedBlockHashLookupKey](/source-reference/Files/dc/df7/predefined__keys_8hpp/#function-getlastfinalizedblockhashlookupkey)**() |


## Functions Documentation

### function GetAuthoritySetKey

```cpp
const std::string & GetAuthoritySetKey()
```


### function GetSetStateKey

```cpp
const std::string & GetSetStateKey()
```


### function GetGenesisBlockHashLookupKey

```cpp
const std::string & GetGenesisBlockHashLookupKey()
```


### function GetLastFinalizedBlockHashLookupKey

```cpp
const std::string & GetLastFinalizedBlockHashLookupKey()
```




## Source code

```cpp
#ifndef SUPERGENIUS_SRC_STORAGE_PREDEFINED_KEYS_HPP
#define SUPERGENIUS_SRC_STORAGE_PREDEFINED_KEYS_HPP

#include <string>

namespace sgns::storage
{
    const std::string &GetAuthoritySetKey()
    {
        static const std::string kAuthoritySetKey = "finality_voters";
        return kAuthoritySetKey;
    }

    const std::string &GetSetStateKey()
    {
        static const std::string kSetStateKey = "finality_completed_round";
        return kSetStateKey;
    }

    const std::string &GetGenesisBlockHashLookupKey()
    {
        static const std::string kGenesisBlockHashLookupKey = ":sgns:genesis_block_hash";
        return kGenesisBlockHashLookupKey;
    }

    const std::string &GetLastFinalizedBlockHashLookupKey()
    {
        static const std::string kLastFinalizedBlockHashLookupKey = ":sgns:last_finalized_block_hash";
        return kLastFinalizedBlockHashLookupKey;
    }

} // namespace sgns::storage

#endif // SUPERGENIUS_SRC_STORAGE_PREDEFINED_KEYS_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

---
title: sgns::MemorySecureStorage
summary: In-memory JSON backend for tests. Stores data in a map — no OS keychain access, no password prompts, no cleanup needed. 

---

# sgns::MemorySecureStorage



In-memory JSON backend for tests. Stores data in a map — no OS keychain access, no password prompts, no cleanup needed. 


`#include <MemorySecureStorage.hpp>`

Inherits from [sgns::JSONBackend](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/), [sgns::ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/), [IComponent](/source-reference/Classes/d1/dbf/class_i_component/), std::enable_shared_from_this< ISecureStorage >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[MemorySecureStorage](/source-reference/Classes/d0/d0d/classsgns_1_1_memory_secure_storage/#function-memorysecurestorage)**(std::string identifier) |
| virtual std::string | **[GetName](/source-reference/Classes/d0/d0d/classsgns_1_1_memory_secure_storage/#function-getname)**() override |
| virtual outcome::result< rapidjson::Document > | **[LoadJSON](/source-reference/Classes/d0/d0d/classsgns_1_1_memory_secure_storage/#function-loadjson)**() const override |
| virtual outcome::result< void > | **[SaveJSON](/source-reference/Classes/d0/d0d/classsgns_1_1_memory_secure_storage/#function-savejson)**(rapidjson::Document document) override |

## Additional inherited members

**Public Functions inherited from [sgns::JSONBackend](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/)**

|                | Name           |
| -------------- | -------------- |
| | **[JSONBackend](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-jsonbackend)**() =default |
| | **[~JSONBackend](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-~jsonbackend)**() override =default |
| virtual outcome::result< [SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype) > | **[Load](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-load)**(const std::string & key) override |
| virtual outcome::result< void > | **[Save](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-save)**(const std::string & key, const [SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype) & buffer) override |
| virtual outcome::result< bool > | **[DeleteKey](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-deletekey)**(const std::string & key) override |

**Public Types inherited from [sgns::ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/)**

|                | Name           |
| -------------- | -------------- |
| using std::string | **[SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype)**  |

**Public Functions inherited from [sgns::ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/)**

|                | Name           |
| -------------- | -------------- |
| | **[~ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#function-~isecurestorage)**() override =default |
| virtual outcome::result< [SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype) > | **[Load](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#function-load)**(const std::string & key) =0 |
| virtual outcome::result< void > | **[Save](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#function-save)**(const std::string & key, const [SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype) & buffer) =0 |
| virtual outcome::result< bool > | **[DeleteKey](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#function-deletekey)**(const std::string & key) =0 |

**Public Functions inherited from [IComponent](/source-reference/Classes/d1/dbf/class_i_component/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IComponent](/source-reference/Classes/d1/dbf/class_i_component/#function-~icomponent)**() =default |


## Public Functions Documentation

### function MemorySecureStorage

```cpp
inline explicit MemorySecureStorage(
    std::string identifier
)
```


### function GetName

```cpp
inline virtual std::string GetName() override
```


**Reimplements**: [sgns::JSONBackend::GetName](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-getname)


### function LoadJSON

```cpp
inline virtual outcome::result< rapidjson::Document > LoadJSON() const override
```


**Reimplements**: [sgns::JSONBackend::LoadJSON](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-loadjson)


### function SaveJSON

```cpp
inline virtual outcome::result< void > SaveJSON(
    rapidjson::Document document
) override
```


**Reimplements**: [sgns::JSONBackend::SaveJSON](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-savejson)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
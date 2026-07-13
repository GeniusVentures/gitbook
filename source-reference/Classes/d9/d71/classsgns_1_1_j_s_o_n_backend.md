---
title: sgns::JSONBackend

---

# sgns::JSONBackend






`#include <JSONBackend.hpp>`

Inherits from [sgns::ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/), [IComponent](/source-reference/Classes/d1/dbf/class_i_component/), std::enable_shared_from_this< ISecureStorage >

Inherited by [sgns::AndroidSecureStorage](/source-reference/Classes/d5/d83/classsgns_1_1_android_secure_storage/), [sgns::AppleSecureStorage](/source-reference/Classes/d9/d1f/classsgns_1_1_apple_secure_storage/), [sgns::LinuxSecureStorage](/source-reference/Classes/dd/de8/classsgns_1_1_linux_secure_storage/), [sgns::MemorySecureStorage](/source-reference/Classes/d0/d0d/classsgns_1_1_memory_secure_storage/), [sgns::WindowsSecureStorage](/source-reference/Classes/db/d24/classsgns_1_1_windows_secure_storage/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[JSONBackend](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-jsonbackend)**() =default |
| | **[~JSONBackend](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-~jsonbackend)**() override =default |
| virtual std::string | **[GetName](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-getname)**() override |
| virtual outcome::result< [SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype) > | **[Load](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-load)**(const std::string & key) override |
| virtual outcome::result< void > | **[Save](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-save)**(const std::string & key, const [SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype) & buffer) override |
| virtual outcome::result< bool > | **[DeleteKey](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-deletekey)**(const std::string & key) override |
| virtual outcome::result< rapidjson::Document > | **[LoadJSON](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-loadjson)**() const =0 |
| virtual outcome::result< void > | **[SaveJSON](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-savejson)**(rapidjson::Document document) =0 |

## Additional inherited members

**Public Types inherited from [sgns::ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/)**

|                | Name           |
| -------------- | -------------- |
| using std::string | **[SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype)**  |

**Public Functions inherited from [sgns::ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/)**

|                | Name           |
| -------------- | -------------- |
| | **[~ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#function-~isecurestorage)**() override =default |

**Public Functions inherited from [IComponent](/source-reference/Classes/d1/dbf/class_i_component/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IComponent](/source-reference/Classes/d1/dbf/class_i_component/#function-~icomponent)**() =default |


## Public Functions Documentation

### function JSONBackend

```cpp
JSONBackend() =default
```


### function ~JSONBackend

```cpp
~JSONBackend() override =default
```


### function GetName

```cpp
inline virtual std::string GetName() override
```


**Reimplements**: [IComponent::GetName](/source-reference/Classes/d1/dbf/class_i_component/#function-getname)


**Reimplemented by**: [sgns::LinuxSecureStorage::GetName](/source-reference/Classes/dd/de8/classsgns_1_1_linux_secure_storage/#function-getname), [sgns::MemorySecureStorage::GetName](/source-reference/Classes/d0/d0d/classsgns_1_1_memory_secure_storage/#function-getname), [sgns::WindowsSecureStorage::GetName](/source-reference/Classes/db/d24/classsgns_1_1_windows_secure_storage/#function-getname)


### function Load

```cpp
virtual outcome::result< SecureBufferType > Load(
    const std::string & key
) override
```


**Reimplements**: [sgns::ISecureStorage::Load](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#function-load)


### function Save

```cpp
virtual outcome::result< void > Save(
    const std::string & key,
    const SecureBufferType & buffer
) override
```


**Reimplements**: [sgns::ISecureStorage::Save](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#function-save)


### function DeleteKey

```cpp
virtual outcome::result< bool > DeleteKey(
    const std::string & key
) override
```


**Reimplements**: [sgns::ISecureStorage::DeleteKey](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#function-deletekey)


### function LoadJSON

```cpp
virtual outcome::result< rapidjson::Document > LoadJSON() const =0
```


**Reimplemented by**: [sgns::AndroidSecureStorage::LoadJSON](/source-reference/Classes/d5/d83/classsgns_1_1_android_secure_storage/#function-loadjson), [sgns::AppleSecureStorage::LoadJSON](/source-reference/Classes/d9/d1f/classsgns_1_1_apple_secure_storage/#function-loadjson), [sgns::LinuxSecureStorage::LoadJSON](/source-reference/Classes/dd/de8/classsgns_1_1_linux_secure_storage/#function-loadjson), [sgns::MemorySecureStorage::LoadJSON](/source-reference/Classes/d0/d0d/classsgns_1_1_memory_secure_storage/#function-loadjson), [sgns::WindowsSecureStorage::LoadJSON](/source-reference/Classes/db/d24/classsgns_1_1_windows_secure_storage/#function-loadjson)


### function SaveJSON

```cpp
virtual outcome::result< void > SaveJSON(
    rapidjson::Document document
) =0
```


**Reimplemented by**: [sgns::AndroidSecureStorage::SaveJSON](/source-reference/Classes/d5/d83/classsgns_1_1_android_secure_storage/#function-savejson), [sgns::AppleSecureStorage::SaveJSON](/source-reference/Classes/d9/d1f/classsgns_1_1_apple_secure_storage/#function-savejson), [sgns::LinuxSecureStorage::SaveJSON](/source-reference/Classes/dd/de8/classsgns_1_1_linux_secure_storage/#function-savejson), [sgns::MemorySecureStorage::SaveJSON](/source-reference/Classes/d0/d0d/classsgns_1_1_memory_secure_storage/#function-savejson), [sgns::WindowsSecureStorage::SaveJSON](/source-reference/Classes/db/d24/classsgns_1_1_windows_secure_storage/#function-savejson)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
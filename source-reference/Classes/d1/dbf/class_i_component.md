---
title: IComponent

---

# IComponent






`#include <IComponent.hpp>`

Inherited by [sgns::storage::face::GenericStorage< Buffer, Buffer >](/source-reference/Classes/da/d5d/structsgns_1_1storage_1_1face_1_1_generic_storage/), [sgns::GeniusNode](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/), [sgns::ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/), [sgns::crypto::Hasher](/source-reference/Classes/dd/d14/classsgns_1_1crypto_1_1_hasher/), [sgns::storage::face::GenericStorage< K, V >](/source-reference/Classes/da/d5d/structsgns_1_1storage_1_1face_1_1_generic_storage/)

## Public Functions

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IComponent](/source-reference/Classes/d1/dbf/class_i_component/#function-~icomponent)**() =default |
| virtual std::string | **[GetName](/source-reference/Classes/d1/dbf/class_i_component/#function-getname)**() =0 |

## Public Functions Documentation

### function ~IComponent

```cpp
virtual ~IComponent() =default
```


### function GetName

```cpp
virtual std::string GetName() =0
```


**Reimplemented by**: [sgns::AndroidSecureStorage::GetName](/source-reference/Classes/d5/d83/classsgns_1_1_android_secure_storage/#function-getname), [sgns::AppleSecureStorage::GetName](/source-reference/Classes/d9/d1f/classsgns_1_1_apple_secure_storage/#function-getname), [sgns::crypto::HasherImpl::GetName](/source-reference/Classes/db/db8/classsgns_1_1crypto_1_1_hasher_impl/#function-getname), [sgns::GeniusNode::GetName](/source-reference/Classes/d1/d00/classsgns_1_1_genius_node/#function-getname), [sgns::JSONBackend::GetName](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-getname), [sgns::JSONSecureStorage::GetName](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-getname), [sgns::LinuxSecureStorage::GetName](/source-reference/Classes/dd/de8/classsgns_1_1_linux_secure_storage/#function-getname), [sgns::MemorySecureStorage::GetName](/source-reference/Classes/d0/d0d/classsgns_1_1_memory_secure_storage/#function-getname), [sgns::storage::rocksdb::GetName](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#function-getname), [sgns::WindowsSecureStorage::GetName](/source-reference/Classes/db/d24/classsgns_1_1_windows_secure_storage/#function-getname)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
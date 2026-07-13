---
title: sgns::AndroidSecureStorage

---

# sgns::AndroidSecureStorage






`#include <Android.hpp>`

Inherits from [sgns::JSONBackend](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/), [sgns::ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/), [IComponent](/source-reference/Classes/d1/dbf/class_i_component/), std::enable_shared_from_this< ISecureStorage >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[AndroidSecureStorage](/source-reference/Classes/d5/d83/classsgns_1_1_android_secure_storage/#function-androidsecurestorage)**(std::string identifier, JavaVM * jvm =nullptr) |
| | **[~AndroidSecureStorage](/source-reference/Classes/d5/d83/classsgns_1_1_android_secure_storage/#function-~androidsecurestorage)**() override |
| virtual std::string | **[GetName](/source-reference/Classes/d5/d83/classsgns_1_1_android_secure_storage/#function-getname)**() override |
| virtual outcome::result< rapidjson::Document > | **[LoadJSON](/source-reference/Classes/d5/d83/classsgns_1_1_android_secure_storage/#function-loadjson)**() const override |
| virtual outcome::result< void > | **[SaveJSON](/source-reference/Classes/d5/d83/classsgns_1_1_android_secure_storage/#function-savejson)**(rapidjson::Document document) override |

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

### function AndroidSecureStorage

```cpp
explicit AndroidSecureStorage(
    std::string identifier,
    JavaVM * jvm =nullptr
)
```


### function ~AndroidSecureStorage

```cpp
~AndroidSecureStorage() override
```


### function GetName

```cpp
inline virtual std::string GetName() override
```


**Reimplements**: [IComponent::GetName](/source-reference/Classes/d1/dbf/class_i_component/#function-getname)


### function LoadJSON

```cpp
virtual outcome::result< rapidjson::Document > LoadJSON() const override
```


**Reimplements**: [sgns::JSONBackend::LoadJSON](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-loadjson)


### function SaveJSON

```cpp
virtual outcome::result< void > SaveJSON(
    rapidjson::Document document
) override
```


**Reimplements**: [sgns::JSONBackend::SaveJSON](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-savejson)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
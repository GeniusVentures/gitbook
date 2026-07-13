---
title: sgns::JSONSecureStorage

---

# sgns::JSONSecureStorage






`#include <JSONSecureStorage.hpp>`

Inherits from [sgns::ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/), [IComponent](/source-reference/Classes/d1/dbf/class_i_component/), std::enable_shared_from_this< ISecureStorage >

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[JSONSecureStorage](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-jsonsecurestorage)**(boost::filesystem::path directory) |
| | **[~JSONSecureStorage](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-~jsonsecurestorage)**() override =default |
| virtual outcome::result< [SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype) > | **[Load](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-load)**(const std::string & key) override |
| virtual outcome::result< void > | **[Save](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-save)**(const std::string & key, const [SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype) & buffer) override |
| virtual outcome::result< bool > | **[DeleteKey](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-deletekey)**(const std::string & key) override |
| virtual std::string | **[GetName](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-getname)**() override |
| outcome::result< rj::Document > | **[LoadJSON](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-loadjson)**() const |
| [JSONSecureStorage](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-jsonsecurestorage) & | **[GetInstance](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-getinstance)**() |

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

### function JSONSecureStorage

```cpp
inline JSONSecureStorage(
    boost::filesystem::path directory
)
```


### function ~JSONSecureStorage

```cpp
~JSONSecureStorage() override =default
```


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


### function GetName

```cpp
inline virtual std::string GetName() override
```


**Reimplements**: [IComponent::GetName](/source-reference/Classes/d1/dbf/class_i_component/#function-getname)


### function LoadJSON

```cpp
outcome::result< rj::Document > LoadJSON() const
```


### function GetInstance

```cpp
static JSONSecureStorage & GetInstance()
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
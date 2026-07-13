---
title: sgns::ISecureStorage

---

# sgns::ISecureStorage






`#include <ISecureStorage.hpp>`

Inherits from [IComponent](/source-reference/Classes/d1/dbf/class_i_component/), std::enable_shared_from_this< ISecureStorage >

Inherited by [sgns::JSONBackend](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/), [sgns::JSONSecureStorage](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/)

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::string | **[SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[~ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#function-~isecurestorage)**() override =default |
| virtual outcome::result< [SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype) > | **[Load](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#function-load)**(const std::string & key) =0 |
| virtual outcome::result< void > | **[Save](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#function-save)**(const std::string & key, const [SecureBufferType](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#using-securebuffertype) & buffer) =0 |
| virtual outcome::result< bool > | **[DeleteKey](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/#function-deletekey)**(const std::string & key) =0 |

## Additional inherited members

**Public Functions inherited from [IComponent](/source-reference/Classes/d1/dbf/class_i_component/)**

|                | Name           |
| -------------- | -------------- |
| virtual | **[~IComponent](/source-reference/Classes/d1/dbf/class_i_component/#function-~icomponent)**() =default |
| virtual std::string | **[GetName](/source-reference/Classes/d1/dbf/class_i_component/#function-getname)**() =0 |


## Public Types Documentation

### using SecureBufferType

```cpp
using sgns::ISecureStorage::SecureBufferType = std::string;
```


## Public Functions Documentation

### function ~ISecureStorage

```cpp
~ISecureStorage() override =default
```


### function Load

```cpp
virtual outcome::result< SecureBufferType > Load(
    const std::string & key
) =0
```


**Reimplemented by**: [sgns::JSONBackend::Load](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-load), [sgns::JSONSecureStorage::Load](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-load)


### function Save

```cpp
virtual outcome::result< void > Save(
    const std::string & key,
    const SecureBufferType & buffer
) =0
```


**Reimplemented by**: [sgns::JSONBackend::Save](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-save), [sgns::JSONSecureStorage::Save](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-save)


### function DeleteKey

```cpp
virtual outcome::result< bool > DeleteKey(
    const std::string & key
) =0
```


**Reimplemented by**: [sgns::JSONBackend::DeleteKey](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/#function-deletekey), [sgns::JSONSecureStorage::DeleteKey](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/#function-deletekey)


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
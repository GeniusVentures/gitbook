---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/ISecureStorage.hpp
summary: Secure Storage Interface class. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/ISecureStorage.hpp



Secure Storage Interface class.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::ISecureStorage](/source-reference/Classes/d5/db7/classsgns_1_1_i_secure_storage/)**  |

## Detailed Description

Secure Storage Interface class. 

**Date**: 2024-06-05 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp


#ifndef _I_SECURE_STORAGE_HPP_
#define _I_SECURE_STORAGE_HPP_

#include <string>

#include "outcome/outcome.hpp"
#include "singleton/IComponent.hpp"

namespace sgns
{
    class ISecureStorage : public IComponent, public std::enable_shared_from_this<ISecureStorage>
    {
    public:
        ~ISecureStorage() override = default;

        using SecureBufferType = std::string;

        virtual outcome::result<SecureBufferType> Load( const std::string &key )                                 = 0;
        virtual outcome::result<void>             Save( const std::string &key, const SecureBufferType &buffer ) = 0;
        virtual outcome::result<bool>             DeleteKey( const std::string &key )                            = 0;
    };
}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

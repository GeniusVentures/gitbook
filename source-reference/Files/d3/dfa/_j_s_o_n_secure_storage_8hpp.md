---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/json/JSONSecureStorage.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/json/JSONSecureStorage.hpp



 [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::JSONSecureStorage](/source-reference/Classes/d4/dd2/classsgns_1_1_j_s_o_n_secure_storage/)**  |

## Detailed Description


**Date**: 2024-06-06 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp


#ifndef JSON_SECURE_STORAGE_HPP
#define JSON_SECURE_STORAGE_HPP

#include "../../ISecureStorage.hpp"

#include <rapidjson/document.h>
#include <boost/filesystem.hpp>

namespace sgns
{
    namespace rj = rapidjson;

    class JSONSecureStorage : public ISecureStorage
    {
    public:
        JSONSecureStorage( boost::filesystem::path directory ) : directory_( std::move( directory ) )
        {
        }

        ~JSONSecureStorage() override = default;

        outcome::result<SecureBufferType> Load( const std::string &key ) override;

        outcome::result<void> Save( const std::string &key, const SecureBufferType &buffer ) override;

        outcome::result<bool> DeleteKey( const std::string &key ) override;

        std::string GetName() override
        {
            return "LocalSecureStorage";
        }

        outcome::result<rj::Document> LoadJSON() const;

        static JSONSecureStorage &GetInstance();

    private:
        boost::filesystem::path directory_;
    };
}

#endif // JSON_SECURE_STORAGE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

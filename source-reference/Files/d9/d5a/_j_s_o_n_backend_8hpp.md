---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/JSONBackend.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/JSONBackend.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::JSONBackend](/source-reference/Classes/d9/d71/classsgns_1_1_j_s_o_n_backend/)**  |




## Source code

```cpp
#ifndef SGNS_JSON_BACKEND_HPP
#define SGNS_JSON_BACKEND_HPP
#include "../ISecureStorage.hpp"

#include <rapidjson/document.h>

namespace sgns
{
    class JSONBackend : public ISecureStorage
    {
    public:
        JSONBackend() = default;

        ~JSONBackend() override = default;

        std::string GetName() override
        {
            return "JSONBackend";
        }

        outcome::result<SecureBufferType> Load( const std::string &key ) override;

        outcome::result<void> Save( const std::string &key, const SecureBufferType &buffer ) override;

        outcome::result<bool> DeleteKey( const std::string &key ) override;

        virtual outcome::result<rapidjson::Document> LoadJSON() const = 0;

        virtual outcome::result<void> SaveJSON( rapidjson::Document document ) = 0;
    };
}

#endif // SGNS_JSON_BACKEND_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

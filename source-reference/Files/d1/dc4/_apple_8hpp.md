---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/Apple.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/Apple.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::AppleSecureStorage](/source-reference/Classes/d9/d1f/classsgns_1_1_apple_secure_storage/)**  |




## Source code

```cpp
#ifndef SGNS_APPLE_SECURE_STORAGE_HPP
#define SGNS_APPLE_SECURE_STORAGE_HPP

#include "JSONBackend.hpp"

namespace sgns
{
    class AppleSecureStorage : public JSONBackend
    {
    public:
        explicit AppleSecureStorage( std::string identifier );

        std::string GetName() override
        {
            return "AppleSecureStorage";
        }

        outcome::result<rapidjson::Document> LoadJSON() const override;

        outcome::result<void> SaveJSON( rapidjson::Document document ) override;

    private:
        std::string identifier_;
    };
}
#endif // SGNS_APPLE_SECURE_STORAGE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/Linux.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/Linux.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::LinuxSecureStorage](/source-reference/Classes/dd/de8/classsgns_1_1_linux_secure_storage/)**  |




## Source code

```cpp
#ifndef LINUX_SECURE_STORAGE_HPP
#define LINUX_SECURE_STORAGE_HPP

#include "JSONBackend.hpp"

#include <libsecret/secret.h>

namespace sgns
{
    class LinuxSecureStorage : public JSONBackend
    {
    public:
        explicit LinuxSecureStorage( std::string identifier );

        ~LinuxSecureStorage() override = default;

        std::string GetName() override
        {
            return "LinuxSecureStorage";
        }

        outcome::result<rapidjson::Document> LoadJSON() const override;

        outcome::result<void> SaveJSON( rapidjson::Document document ) override;

    private:
        std::string  identifier_;
        SecretSchema schema_;
    };
}

#endif // LINUX_SECURE_STORAGE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

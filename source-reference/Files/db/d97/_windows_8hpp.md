---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/Windows.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/Windows.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::WindowsSecureStorage](/source-reference/Classes/db/d24/classsgns_1_1_windows_secure_storage/)**  |




## Source code

```cpp
#ifndef WINDOWS_SECURE_STORAGE_HPP
#define WINDOWS_SECURE_STORAGE_HPP

#include "JSONBackend.hpp"

#include <rapidjson/document.h>

namespace sgns
{
    class WindowsSecureStorage : public JSONBackend
    {
    public:
        explicit WindowsSecureStorage( std::string identifier );

        std::string GetName() override
        {
            return "WindowsSecureStorage";
        }

        outcome::result<rapidjson::Document> LoadJSON() const override;

        outcome::result<void> SaveJSON( rapidjson::Document document ) override;

    private:
        std::string identifier_;
    };
}

#endif // WINDOWS_SECURE_STORAGE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

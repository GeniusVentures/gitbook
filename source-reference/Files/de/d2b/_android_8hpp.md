---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/Android.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/Android.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::AndroidSecureStorage](/source-reference/Classes/d5/d83/classsgns_1_1_android_secure_storage/)**  |




## Source code

```cpp
#ifndef SGNS_ANDROID_SECURE_STORAGE_HPP
#define SGNS_ANDROID_SECURE_STORAGE_HPP

#include "JSONBackend.hpp"

#include <jni.h>

namespace sgns
{
    class AndroidSecureStorage : public JSONBackend
    {
    public:
        explicit AndroidSecureStorage( std::string identifier, JavaVM *jvm = nullptr );

        ~AndroidSecureStorage() override;

        std::string GetName() override
        {
            return "AndroidSecureStorage";
        }

        outcome::result<rapidjson::Document> LoadJSON() const override;

        outcome::result<void> SaveJSON( rapidjson::Document document ) override;

    private:
        JNIEnv *GetJNIEnv() const;

        JavaVM *jvm_;
        jclass  key_store_helper_class_;

        jmethodID load_method_;
        jmethodID save_method_;
        jmethodID delete_method_;
    };
}

#endif // SGNS_ANDROID_SECURE_STORAGE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

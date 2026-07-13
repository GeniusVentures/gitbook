---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/MemorySecureStorage.hpp
summary: In-memory JSON backend for testing — no keychain access. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/local_secure_storage/impl/MemorySecureStorage.hpp



In-memory JSON backend for testing — no keychain access.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::MemorySecureStorage](/source-reference/Classes/d0/d0d/classsgns_1_1_memory_secure_storage/)** <br/>In-memory JSON backend for tests. Stores data in a map — no OS keychain access, no password prompts, no cleanup needed.  |

## Detailed Description

In-memory JSON backend for testing — no keychain access. 

**Date**: 2026-06-01 



## Source code

```cpp

#ifndef MEMORY_SECURE_STORAGE_HPP
#define MEMORY_SECURE_STORAGE_HPP

#include "JSONBackend.hpp"

#include <rapidjson/document.h>
#include <rapidjson/stringbuffer.h>
#include <rapidjson/writer.h>

#include <string>
#include <unordered_map>

namespace sgns
{
    class MemorySecureStorage : public JSONBackend
    {
    public:
        explicit MemorySecureStorage( std::string identifier ) : identifier_( std::move( identifier ) )
        {
        }

        std::string GetName() override
        {
            return "MemorySecureStorage";
        }

        outcome::result<rapidjson::Document> LoadJSON() const override
        {
            auto it = store_.find( identifier_ );
            if ( it == store_.end() )
            {
                return rapidjson::Document( rapidjson::Type::kObjectType );
            }

            rapidjson::Document d;
            d.Parse( it->second.c_str(), it->second.size() );
            if ( d.HasParseError() )
            {
                return outcome::failure( std::errc::bad_message );
            }
            return d;
        }

        outcome::result<void> SaveJSON( rapidjson::Document document ) override
        {
            rapidjson::StringBuffer buffer;
            rapidjson::Writer       writer( buffer );
            document.Accept( writer );
            store_[identifier_] = std::string( buffer.GetString(), buffer.GetLength() );
            return outcome::success();
        }

    private:
        std::string                                                identifier_;
        static inline std::unordered_map<std::string, std::string> store_;
    };
} // namespace sgns

#endif // MEMORY_SECURE_STORAGE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

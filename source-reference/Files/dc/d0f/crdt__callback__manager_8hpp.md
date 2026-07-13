---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/crdt_callback_manager.hpp
summary: CRDT callback manager header for when an element gets added/removed. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/crdt_callback_manager.hpp



CRDT callback manager header for when an element gets added/removed.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::CRDTCallbackManager](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/)**  |
| struct | **[sgns::crdt::CRDTCallbackManager::NewDataCallbackEntry](/source-reference/Classes/d3/d91/structsgns_1_1crdt_1_1_c_r_d_t_callback_manager_1_1_new_data_callback_entry/)**  |
| struct | **[sgns::crdt::CRDTCallbackManager::DeletedDataCallbackEntry](/source-reference/Classes/de/d54/structsgns_1_1crdt_1_1_c_r_d_t_callback_manager_1_1_deleted_data_callback_entry/)**  |

## Detailed Description

CRDT callback manager header for when an element gets added/removed. 

**Date**: 2025-09-05 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef SGNS_CRDT_CALLBACK_MANAGER_HPP
#define SGNS_CRDT_CALLBACK_MANAGER_HPP

#include <functional>
#include <memory>
#include <regex>
#include <string>
#include <shared_mutex>
#include <vector>

#include "base/buffer.hpp"
#include "base/logger.hpp"

namespace sgns::crdt
{
    class CRDTWorkJournal;

    class CRDTCallbackManager
    {
    public:
        using NewDataPair     = std::pair<std::string, base::Buffer>;
        using NewDataCallback = std::function<void( NewDataPair new_data, std::string cid )>;

        struct NewDataCallbackEntry
        {
            std::string     pattern;
            std::regex      regex;
            NewDataCallback callback;
        };

        using NewDataCallbackRegistry = std::vector<std::shared_ptr<const NewDataCallbackEntry>>;

        using DeletedDataCallback = std::function<void( std::string deleted_key, std::string cid )>;

        struct DeletedDataCallbackEntry
        {
            std::string         pattern;
            std::regex          regex;
            DeletedDataCallback callback;
        };

        using DeletedDataCallbackRegistry = std::vector<std::shared_ptr<const DeletedDataCallbackEntry>>;

        explicit CRDTCallbackManager( std::shared_ptr<CRDTWorkJournal> work_journal );
        ~CRDTCallbackManager();
        bool RegisterNewDataCallback( const std::string &pattern, NewDataCallback callback );
        bool RegisterDeletedDataCallback( const std::string &pattern, DeletedDataCallback callback );
        void UnregisterNewDataCallback( const std::string &pattern );
        void UnregisterDeletedDataCallback( const std::string &pattern );

        void PutDataCallback( const std::string &key, const base::Buffer &value, const std::string &cid );

        void DeleteDataCallback( const std::string &deleted_key, const std::string &cid );

    private:
        std::shared_ptr<CRDTWorkJournal> work_journal_;
        std::shared_mutex new_data_callback_registry_mutex_; 
        NewDataCallbackRegistry new_data_callback_registry_; 
        std::shared_mutex
            deleted_data_callback_registry_mutex_; 
        DeletedDataCallbackRegistry deleted_data_callback_registry_; 

        base::Logger logger_ = base::createLogger( "CRDTCallbackManager" ); 
    };

}

#endif // SGNS_CRDT_CALLBACK_MANAGER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

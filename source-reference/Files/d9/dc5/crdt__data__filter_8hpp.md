---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/crdt_data_filter.hpp
summary: Header file of the CRDT Filter class. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/crdt_data_filter.hpp



Header file of the CRDT Filter class.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::CRDTDataFilter](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/)**  |
| struct | **[sgns::crdt::CRDTDataFilter::FilterCallbackEntry](/source-reference/Classes/df/d7c/structsgns_1_1crdt_1_1_c_r_d_t_data_filter_1_1_filter_callback_entry/)**  |

## Detailed Description

Header file of the CRDT Filter class. 

**Date**: 2025-04-07 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp


#ifndef _CRDT_DATA_FILTER_HPP_
#define _CRDT_DATA_FILTER_HPP_

#include <functional>
#include <string>
#include <memory>
#include <regex>
#include <shared_mutex>
#include <vector>

#include "crdt/proto/delta.pb.h"

namespace sgns::crdt
{
    class CRDTWorkJournal;

    class CRDTDataFilter
    {
    public:
        using ElementFilterCallback = std::function<std::optional<std::vector<pb::Element>>( const pb::Element & )>;

        struct FilterCallbackEntry
        {
            std::string           pattern;
            std::regex            regex;
            ElementFilterCallback filter;
        };

        using FilterCallbackRegistry = std::vector<std::shared_ptr<const FilterCallbackEntry>>;

        explicit CRDTDataFilter( std::shared_ptr<CRDTWorkJournal> work_journal, bool accept_by_default = true );

        ~CRDTDataFilter() = default;

        bool RegisterElementFilter( const std::string &pattern, ElementFilterCallback filter );

        bool RegisterTombstoneFilter( const std::string &pattern, ElementFilterCallback filter );

        void UnregisterElementFilter( const std::string &pattern );

        void UnregisterTombstoneFilter( const std::string &pattern );

        void FilterElementsOnDelta( pb::Delta &delta ) const;

        void FilterTombstonesOnDelta( pb::Delta &delta );

    private:
        std::shared_ptr<CRDTWorkJournal> work_journal_;
        const bool                accept_by_default_;      
        mutable std::shared_mutex element_registry_mutex_; 
        std::shared_mutex         tombstone_registry_mutex_; 
        FilterCallbackRegistry    element_registry_;         
        FilterCallbackRegistry    tombstone_registry_;       
    };

}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

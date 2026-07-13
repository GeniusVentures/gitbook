---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/globaldb/crdt_work_journal.hpp
summary: Persistent work-journal for CRDT key processing state. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/globaldb/crdt_work_journal.hpp



Persistent work-journal for CRDT key processing state.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::storage](/source-reference/Namespaces/d0/dbf/namespacesgns_1_1storage/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::CRDTWorkJournal](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/)** <br/>Tracks key processing lifecycle persisted in RocksDB.  |
| struct | **[sgns::crdt::CRDTWorkJournal::Entry](/source-reference/Classes/d6/db5/structsgns_1_1crdt_1_1_c_r_d_t_work_journal_1_1_entry/)** <br/>Serialized work-journal entry for a key.  |

## Detailed Description

Persistent work-journal for CRDT key processing state. 

**Date**: 2026-04-21 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp


#ifndef SUPERGENIUS_CRDT_WORK_JOURNAL_HPP
#define SUPERGENIUS_CRDT_WORK_JOURNAL_HPP

#include <chrono>
#include <cstdint>
#include <memory>
#include <mutex>
#include <optional>
#include <string>
#include <string_view>
#include <vector>

namespace sgns::storage
{
    class rocksdb;
}

namespace sgns::crdt
{
    class CRDTWorkJournal
    {
    public:
        enum class State : uint8_t
        {
            Seen       = 0, 
            Processing = 1, 
            Stalled    = 2, 
        };

        struct Entry
        {
            std::string key;                          
            State       state          = State::Seen; 
            uint64_t    attempt_count  = 0;           
            uint64_t    updated_at_ms  = 0;           
            uint64_t    lease_until_ms = 0;           
        };

        static std::shared_ptr<CRDTWorkJournal> New( std::shared_ptr<storage::rocksdb> datastore );

        void MarkSeen( const std::string &key );

        void MarkProcessing( const std::string &key, std::chrono::milliseconds lease = std::chrono::minutes( 3 ) );

        void MarkStalled( const std::string &key, std::chrono::milliseconds lease = std::chrono::minutes( 3 ) );

        bool MarkDone( const std::string &key );

        std::optional<Entry> GetEntry( const std::string &key ) const;

        std::vector<Entry> ListUnfinished( std::string_view key_pattern = {} ) const;

        size_t RecoverStaleProcessing( std::string_view          key_pattern,
                                       std::chrono::milliseconds stale = std::chrono::milliseconds( 0 ) );

    private:
        static constexpr std::string_view NAMESPACE_PREFIX = "/crdt/work/"; 

        explicit CRDTWorkJournal( std::shared_ptr<storage::rocksdb> datastore );

        static uint64_t NowMs();

        std::string BuildStorageKey( const std::string &key ) const;

        static std::optional<Entry> DeserializeEntry( std::string_view storage_key, std::string_view value );

        static std::string SerializeEntry( const Entry &entry );

        static std::vector<std::string> Split( const std::string &value, char separator );

        std::optional<Entry> GetEntryUnlocked( const std::string &key ) const;

        bool PutEntryUnlocked( const Entry &entry ) const;

        std::shared_ptr<storage::rocksdb> datastore_; 
        mutable std::mutex                mutex_;     
    };
}

#endif // SUPERGENIUS_CRDT_WORK_JOURNAL_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

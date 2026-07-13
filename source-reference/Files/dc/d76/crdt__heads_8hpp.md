---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/crdt_heads.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/crdt_heads.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::CrdtHeads](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/)** <br/>[CrdtHeads](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/) manages the current Merkle-CRDT heads.  |




## Source code

```cpp
#ifndef SUPERGENIUS_CRDT_HEADS_HPP
#define SUPERGENIUS_CRDT_HEADS_HPP

#include <shared_mutex>
#include <map>
#include <set>
#include <unordered_set>

#include <storage/rocksdb/rocksdb.hpp>
#include "base/logger.hpp"
#include "hierarchical_key.hpp"

#include <primitives/cid/cid.hpp>

namespace sgns::crdt
{
    class CrdtHeads
    {
    public:
        using DataStore      = storage::rocksdb;
        using Buffer         = base::Buffer;
        using CRDTHeadList   = std::unordered_map<std::string, std::set<CID>>;
        using CRDTListResult = std::pair<CRDTHeadList, uint64_t>;

        CrdtHeads( std::shared_ptr<DataStore> aDatastore, const HierarchicalKey &aNamespace );

        CrdtHeads( const CrdtHeads & );

        virtual ~CrdtHeads() = default;

        bool operator==( const CrdtHeads & ) const;

        bool operator!=( const CrdtHeads & ) const;

        CrdtHeads &operator=( const CrdtHeads & );

        HierarchicalKey GetNamespaceKey() const;

        outcome::result<HierarchicalKey> GetKey( const std::string &topic, const CID &aCid ) const;

        bool IsHead( const CID &aCid, const std::string &topic ) const;

        [[nodiscard]] outcome::result<uint64_t> GetHeadHeight( const CID &aCid, const std::string &topic ) const;

        outcome::result<size_t> GetLength( const std::string &topic = "" ) const;

        outcome::result<void> Add( const CID &aCid, uint64_t aHeight, const std::string &topic );

        outcome::result<void> Remove( const CID &aCid, const std::string &topic );

        outcome::result<void> Replace( const CID         &aCidHead,
                                       const CID         &aNewHeadCid,
                                       uint64_t           aHeight,
                                       const std::string &topic );

        outcome::result<CRDTListResult> GetList( const std::unordered_set<std::string> &topics = {} ) const;

        outcome::result<void> PrimeCache();

    protected:
        outcome::result<void> Write( storage::BufferBatch &aDataStore,
                                     const CID            &aCid,
                                     uint64_t              aHeight,
                                     const std::string    &topic ) const;

        outcome::result<void> Delete( const std::unique_ptr<storage::BufferBatch> &aDataStore,
                                      const CID                                   &aCid,
                                      const std::string                           &topic ) const;

    private:
        CrdtHeads() = default;

        mutable std::shared_mutex                                mutex_;
        std::shared_ptr<DataStore>                               dataStore_;
        std::unordered_map<std::string, std::map<CID, uint64_t>> cache_;
        HierarchicalKey                                          namespaceKey_;
        base::Logger                                             logger_ = base::createLogger( "CrdtHeads" );
    };

} // namespace sgns::crdt

#endif //SUPERGENIUS_CRDT_HEADS_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

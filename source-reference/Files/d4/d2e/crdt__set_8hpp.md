---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/crdt_set.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/crdt_set.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::CrdtSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/)** <br/>[CrdtSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/) implements an Add-Wins Observed-Remove Set using delta-CRDTs ([https://arxiv.org/abs/1410.2803](https://arxiv.org/abs/1410.2803)) and backing all the data in a datastore. It is fully agnostic to MerkleCRDTs or the delta distribution layer. It chooses the Value with most priority for a Key as the current Value. When two values have the same priority, it chooses by alphabetically sorting their unique IDs alphabetically.  |




## Source code

```cpp
#ifndef SUPERGENIUS_CRDT_SET_HPP
#define SUPERGENIUS_CRDT_SET_HPP

#include <mutex>
#include <storage/rocksdb/rocksdb.hpp>
#include "crdt/hierarchical_key.hpp"
#include "crdt/proto/delta.pb.h"

namespace sgns::crdt
{
    class CrdtSet
    {
    public:
        using Delta       = pb::Delta;
        using Element     = pb::Element;
        using Buffer      = base::Buffer;
        using DataStore   = storage::rocksdb;
        using QueryResult = DataStore::QueryResult;

        enum class QuerySuffix
        {
            QUERY_ALL,
            QUERY_VALUESUFFIX,
            QUERY_PRIORITYSUFFIX,
        };

        using PutHookPtr = std::function<void( const std::string &k, const Buffer &v, const std::string &cid )>;

        using DeleteHookPtr = std::function<void( const std::string &k, const std::string &cid )>;

        CrdtSet( std::shared_ptr<DataStore> aDatastore,
                 const HierarchicalKey     &aNamespace,
                 PutHookPtr                 aPutHookPtr    = nullptr,
                 DeleteHookPtr              aDeleteHookPtr = nullptr );

        CrdtSet( const CrdtSet & );

        virtual ~CrdtSet() = default;

        bool operator==( const CrdtSet & ) const;

        bool operator!=( const CrdtSet & ) const;

        CrdtSet &operator=( const CrdtSet & );

        static std::string GetPrioritySuffix()
        {
            return std::string( prioritySuffix_ );
        }

        static std::string GetValueSuffix()
        {
            return std::string( valueSuffix_ );
        }

        outcome::result<std::string> GetValueFromDatastore( const HierarchicalKey &aKey ) const;

        static outcome::result<std::shared_ptr<Delta>> CreateDeltaToAdd( const std::string &aKey,
                                                                         const std::string &aValue );

        outcome::result<std::shared_ptr<Delta>> CreateDeltaToRemove( const std::string &aKey ) const;

        outcome::result<Buffer> GetElement( const std::string &aKey ) const;

        outcome::result<QueryResult> QueryElements( std::string_view   aPrefix,
                                                    const QuerySuffix &aSuffix = QuerySuffix::QUERY_ALL ) const;

        outcome::result<QueryResult> QueryElements( const std::string &prefix_base,
                                                    const std::string &middle_part,
                                                    const std::string &remainder_prefix,
                                                    const QuerySuffix &aSuffix = QuerySuffix::QUERY_ALL ) const;

        // TODO: Need to implement query with prefix from datastore
        //func (s *set) Elements(q query.Query) (query.Results, error) {

        outcome::result<bool> IsValueInSet( const std::string &aKey ) const;

        outcome::result<bool> InElemsNotTombstoned( const std::string &aKey ) const;

        HierarchicalKey KeyPrefix( const std::string &aKey ) const;

        HierarchicalKey ElemsPrefix( const std::string &aKey ) const;

        HierarchicalKey TombsPrefix( const std::string &aKey ) const;

        HierarchicalKey KeysKey( std::string_view aKey ) const;

        HierarchicalKey ValueKey( const std::string &aKey ) const;

        HierarchicalKey PriorityKey( const std::string &aKey ) const;

        outcome::result<uint64_t> GetPriority( const std::string &aKey ) const;

        outcome::result<void> SetPriority( const std::string &aKey, uint64_t aPriority );

        outcome::result<void> SetValue( const std::string &aKey,
                                        const std::string &aID,
                                        const Buffer      &aValue,
                                        uint64_t           aPriority );

        outcome::result<void> SetValue( const std::unique_ptr<storage::BufferBatch> &aDataStore,
                                        const std::string                           &aKey,
                                        const std::string                           &aID,
                                        const Buffer                                &aValue,
                                        uint64_t                                     aPriority );

        outcome::result<void> PutElems( std::vector<Element> &aElems, const std::string &aID, uint64_t aPriority );

        outcome::result<void> PutTombs( const std::vector<Element> &aTombs, const std::string &aID ) const;

        outcome::result<void> Merge( const Delta &aDelta, const std::string &aID );

        outcome::result<bool> InTombsKeyID( const std::string &aKey, const std::string &aID ) const;

        void SetPutHook( const PutHookPtr &putHookPtr );

        void SetDeleteHook( const DeleteHookPtr &deleteHookPtr );

        outcome::result<void> DataStoreSync( const std::vector<HierarchicalKey> &aKeyList );

        void PrintDataStore() const;

    private:
        CrdtSet() = default;

        static void PrintTombs( const std::vector<Element> &aTombs );

        outcome::result<void> SetPriority( const std::unique_ptr<storage::BufferBatch> &aDataStore,
                                           const std::string                           &aKey,
                                           uint64_t                                     aPriority );

        std::shared_ptr<DataStore> dataStore_ = nullptr;
        HierarchicalKey            namespaceKey_;
        std::mutex                 mutex_;
        PutHookPtr                 putHookFunc_    = nullptr;
        DeleteHookPtr              deleteHookFunc_ = nullptr;

        static constexpr std::string_view elemsNamespace_ = "s"; // "s" -> elements namespace /set/s/<key>/<block>
        static constexpr std::string_view tombsNamespace_ = "t"; // "t" -> tombstones namespace /set/t/<key>/<block>
        static constexpr std::string_view keysNamespace_  = "k"; // "k" -> keys namespace /set/k/<key>/{v,p}
        static constexpr std::string_view valueSuffix_    = "v"; // "v" for /keys namespace
        static constexpr std::string_view prioritySuffix_ = "p"; // "p" for /keys namespace
    };

} // namespace sgns::crdt

#endif //SUPERGENIUS_CRDT_SET_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/atomic_transaction.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/atomic_transaction.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/)** <br/>[AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/) provides atomic multi-key operations for CRDT datastore All operations within a transaction are combined into a single delta and published atomically to ensure consistency.  |




## Source code

```cpp
#ifndef SUPERGENIUS_ATOMIC_TRANSACTION_HPP
#define SUPERGENIUS_ATOMIC_TRANSACTION_HPP

#include "base/buffer.hpp"
#include "crdt/hierarchical_key.hpp"
#include "crdt/proto/delta.pb.h"
#include "outcome/outcome.hpp"
#include "primitives/cid/cid.hpp"
#include <memory>
#include <mutex>
#include <vector>
#include <optional>
#include <unordered_set>

namespace sgns::crdt
{
    class CrdtDatastore;
    class AtomicTransaction;

    class AtomicTransaction
    {
    public:
        using Buffer = base::Buffer;
        using Delta  = pb::Delta;

        explicit AtomicTransaction( std::shared_ptr<CrdtDatastore> datastore );

        ~AtomicTransaction();

        outcome::result<void> Put( HierarchicalKey key, Buffer value );

        outcome::result<void> Remove( const HierarchicalKey &key );

        outcome::result<Buffer> Get( const HierarchicalKey &key ) const;

        outcome::result<void> Erase( const HierarchicalKey &key );

        bool HasKey( const HierarchicalKey &key ) const;

        outcome::result<void> AddTopic( const std::string &topic );

        outcome::result<void> AddTopics( const std::unordered_set<std::string> &topics );

        outcome::result<CID> Commit( const std::unordered_set<std::string> &topics );

    private:
        enum class Operation
        {
            PUT,
            REMOVE
        };

        struct PendingOperation
        {
            Operation       type;
            HierarchicalKey key;
            Buffer          value;
        };

        void Rollback();

        std::optional<PendingOperation> FindLatestOperation( const HierarchicalKey &key ) const;

        std::shared_ptr<CrdtDatastore>  datastore_;
        std::vector<PendingOperation>   operations_;
        std::unordered_set<std::string> modified_keys_; // Track which keys have been modified
        std::unordered_set<std::string> stored_topics_; // Topics accumulated before commit
        bool                            is_committed_;
        mutable std::mutex              mutex_;
    };

} // namespace sgns::crdt

#endif // SUPERGENIUS_ATOMIC_TRANSACTION_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

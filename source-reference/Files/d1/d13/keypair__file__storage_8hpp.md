---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/globaldb/keypair_file_storage.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/globaldb/keypair_file_storage.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::KeyPairFileStorage](/source-reference/Classes/d6/d1e/classsgns_1_1crdt_1_1_key_pair_file_storage/)**  |




## Source code

```cpp
#ifndef SUPERGENIUS_CRDT_KEYPAIR_FILE_STORAGE_HPP
#define SUPERGENIUS_CRDT_KEYPAIR_FILE_STORAGE_HPP

#include "outcome/outcome.hpp"
#include "base/logger.hpp"
#include <boost/filesystem/path.hpp>
#include <libp2p/crypto/key.hpp>

namespace sgns::crdt
{
class KeyPairFileStorage
{
public:
    KeyPairFileStorage( boost::filesystem::path keyPath );

    [[nodiscard]] outcome::result<libp2p::crypto::KeyPair> GetKeyPair() const;

private:
    boost::filesystem::path m_keyPath;
    sgns::base::Logger m_logger = sgns::base::createLogger("KeyPairFileStorage");
};
}

#endif // SUPERGENIUS_CRDT_KEYPAIR_FILE_STORAGE_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

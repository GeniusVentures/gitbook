---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/broadcaster.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/broadcaster.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/)** <br/>A [Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/) provides a way to send (notify) an opaque payload to all replicas and to retrieve payloads broadcasted.  |




## Source code

```cpp
#ifndef SUPERGENIUS_BROADCASTER_HPP
#define SUPERGENIUS_BROADCASTER_HPP

#include "base/buffer.hpp"
#include <libp2p/peer/peer_info.hpp>
#include <boost/optional.hpp>
#include <tuple>
#include <string>
#include <optional>

namespace sgns::crdt
{
    class Broadcaster
    {
    public:
        virtual ~Broadcaster() = default;

        enum class ErrorCode
        {
            Success            = 0, /*> 0 should not represent an error */
            ErrNoMoreBroadcast = 1, /*> no more data to broadcast */
        };

        virtual outcome::result<void> Broadcast( const base::Buffer &buff, std::string topic, boost::optional<libp2p::peer::PeerInfo> peerInfo = boost::none ) = 0;

        virtual outcome::result<base::Buffer> Next() = 0;

        virtual bool HasTopic( const std::string &topic ) = 0;

        virtual std::shared_ptr<void> GetDagSyncer() const { return nullptr; }
    };
} // namespace sgns::crdt

#endif // SUPERGENIUS_BROADCASTER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

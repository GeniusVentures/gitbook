---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/crdt_options.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/crdt/crdt_options.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::crdt](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::crdt::CrdtOptions](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/)** <br/>Options holds configurable values for [CrdtDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/).  |




## Source code

```cpp
#ifndef SUPERGENIUS_CRDT_OPTIONS_HPP
#define SUPERGENIUS_CRDT_OPTIONS_HPP

#include "base/buffer.hpp"
#include "base/logger.hpp"
#include "crdt/hierarchical_key.hpp"
#include <functional>

namespace sgns::crdt
{
  struct CrdtOptions
  {
    using Buffer = base::Buffer;
    using Logger = base::Logger;


    Logger logger = nullptr;

    long long rebroadcastIntervalMilliseconds = 0;

    long long dagSyncerTimeoutSec = 0;

    int numWorkers = 0;


    enum class VerifyErrorCode
    {
      Success = 0, // 0 should not represent an error
      InvalidRebroadcastInterval, // invalid RebroadcastInterval
      LoggerUndefinied, // the Logger is undefined
      BadNumberOfNumWorkers, // bad number of NumWorkers
      InvalidDAGSyncerTimeout, // invalid DAGSyncerTimeout
    };

    static std::shared_ptr<CrdtOptions> DefaultOptions()
    {
      auto options = std::make_shared<CrdtOptions>();
      options->logger = base::createLogger("CrdtDatastore");
      options->rebroadcastIntervalMilliseconds = 60000; // 10s
      options->dagSyncerTimeoutSec = 300; // 5 mins
      options->numWorkers = 1;
      return options;
    }

    outcome::result<VerifyErrorCode> Verify() const
    {
      if (rebroadcastIntervalMilliseconds <= 0)
      {
        return VerifyErrorCode::InvalidRebroadcastInterval;
      }
      if (numWorkers <= 0)
      {
        return VerifyErrorCode::BadNumberOfNumWorkers;
      }
      if (dagSyncerTimeoutSec < 0)
      {
        return VerifyErrorCode::InvalidDAGSyncerTimeout;
      }
      return VerifyErrorCode::Success;
    }

    bool operator==( const CrdtOptions &rhs ) const
    {
      return logger == rhs.logger && rebroadcastIntervalMilliseconds == rhs.rebroadcastIntervalMilliseconds;
    }

    bool operator!=( const CrdtOptions &rhs ) const
    {
      return !operator==( rhs );
    }

  };
} // namespace sgns::crdt

#endif //SUPERGENIUS_CRDT_OPTIONS_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

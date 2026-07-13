---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/logger.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/logger.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/)**  |

## Types

|                | Name           |
| -------------- | -------------- |
| using std::shared_ptr< spdlog::logger > | **[Logger](/source-reference/Files/d6/da3/logger_8hpp/#using-logger)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| Logger | **[createLogger](/source-reference/Files/d6/da3/logger_8hpp/#function-createlogger)**(const std::string & tag, const std::string & basepath ="")<br/>Create a logger instance.  |

## Types Documentation

### using Logger

```cpp
using sgns::base::Logger = std::shared_ptr<spdlog::logger>;
```



## Functions Documentation

### function createLogger

```cpp
Logger createLogger(
    const std::string & tag,
    const std::string & basepath =""
)
```

Create a logger instance. 

**Parameters**: 

  * **tag** Tagging name for identifying logger. 
  * **basepath** Optional base path for log output (platform dependent). 


**Return**: [Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) object. 



## Source code

```cpp
#ifndef SUPERGENIUS_LOGGER_HPP
#define SUPERGENIUS_LOGGER_HPP

#include <spdlog/fmt/ostr.h>
#include <spdlog/spdlog.h>

#if defined( ANDROID )
#include <spdlog/sinks/android_sink.h>
#endif

namespace sgns::base
{
    using Logger = std::shared_ptr<spdlog::logger>;

    Logger createLogger( const std::string &tag, const std::string &basepath = "" );
} // namespace sgns::base

#endif // SUPERGENIUS_LOGGER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

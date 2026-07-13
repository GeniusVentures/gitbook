---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/logger.cpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/logger.cpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| Logger | **[createLogger](/source-reference/Files/d3/d30/logger_8cpp/#function-createlogger)**(const std::string & tag, const std::string & basepath ="")<br/>Create a logger instance.  |


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
#include "base/logger.hpp"
#include <spdlog/sinks/stdout_color_sinks.h>
#include <spdlog/sinks/basic_file_sink.h>

namespace
{
    void setGlobalPattern( spdlog::logger &logger )
    {
        logger.set_pattern( "[%Y-%m-%d %H:%M:%S][%l][%n] %v" );
    }

    void setDebugPattern( spdlog::logger &logger )
    {
        logger.set_pattern( "[%Y-%m-%d %H:%M:%S.%F][th:%t][%l][%n] %v" );
    }

    std::shared_ptr<spdlog::logger> createLogger( const std::string &tag,
                                                  bool               debug_mode = false,
                                                  const std::string &basepath   = "" )
    {
        std::shared_ptr<spdlog::logger> logger;
#if defined( ANDROID )
        if ( basepath.size() > 0 )
        {
            logger = spdlog::basic_logger_mt( tag, basepath );
        }
        else
        {
            logger = spdlog::android_logger_mt( tag );
        }

#else
        if ( basepath.size() > 0 )
        {
            logger = spdlog::basic_logger_mt( tag, basepath );
            // Note: flush_on level will be set per-logger in InitLoggers based on the actual log level used
        }
        else
        {
            logger = spdlog::stdout_color_mt( tag );
        }

#endif
        if ( debug_mode )
        {
            setDebugPattern( *logger );
        }
        else
        {
            setGlobalPattern( *logger );
        }
        return logger;
    }
} // namespace

namespace sgns::base
{
    Logger createLogger( const std::string &tag, const std::string &basepath )
    {
        static std::mutex           mutex;
        std::lock_guard<std::mutex> lock( mutex );
        auto                        logger = spdlog::get( tag );
        if ( logger != nullptr && !basepath.empty() )
        {
            // Drop any existing logger with this name to force recreation with file sink
            logger = nullptr;
            spdlog::drop( tag );
            logger = ::createLogger( tag, false, basepath );
            return logger;
        }

        // For console loggers, use existing if available

        if ( logger == nullptr )
        {
            logger = ::createLogger( tag, false, basepath );
        }
        return logger;
    }
} // namespace sgns::base
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

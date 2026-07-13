---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/sgns_version.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/sgns_version.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::version](/source-reference/Namespaces/d8/d5b/namespacesgns_1_1version/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| uint64_t | **[SuperGeniusVersionNum](/source-reference/Files/de/d68/sgns__version_8hpp/#function-supergeniusversionnum)**()<br/>Retrieves the complete version number of SuperGenius.  |
| uint32_t | **[SuperGeniusVersionMajor](/source-reference/Files/de/d68/sgns__version_8hpp/#function-supergeniusversionmajor)**()<br/>Retrieves the major version of SuperGenius.  |
| uint32_t | **[SuperGeniusVersionMinor](/source-reference/Files/de/d68/sgns__version_8hpp/#function-supergeniusversionminor)**()<br/>Retrieves the minor version of SuperGenius.  |
| uint32_t | **[SuperGeniusVersionPatch](/source-reference/Files/de/d68/sgns__version_8hpp/#function-supergeniusversionpatch)**()<br/>Retrieves the patch version of SuperGenius.  |
| uint32_t | **[ProcessingVersion](/source-reference/Files/de/d68/sgns__version_8hpp/#function-processingversion)**()<br/>Retrieves the processing version used by processing task storage keys.  |
| std::string | **[SuperGeniusVersionString](/source-reference/Files/de/d68/sgns__version_8hpp/#function-supergeniusversionstring)**()<br/>Retrieves the short version string of SuperGenius.  |
| std::string | **[SuperGeniusVersionFullString](/source-reference/Files/de/d68/sgns__version_8hpp/#function-supergeniusversionfullstring)**()<br/>Retrieves the full version string of SuperGenius.  |
| std::string | **[SuperGeniusVersionText](/source-reference/Files/de/d68/sgns__version_8hpp/#function-supergeniusversiontext)**()<br/>Retrieves the display version text of SuperGenius.  |
| uint16_t | **[GetNetworkID](/source-reference/Files/de/d68/sgns__version_8hpp/#function-getnetworkid)**() |
| std::string | **[GetNetAndVersionAppendix](/source-reference/Files/de/d68/sgns__version_8hpp/#function-getnetandversionappendix)**() |
| std::string | **[GetNetAndVersionAppendix](/source-reference/Files/de/d68/sgns__version_8hpp/#function-getnetandversionappendix)**(uint32_t version_major, uint32_t version_minor, uint16_t net_id) |
| void | **[SetNetworkId](/source-reference/Files/de/d68/sgns__version_8hpp/#function-setnetworkid)**(uint16_t net_id) |

## Attributes

|                | Name           |
| -------------- | -------------- |
| std::uint16_t | **[MAIN_NET_ID](/source-reference/Files/de/d68/sgns__version_8hpp/#variable-main_net_id)**  |
| std::uint16_t | **[TEST_NET_ID](/source-reference/Files/de/d68/sgns__version_8hpp/#variable-test_net_id)**  |
| std::uint16_t | **[DEV_NET_ID](/source-reference/Files/de/d68/sgns__version_8hpp/#variable-dev_net_id)**  |
| std::string_view | **[NET_ID_APPENDIX](/source-reference/Files/de/d68/sgns__version_8hpp/#variable-net_id_appendix)**  |
| std::string_view | **[SGNS_VERSION_APPENDIX](/source-reference/Files/de/d68/sgns__version_8hpp/#variable-sgns_version_appendix)**  |


## Functions Documentation

### function SuperGeniusVersionNum

```cpp
uint64_t SuperGeniusVersionNum()
```

Retrieves the complete version number of SuperGenius. 

**Return**: uint64_t representing the version number. 

### function SuperGeniusVersionMajor

```cpp
uint32_t SuperGeniusVersionMajor()
```

Retrieves the major version of SuperGenius. 

**Return**: uint32_t representing the major version. 

### function SuperGeniusVersionMinor

```cpp
uint32_t SuperGeniusVersionMinor()
```

Retrieves the minor version of SuperGenius. 

**Return**: uint32_t representing the minor version. 

### function SuperGeniusVersionPatch

```cpp
uint32_t SuperGeniusVersionPatch()
```

Retrieves the patch version of SuperGenius. 

**Return**: uint32_t representing the patch version. 

### function ProcessingVersion

```cpp
uint32_t ProcessingVersion()
```

Retrieves the processing version used by processing task storage keys. 

**Return**: uint32_t processing version. 

### function SuperGeniusVersionString

```cpp
std::string SuperGeniusVersionString()
```

Retrieves the short version string of SuperGenius. 

**Return**: std::string representing the short version. 

### function SuperGeniusVersionFullString

```cpp
std::string SuperGeniusVersionFullString()
```

Retrieves the full version string of SuperGenius. 

**Return**: std::string representing the full version. 

### function SuperGeniusVersionText

```cpp
std::string SuperGeniusVersionText()
```

Retrieves the display version text of SuperGenius. 

**Return**: std::string representing the version text. 

### function GetNetworkID

```cpp
uint16_t GetNetworkID()
```


### function GetNetAndVersionAppendix

```cpp
std::string GetNetAndVersionAppendix()
```


### function GetNetAndVersionAppendix

```cpp
std::string GetNetAndVersionAppendix(
    uint32_t version_major,
    uint32_t version_minor,
    uint16_t net_id
)
```


### function SetNetworkId

```cpp
void SetNetworkId(
    uint16_t net_id
)
```



## Attributes Documentation

### variable MAIN_NET_ID

```cpp
static std::uint16_t MAIN_NET_ID = 369;
```


### variable TEST_NET_ID

```cpp
static std::uint16_t TEST_NET_ID = 963;
```


### variable DEV_NET_ID

```cpp
static std::uint16_t DEV_NET_ID = 144;
```


### variable NET_ID_APPENDIX

```cpp
static std::string_view NET_ID_APPENDIX = ".%hu";
```


### variable SGNS_VERSION_APPENDIX

```cpp
static std::string_view SGNS_VERSION_APPENDIX = ".%hu.%hu";
```



## Source code

```cpp
#ifndef SGNS_SGNS_VERSION_HPP
#define SGNS_SGNS_VERSION_HPP

#include <cstdint>
#include <string>
#include <string_view>

namespace sgns
{
    namespace version
    {
        static constexpr std::uint16_t    MAIN_NET_ID           = 369;
        static constexpr std::uint16_t    TEST_NET_ID           = 963;
        static constexpr std::uint16_t    DEV_NET_ID            = 144;
        static constexpr std::string_view NET_ID_APPENDIX       = ".%hu";
        static constexpr std::string_view SGNS_VERSION_APPENDIX = ".%hu.%hu";
        uint64_t SuperGeniusVersionNum();

        uint32_t SuperGeniusVersionMajor();

        uint32_t SuperGeniusVersionMinor();

        uint32_t SuperGeniusVersionPatch();

        uint32_t ProcessingVersion();

        std::string SuperGeniusVersionString();

        std::string SuperGeniusVersionFullString();

        std::string SuperGeniusVersionText();

        uint16_t GetNetworkID();

        std::string GetNetAndVersionAppendix();
        std::string GetNetAndVersionAppendix( uint32_t version_major, uint32_t version_minor, uint16_t net_id );

        void SetNetworkId( uint16_t net_id );
    }
}

#endif // SGNS_SGNS_VERSION_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

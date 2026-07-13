---
title: sgns::NilFileHelper

---

# sgns::NilFileHelper






`#include <NilFileHelper.hpp>`

## Public Functions

|                | Name           |
| -------------- | -------------- |
| template <typename MarshalledData \> <br/>bool | **[PrintMarshalledData](/source-reference/Classes/d4/d4f/classsgns_1_1_nil_file_helper/#function-printmarshalleddata)**(const MarshalledData & output, std::ostream & out =std::cout, bool binary =true) |
| template <typename MarshalledData \> <br/>std::vector< uint8_t > | **[GetMarshalledData](/source-reference/Classes/d4/d4f/classsgns_1_1_nil_file_helper/#function-getmarshalleddata)**(const MarshalledData & output, bool binary =true) |
| template <typename MarshalledData \> <br/>outcome::result< MarshalledData > | **[DecodeMarshalledData](/source-reference/Classes/d4/d4f/classsgns_1_1_nil_file_helper/#function-decodemarshalleddata)**(std::ifstream & in, bool binary =true) |

## Public Functions Documentation

### function PrintMarshalledData

```cpp
template <typename MarshalledData >
static inline bool PrintMarshalledData(
    const MarshalledData & output,
    std::ostream & out =std::cout,
    bool binary =true
)
```


### function GetMarshalledData

```cpp
template <typename MarshalledData >
static inline std::vector< uint8_t > GetMarshalledData(
    const MarshalledData & output,
    bool binary =true
)
```


### function DecodeMarshalledData

```cpp
template <typename MarshalledData >
static inline outcome::result< MarshalledData > DecodeMarshalledData(
    std::ifstream & in,
    bool binary =true
)
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
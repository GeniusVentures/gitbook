---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/blob.cpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/blob.cpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| | **[OUTCOME_CPP_DEFINE_CATEGORY_3](/source-reference/Files/dd/dc0/blob_8cpp/#function-outcome_cpp_define_category_3)**([sgns::base](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/) , BlobError , e ) |


## Functions Documentation

### function OUTCOME_CPP_DEFINE_CATEGORY_3

```cpp
OUTCOME_CPP_DEFINE_CATEGORY_3(
    sgns::base ,
    BlobError ,
    e 
)
```




## Source code

```cpp
#include "base/blob.hpp"

OUTCOME_CPP_DEFINE_CATEGORY_3(sgns::base, BlobError, e) {
  using sgns::base::BlobError;

  switch(e) {
    case BlobError::INCORRECT_LENGTH:
      return "Input string has incorrect length, not matching the blob size";
  }

  return "Unknown error";
}

namespace sgns::base {

  // explicit instantiations for the most frequently used blobs
  template class Blob<8ul>;
  template class Blob<16ul>;
  template class Blob<32ul>;
  template class Blob<64ul>;

}  // namespace sgns::base
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

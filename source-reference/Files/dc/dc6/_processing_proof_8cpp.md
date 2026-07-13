---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/proof/ProcessingProof.cpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/proof/ProcessingProof.cpp



 [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[nil::crypto3::algebra::curves](/source-reference/Namespaces/db/dc3/namespacenil_1_1crypto3_1_1algebra_1_1curves/)**  |

## Detailed Description


**Date**: 2024-09-29 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#include "ProcessingProof.hpp"
#include <nil/crypto3/multiprecision/cpp_int.hpp>
#include <nil/crypto3/algebra/curves/pallas.hpp>
#include <nil/crypto3/hash/algorithm/hash.hpp>
#include <nil/crypto3/hash/adaptor/hashed.hpp>
#include <nil/crypto3/algebra/marshalling.hpp>
#include "proof/proto/SGProof.pb.h"

using namespace nil::crypto3::algebra::curves;

namespace sgns
{

    outcome::result<std::vector<uint8_t>> ProcessingProof::SerializeFullProof(
        const SGProof::BaseProofData &base_proof )
    {
        return std::vector<uint8_t>{};
    }

    std::pair<boost::json::array, boost::json::array> ProcessingProof::GenerateJsonParameters()
    {
        boost::json::array public_inputs_json_array;
        boost::json::array private_inputs_json_array;

        return std::make_pair( public_inputs_json_array, private_inputs_json_array );
    }

    outcome::result<std::pair<boost::json::array, boost::json::array>> ProcessingProof::DeSerializePublicParams(
        const std::vector<uint8_t> &full_proof_data )
    {
        boost::json::array public_inputs_json_array;
        boost::json::array private_inputs_json_array;

        return std::make_pair( public_inputs_json_array, private_inputs_json_array );
    }

}
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

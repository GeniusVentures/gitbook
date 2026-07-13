---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/proof/ProcessingProof.hpp
summary: Derived class for generating and verifying processing proofs. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/proof/ProcessingProof.hpp



Derived class for generating and verifying processing proofs.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::ProcessingProof](/source-reference/Classes/df/df1/classsgns_1_1_processing_proof/)** <br/>A class for generating and verifying processing proofs.  |

## Detailed Description

Derived class for generating and verifying processing proofs. 

**Date**: 2024-09-29 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp


#ifndef _PROCESSING_PROOF_HPP_
#define _PROCESSING_PROOF_HPP_

#include <string>
#include <cstdint>
#include <array>
#include <utility>
#include <boost/json.hpp>
#include <string_view>
#include "IBasicProof.hpp"

namespace sgns
{
    class ProcessingProof : public IBasicProof
    {
    public:
        explicit ProcessingProof( std::string subtask_id ) :
            IBasicProof( "Bypass" ), //
            subtask_id_m( std::move( subtask_id ) )
        {
        }

        ~ProcessingProof() = default;

        std::string GetProofType() const override
        {
            return std::string( PROCESSING_TYPE_NAME );
        }

    private:
        std::string subtask_id_m; 

        outcome::result<std::vector<uint8_t>> SerializeFullProof(
            const SGProof::BaseProofData &base_proof_data ) override;

        std::pair<boost::json::array, boost::json::array> GenerateJsonParameters() override;

        static outcome::result<std::pair<boost::json::array, boost::json::array>> DeSerializePublicParams(
            const std::vector<uint8_t> &full_proof_data );

        static constexpr std::string_view PROCESSING_TYPE_NAME = "Processing";

        static inline bool Register()
        {
            RegisterDeserializer( std::string( PROCESSING_TYPE_NAME ), &ProcessingProof::DeSerializePublicParams );
            RegisterBytecode( std::string( PROCESSING_TYPE_NAME ), "Bypass" );
            return true;
        }

        static inline bool registered = Register();
    };
}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

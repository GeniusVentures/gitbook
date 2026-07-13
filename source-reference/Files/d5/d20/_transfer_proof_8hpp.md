---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/proof/TransferProof.hpp
summary: Derived class for generating and verifying transfer proofs. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/proof/TransferProof.hpp



Derived class for generating and verifying transfer proofs.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::TransferProof](/source-reference/Classes/d5/d48/classsgns_1_1_transfer_proof/)** <br/>A class for generating and verifying transfer proofs.  |

## Detailed Description

Derived class for generating and verifying transfer proofs. 

**Date**: 2024-09-29 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp


#ifndef _TRANSFER_PROOF_HPP_
#define _TRANSFER_PROOF_HPP_

#include <string>
#include <cstdint>
#include <array>
#include <utility>
#include <optional>
#include <boost/json.hpp>
#include <string_view>
#include "IBasicProof.hpp"
#include "circuits/TransactionVerifierCircuit.hpp"

namespace sgns
{
    class TransferProof : public IBasicProof
    {
    public:
        explicit TransferProof( uint64_t balance, uint64_t amount, std::optional<std::string> bytecode = std::nullopt );

        ~TransferProof() = default;

        std::string GetProofType() const override
        {
            return std::string( TRANSFER_TYPE_NAME );
        }

        template <typename T>
        static boost::json::object GenerateCurveParameter( T value );

    protected:
        static constexpr uint64_t generator_X_point = 1;     
        static constexpr uint64_t generator_Y_point = 2;     
        static constexpr uint64_t base_seed         = 12345; 
        static constexpr uint64_t provided_totp     = 67890; 

        static constexpr std::array<uint64_t, 4> ranges = { 1000, 2000, 3000, 4000 };
        outcome::result<std::vector<uint8_t>> SerializeFullProof(
            const SGProof::BaseProofData &base_proof_data ) override;

        std::pair<boost::json::array, boost::json::array> GenerateJsonParameters() override;

    private:
        uint64_t balance_; 
        uint64_t amount_;  

        static outcome::result<std::pair<boost::json::array, boost::json::array>> DeSerializePublicParams(
            const std::vector<uint8_t> &full_proof_data );

        static constexpr std::string_view TRANSFER_TYPE_NAME = "Transfer";

        static inline bool Register()
        {
            RegisterDeserializer( std::string( TRANSFER_TYPE_NAME ), &TransferProof::DeSerializePublicParams );
#ifdef RELEASE_BYTECODE_CIRCUITS
            RegisterBytecode( std::string( TRANSFER_TYPE_NAME ), std::string( TransactionCircuit ) );
#else
            RegisterBytecode( std::string( TRANSFER_TYPE_NAME ), std::string( TransactionCircuit ) );
#endif

            return true;
        }

        static inline bool registered = Register();
    };
}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

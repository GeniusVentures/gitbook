---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/proof/RecursiveTransferProof.hpp
summary: Header file of the RecursiveTransferProof. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/proof/RecursiveTransferProof.hpp



Header file of the RecursiveTransferProof.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::RecursiveTransferProof](/source-reference/Classes/d3/d2f/classsgns_1_1_recursive_transfer_proof/)** <br/>A class for generating a recursive Transfer Proof.  |

## Detailed Description

Header file of the RecursiveTransferProof. 

**Date**: 2025-01-29 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp


#ifndef _RECURSIVE_TRANSFER_PROOF_HPP_
#define _RECURSIVE_TRANSFER_PROOF_HPP_

#include <string>
#include <cstdint>
#include <array>
#include <utility>
#include <boost/json.hpp>
#include <string_view>
#include "GeniusProver.hpp"
#include "IBasicProof.hpp"
#include "TransferProof.hpp"

#include "circuits/RecursiveTransactionCircuit.hpp"

namespace sgns
{
    class RecursiveTransferProof : public TransferProof
    {
    public:
        explicit RecursiveTransferProof( uint64_t balance, uint64_t amount, GeniusProver::ProofSnarkType snark );

        ~RecursiveTransferProof() = default;

        std::string GetProofType() const override
        {
            return std::string( RECURSIVE_TRANSFER_TYPE_NAME );
        }

    protected:
        outcome::result<std::vector<uint8_t>> SerializeFullProof(
            const SGProof::BaseProofData &base_proof_data ) override;

        std::pair<boost::json::array, boost::json::array> GenerateJsonParameters() override;

    private:

        static outcome::result<std::pair<boost::json::array, boost::json::array>> DeSerializePublicParams(
            const std::vector<uint8_t> &full_proof_data );

        static constexpr std::string_view RECURSIVE_TRANSFER_TYPE_NAME = "RecursiveTransfer";

        static inline bool Register()
        {
            RegisterDeserializer( std::string( RECURSIVE_TRANSFER_TYPE_NAME ), &RecursiveTransferProof::DeSerializePublicParams );
#ifdef RELEASE_BYTECODE_CIRCUITS
            RegisterBytecode( std::string( RECURSIVE_TRANSFER_TYPE_NAME ), std::string( RecursiveTransactionCircuit ) );
#else
            RegisterBytecode( std::string( RECURSIVE_TRANSFER_TYPE_NAME ), std::string( RecursiveTransactionCircuit ) );
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

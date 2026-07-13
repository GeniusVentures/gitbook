---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/proof/IBasicProof.hpp
summary: Base proof class header file. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/proof/IBasicProof.hpp



Base proof class header file.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::IBasicProof](/source-reference/Classes/d9/dbe/classsgns_1_1_i_basic_proof/)** <br/>Base proof class header file.  |

## Functions

|                | Name           |
| -------------- | -------------- |
| | **[OUTCOME_HPP_DECLARE_ERROR_2](/source-reference/Files/de/d4a/_i_basic_proof_8hpp/#function-outcome_hpp_declare_error_2)**([sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/) , IBasicProof::Error )<br/>Macro for declaring error handling in the IBasicProof class.  |

## Detailed Description

Base proof class header file. 

**Date**: 2024-09-29 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 

## Functions Documentation

### function OUTCOME_HPP_DECLARE_ERROR_2

```cpp
OUTCOME_HPP_DECLARE_ERROR_2(
    sgns ,
    IBasicProof::Error 
)
```

Macro for declaring error handling in the IBasicProof class. 



## Source code

```cpp


#ifndef _IBASIC_PROOF_HPP_
#define _IBASIC_PROOF_HPP_
#include <string>
#include <vector>
#include <cstdint>
#include <memory>
#include <utility>
#include <boost/json.hpp>
#include "proof/proto/SGProof.pb.h"
#include "outcome/outcome.hpp"

namespace sgns
{
    class IBasicProof
    {
    public:
        using PublicParamDeserializeFn = std::function<
            outcome::result<std::pair<boost::json::array, boost::json::array>>( const std::vector<uint8_t> & )>;

        explicit IBasicProof( std::string bytecode_payload );

        virtual ~IBasicProof() = default;

        enum class Error
        {
            INSUFFICIENT_FUNDS = 0,   
            INVALID_PROOF,            
            BYTECODE_NOT_FOUND,       
            INVALID_CIRCUIT,          
            INVALID_PROTO_PROOF,      
            INVALID_PROOF_TYPE,       
            UNEXPECTED_PROOF_TYPE,    
            INVALID_PUBLIC_PARAMETERS 
        };

        virtual std::string GetProofType() const = 0;

        outcome::result<std::vector<uint8_t>> GenerateFullProof();

        static outcome::result<bool> VerifyFullProof( const std::vector<uint8_t> &full_proof_data );
        static outcome::result<bool> VerifyFullProof(
            const std::pair<boost::json::array, boost::json::array> &parameters,
            const SGProof::BaseProofData                            &proof_data,
            std::string                                              proof_bytecode );

        static boost::json::object GenerateIntParameter( uint64_t value );

        template <std::size_t N>
        static boost::json::object GenerateArrayParameter( const std::array<uint64_t, N> &values )
        {
            boost::json::array field_array;

            for ( const auto &value : values )
            {
                field_array.push_back( GenerateFieldParameter( value ) );
            }

            boost::json::object array_obj;
            array_obj["array"] = field_array;

            return array_obj;
        }

        static boost::json::object GenerateFieldParameter( uint64_t value );

    protected:
        static inline std::map<std::string, PublicParamDeserializeFn> PublicParamDeSerializers;

        static inline std::map<std::string, std::string> ByteCodeMap;

        static void RegisterDeserializer( const std::string &proof_type, PublicParamDeserializeFn fn );

        static void RegisterBytecode( const std::string &proof_type, std::string bytecode )
        {
            ByteCodeMap[proof_type] = std::move( bytecode );
        }

        static outcome::result<SGProof::BaseProofProto> DeSerializeBaseProof( const std::vector<uint8_t> &proof_data );

        virtual outcome::result<std::vector<uint8_t>> SerializeFullProof(
            const SGProof::BaseProofData &base_proof_data ) = 0;

    private:
        const std::string bytecode_payload_; 

        outcome::result<SGProof::BaseProofData> GenerateProof();

        virtual std::pair<boost::json::array, boost::json::array> GenerateJsonParameters() = 0;
    };

}

OUTCOME_HPP_DECLARE_ERROR_2( sgns, IBasicProof::Error );

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700

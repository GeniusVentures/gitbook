---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/MintTransaction.hpp
summary: Transaction type used to mint tokens from an external chain reference. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/MintTransaction.hpp



Transaction type used to mint tokens from an external chain reference.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::MintTransaction](/source-reference/Classes/d7/d9c/classsgns_1_1_mint_transaction/)** <br/>Transaction that mints tokens after proving a corresponding source-chain event.  |

## Detailed Description

Transaction type used to mint tokens from an external chain reference. 

**Date**: 2024-03-15 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef _MINT_TRANSACTION_HPP_
#define _MINT_TRANSACTION_HPP_

#include <vector>
#include <cstdint>

#include "account/GeniusTransaction.hpp"
#include "account/TokenID.hpp"

namespace sgns
{
    class MintTransaction final : public GeniusTransaction
    {
    public:
        ~MintTransaction() override = default;

        static std::shared_ptr<MintTransaction> DeSerializeByteVector( const std::vector<uint8_t> &data );

        static MintTransaction New( uint64_t                                        new_amount,
                                    std::string                                     chain_id,
                                    TokenID                                         token_id,
                                    SGTransaction::DAGStruct                        dag );

        using GeniusTransaction::SerializeByteVector;

        using GeniusTransaction::SerializeToEmbeddedTransaction;
        EmbeddedTransaction SerializeToEmbeddedTransaction( const SGTransaction::DAGStruct &dag ) const override;
        std::vector<uint8_t> SerializeByteVector( const SGTransaction::DAGStruct &dag ) const override;

        uint64_t GetAmount() const;

        TokenID GetTokenID() const;

        std::string GetChainId() const override;

        std::string GetTransactionSpecificPath() const override
        {
            return GetType();
        }

    private:
        MintTransaction( uint64_t new_amount, std::string chain_id, TokenID token_id, SGTransaction::DAGStruct dag );

        uint64_t    amount;   
        std::string chain_id; 
        TokenID     token_id; 

        static bool Register()
        {
            RegisterDeserializer( "mint", &MintTransaction::DeSerializeByteVector );
            return true;
        }

        static inline bool registered = Register();
    };
}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

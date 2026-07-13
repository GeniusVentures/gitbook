---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/MintTransactionV2.hpp
summary: Header file of the Version 2 of the Mint transaction class. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/MintTransactionV2.hpp



Header file of the Version 2 of the Mint transaction class.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::MintTransactionV2](/source-reference/Classes/db/d6b/classsgns_1_1_mint_transaction_v2/)** <br/>Implements a Mint Version 2 transaction.  |

## Detailed Description

Header file of the Version 2 of the Mint transaction class. 

**Date**: 2026-03-19 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef SGNS_MINT_TRANSACTION_V2_HPP
#define SGNS_MINT_TRANSACTION_V2_HPP

#include <vector>
#include <cstdint>

#include "account/GeniusTransaction.hpp"
#include "account/TokenID.hpp"
#include "account/UTXOStructs.hpp"

namespace sgns
{
    class MintTransactionV2 final : public GeniusTransaction
    {
    public:
        using GeniusTransaction::SerializeByteVector;

        using GeniusTransaction::SerializeToEmbeddedTransaction;
        EmbeddedTransaction SerializeToEmbeddedTransaction( const SGTransaction::DAGStruct &dag ) const override;
        ~MintTransactionV2() override = default;

        static std::shared_ptr<MintTransactionV2> DeSerializeByteVector( const std::vector<uint8_t> &data );

        static MintTransactionV2 New( uint64_t                   new_amount,
                                      std::string                chain_id,
                                      TokenID                    token_id,
                                      SGTransaction::DAGStruct   dag,
                                      std::vector<InputUTXOInfo> mint_inputs,
                                      std::string                mint_destination );

        std::vector<uint8_t> SerializeByteVector( const SGTransaction::DAGStruct &dag ) const override;

        uint64_t GetAmount() const;

        TokenID GetTokenID() const;

        std::string GetChainId() const override;

        UTXOTxParameters GetUTXOParameters() const;

        bool HasUTXOParameters() const override;

        std::optional<UTXOTxParameters> GetUTXOParametersOpt() const override;

        std::string GetTransactionSpecificPath() const override
        {
            return GetType();
        }

        std::unordered_set<std::string> GetTopics() const override;

        std::string GetSlotID() const override;

    private:
        MintTransactionV2( UTXOTxParameters         utxo_params,
                           std::string              chain_id,
                           TokenID                  token_id,
                           SGTransaction::DAGStruct dag );

        UTXOTxParameters utxo_params_; 
        std::string      chain_id_;    
        TokenID          token_id_;    

        static bool Register()
        {
            RegisterDeserializer( "mint-v2", &MintTransactionV2::DeSerializeByteVector );
            return true;
        }

        static inline bool registered = Register();
    };
}

#endif // SGNS_MINT_TRANSACTION_V2_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

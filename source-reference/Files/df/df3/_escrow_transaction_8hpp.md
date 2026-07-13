---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/EscrowTransaction.hpp
summary: Transaction type used to lock UTXO funds into an escrow address. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/EscrowTransaction.hpp



Transaction type used to lock UTXO funds into an escrow address.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::EscrowTransaction](/source-reference/Classes/db/d70/classsgns_1_1_escrow_transaction/)** <br/>Transaction that reserves funds for a job escrow while tracking peer payout metadata.  |

## Detailed Description

Transaction type used to lock UTXO funds into an escrow address. 

**Date**: 2024-04-24 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef _ESCROW_TRANSACTION_HPP_
#define _ESCROW_TRANSACTION_HPP_

#include <string>
#include "account/GeniusTransaction.hpp"
#include "UTXOStructs.hpp"

namespace sgns
{
    class EscrowTransaction : public GeniusTransaction
    {
    public:
        static EscrowTransaction New( UTXOTxParameters         params,
                                      uint64_t                 amount,
                                      std::string              dev_addr,
                                      uint64_t                 peers_cut,
                                      SGTransaction::DAGStruct dag );

        static std::shared_ptr<EscrowTransaction> DeSerializeByteVector( const std::vector<uint8_t> &data );

        ~EscrowTransaction() override = default;

        using GeniusTransaction::SerializeByteVector;

        std::vector<uint8_t> SerializeByteVector( const SGTransaction::DAGStruct &dag ) const override;

        using GeniusTransaction::SerializeToEmbeddedTransaction;
        EmbeddedTransaction SerializeToEmbeddedTransaction( const SGTransaction::DAGStruct &dag ) const override;

        uint64_t GetNumChunks() const;

        std::string GetTransactionSpecificPath() const override
        {
            return GetType();
        }

        UTXOTxParameters GetUTXOParameters() const
        {
            return utxo_params_;
        }

        bool HasUTXOParameters() const override
        {
            return true;
        }

        std::optional<UTXOTxParameters> GetUTXOParametersOpt() const override
        {
            return utxo_params_;
        }

        std::string GetDevAddress() const
        {
            return dev_addr_;
        }

        uint64_t GetAmount() const
        {
            return amount_;
        }

        uint64_t GetPeersCut() const
        {
            return peers_cut_;
        }

    private:
        EscrowTransaction( UTXOTxParameters         params,
                           uint64_t                 amount,
                           std::string              dev_addr,
                           uint64_t                 peers_cut,
                           SGTransaction::DAGStruct dag );

        UTXOTxParameters utxo_params_; 
        uint64_t         amount_;      
        std::string      dev_addr_;    
        uint64_t         peers_cut_;   

        static bool Register()
        {
            RegisterDeserializer( "escrow-hold", &EscrowTransaction::DeSerializeByteVector );
            return true;
        }

        static inline bool registered = Register();
    };
}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

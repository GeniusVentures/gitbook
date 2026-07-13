---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/TransferTransaction.hpp
summary: Transaction of currency transfer. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/TransferTransaction.hpp



Transaction of currency transfer.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::TransferTransaction](/source-reference/Classes/de/d98/classsgns_1_1_transfer_transaction/)** <br/>Transaction for transferring funds between UTXO inputs and outputs.  |

## Detailed Description

Transaction of currency transfer. 

**Date**: 2024-03-11 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef _TRANSFER_TRANSACTION_HPP_
#define _TRANSFER_TRANSACTION_HPP_

#include "account/GeniusTransaction.hpp"
#include "UTXOStructs.hpp"
#include "account/proto/SGTransaction.pb.h"

namespace sgns
{
    class TransferTransaction final : public GeniusTransaction
    {
    public:
        static TransferTransaction New( std::vector<InputUTXOInfo>  inputs,
                                        std::vector<OutputDestInfo> destinations,
                                        SGTransaction::DAGStruct    dag );
        ~TransferTransaction() override = default;

        using GeniusTransaction::SerializeByteVector;
        std::vector<uint8_t> SerializeByteVector( const SGTransaction::DAGStruct &dag ) const override;

        using GeniusTransaction::SerializeToEmbeddedTransaction;
        EmbeddedTransaction SerializeToEmbeddedTransaction( const SGTransaction::DAGStruct &dag ) const override;

        static std::shared_ptr<TransferTransaction> DeSerializeByteVector( const std::vector<uint8_t> &data );

        std::vector<OutputDestInfo> GetDstInfos() const;
        std::vector<InputUTXOInfo>  GetInputInfos() const;

        bool                        HasUTXOParameters() const override;

        std::optional<UTXOTxParameters> GetUTXOParametersOpt() const override;

        std::string GetTransactionSpecificPath() const override
        {
            return GetType();
        }

        std::unordered_set<std::string> GetTopics() const override;

    private:
        TransferTransaction( std::vector<OutputDestInfo> destinations,
                             std::vector<InputUTXOInfo>  inputs,
                             SGTransaction::DAGStruct    dag );

        std::vector<InputUTXOInfo>  input_tx_;
        std::vector<OutputDestInfo> outputs_;

        static bool Register()
        {
            RegisterDeserializer( "transfer", &TransferTransaction::DeSerializeByteVector );
            return true;
        }

        static inline bool registered = Register();
    };

}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

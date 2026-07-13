---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/ProcessingTransaction.hpp
summary: Transaction of processing data. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/ProcessingTransaction.hpp



Transaction of processing data.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::ProcessingTransaction](/source-reference/Classes/d6/d7f/classsgns_1_1_processing_transaction/)**  |

## Detailed Description

Transaction of processing data. 

**Date**: 2024-03-11 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef _PROCESSING_TRANSACTION_HPP_
#define _PROCESSING_TRANSACTION_HPP_
#include <string>

#include <boost/multiprecision/cpp_int.hpp>

#include "account/GeniusTransaction.hpp"

namespace sgns
{
    using namespace boost::multiprecision;

    class ProcessingTransaction final : public GeniusTransaction
    {
    public:
        static std::shared_ptr<ProcessingTransaction> DeSerializeByteVector( const std::vector<uint8_t> &data );

        static ProcessingTransaction New( std::string              job_id,
                                          std::vector<std::string> subtask_ids,
                                          std::vector<std::string> node_addresses,
                                          SGTransaction::DAGStruct dag );

        ~ProcessingTransaction() override = default;

        using GeniusTransaction::SerializeByteVector;

        using GeniusTransaction::SerializeToEmbeddedTransaction;
        EmbeddedTransaction SerializeToEmbeddedTransaction( const SGTransaction::DAGStruct &dag ) const override;
        std::vector<uint8_t> SerializeByteVector( const SGTransaction::DAGStruct &dag ) const override;

        uint256_t GetJobHash() const
        {
            return job_hash_;
        }

        std::vector<std::string> GetSubtaskIDs() const
        {
            return subtask_ids_;
        }

        std::vector<std::string> GetNodeAddresses() const
        {
            return node_addresses_;
        }

        std::string GetTaskID() const
        {
            return job_id_;
        }

        std::string GetTransactionSpecificPath() const override
        {
            boost::format processing_fmt( GetType() + "/%s" );

            processing_fmt % job_id_;
            return processing_fmt.str();
        }

    private:
        ProcessingTransaction( std::string              job_id,
                               std::vector<std::string> subtask_ids,
                               std::vector<std::string> node_addresses,
                               SGTransaction::DAGStruct dag );

        std::string              job_id_;         
        uint256_t                job_hash_;       
        std::vector<std::string> subtask_ids_;    
        std::vector<std::string> node_addresses_; 

        static bool Register()
        {
            RegisterDeserializer( "process", &ProcessingTransaction::DeSerializeByteVector );
            return true;
        }

        static inline bool registered = Register();
    };
}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

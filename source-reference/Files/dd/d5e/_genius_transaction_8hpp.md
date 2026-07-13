---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/GeniusTransaction.hpp
summary: Header file of the base GeniusTransaction class. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/account/GeniusTransaction.hpp



Header file of the base GeniusTransaction class.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/)** <br/>Base class of the [GeniusTransaction](/source-reference/Classes/d6/dc8/classsgns_1_1_genius_transaction/).  |

## Detailed Description

Header file of the base GeniusTransaction class. 

**Date**: 2024-03-11 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 



## Source code

```cpp

#ifndef SGNS_GENIUS_TRANSACTION_HPP
#define SGNS_GENIUS_TRANSACTION_HPP

#include <utility>
#include <vector>
#include <string>
#include <optional>

#include <boost/format.hpp>

#include "outcome/outcome.hpp"
#include "account/proto/SGTransaction.pb.h"
#include "blockchain/impl/proto/Consensus.pb.h"
#include "account/UTXOStructs.hpp"
#include "GeniusAccount.hpp"

#include <gsl/span>

namespace sgns
{
    using namespace boost::multiprecision;

    class GeniusTransaction
    {
    public:
        static constexpr std::string_view GENIUS_CHAIN_ID = "supergenius_chain";

        using TransactionDeserializeFn =
            std::function<std::shared_ptr<GeniusTransaction>( const std::vector<uint8_t> & )>;

        GeniusTransaction( std::string type, SGTransaction::DAGStruct dag ) :
            dag_st( std::move( dag ) ), transaction_type( std::move( type ) )
        {
        }

        virtual ~GeniusTransaction() = default;

        [[nodiscard]] std::string GetType() const
        {
            return transaction_type;
        }

        static outcome::result<SGTransaction::DAGStruct> DeSerializeDAGStruct( const std::vector<uint8_t> &data );

        static outcome::result<SGTransaction::DAGStruct> DeSerializeDAGStruct( const std::string &data );

        static SGTransaction::DAGStruct SetDAGWithType( SGTransaction::DAGStruct dag, const std::string &type )
        {
            dag.set_type( type );
            return dag;
        }

        virtual std::vector<uint8_t> SerializeByteVector( const SGTransaction::DAGStruct &dag ) const = 0;

        virtual EmbeddedTransaction SerializeToEmbeddedTransaction( const SGTransaction::DAGStruct &dag ) const = 0;

        EmbeddedTransaction SerializeToEmbeddedTransaction() const
        {
            return SerializeToEmbeddedTransaction( dag_st );
        }

        std::vector<uint8_t> SerializeByteVector() const
        {
            return SerializeByteVector( dag_st );
        }

        virtual bool HasUTXOParameters() const
        {
            return false;
        }

        virtual std::optional<UTXOTxParameters> GetUTXOParametersOpt() const
        {
            return std::nullopt;
        }

        virtual std::string GetChainId() const
        {
            return std::string( GENIUS_CHAIN_ID );
        }

        virtual std::string GetTransactionSpecificPath() const = 0;

        static std::string GetTransactionFullPath( const std::string &tx_hash )
        {
            return "tx/" + tx_hash;
        }

        std::string GetTransactionFullPath() const
        {
            return "tx/" + GetHash();
        }

        std::string GetProofFullPath() const
        {
            return "proof/" + GetHash();
        }

        std::string GetSrcAddress() const
        {
            return dag_st.source_addr();
        }

        [[nodiscard]] std::string GetHash() const;

        [[nodiscard]] std::string GetPreviousHash() const;

        [[nodiscard]] std::string GetUncleHash() const;

        uint64_t GetTimestamp() const
        {
            return dag_st.timestamp();
        }

        uint64_t GetNonce() const
        {
            return dag_st.nonce();
        }

        virtual std::unordered_set<std::string> GetTopics() const;

        void FillHash();

        bool CheckHash() const;

        std::vector<uint8_t> MakeSignature( GeniusAccount &account );

        bool CheckSignature() const;

        bool CheckDAGSignatureLegacy() const;

        virtual std::string GetSlotID() const
        {
            return GetSrcAddress() + ":" + std::to_string( GetNonce() );
        }

        SGTransaction::DAGStruct dag_st;

    private:
        static inline std::unordered_map<std::string, TransactionDeserializeFn> deserializers_map;
        const std::string transaction_type;

    public:
        static void RegisterDeserializer( const std::string &transaction_type, TransactionDeserializeFn fn )
        {
            deserializers_map[transaction_type] = std::move( fn );
        }

        static std::unordered_map<std::string, TransactionDeserializeFn> &GetDeSerializers()
        {
            return deserializers_map;
        }
    };
}

#endif // SGNS_GENIUS_TRANSACTION_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

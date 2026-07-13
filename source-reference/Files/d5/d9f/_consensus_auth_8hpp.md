---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/blockchain/ConsensusAuth.hpp
summary: Header-only helpers for consensus signing and validation. 

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/blockchain/ConsensusAuth.hpp



Header-only helpers for consensus signing and validation.  [More...](#detailed-description)

## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| outcome::result< std::vector< uint8_t > > | **[ProposalSigningBytes](/source-reference/Files/d5/d9f/_consensus_auth_8hpp/#function-proposalsigningbytes)**(const ConsensusProposal & proposal)<br/>Builds canonical bytes used to sign a consensus proposal.  |
| outcome::result< std::vector< uint8_t > > | **[VoteSigningBytes](/source-reference/Files/d5/d9f/_consensus_auth_8hpp/#function-votesigningbytes)**(const ConsensusVote & vote)<br/>Builds canonical bytes used to sign a consensus vote.  |
| outcome::result< std::vector< uint8_t > > | **[VoteBundleSigningBytes](/source-reference/Files/d5/d9f/_consensus_auth_8hpp/#function-votebundlesigningbytes)**(const ConsensusVoteBundle & bundle)<br/>Builds canonical bytes used to sign a consensus vote bundle.  |
| outcome::result< std::string > | **[ComputeProposalId](/source-reference/Files/d5/d9f/_consensus_auth_8hpp/#function-computeproposalid)**(const ConsensusProposal & proposal)<br/>Computes deterministic proposal id from proposal content.  |
| bool | **[ValidateProposal](/source-reference/Files/d5/d9f/_consensus_auth_8hpp/#function-validateproposal)**(const ConsensusProposal & proposal)<br/>Validates proposal basic shape, signature, and computed id.  |

## Detailed Description

Header-only helpers for consensus signing and validation. 

**Date**: 2026-02-07 Henrique A. Klein ([hklein@gnus.ai](mailto:hklein@gnus.ai)) 

## Functions Documentation

### function ProposalSigningBytes

```cpp
inline outcome::result< std::vector< uint8_t > > ProposalSigningBytes(
    const ConsensusProposal & proposal
)
```

Builds canonical bytes used to sign a consensus proposal. 

**Parameters**: 

  * **proposal** Proposal object to serialize for signing. 


**Return**: Serialized signing bytes on success, or `std::errc::invalid_argument` when protobuf serialization fails. 

The signature field is cleared before serialization so signatures are never part of their own signing payload.


### function VoteSigningBytes

```cpp
inline outcome::result< std::vector< uint8_t > > VoteSigningBytes(
    const ConsensusVote & vote
)
```

Builds canonical bytes used to sign a consensus vote. 

**Parameters**: 

  * **vote** Vote object to serialize for signing. 


**Return**: Serialized signing bytes on success, or `std::errc::invalid_argument` when protobuf serialization fails. 

The signature field is cleared before serialization so signatures are never part of their own signing payload.


### function VoteBundleSigningBytes

```cpp
inline outcome::result< std::vector< uint8_t > > VoteBundleSigningBytes(
    const ConsensusVoteBundle & bundle
)
```

Builds canonical bytes used to sign a consensus vote bundle. 

**Parameters**: 

  * **bundle** Vote bundle to serialize for signing. 


**Return**: Serialized signing bytes on success, or `std::errc::invalid_argument` when protobuf serialization fails. 

The signature field is cleared before serialization so signatures are never part of their own signing payload.


### function ComputeProposalId

```cpp
inline outcome::result< std::string > ComputeProposalId(
    const ConsensusProposal & proposal
)
```

Computes deterministic proposal id from proposal content. 

**Parameters**: 

  * **proposal** Proposal used to derive the identifier. 


**Return**: Lowercase hex SHA-256 proposal id on success, or propagated error when signing bytes cannot be produced. 

The proposal id field is cleared before hashing to guarantee stable id derivation from the signed payload content only.


### function ValidateProposal

```cpp
inline bool ValidateProposal(
    const ConsensusProposal & proposal
)
```

Validates proposal basic shape, signature, and computed id. 

**Parameters**: 

  * **proposal** Proposal to validate. 


**Return**: `true` when proposer id/signature/id are present, signature is valid, and computed proposal id matches; otherwise `false`. 



## Source code

```cpp

#ifndef SGNS_CONSENSUS_AUTH_HPP
#define SGNS_CONSENSUS_AUTH_HPP

#include <system_error>
#include <vector>

#include "account/GeniusAccount.hpp"
#include "base/hexutil.hpp"
#include "blockchain/impl/proto/Consensus.pb.h"
#include "crypto/hasher/hasher_impl.hpp"
#include <gsl/span>
#include "outcome/outcome.hpp"

namespace sgns
{
    inline outcome::result<std::vector<uint8_t>> ProposalSigningBytes( const ConsensusProposal &proposal )
    {
        ConsensusProposal copy = proposal;
        copy.clear_signature();
        std::string serialized;
        if ( !copy.SerializeToString( &serialized ) )
        {
            return outcome::failure( std::errc::invalid_argument );
        }
        return std::vector<uint8_t>( serialized.begin(), serialized.end() );
    }

    inline outcome::result<std::vector<uint8_t>> VoteSigningBytes( const ConsensusVote &vote )
    {
        ConsensusVote copy = vote;
        copy.clear_signature();
        std::string serialized;
        if ( !copy.SerializeToString( &serialized ) )
        {
            return outcome::failure( std::errc::invalid_argument );
        }
        return std::vector<uint8_t>( serialized.begin(), serialized.end() );
    }

    inline outcome::result<std::vector<uint8_t>> VoteBundleSigningBytes( const ConsensusVoteBundle &bundle )
    {
        ConsensusVoteBundle copy = bundle;
        copy.clear_signature();
        std::string serialized;
        if ( !copy.SerializeToString( &serialized ) )
        {
            return outcome::failure( std::errc::invalid_argument );
        }
        return std::vector<uint8_t>( serialized.begin(), serialized.end() );
    }

    inline outcome::result<std::string> ComputeProposalId( const ConsensusProposal &proposal )
    {
        ConsensusProposal copy = proposal;
        copy.clear_proposal_id();
        auto signing_bytes = ProposalSigningBytes( copy );
        if ( signing_bytes.has_error() )
        {
            return outcome::failure( signing_bytes.error() );
        }

        sgns::crypto::HasherImpl hasher;
        auto                     hash = hasher.sha2_256( signing_bytes.value().data(), signing_bytes.value().size() );
        return base::hex_lower( gsl::span<const uint8_t>( hash.data(), hash.size() ) );
    }

    inline bool ValidateProposal( const ConsensusProposal &proposal )
    {
        if ( proposal.proposer_id().empty() || proposal.signature().empty() || proposal.proposal_id().empty() )
        {
            return false;
        }

        auto signing_bytes = ProposalSigningBytes( proposal );
        if ( signing_bytes.has_error() )
        {
            return false;
        }

        if ( !GeniusAccount::VerifySignature( proposal.proposer_id(), proposal.signature(), signing_bytes.value() ) )
        {
            return false;
        }

        auto computed_id = ComputeProposalId( proposal );
        if ( computed_id.has_error() )
        {
            return false;
        }

        return computed_id.value() == proposal.proposal_id();
    }
}

#endif // SGNS_CONSENSUS_AUTH_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700

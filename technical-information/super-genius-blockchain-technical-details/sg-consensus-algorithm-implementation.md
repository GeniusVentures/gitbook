# SG Consensus Algorithm Implementation

> **Current implementation note (October 2026):** The message sequence below is an earlier protocol illustration, not a full specification of current validator admission or quorum. The current SuperGenius code has a genesis-seeded `TrustedPeerRegistry`, quorum-controlled membership updates, and `ValidatorRegistry` logic. General participation in compute jobs must not be confused with the validator/signer set. Consult the pinned source for current configuration and security assumptions. See [Platform Status](../../about-gnus.ai/release-status.md).

* SG Consensus algorithm is based on GOSSIP protocol.
* System uses libp2p library for P2P Gossip messaging.

**Gossip Message Types**

* BLOCK ANNOUNCE
* VERIFICATION
* TRANSACTIONS
* STATUS
* BLOCK REQUEST

Consensus protocol uses `VERIFICATION` gossip message for consensus process. There are two different types of VERIFICATION message

1. VOTE message
2. FIN message

There are three different types of Vote Messages\
\
**Primary Propose**\
Primary node broadcasts Primary Propose message to all nodes to validate a transaction.\
**Pre Vote**\
Nodes after receiving Primary Propose send Pre-Vote message (initial vote) to all other nodes.\
**Pre Commit**\
Nodes after receiving pre-votes from other nodes sends stronger commitment using pre-commit vote.<br>

**Vote Message Format**\
\| `Voting Round Number` | `Membership Counter` | `Message Data` |

## Consensus Protocol Message Sequences

```mermaid
sequenceDiagram
    PN->>N1: Primary Propose 
    PN->>N2: Primary Propose 
    N1->>N2: Pre-Vote
    PN->>N1: Pre-Vote
    PN->>N2: Pre-Vote
    N2->>N1: Pre-vote
    N2->>PN: Pre-Vote 
    N1->>PN: Pre-Vote 
    N2->>PN: Pre-Commit 
    PN->>N1: Pre-Commit
    N2->>N1: Pre-Commit
    N1->>PN: Pre-Commit
    N1->>N2: Pre-Commit
    PN->>N2: Pre-Commit 
    N1->>N2: Fin 
    PN->>N2: Fin
    PN->>N1: Fin
    N2->>PN: Fin
    N1->>PN: Fin 
    N2->>N1: Fin
```

# SG Consensus Algorithm Implementation

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

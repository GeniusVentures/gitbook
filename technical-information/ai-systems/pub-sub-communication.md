# Pub/Sub Communication

## Communication Workflow

- Queries and updates are handled through **libP2P pub/sub channels**.
- Fault-tolerant message propagation ensures that even if some nodes fail, others can handle the query.

```mermaid
graph LR
    PubSubChannel --> Node1[Edge Node 1]
    PubSubChannel --> Node2[Edge Node 2]
    Node1 --> Aggregator
    Node2 --> Aggregator
    Aggregator --> PubSubChannel
```

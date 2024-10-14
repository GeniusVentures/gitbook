# Overview

The GNUS.ai system integrates multiple open-source technologies to build a fully decentralized Retrieval-Augmented Generation (RAG) architecture. 
It leverages:

- **RocksDB over IPFS** for distributed storage and CRDT-based synchronization.
- **Vulkan shaders and ggml** for high-performance inference on GPUs.
- **MNN (Mobile Neural Network)** to dynamically load and execute models at the edge nodes.
- **Pub/Sub communication over libP2P** for distributed query handling across nodes.
- **Federated learning principles** to allow local model retraining and fine-tuning on each node.

This architecture ensures scalability, fault tolerance, and security while minimizing latency in both data access and inference.

```mermaid
graph TD;
    SystemArchitecture -->|Data Storage| RocksDB[Edge Nodes using RocksDB + IPFS]
    SystemArchitecture -->|Inference| Vulkan[Vulkan Accelerated Inference]
    SystemArchitecture -->|Communication| PubSub[libP2P Pub/Sub Channels]
    SystemArchitecture -->|Retraining| FL[Federated Learning Nodes]
    RocksDB -->|CRDT Syncing| IPFS[IPFS Cache]
    FL -->|Model Updates| EdgeNode1[Edge Node 1]
    FL -->|Model Updates| EdgeNode2[Edge Node 2]
```

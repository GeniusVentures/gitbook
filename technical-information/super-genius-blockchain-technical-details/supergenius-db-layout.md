---
description: This page explains the SuperGenius Layout of the CRDT database
---

# SuperGenius DB Layout

The storing of processing data, transaction data, proof data and blockchain data of SuperGenius is done in CRDT database. The storage is accessed by a Key-Value mechanism, where each type of data has a specific format of key, making sure that each SuperGenius node instantly knows how to construct the key to search for a specific value.

The processing data comes from splitting a Job into Macro and Micro Jobs. Their key format is expected to be:

```
Processing/${JobID}/${SubTaskID}/${ProtocolType}/Output
```

The IDs are assigned when the input data is split into workable packets, as for the Protocol Type is associated with the kind of protocol used for the processing (IPFS, MNN, file...)

The remainder of key types formats start with "bc-" followed by the 3 digit ID of the type of net being used.

```bash
bc-${net_iD}/
```

The blockchain data is store in the format:

```
bc-${net_ID}/blockchain/${blockNumber}/tx/${transactionNumber}
```

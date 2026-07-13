---
title: sgns::crdt

---

# sgns::crdt





## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::crdt::AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/)** <br/>[AtomicTransaction](/source-reference/Classes/d8/da6/classsgns_1_1crdt_1_1_atomic_transaction/) provides atomic multi-key operations for CRDT datastore All operations within a transaction are combined into a single delta and published atomically to ensure consistency.  |
| class | **[sgns::crdt::Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/)** <br/>A [Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/) provides a way to send (notify) an opaque payload to all replicas and to retrieve payloads broadcasted.  |
| class | **[sgns::crdt::CRDTCallbackManager](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/)**  |
| class | **[sgns::crdt::CRDTDataFilter](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/)**  |
| class | **[sgns::crdt::CrdtDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/)** <br/>Forward declaration of CRDT Set class.  |
| class | **[sgns::crdt::CrdtHeads](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/)** <br/>[CrdtHeads](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/) manages the current Merkle-CRDT heads.  |
| struct | **[sgns::crdt::CrdtOptions](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/)** <br/>Options holds configurable values for [CrdtDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/).  |
| class | **[sgns::crdt::CrdtSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/)** <br/>[CrdtSet](/source-reference/Classes/dd/d80/classsgns_1_1crdt_1_1_crdt_set/) implements an Add-Wins Observed-Remove Set using delta-CRDTs ([https://arxiv.org/abs/1410.2803](https://arxiv.org/abs/1410.2803)) and backing all the data in a datastore. It is fully agnostic to MerkleCRDTs or the delta distribution layer. It chooses the Value with most priority for a Key as the current Value. When two values have the same priority, it chooses by alphabetically sorting their unique IDs alphabetically.  |
| class | **[sgns::crdt::DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/)** <br/>A [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/) is an abstraction to an IPLD-based p2p storage layer. A [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/) is a DAGService with the ability to publish new ipld nodes to the network, and retrieving others from it.  |
| class | **[sgns::crdt::CRDTWorkJournal](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/)** <br/>Tracks key processing lifecycle persisted in RocksDB.  |
| class | **[sgns::crdt::GlobalDB](/source-reference/Classes/da/d32/classsgns_1_1crdt_1_1_global_d_b/)**  |
| class | **[sgns::crdt::KeyPairFileStorage](/source-reference/Classes/d6/d1e/classsgns_1_1crdt_1_1_key_pair_file_storage/)**  |
| class | **[sgns::crdt::PubSubBroadcaster](/source-reference/Classes/d7/df4/classsgns_1_1crdt_1_1_pub_sub_broadcaster/)**  |
| class | **[sgns::crdt::PubSubBroadcasterExt](/source-reference/Classes/da/d80/classsgns_1_1crdt_1_1_pub_sub_broadcaster_ext/)** <br/>Extended PubSub broadcaster that integrates with a CRDT datastore and Graphsync DAG syncer.  |
| class | **[sgns::crdt::GraphsyncDAGSyncer](/source-reference/Classes/d0/d05/classsgns_1_1crdt_1_1_graphsync_d_a_g_syncer/)** <br/>A [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/) is an abstraction to an IPLD-based p2p storage layer. A [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/) is a DAGService with the ability to publish new ipld nodes to the network, and retrieving others from it.  |
| class | **[sgns::crdt::HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/)** <br/>A Key represents the unique identifier of an object, inspired by file systems and Google App Engine key model. Keys are meant to be unique across a system. Keys are hierarchical, incorporating more and more specific namespaces. Thus keys can be deemed 'children' or 'ancestors' of other keys:: Key("/Comedy") Key("/Comedy/MontyPython") Also, every namespace can be parametrized to embed relevant object information. For example, the Key `name` (most specific namespace) could include the object type:: Key("/Comedy/MontyPython/Actor:JohnCleese") Key("/Comedy/MontyPython/Sketch:CheeseShop") Key("/Comedy/MontyPython/Sketch:CheeseShop/Character:Mousebender").  |

## Types

|                | Name           |
| -------------- | -------------- |
| using crdt::CrdtOptions | **[CrdtOptions](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#using-crdtoptions)**  |
| using crdt::CrdtDatastore | **[CrdtDatastore](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#using-crdtdatastore)**  |
| using crdt::HierarchicalKey | **[HierarchicalKey](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#using-hierarchicalkey)**  |
| using crdt::GraphsyncDAGSyncer | **[GraphsyncDAGSyncer](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#using-graphsyncdagsyncer)**  |
| using ipfs_lite::ipfs::RocksdbDatastore | **[RocksdbDatastore](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#using-rocksdbdatastore)**  |
| using ipfs_lite::rocksdb | **[IpfsRocksDb](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#using-ipfsrocksdb)**  |
| using ipfs_pubsub::GossipPubSub | **[GossipPubSub](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#using-gossippubsub)**  |
| using ipfs_lite::ipfs::graphsync::GraphsyncImpl | **[GraphsyncImpl](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#using-graphsyncimpl)**  |
| using libp2p::crypto::CryptoProviderImpl | **[CryptoProvider](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#using-cryptoprovider)**  |
| using libp2p::crypto::marshaller::KeyMarshallerImpl | **[KeyMarshaller](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#using-keymarshaller)**  |
| using libp2p::crypto::validator::KeyValidatorImpl | **[KeyValidator](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#using-keyvalidator)**  |
| using pb::CRDTBroadcast | **[CRDTBroadcast](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#using-crdtbroadcast)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| [base::Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) | **[CRDTSet](/source-reference/Namespaces/d4/dd0/namespacesgns_1_1crdt/#function-crdtset)**() |

## Types Documentation

### using CrdtOptions

```cpp
using sgns::crdt::CrdtOptions = crdt::CrdtOptions;
```


### using CrdtDatastore

```cpp
using sgns::crdt::CrdtDatastore = crdt::CrdtDatastore;
```


### using HierarchicalKey

```cpp
using sgns::crdt::HierarchicalKey = crdt::HierarchicalKey;
```


### using GraphsyncDAGSyncer

```cpp
using sgns::crdt::GraphsyncDAGSyncer = crdt::GraphsyncDAGSyncer;
```


### using RocksdbDatastore

```cpp
using sgns::crdt::RocksdbDatastore = ipfs_lite::ipfs::RocksdbDatastore;
```


### using IpfsRocksDb

```cpp
using sgns::crdt::IpfsRocksDb = ipfs_lite::rocksdb;
```


### using GossipPubSub

```cpp
using sgns::crdt::GossipPubSub = ipfs_pubsub::GossipPubSub;
```


### using GraphsyncImpl

```cpp
using sgns::crdt::GraphsyncImpl = ipfs_lite::ipfs::graphsync::GraphsyncImpl;
```


### using CryptoProvider

```cpp
using sgns::crdt::CryptoProvider = libp2p::crypto::CryptoProviderImpl;
```


### using KeyMarshaller

```cpp
using sgns::crdt::KeyMarshaller = libp2p::crypto::marshaller::KeyMarshallerImpl;
```


### using KeyValidator

```cpp
using sgns::crdt::KeyValidator = libp2p::crypto::validator::KeyValidatorImpl;
```


### using CRDTBroadcast

```cpp
using sgns::crdt::CRDTBroadcast = pb::CRDTBroadcast;
```



## Functions Documentation

### function CRDTSet

```cpp
base::Logger CRDTSet()
```






-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
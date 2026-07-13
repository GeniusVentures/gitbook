---
title: sgns::crdt::CrdtDatastore
summary: Forward declaration of CRDT Set class. 

---

# sgns::crdt::CrdtDatastore



Forward declaration of CRDT Set class.  [More...](#detailed-description)


`#include <crdt_datastore.hpp>`

Inherits from std::enable_shared_from_this< CrdtDatastore >

## Protected Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[RootCIDJob](/source-reference/Classes/d1/de1/structsgns_1_1crdt_1_1_crdt_datastore_1_1_root_c_i_d_job/)**  |
| struct | **[DagWorker](/source-reference/Classes/db/d23/structsgns_1_1crdt_1_1_crdt_datastore_1_1_dag_worker/)**  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| enum class| **[JobStatus](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#enum-jobstatus)** { PENDING, COMPLETED, FAILED} |
| enum class| **[Error](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#enum-error)** { INVALID_PARAM = 0, FETCH_ROOT_NODE, NODE_DESERIALIZATION, FETCHING_GRAPH, NODE_CREATION, GET_NODE, INVALID_JOB} |
| using [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) | **[Buffer](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-buffer)**  |
| using [base::Logger](/source-reference/Namespaces/d4/dcb/namespacesgns_1_1base/#using-logger) | **[Logger](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-logger)**  |
| using [storage::rocksdb](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/) | **[RocksDB](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-rocksdb)**  |
| using [RocksDB::QueryResult](/source-reference/Classes/d5/dbf/classsgns_1_1storage_1_1rocksdb/#using-queryresult) | **[QueryResult](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-queryresult)**  |
| using pb::Delta | **[Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta)**  |
| using pb::Element | **[Element](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-element)**  |
| using ipfs_lite::ipld::IPLDNode | **[IPLDNode](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-ipldnode)**  |
| using [CRDTDataFilter::ElementFilterCallback](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#using-elementfiltercallback) | **[CRDTElementFilterCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-crdtelementfiltercallback)**  |
| using [CRDTCallbackManager::NewDataCallback](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#using-newdatacallback) | **[CRDTNewElementCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-crdtnewelementcallback)**  |
| using [CRDTCallbackManager::DeletedDataCallback](/source-reference/Classes/d7/d42/classsgns_1_1crdt_1_1_c_r_d_t_callback_manager/#using-deleteddatacallback) | **[CRDTDeletedElementCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-crdtdeletedelementcallback)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| std::shared_ptr< [CrdtDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-crdtdatastore) > | **[New](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-new)**(std::shared_ptr< [RocksDB](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-rocksdb) > aDatastore, const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & aKey, std::shared_ptr< [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/) > aDagSyncer, std::shared_ptr< [Broadcaster](/source-reference/Classes/d9/de2/classsgns_1_1crdt_1_1_broadcaster/) > aBroadcaster, std::shared_ptr< [CrdtOptions](/source-reference/Classes/db/d77/structsgns_1_1crdt_1_1_crdt_options/) > aOptions)<br/>Factory method to create a shared_ptr to a [CrdtDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/).  |
| std::shared_ptr< [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) > | **[DeltaMerge](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-deltamerge)**(const std::shared_ptr< [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) > & aDelta1, const std::shared_ptr< [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) > & aDelta2) |
| std::string | **[GetValueSuffix](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-getvaluesuffix)**() |
| outcome::result< std::vector< CID > > | **[DecodeBroadcast](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-decodebroadcast)**(const [Buffer](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-buffer) & buff) |
| outcome::result< std::shared_ptr< [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) > > | **[CreateDeltaToAdd](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-createdeltatoadd)**(const std::string & key, const std::string & value) |
| void | **[Start](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-start)**()<br/>Starts the datastore threads.  |
| void | **[StartCIDProcessing](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-startcidprocessing)**() |
| void | **[StartRebroadcastHeads](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-startrebroadcastheads)**() |
| virtual | **[~CrdtDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-~crdtdatastore)**()<br/>Destructor of the CRDT datastore.  |
| outcome::result< [Buffer](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-buffer) > | **[GetKey](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-getkey)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & aKey) const |
| outcome::result< [QueryResult](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-queryresult) > | **[QueryKeyValues](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-querykeyvalues)**(std::string_view aPrefix) const |
| outcome::result< [QueryResult](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-queryresult) > | **[QueryKeyValues](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-querykeyvalues)**(const std::string & prefix_base, const std::string & middle_part, const std::string & remainder_prefix) const<br/>Queries with a middle part that can be a wildcard, negated string or normal string.  |
| std::string | **[GetKeysPrefix](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-getkeysprefix)**() const |
| outcome::result< CID > | **[PutKey](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-putkey)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & aKey, const [Buffer](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-buffer) & aValue, const std::unordered_set< std::string > & topics)<br/>Stores the given value in the CRDT store.  |
| outcome::result< bool > | **[HasKey](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-haskey)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & aKey) const |
| outcome::result< CID > | **[DeleteKey](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-deletekey)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & aKey, const std::unordered_set< std::string > & topics) |
| outcome::result< CID > | **[Publish](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-publish)**(const std::shared_ptr< [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) > & aDelta, const std::unordered_set< std::string > & topics)<br/>Publishes a [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta). Creates a DAG node from the given [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta), merges it into the CRDT, and broadcasts the node.  |
| outcome::result< void > | **[PrintDAG](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-printdag)**() |
| outcome::result< std::shared_ptr< [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) > > | **[CreateDeltaToRemove](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-createdeltatoremove)**(const std::string & key) const |
| void | **[PrintDataStore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-printdatastore)**() |
| void | **[Close](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-close)**() |
| void | **[CancelAndCloseNow](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-cancelandclosenow)**()<br/>Immediately cancels CRDT work and closes all worker threads. Safe to call multiple times.  |
| bool | **[RegisterElementFilter](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-registerelementfilter)**(const std::string & pattern, [CRDTElementFilterCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-crdtelementfiltercallback) filter) |
| bool | **[RegisterNewElementCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-registernewelementcallback)**(const std::string & pattern, [CRDTNewElementCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-crdtnewelementcallback) callback) |
| bool | **[RegisterDeletedElementCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-registerdeletedelementcallback)**(const std::string & pattern, [CRDTDeletedElementCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-crdtdeletedelementcallback) callback) |
| void | **[UnregisterElementFilter](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-unregisterelementfilter)**(const std::string & pattern) |
| void | **[UnregisterNewElementCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-unregisternewelementcallback)**(const std::string & pattern) |
| void | **[UnregisterDeletedElementCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-unregisterdeletedelementcallback)**(const std::string & pattern) |
| std::shared_ptr< [CRDTWorkJournal](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/) > | **[GetWorkJournal](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-getworkjournal)**() const |
| void | **[AddTopicName](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-addtopicname)**(const std::string & topic)<br/>Configure which topic this datastore should filter on.  |
| outcome::result< [CrdtHeads::CRDTListResult](/source-reference/Classes/d5/dea/classsgns_1_1crdt_1_1_crdt_heads/#using-crdtlistresult) > | **[GetHeadList](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-getheadlist)**() |
| outcome::result< void > | **[RemoveHead](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-removehead)**(const CID & aCid, const std::string & topic) |
| outcome::result< uint64_t > | **[GetHeadHeight](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-getheadheight)**(const CID & aCid, const std::string & topic) |
| outcome::result< void > | **[AddHead](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-addhead)**(const CID & aCid, const std::string & topic, uint64_t priority) |
| outcome::result< [JobStatus](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#enum-jobstatus) > | **[GetJobStatus](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-getjobstatus)**(const CID & cid) |
| outcome::result< void > | **[BroadcastHeadsForTopics](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-broadcastheadsfortopics)**(const std::set< std::string > & topics)<br/>Broadcast heads for the specified topics.  |
| bool | **[IsBroadcastEnabled](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-isbroadcastenabled)**() const<br/>Query whether outgoing head broadcasts are enabled.  |
| std::unordered_set< std::string > | **[GetTopicNames](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-gettopicnames)**() const |
| outcome::result< std::vector< std::pair< std::string, [base::Buffer](/source-reference/Classes/de/dd5/classsgns_1_1base_1_1_buffer/) > > > | **[GetILPDNodeContent](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-getilpdnodecontent)**(const std::string & cid_string) |

## Protected Functions

|                | Name           |
| -------------- | -------------- |
| void | **[HandleCIDBroadcast](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-handlecidbroadcast)**()<br/>Handles when a CID broadcast gets received If the CID is not known triggers [HandleRootCIDBlock](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-handlerootcidblock).  |
| outcome::result< void > | **[HandleRootCIDBlock](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-handlerootcidblock)**(const CID & aCid)<br/>Handles a root CID block by creating a job to fetch and process its content.  |
| outcome::result< [RootCIDJob](/source-reference/Classes/d1/de1/structsgns_1_1crdt_1_1_crdt_datastore_1_1_root_c_i_d_job/) > | **[CreateRootJob](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-createrootjob)**(const CID & aRootCID)<br/>Creates a [RootCIDJob](/source-reference/Classes/d1/de1/structsgns_1_1crdt_1_1_crdt_datastore_1_1_root_c_i_d_job/) for the given root CID.  |
| outcome::result< std::set< CID > > | **[GetLinksToFetch](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-getlinkstofetch)**(const [RootCIDJob](/source-reference/Classes/d1/de1/structsgns_1_1crdt_1_1_crdt_datastore_1_1_root_c_i_d_job/) & job)<br/>Gets the links to fetch for a given node in a job.  |
| outcome::result< void > | **[FetchNodes](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-fetchnodes)**(const [RootCIDJob](/source-reference/Classes/d1/de1/structsgns_1_1crdt_1_1_crdt_datastore_1_1_root_c_i_d_job/) & aRootJob, const std::set< CID > & aLinks)<br/>Fetches the nodes for the given links and root job.  |
| outcome::result< [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) > | **[GetDeltaFromNode](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-getdeltafromnode)**(const [IPLDNode](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-ipldnode) & aNode, bool created_by_self)<br/>Gets the [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) from a given IPLD node, filtering it if it wasn't created by self.  |
| outcome::result< void > | **[MergeDataFromDelta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-mergedatafromdelta)**(const CID & node_cid, const [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) & aDelta)<br/>Merges the data from a given [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) into the CRDT set.  |
| outcome::result< void > | **[ProcessJobIteration](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-processjobiteration)**(const [RootCIDJob](/source-reference/Classes/d1/de1/structsgns_1_1crdt_1_1_crdt_datastore_1_1_root_c_i_d_job/) & job_to_process)<br/>Processes A Root CID job.  |
| outcome::result< void > | **[Sync](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-sync)**(const [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) & aKey) |
| outcome::result< void > | **[PrintDAGRec](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-printdagrec)**(const CID & aCID, uint64_t aDepth, std::vector< CID > & aSet) |
| void | **[RebroadcastHeads](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-rebroadcastheads)**() |
| outcome::result< void > | **[Broadcast](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-broadcast)**(const std::set< CID > & cids, const std::string & topic, boost::optional< libp2p::peer::PeerInfo > peerInfo =boost::none)<br/>Broadcasts a set of CIDs. Encodes and broadcasts the provided list of CIDs.  |
| outcome::result< [Buffer](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-buffer) > | **[EncodeBroadcast](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-encodebroadcast)**(const std::set< CID > & heads) |
| outcome::result< std::shared_ptr< [IPLDNode](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-ipldnode) > > | **[CreateIPLDNode](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-createipldnode)**(const std::vector< std::pair< CID, std::string > > & aHeads, const std::shared_ptr< [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) > & aDelta, const std::unordered_set< std::string > & topics) const |
| outcome::result< std::shared_ptr< [IPLDNode](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-ipldnode) > > | **[CreateDAGNode](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-createdagnode)**(const std::shared_ptr< [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) > & aDelta, const std::unordered_set< std::string > & topics) |
| outcome::result< CID > | **[AddDAGNode](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-adddagnode)**(const std::shared_ptr< [CrdtDatastore::IPLDNode](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-ipldnode) > & node) |
| outcome::result< void > | **[SyncDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-syncdatastore)**(const std::vector< [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) > & aKeyList) |
| void | **[PutElementsCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-putelementscallback)**(const std::string & key, const [Buffer](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-buffer) & value, const std::string & cid) |
| void | **[DeleteElementsCallback](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-deleteelementscallback)**(const std::string & key, const std::string & cid) |
| void | **[UpdateCRDTHeads](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-updatecrdtheads)**(const CID & rootCID, uint64_t rootPriority, bool add_topics_to_broadcast) |
| bool | **[EnqueueRootCID](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-enqueuerootcid)**(const CID & cid) |
| outcome::result< CID > | **[WaitForJob](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-waitforjob)**(const CID & cid) |
| outcome::result< [Buffer](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-buffer) > | **[EncodeBroadcastStatic](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-encodebroadcaststatic)**(const std::set< CID > & heads) |

## Friends

|                | Name           |
| -------------- | -------------- |
| class | **[PubSubBroadcasterExt](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#friend-pubsubbroadcasterext)**  |

## Detailed Description

```cpp
class sgns::crdt::CrdtDatastore;
```

Forward declaration of CRDT Set class. 

CRDT datastore class based on [https://github.com/ipfs/go-ds-crdt](https://github.com/ipfs/go-ds-crdt)

## Public Types Documentation

### enum JobStatus

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| PENDING | |   |
| COMPLETED | |   |
| FAILED | |   |




### enum Error

| Enumerator | Value | Description |
| ---------- | ----- | ----------- |
| INVALID_PARAM | 0|   |
| FETCH_ROOT_NODE | |   |
| NODE_DESERIALIZATION | |   |
| FETCHING_GRAPH | |   |
| NODE_CREATION | |   |
| GET_NODE | |   |
| INVALID_JOB | |   |




### using Buffer

```cpp
using sgns::crdt::CrdtDatastore::Buffer = base::Buffer;
```


### using Logger

```cpp
using sgns::crdt::CrdtDatastore::Logger = base::Logger;
```


### using RocksDB

```cpp
using sgns::crdt::CrdtDatastore::RocksDB = storage::rocksdb;
```


### using QueryResult

```cpp
using sgns::crdt::CrdtDatastore::QueryResult = RocksDB::QueryResult;
```


### using Delta

```cpp
using sgns::crdt::CrdtDatastore::Delta = pb::Delta;
```


### using Element

```cpp
using sgns::crdt::CrdtDatastore::Element = pb::Element;
```


### using IPLDNode

```cpp
using sgns::crdt::CrdtDatastore::IPLDNode = ipfs_lite::ipld::IPLDNode;
```


### using CRDTElementFilterCallback

```cpp
using sgns::crdt::CrdtDatastore::CRDTElementFilterCallback = CRDTDataFilter::ElementFilterCallback;
```


### using CRDTNewElementCallback

```cpp
using sgns::crdt::CrdtDatastore::CRDTNewElementCallback = CRDTCallbackManager::NewDataCallback;
```


### using CRDTDeletedElementCallback

```cpp
using sgns::crdt::CrdtDatastore::CRDTDeletedElementCallback = CRDTCallbackManager::DeletedDataCallback;
```


## Public Functions Documentation

### function New

```cpp
static std::shared_ptr< CrdtDatastore > New(
    std::shared_ptr< RocksDB > aDatastore,
    const HierarchicalKey & aKey,
    std::shared_ptr< DAGSyncer > aDagSyncer,
    std::shared_ptr< Broadcaster > aBroadcaster,
    std::shared_ptr< CrdtOptions > aOptions
)
```

Factory method to create a shared_ptr to a [CrdtDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/). 

**Parameters**: 

  * **aDatastore** The underlying database where CRDT is stored 
  * **aKey** The namespace key on the database where CRDT's variables will be stored 
  * **aDagSyncer** The MerkleDAG syncer to request content of CIDs 
  * **aBroadcaster** The broadcaster to publish CIDs 
  * **aOptions** Options to construct the object 


**Return**: A new instance of [CrdtDatastore](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/)

### function DeltaMerge

```cpp
static std::shared_ptr< Delta > DeltaMerge(
    const std::shared_ptr< Delta > & aDelta1,
    const std::shared_ptr< Delta > & aDelta2
)
```


**Parameters**: 

  * **aDelta1** [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) to merge 
  * **aDelta2** [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) to merge 


**Return**: pointer to merged delta 

Static function to merge delta elements and tombstones, use highest priority for the result delta 


### function GetValueSuffix

```cpp
static std::string GetValueSuffix()
```


**Return**: value suffix 

Get value suffix used in set, e.g. /v 


### function DecodeBroadcast

```cpp
static outcome::result< std::vector< CID > > DecodeBroadcast(
    const Buffer & buff
)
```


**Parameters**: 

  * **buff** [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) data to decode 


**Return**: vector of CIDs or outcome::failure on error 

DecodeBroadcast decodes CRDT broadcast data 


### function CreateDeltaToAdd

```cpp
static outcome::result< std::shared_ptr< Delta > > CreateDeltaToAdd(
    const std::string & key,
    const std::string & value
)
```


**Parameters**: 

  * **key** - delta key to add to datastore 
  * **value** - delta value to add to datastore 


**Return**: pointer to new delta or outcome::failure on error 

Returns a new delta-set adding the given key/value. 


### function Start

```cpp
void Start()
```

Starts the datastore threads. 

### function StartCIDProcessing

```cpp
void StartCIDProcessing()
```


### function StartRebroadcastHeads

```cpp
void StartRebroadcastHeads()
```


### function ~CrdtDatastore

```cpp
virtual ~CrdtDatastore()
```

Destructor of the CRDT datastore. 

### function GetKey

```cpp
outcome::result< Buffer > GetKey(
    const HierarchicalKey & aKey
) const
```


**Parameters**: 

  * **aKey** Hierarchical key to get 


**Return**: value as a [Buffer](/source-reference/Classes/d5/d2a/class_buffer/)

Get the value of an element not tombstoned from the CRDT set by key 


### function QueryKeyValues

```cpp
outcome::result< QueryResult > QueryKeyValues(
    std::string_view aPrefix
) const
```


**Parameters**: 

  * **aPrefix** prefix to search, if empty string, return all 


**Return**: list of key-value pairs matches prefix 

Query CRDT set key-value pairs by prefix, if prefix empty return all elements are not tombstoned 


### function QueryKeyValues

```cpp
outcome::result< QueryResult > QueryKeyValues(
    const std::string & prefix_base,
    const std::string & middle_part,
    const std::string & remainder_prefix
) const
```

Queries with a middle part that can be a wildcard, negated string or normal string. 

**Parameters**: 

  * **prefix_base** The base prefix to query 
  * **middle_part** Either a string (normal query), '*' or !string 
  * **remainder_prefix** The remainder part of the query prefix 


**Return**: A list of key value pairs 

### function GetKeysPrefix

```cpp
std::string GetKeysPrefix() const
```


**Return**: key prefix 

Get key prefix used in set, e.g. /namespace/s/k/ 


### function PutKey

```cpp
outcome::result< CID > PutKey(
    const HierarchicalKey & aKey,
    const Buffer & aValue,
    const std::unordered_set< std::string > & topics
)
```

Stores the given value in the CRDT store. 

**Parameters**: 

  * **aKey** Hierarchical key to put 
  * **aValue** Value to be stored 
  * **topics** Topics to publish to 


**Return**: outcome::success if stored and broadcasted successfully, or outcome::failure otherwise. 

### function HasKey

```cpp
outcome::result< bool > HasKey(
    const HierarchicalKey & aKey
) const
```


**Parameters**: 

  * **aKey** [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) to look for in set 


**Return**: true if key found or false if not found or outcome::failure on error 

HasKey returns whether the `key` is mapped to a `value` in set 


### function DeleteKey

```cpp
outcome::result< CID > DeleteKey(
    const HierarchicalKey & aKey,
    const std::unordered_set< std::string > & topics
)
```


**Parameters**: 

  * **aKey** [HierarchicalKey](/source-reference/Classes/d6/dfe/classsgns_1_1crdt_1_1_hierarchical_key/) to delete from set 
  * **topics** Topics to publish to 


**Return**: outcome::failure on error or success otherwise 

Delete removes the value for given `key`. 


### function Publish

```cpp
outcome::result< CID > Publish(
    const std::shared_ptr< Delta > & aDelta,
    const std::unordered_set< std::string > & topics
)
```

Publishes a [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta). Creates a DAG node from the given [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta), merges it into the CRDT, and broadcasts the node. 

**Parameters**: 

  * **aDelta** [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) to publish 
  * **topics** Topics to publish to 


**Return**: returns outcome::success on success or outcome::failure otherwise 

### function PrintDAG

```cpp
outcome::result< void > PrintDAG()
```


**Return**: returns outcome::success on success or outcome::failure otherwise 

PrintDAG pretty prints the current Merkle-DAG using the given printFunc 


### function CreateDeltaToRemove

```cpp
outcome::result< std::shared_ptr< Delta > > CreateDeltaToRemove(
    const std::string & key
) const
```


**Parameters**: 

  * **key** - delta key to remove from datastore 


**Return**: pointer to delta or outcome::failure on error 

Returns a new delta-set removing the given keys with prefix /namespace/s/key 


### function PrintDataStore

```cpp
void PrintDataStore()
```


### function Close

```cpp
void Close()
```


Close shuts down the CRDT datastore and worker threads. It should not be used afterwards. 


### function CancelAndCloseNow

```cpp
void CancelAndCloseNow()
```

Immediately cancels CRDT work and closes all worker threads. Safe to call multiple times. 

### function RegisterElementFilter

```cpp
bool RegisterElementFilter(
    const std::string & pattern,
    CRDTElementFilterCallback filter
)
```


### function RegisterNewElementCallback

```cpp
bool RegisterNewElementCallback(
    const std::string & pattern,
    CRDTNewElementCallback callback
)
```


### function RegisterDeletedElementCallback

```cpp
bool RegisterDeletedElementCallback(
    const std::string & pattern,
    CRDTDeletedElementCallback callback
)
```


### function UnregisterElementFilter

```cpp
void UnregisterElementFilter(
    const std::string & pattern
)
```


### function UnregisterNewElementCallback

```cpp
void UnregisterNewElementCallback(
    const std::string & pattern
)
```


### function UnregisterDeletedElementCallback

```cpp
void UnregisterDeletedElementCallback(
    const std::string & pattern
)
```


### function GetWorkJournal

```cpp
std::shared_ptr< CRDTWorkJournal > GetWorkJournal() const
```


### function AddTopicName

```cpp
void AddTopicName(
    const std::string & topic
)
```

Configure which topic this datastore should filter on. 

**Parameters**: 

  * **topic** The topic name to use when filtering links. Only links whose `IPLDLinkImpl::getName()` equals this string will be processed. 


When processing or rebroadcasting Merkle-DAG links, only those whose name exactly matches the topic set via this call will be considered.


### function GetHeadList

```cpp
outcome::result< CrdtHeads::CRDTListResult > GetHeadList()
```


### function RemoveHead

```cpp
outcome::result< void > RemoveHead(
    const CID & aCid,
    const std::string & topic
)
```


### function GetHeadHeight

```cpp
outcome::result< uint64_t > GetHeadHeight(
    const CID & aCid,
    const std::string & topic
)
```


### function AddHead

```cpp
outcome::result< void > AddHead(
    const CID & aCid,
    const std::string & topic,
    uint64_t priority
)
```


### function GetJobStatus

```cpp
outcome::result< JobStatus > GetJobStatus(
    const CID & cid
)
```


### function BroadcastHeadsForTopics

```cpp
outcome::result< void > BroadcastHeadsForTopics(
    const std::set< std::string > & topics
)
```

Broadcast heads for the specified topics. 

**Parameters**: 

  * **topics** Vector of topic names to broadcast heads for 


**Return**: outcome::success on success, or outcome::failure on error 

### function IsBroadcastEnabled

```cpp
bool IsBroadcastEnabled() const
```

Query whether outgoing head broadcasts are enabled. 

**Return**: true when broadcasts are enabled. 

### function GetTopicNames

```cpp
std::unordered_set< std::string > GetTopicNames() const
```


### function GetILPDNodeContent

```cpp
outcome::result< std::vector< std::pair< std::string, base::Buffer > > > GetILPDNodeContent(
    const std::string & cid_string
)
```


## Protected Functions Documentation

### function HandleCIDBroadcast

```cpp
void HandleCIDBroadcast()
```

Handles when a CID broadcast gets received If the CID is not known triggers [HandleRootCIDBlock](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-handlerootcidblock). 

### function HandleRootCIDBlock

```cpp
outcome::result< void > HandleRootCIDBlock(
    const CID & aCid
)
```

Handles a root CID block by creating a job to fetch and process its content. 

**Parameters**: 

  * **aCid** The root CID to be handled 


**Return**: Success if the Root Job was created, or failure otherwise 

### function CreateRootJob

```cpp
outcome::result< RootCIDJob > CreateRootJob(
    const CID & aRootCID
)
```

Creates a [RootCIDJob](/source-reference/Classes/d1/de1/structsgns_1_1crdt_1_1_crdt_datastore_1_1_root_c_i_d_job/) for the given root CID. 

**Parameters**: 

  * **aRootCID** The root CID to create the job for 


**Return**: Success if Root Job created, or failure otherwise 

### function GetLinksToFetch

```cpp
outcome::result< std::set< CID > > GetLinksToFetch(
    const RootCIDJob & job
)
```

Gets the links to fetch for a given node in a job. 

**Parameters**: 

  * **job** The root job of the current links to fetch 


**Return**: List of CIDs to fetch, or failure otherwise 

### function FetchNodes

```cpp
outcome::result< void > FetchNodes(
    const RootCIDJob & aRootJob,
    const std::set< CID > & aLinks
)
```

Fetches the nodes for the given links and root job. 

**Parameters**: 

  * **aRootJob** The root job of the current links to fetch 
  * **aLinks** The links to fetch 


**Return**: Success if the nodes were fetched, or failure otherwise 

### function GetDeltaFromNode

```cpp
outcome::result< Delta > GetDeltaFromNode(
    const IPLDNode & aNode,
    bool created_by_self
)
```

Gets the [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) from a given IPLD node, filtering it if it wasn't created by self. 

**Parameters**: 

  * **aNode** The IPLD node to get the [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) from 
  * **created_by_self** True if the node was created by self, false otherwise 


**Return**: The [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) contained in the node, or failure otherwise 

### function MergeDataFromDelta

```cpp
outcome::result< void > MergeDataFromDelta(
    const CID & node_cid,
    const Delta & aDelta
)
```

Merges the data from a given [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) into the CRDT set. 

**Parameters**: 

  * **node_cid** The CID of the node from which the [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) was obtained 
  * **aDelta** The [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) to be merged 


**Return**: Success if the [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) was merged, or failure otherwise 

### function ProcessJobIteration

```cpp
outcome::result< void > ProcessJobIteration(
    const RootCIDJob & job_to_process
)
```

Processes A Root CID job. 

**Parameters**: 

  * **job_to_process** The job received by either [HandleCIDBroadcast](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-handlecidbroadcast) or by [AddDAGNode](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#function-adddagnode)


**Return**: Success if the job was processed, or failure otherwise 

### function Sync

```cpp
outcome::result< void > Sync(
    const HierarchicalKey & aKey
)
```


**Return**: returns outcome::success on success or outcome::failure otherwise 

Sync ensures that all the data under the given prefix is flushed to disk in the underlying datastore 


### function PrintDAGRec

```cpp
outcome::result< void > PrintDAGRec(
    const CID & aCID,
    uint64_t aDepth,
    std::vector< CID > & aSet
)
```


**Parameters**: 

  * **aCID** CID of DAG record 
  * **aDepth** depth used for indenting printed records 
  * **aSet** set of CIDs to print 


**Return**: returns outcome::success on success or outcome::failure otherwise 

Helper funtion to print Merkle-DAG records 


### function RebroadcastHeads

```cpp
void RebroadcastHeads()
```


Regularly send out a list of heads that we have not recently seen 


### function Broadcast

```cpp
outcome::result< void > Broadcast(
    const std::set< CID > & cids,
    const std::string & topic,
    boost::optional< libp2p::peer::PeerInfo > peerInfo =boost::none
)
```

Broadcasts a set of CIDs. Encodes and broadcasts the provided list of CIDs. 

**Parameters**: 

  * **cids** The list of CIDs to broadcast. 
  * **topic** The topic to broadcast to. 
  * **peerInfo** Optional peer info to avoid repeated GetPeerInfo calls. 


**Return**: outcome::success on success, or outcome::failure if an error occurs. 

### function EncodeBroadcast

```cpp
outcome::result< Buffer > EncodeBroadcast(
    const std::set< CID > & heads
)
```


**Parameters**: 

  * **heads** list of CIDs 


**Return**: data encoded into [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) data or outcome::failure on error 

EncodeBroadcast encodes list of CIDs to CRDT broadcast data 


### function CreateIPLDNode

```cpp
outcome::result< std::shared_ptr< IPLDNode > > CreateIPLDNode(
    const std::vector< std::pair< CID, std::string > > & aHeads,
    const std::shared_ptr< Delta > & aDelta,
    const std::unordered_set< std::string > & topics
) const
```


**Parameters**: 

  * **aHeads** list of CIDs to add to node as IPLD links 
  * **aDelta** [Delta](/source-reference/Classes/db/dbb/classsgns_1_1crdt_1_1_crdt_datastore/#using-delta) to serialize into IPLD node 
  * **topics** Topics to add as links 


**Return**: IPLD node or outcome::failure on error 

CreateIPLDNode add block node to [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/)


### function CreateDAGNode

```cpp
outcome::result< std::shared_ptr< IPLDNode > > CreateDAGNode(
    const std::shared_ptr< Delta > & aDelta,
    const std::unordered_set< std::string > & topics
)
```


### function AddDAGNode

```cpp
outcome::result< CID > AddDAGNode(
    const std::shared_ptr< CrdtDatastore::IPLDNode > & node
)
```


**Parameters**: 

  * **node** Node to add and process 


**Return**: CID or outcome::failure on error 

AddDAGNode adds node to [DAGSyncer](/source-reference/Classes/d5/d05/classsgns_1_1crdt_1_1_d_a_g_syncer/) and processes new blocks. 


### function SyncDatastore

```cpp
outcome::result< void > SyncDatastore(
    const std::vector< HierarchicalKey > & aKeyList
)
```


**Parameters**: 

  * **aKeyList** all heads and the set entries related to the given prefix 


**Return**: returns outcome::success on success or outcome::failure otherwise 

SyncDatastore sync heads and set datastore 


### function PutElementsCallback

```cpp
void PutElementsCallback(
    const std::string & key,
    const Buffer & value,
    const std::string & cid
)
```


### function DeleteElementsCallback

```cpp
void DeleteElementsCallback(
    const std::string & key,
    const std::string & cid
)
```


### function UpdateCRDTHeads

```cpp
void UpdateCRDTHeads(
    const CID & rootCID,
    uint64_t rootPriority,
    bool add_topics_to_broadcast
)
```


### function EnqueueRootCID

```cpp
bool EnqueueRootCID(
    const CID & cid
)
```


### function WaitForJob

```cpp
outcome::result< CID > WaitForJob(
    const CID & cid
)
```


### function EncodeBroadcastStatic

```cpp
static outcome::result< Buffer > EncodeBroadcastStatic(
    const std::set< CID > & heads
)
```


**Parameters**: 

  * **heads** list of CIDs 


**Return**: data encoded into [Buffer](/source-reference/Classes/d5/d2a/class_buffer/) data or outcome::failure on error 

EncodeBroadcastStatic encodes list of CIDs to CRDT broadcast data 


## Friends

### friend PubSubBroadcasterExt

```cpp
friend class PubSubBroadcasterExt(
    PubSubBroadcasterExt 
);
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
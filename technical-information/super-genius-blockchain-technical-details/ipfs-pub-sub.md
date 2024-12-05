# IPFS Pub Sub

## Description

Pub/Sub in general uses ifps-pubsub library which is using the libp2p [gossip protocol](https://docs.libp2p.io/concepts/publish-subscribe/)

All communications should be defined in OpenAPI yaml files under the project gRPCForSuperGenius.

The readme for how to generate C++ code is in the README.md in that project

## Processing pub/sub

After a processing block is in the database, the processing nodes (clients device), syncs to the database using CRDT system. Once they find a node to be processed they use pub/sub to Join or Create pub/sub room for processing a set of blocks.

On the SGNUS SDK side, it should be fairly straightforward to make functions for multiple devices, basically using pub/sub over ipfs to communicate to find microjobs. The node grabbing the job can break it up into 10 microjobs and publish a channel. The channel could have jobprocessing\_%BLOCKID% in which BLOCKID is the CRDT database node that contains the processing information.

Each of these rooms would then have a sub-room which is the microjobs #. For instance, if there are 1,000 sub-blocks to process, then there would be 100 1,000/10 microjob rooms.

jobprocessing\_%BLOCKID%\_%MICROJOB% pub/sub channel/room

The pub/sub ARE nodes to find microjobs, this is very similar to a game player looking for a lobby to join a peer-to-peer game.

The pub/sub to find jobs is basically a cache of jobs in the queue eventually.

Each processing node will use the function in Genius SDK to get MicroJob and then publish the results. Right now the processing can be stubbed out like this.

```cpp

// This comes from the Dapp and randomSeed if used to choose verifier block.
typedef struct _JOB {
  UUID ipfsBlock;                // source block data to be processed
  unsigned long BlockLen;        // and ipfs block's length in bytes
  unsigned long BlockStride;     // Stride to use for access pattern
  unsigned long BlockLineStride; // Line stride in bytes to get to next block start
  float randomSeed;              // used to randomly choose verifier block
  PUBSUBCHANNEL resultsChannel;  // which channel to publish results to.
} JOB;

typedef struct _PROCESSSUBCHUNKS {
  UUID chunkID;                   // unique process chunk ID
  unsigned long Offset;           // offset into data
  unsigned long SubChunkWidth;    // width of subchunk/subblock
  unsigned long SubChunkHeight;   // height of chunk/block
  unsigned long Stride;           // stride to use for overall data chunk
  unsigned long LineStride;       // stride of one line of data
  unsigned long nSubChunks;       // number of chunks to process  
} PROCESSSUBCHUNKS;


typedef struct _MICROJOB {
  UUID ipfsBlock;                 // source block data to be processed
  PROCESSSUBCHUNK chunksToProcess[]; // array of chunks to process
  unsigned long datalen;          // length of ipfs Block?
  PUBSUBCHANNEL resultsChannel;   // channel to publish results to
} MICROJOB;

typedef struct _RESULTSMICROJOB {
  unsigned long resultHash;       // hash of results
  unsigned long chunkHashes[];    // the hashes for each chunk
  UUID ipfsResultsData;           // UUID of the results data on ipfs
} RESULTSMICROJOB;

// node that created processing channel
DoProcessing(JOB *job) {
   MICROJOBS microJobs[] = SplitJob(job);
   
   for (unsigned long i = 0; i < microjobs; i++) {
      PublishMessage(DoProcessing, micrfoJobs[i], uniquePeerID);
   }
}

// each Peer ID
DoProcessing(MICROJOB *mjob, UUID peerID) {

    if (peerID != myUUID) {
       // won't validate because hash will be incorrect
       return;
    }


    RESULTSMICROJOB resultsMicroJob = ProcessSubChunks(chunksToProcess[i], peerID);

    unsigned long hashCode = peerID;
    for (unsigned long i = 0; i< resultsMicroJob->chunkHashes.size; i+=) {
       hashCode ^= resultsMicroJob->chunkHashes[i];
    }
    
    resultsMicroJob->results = hashCode;
    AddSGNUSPendingBlock(resultsMicroJob);
    PublishResults(resultsMicroJob);
   }
}
```

## Handling of processing grid structure changes

If a host leaves, somebody else will have to take the position by either recreating the microjob list or grabbing it on the first entry into the room.

Also if a peer leaves the room (drops connection) or doesn't respond within XX timelimit for processing, they get kicked out of the room so another can process the data. Each room (pub/sub topic) also has a limit of # processors to join. Probably 11 to start. 10 processors and 1 verifier node. The verifier is randomly chosen and it is unknown by anybody even the verifier until all processing is done and they have to submit to SGNUS node that processing is complete and verified.

## Processing Chunks.

A Chunk structure is defined to allow widths and strides (line and block) to be able to define sub-blocks within a data stream.

# Verification and Hash Results from Processing

## Jobs/Macro Jobs/Micro Jobs, oh my!

A job is a set of data that will be processed using AI/ML learning/inference models and the results stored back into a stream (IPFS, websockets, FTP, etc). Currently, we will only support IFPS.

#### Job Creation and Escrow

When a Job request is started via the Wallet/Dapp, that node/device is responsible for opening an Escrow and depositing GNUS tokens to be distributed to the nodes that process the jobs. (Job Requestor)

The Job Requestor will first make a read-only call to get a unique ID to be used as a pseudo random seed.

This will be used as the starting point of a pseudo random number generator for slicing and selecting the verifier node of the JOB

The Job Requestor then makes a call to the EVM contract (Polygon RPC call) to open up an Escrow. This will cost MATIC gas fees and GNUS tokens, TODO: Gasless fees how to do that?

#### Slicing

A slicer slices the Job into Macro Jobs, Micro jobs using block size that as predefined default values.

The slicing code will produce N+1 Microjobs. The +1 is the verification data in which the slicer selects 1 block from each of the other microjob blocks randomly and places them into the N+1 microjob. Nodes will not know if they are verifying or processing data.

The N+1 blocks use the same GPU code so will generate a hash for a block. The micro job saves hashes, not a single hash of the microjob, it saves a hash per block of the microjob.

The slicer will have predefine defines for the size of blocks in the code which can be overridden/changed in the dapp. For instance.

This is an example of the default values that can be used to slice the AI/ML data to be processed

```C++
#define MICROJOB_BLOCK_WIDTH = 256;
#define MCROJOB_BLOCK_HEIGHT = 256;
#define MICROJOB_X_BLOCK_COUNT = 4;
#define MICROJOB_Y_BLOCK_COUNT = 4;

#define MICROJOB_BLOCK_SIZE = (MICROJOB_BLOCK_WIDTH*MCROJOB_BLOCK_HEIGHT * sizeof(FLOAT32))
#define MICROJOB_SIZE = (MICROJOB_X_BLOCK_COUNT * MCROJOB__Y_BLOCK_COUNT) * MICROJOB_BLOCK_SIZE
```

This would make 1024x1024 \* 32-bit float data (4 MegaBytes of data) to process for a microjob.

A macro job could have 10 of these for 40 Megabytes of data.

A Job could have 5 of these for 200 Megabytes of data

The number of hashes generated would be 16 (MICROJOB\_X\_BLOCK\_COUNT \* MICROJOB\_Y\_BLOCK\_COUNT) for each microjob. These values are store with the processed data in the data storage (currently only IPFS).

## Finalization (Signing) of Microblocks

Once an Escrow is opened for a Job to be completed on the EVM blockchain (Ethereum, Polygon, etc). There are a few parameters stored in the blockchain for the job. These will all be used with [Zokrates](https://github.com/Zokrates/ZoKrates) Solidity code for verification

```Solidity
struct EscrowAIJob {
   uint256 ownerAddress;
   uint256 SliceParameterEncoding;  // zkSnark encoding of slicing parameters & timestamp & previous Super Genius block hash
   bool isFinalized;
};
```

Storage in Super Genius Blockchain DB/chain

```Solidity
struct ProcessedJobInfo {
  uint microJobBlockNumber;        // the index of the microjob processed
  uint256 hashOfDataProcessed;     // hash of the data processed
  struct Hashes {
    uint256 blockHash;             // hash of base struct not including hashes & SliceParameterEncoding from AI Escrow Job & previous block hash
    uint256 signature;           // signature of everything except signedBlock
  }
}
```

When calling Zokrates (ZKSnark) solidity code for signing of microjobs sets. Zokrates Implementation Info

* Assumes 10 microjob(s) \* 10 blocks processes + 1 verify job \* 10 blocks processed
* Last node of this job, sends all hashes in an array and internal Zokrates code gets JOB id and starting pseudo random number to pick out the verifier nodes hashes and can index other nodes hashes for verification.
* The Solidity contract can also verify the merkle nodes match back up to the root hash of microjobs processed
* This constructs the indices of the matches, step must be odd
  * i.e. Found matching hashOfDataProcessed in microjob 1 at index 5 etc., indices should match SliceParameterEncoding
    * Example (5, 6, 7, 8, 9, 0, 1, 2, 3, 4) hashed, step 1
    * Another Example (5, 8, 1, 4, 7, 0, 3, 6, 9, 2) hashed, step 3

Pseudo Code function call in EVM contract. Zokrates encodes this into ZKSnark Solidity Code. Calls to RPC blockchain will be gas free since these are just public view (read-only) functions.

```Solidity
   // Close Escrow Code
   CloseEscrow(uint256 jobID, uint256 signature, uint256 prevBlockHash, ProcessedJobInfo[] jobInfo, address nodeProcessors[], uint256 amounts[]) public {
        require(EscrowAI.Jobs[jobID].finalized != true);
        require(verifyZKSignature(jobInfo, prevBlockHash));
        _mintBatch(nodeProcessors, amounts);
        // set internal job finalized and
        EscrowAI.Jobs[jobID].finalized = true;
   }
```

```Solidity
   // Zokrates code
   function getZKSignature(ProcessedJobInfo[] jobInfo, uint256 indexHash) public view returns (uint256 signature) {
       uint256 indexStart, step = decode(EscrowAIJob.SliceParameterEncoding);
       uint256 verifiedHashStart = (indexStart * step * 10) % 11;
       uint verifiedIndex = 0;
       uint matchingBlocks = 0;
       for (uint i = indexStart; i < 10; i += step) {
         if (jobInfo[i].hashOfDataProcessed == jobInfo[verifiedIndex++].hashOfDataProcessed) {
           matchingBlocks++;
         }
       return keccak256(indexHash, matchingBlocks);
   }
```

```Solidity
   function verifyZKSignature(ProcessedJobInfo jobInfo, uint256 previousBlockHash) public view returns (boolean) {
      return wasSigned(jobInfo.signature, EscrowAIJob.SlicingParameterEncoding, jobInfo.Hashes.blockHash, previousBlockHash); 
        
   }

```

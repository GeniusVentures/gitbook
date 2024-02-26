# Job Processing Flow

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

All queueing of Jobs/MacroJobs/MicroJobs uses a locking queue with a timeout to handle node dropouts/disconnects when joining a room for a MicroJob or creating a MacroJob room. When querying open jobs (Jobs, MacroJobs, MicroJobs), it is the union of jobs that have exceeded the timestamp lock & jobs that have not been previously locked.

### Job Placement

DApp creates a Job:

1. DApp specifies the job code (shader/Tensorflow/OpenCL) and the URI to source from (IPFS/SFTP/WS/HTTPS).
2. DApp specifies Job data URI to source from (IPFS/SFTP/WS/HTTPS).
3. DApp fills a JobInfo structure, including Job slicing parameters and seed for the random number generator, and places it into CRDT.
4. Dapp Slices Job with slicing parameters and creates MacroJobs & MicroJobs with random IDs from random seed saving into the CRDT DB.
5. DApp doesn't need to wait until job completion as the Super Genius BlockChain will create blocks verified using zkSnarks. &#x20;

### Processing node initialization

1. Once a Job processor is started, it is linked/synced to CRDT DB.
2. Create or Join Jobs PubSub Channel (first bootstrap node should do this)

### Job Processing

1. The job processor asks for open jobs via the PubSub Channel. If none exist, loop here (step 3)
2. Join Job{ID}/MacroJob PubSub channel

### MacroJob Processing

1. The Job processor asks for open MacroJobs from the PubSub Channel. CRDT is not used as MacroJobs storage.
2.  if MacroJob open, Join Job{id}/MacroJob{id} Channel, goto 'MicroJob Processing'.

    \*\*\* This can also, in the future, check for the locality of processing nodes
3. If no MacroJobs are open, go to 'Job Processing'.
4. **Create an in-memory MicroJob queue and set itself as the current queue owner. To create a validation MicroJob, a random number generator should be used with a seed equal to Job input seed + MacroJob index {id}**
5. **Create PubSub channel Job{id}/MacroJob{id} and notify the Job PubSub channel about the created MacroJob channel.**
6. Job Processor joins MacroJob PubSub Channel.
7. Go to MicroJob Processing

### MicroJob Processing

1. Job Processor requests for in-memory MicroJob queue via PubSub. Once a Microjob queue owner receives the request, it marks the requestor as the current queue owner and sends the queue to PubSub. Note: All Processors receive the updated in-memory queue, but only the current queue owner can operate with it.
2. The job processor receives the MicrJobs queue. If it is marked as the current queue, it checks for an open Microjob, marks it with timeout timestamp/lock, and notifies PubSub Channel.
3. The Job processor applies the coding algorithm for data blocks specified in the MicroJob.
4. The job processor writes MicroJob processing results into CRDT when the MicroJob processing is finished. a. Data should be written to IPFS b. CRDT record should be written with Job{ID}/MacroJob{ID}/MicroJob{ID} = data: { wallet address, hashes of processed blocks } + hash (Job{ID}/MacroJob{ID}/MicroJob{ID} & data) c. Job processor publishes to Job channel, 1 MicroJob is complete
5. Job Processor checks if the final MicroJob for a Job. If so, jump to Job Finalization.
6. Job processor checks if there are non-processed Micro Jobs and repeats p.1-6 until all Micro Jobs are processed.
7. Go to 'Macro Job Processing'

### Job Finalization.

1. When a Job processor finishes a MicroJob processing, it checks if the Job's MicroJob count finished equals the MicroJob count.
2. if not, go to Job Processing
3. Last, MicroJob scans MacroJobs and finds verifier hashes by checking all MicroJob hashes to see which matches the other ten nodes' hashes.
4. It sends this hash to the Smart Contract along with wallet addresses to release the Escrow
5.  Smart Contract ZkSnark algorithm can verify because {ID}'s are generated from RandomSeed, encrypted with zkSnark

    \*\*\* If the smart contract fails to verify. The culprit can be figured out by getting the index of the MacroJob verifier node and checking hashes against other non-verifier nodes to find the mismatch.

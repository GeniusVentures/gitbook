# AI Data Blocks

## AI Processing Data blocks pulled from ipfs via IPFS CID/UUID

Chunk processing is similar to how jpeg blocks are processed but block size can be anything 4x4, 8x8, 12x16, etc.

It also is very similar to how a GPU handles tiling.

![GPU-Tiling](<../../.gitbook/assets/GPU Tiling.png>)

## Job Data Structure.

(Picture of Soccer Player in Picture Above)

```
typedef struct _JOB {
  IPFSCID ipfsBlock;             // source block data to be processed
  IPFSCID ipfsProgramBlock;      // can be an array 
  unsigned long BlockLen;        // and ipfs block's length in bytes
  unsigned long BlockStride;     // Stride to use for access pattern
  unsigned long BlockLineStride; // Line stride in bytes to get to next block start
  float randomSeed;              // used to randomly choose verifier block
  UUID resultsChannelUUID;       // results written to CRDT database unique ID (/blockchain/{BlockChainID}/{resultsChannelUUID}/{MacroJobUUID}/{MicrojobUUID}
} JOB;
```

## Chunk (Macro & Micro Job) Data Structure

(Macro -> Grid in picture Block-n, Block m are Macro jobs, AC01, AC07 & Tiles in second picture are Microjobs)

```
typedef struct PROCESSCHUNK {
  IPFSCID dataChunkID;            // the UUID of the data chunk to be processed
  IFPSCID programChunkID;         // the UUID of the program to run on the data (ipfs CID)
  unsigned long Offset;           // offset into data
  unsigned long SubChunkWidth;    // width of subchunk/subblock
  unsigned long SubChunkHeight;   // height of chunk/block
  unsigned long Stride;           // stride to use for overall data chunk
  unsigned long LineStride;       // stride of one line of data
  unsigned long nSubChunks;       // number of chunks to process (this breaks down into microjobs) 
  UUID chunkUUID;                 // the macro/micro job id to use for writing results
} PROCESSCHUNK;

```

## Access Patterns of the Chunk/Blocks of Data

The block stride is the number of bytes to get you to the next block.

* if block stride = width of block in bytes, then processing of blocks source the blocks horizontally.
* if block stride = line width of data \* height of block, then processing of blocks source the blocks vertically
* Other access patterns can be achieved
  * for instance if block stride = 2 \* width of data \* height of block, then processing of blocks will source every 2nd block in the horizontal direction

Those parameters allow you sample in any pattern. Blocks could be top to bottom in a column, you can sample in a row or even diagonally given block stride value

The line stride is the number of bytes to get you to the next line in the block (usually the width of the data).

The block width is the number of bytes in single line of a block. Height of the block is the number of lines of the block.

Offset is starting byte position of ipfs data.

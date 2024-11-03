# Slicing Data for Macro MicroJobs

MacroJobs and Microjobs using slicing parameters for access patterns. One of the nodes (randomly chosen) uses a slicing pattern that includes an extra block to skip so that verifier node grabs 1/10th of the blocks from the each of the other nodes.

```
// temporary testing
RanomSeed(gettime() ^ 0xdeadc0de);

int getContractRandom() {
// call ETH contract to get RandomSeed
// return eth.call.getContractRandom();
  // dummy for now
  return Random();
}

RandomSeed(getContractRandom());
for (int i=0; i< nMacroJobs; i++) {
  macroJob[i].randomSeed = Random() + i;
  macroJob[i].UUID = GetUUUD();
}

#define MICROJOB_COUNT 10
// create Microjobs
void CreateMicroJobs(MacroJob *macroJob) {

RandomSeed(macroJob.randomSeed);
int verifier_node = Random(1, MICROJOB_COUNT);
for (int i=0; i< MICROJOB_COUNT + 1; i++)
{
  if(i != verifier_node) {
    SliceData(&macroJob->sliceParameters, &microjob[i], 0, MICROJOB_COUNT);
  } else {
    uint offset = Random(1, MICROJOB_COUNT) * microJobBlockSize; 
    SliceRandomData(&macroJob->sliceparameters, &microjob[i], offset, MICROJOB_COUNT+1);
}
 
// SliceData creates slicing parameters for Microjob
SliceData(SliceParameters *sliceParameters, MicroJob *microJob, uint offset, uint nextBlock)
{
  microjob->slicingParameters.offset = offset;
  microjob->slicingParameters.nextBlock = nextBlock;

  // Copy macroJob->slicingParameters or calculate rest of them
   
} 
```

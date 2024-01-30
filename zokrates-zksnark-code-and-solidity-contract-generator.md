# Zokrates/ZKSnark Code and Solidity Contract Generator

Zokrates is used to code the ZKSnark circuit code to be able to verify the 'Random Stride Hash Parity Verifier Checks' (soon to be a patent application) system.

You will need to compile Zokrates with rust compiler on your machine in the Zokrates submodule directory of THE TokenContracts repo https://github.com/GeniusVentures/TokenContracts.

In the submodule gnus-ai the directory zokrates contains the SGVerifer.zok file which compiles to SGVerifier.sol file (WIP). This is the ZKSnark verifier code is written in Zokrates. All compiling, etc., is done directly in the gnus-ai/zokrates directory to generate the gnus-ai/contracts/SGVerifier.sol file

Testing should be in main directory of gnus-ai and use the mocha/typescript system already built in.

For Zokrates to be be able to generate the public keys from the witness, there should be an abi.json file that is written (**SGVerifierSample-abi.json**) and used in genSol.sh and is used to generate witness public keys. This is the format of the abi.json files. [JSON ABI - ZoKrates](https://zokrates.github.io/toolbox/abi.html)

Here is an example of the commands that are executed to generate the solidity file for the project. These should be located in genSol.sh (WIP). The genSol.sh file should be added to the main gnus-ai build to preprocess and build all the .zok files under zokrates directory prior to running the solidity compiler.

```
../../ZoKrates/target/release/zokrates compile -i SGVerifier.zok -o SGVerifier.zkbin --stdlib-path=../../ZoKrates/zokrates_stdlib/stdlib/`
```

This generates the witness and proof keys

```
../../ZoKrates/target/release/zokrates compute-witness --verbose -i SGVerifier.zkbin -s SGVerifierSample-abi.json
../../ZoKrates/target/release/zokrates generate-proof -i SGVerifier.zkbin
```

This verifies the proof

```
../../ZoKrates/target/release/zokrate verify 
```

The abi data is the parameters to the main function inside SGVerifier.zok, which is a random seed (which will be encoded by the public witness key) and the data block header(s) from the SuperGenius processed data and the previously processed uncle block (which the proof doesn't check, but he solidity wrapper code will check)

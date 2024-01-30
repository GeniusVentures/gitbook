# GNUS.ai Technicial Details

The code is based on the following patent:

[Distributed General Purpose Computing System with CryptoToken Payment System - Patent #US11451393](https://github.com/GeniusVentures/GeniusTokens/files/10827213/US11451393-final.pdf)

## This is the general flow of the Genius Tokens system

![Genius CryptoToken Process-Flow](<../../.gitbook/assets/Process Flow print.jpg>)

## These are the components of the System

* Generic BlockChain CryptoToken = Ethereum based smart contract using an Escrow like system that feeds the “Real” POW hash codes to Smart Contract to check consensus. Wiki/Repo
* Communication Component = ipfs pub/sub using Gossip protocol. Wiki/Repo
* Proof of Work Component = partially built, but gathers all “real” POW from all nodes and passes them to the smart contract for consensus check
* Directed Acyclic CryptoToken = Partially built DAG system built off of IPFS DAG, POW/POS Blended Consensys. Wiki/Repo
* Distributed File System = ipfs-lite (already built) Wiki/Repo
* Delivery/Storage Component – RocksDB with ipfs backing, CRDT library needs to be integrated as full DAG is stored on ifps and branch roots and sub-branches need to be synchronized
  * https://arxiv.org/abs/2004.00107 paper on similar system
  * CRDT cpp library is available. [Repo](https://github.com/CBaquero/delta-enabled-crdts), ipfs-lite, [RocksDB](https://github.com/facebook/rocksdb/), ifps pub/sub gossip are already integrated.
* CryptoToken Wallet = Flutter/Parabeac design and Dart code in development, Wallet is actually Wallet for two Crypto’s Genius Token (GNUS) and SuperGenius Token (SGNUS) and DApp combined. Wiki/Repo
* Processing Component = Work to be done by for integration with Games/App Shader/OpenCL processing will be part of SDK. Wiki/Repo
* Software Development Kit API = work to be done for interface to Processing Component and checking wallet balance for In-App Purchases. Wiki/Repo
* (Not Shown) Third Party support library, includes cross Platform libraries for Boost, GSL, GTest, Curl, Cryptopp, 25519, flutter, Parabeac, gnostic, grpc, hat-trie, ipfs-lite-cpp, openssl, json, leveldb, libp2p, lmdb rapidjson, restclient-cpp, spdlog Repo

### Please adhere to the coding standards documentation

C++ Coding Standards

### Preferred contributor guidelines

* Use the develop branch unless you are working on a major change that you think will be hard to fix breaking the develop branch, or is a major feature then use a feature branch and do a pull request to the develop branch.
* Use git rebase instead of merge [Here's Why](https://spin.atomicobject.com/2017/04/23/maintain-clean-git-history/)
* Pulls to master will be done on an as-needed basis, since we are in MVP, this won't be very often.

### Also please read this blog about the appropriate way to use git rebase workflows.

[Git Rebase Workflow](https://nvie.com/posts/a-successful-git-branching-model/)

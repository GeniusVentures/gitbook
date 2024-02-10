---
description: The prover specification (variables, types, general structure)
---

# Prover specification

For each SuperGenius set of keys, the prover will generate a KDF, deriving a new shared secret to be used by the Verifier and Revealer. This secret can be used to derive a new Bitcoin/Ethereum address to avoid using the original address.&#x20;

As mentioned in the KDF explanation, the account key will be composed of the currency address and the SuperGenius KDF private key:

```cpp
struct{
  uint256 publicAddress;   ///< Public BTC/ETH address
  uint256 KDFPrivateKey;   ///< KDF private key
  std::Array<uint8> proof; ///< proof of correctly created account
} EncryptedAccount;
```

The encryption of the data would then be verified in zkSnark and stored in SuperGenius in CRDT, under /Accounts/\<new KDF public key>/EncryptedAccount.

The transaction's structure will hold the number of transactions, GNUS token IDs, an El Gamal encrypted amount field, and a proof or an aggregate proof (folding, etc):

```cpp
struct {
  uint256 nTransactions;    ///< Non-encrypted number of tokenIDs and Amounts
  uint256 tokenID[];        ///< Non-encrypted GNUS ERC1155 token IDs (could be child tokens array)
  uint256 Amount[];         ///< Exponential El Gamal encrypted amounts
  std::Array<uint8> proof;  ///< proof of valid account transfer
  } Transactions;
```

---
description: The prover specification (variables, types, general structure)
---

# Prover specification

For each SuperGenius set of keys the prover will generate a KDF, deriving a new shared secret to be used by the Verifier and Revealer. This secret can be used to derive a new Bitcoin/Ethereum address to avoid using the original address.&#x20;

As mentioned on the KDF explanation, the account key will be composed by the currency address and the SuperGenius KDF private key:

```cpp
struct{
  uint256 publicAddress; ///<Public BTC/ETH address
  uint256 KDFPrivateKey; ///<KDF private key
} EncryptedAccount;
```

The encryption of the data would then be verified in zkSnark and it would be stored in SuperGenius in CRDT, under /Accounts/\<new KDF public key>/EncryptedAccount.

The transactions structure will hold the number of transactions, GNUS token IDs and an El Gamal encryped amount field:

```cpp
struct {
  uint256 nTransactions;///< Non-encrypted number of tokenIDs and Amounts
  uint256 tokenID[];    ///< Non-encrypted GNUS ERC1155 token IDs (could be child tokens array)
  uint256 Amount[];     ///< Exponential El Gamal encrypted amounts
} Transactions;
```

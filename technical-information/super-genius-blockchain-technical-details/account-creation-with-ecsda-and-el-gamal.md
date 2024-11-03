# Account creation with ECSDA and El Gamal

#### System Overview

This system utilizes ECDSA (Elliptic Curve Digital Signature Algorithm) keys from a user's current wallet to initiate a multi-step process that securely manages and encrypts wallet keys and signatures.  Specifically the Trust Wallet core functionality, upon which the GNUS wallet is based, initializes by importing addresses (e.g. BTC, ETH) or, otherwise, creating new ECDSA keys and addresses for these (non-GNUS) L1s.  These will be called "Original Keys" and "Original Addresses".  With each Original Key so imported or created, the GNUS wallet then generates additional keys and addresses ("Proxy Keys" and "Proxy Addresses") that, among other things, provides privacy of Original Addresses.  That is, for tokens bridged in or out of the GNUS network, only Proxy Addresses appear on the GNUS network.

#### Step-by-Step Process

1. **ECDSA Proxy Address Generation**:
   * Whenever a new Original Key is imported or created, the GNUS wallet will then generate a corresponding L1 proxy ECDSA key-pair and address ("Proxy Keys").  For this, the GNUS network retains a fixed set of predefined ElGamal key pairs ("Gate Keys").  The system signs (with the current private Original Key) a public Gate Key, selected as a function of the user's Original Key, and feeds this "K-Seed" into a  [key-derivation-function.md](key-derivation-function.md "mention") (KDF), which deterministically returns a value ("Key Gen") to be used to generate the Proxy Key pairs and addresses.&#x20;
2. **ElGamal Key Generation**:
   * The KDF-derived Key Gen value is then also used to generate ElGamal encryption keys. This step introduces an additional layer of cryptographic security, enabling secure message encryption and decryption capabilities.
3. **Encryption with ElGamal Keys**:
   * The system then utilizes one Gate Key to encrypt the K-Seed (ECDSA signature) and the private Proxy Key. This encrypted data ensures that sensitive information, such as signatures and private keys, is securely stored and transmitted.
4. **Regeneration of KDF Keys**:
   * Users do not need to store their KDF keys across sessions. Instead, these keys can be deterministically regenerated using the original ECDSA signature. This feature simplifies key management and enhances security by reducing the need to store sensitive information.
5. **Integration with zk-SNARKs**:
   * Although the newly derived KDF could theoretically be used in various cryptographic applications, its direct use as a prover key in a zk-SNARK system is unlikely due to the circuit-specific nature of zk-SNARK proofs and the requirement for a Universal Common Reference String (CRS). However, this does not preclude its use in other aspects of a zk-SNARK-based system or in ensuring privacy and security through other means.

A pseudo-code of the account creation is shown below:

```cpp
BitcoinNode CreateAccount( const ECDSA<private_key> &prvt_key )
{
    auto elgamal_pubkey_predefined = GetAddressFromTable();

    auto cypher_signature = prvt_key.sign(elgamal_pubkey_predefined);

    auto new_derived_key_value = GenerateKDF(cypher_signature);

    BitcoinNode proxy_bitcoin_node(new_derived_key_value);
    ELGamal<key_pair> new_keys_elgamal(new_derived_key_value);

    auto encrypted_signature = new_keys_elgamal.encrypt(cypher_signature);
    auto encrypted_kdf = new_keys_elgamal.encrypt(new_derived_key_value);

    CRDT.store(encrypted_signature);
    CRDT.store(encrypted_kdf);

    return proxy_bitcoin_node;

}
```

#### Security and Privacy Implications

This system is designed with a focus on security and privacy, leveraging the strengths of ECDSA, KDF, and ElGamal encryption to protect user data and transactions. The ability to encrypt key information and signatures with ElGamal keys, coupled with the privacy offered by proxy addresses and the security of deterministic KDF key regeneration, provides a robust framework for secure and private cryptocurrency transactions.

#### Conclusion

The described cryptographic system offers a comprehensive approach to enhancing security and privacy in cryptocurrency transactions. By integrating ECDSA, KDF, and ElGamal encryption, and acknowledging the potential (though circuit-specific) integration with zk-SNARKs, it presents a sophisticated model for secure cryptographic operations within the blockchain ecosystem.

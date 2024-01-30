# Key Derivation Function - Shared Secret Generation

This module aims to generate a shared secret between the Proof System and the SuperGenius System and a new derived key.

The Prover will have its own private keys for Ethereum/Bitcoin, which will be used to sign public keys from SuperGenius. The signed message will be used as a seed for creating a new derived key. Both data will be concatenated and encoded with a session key calculated using ECDH, meaning SuperGenius could decode and verify the validity of the signed message and retrieve the new derived key.

This signed message is a private parameter for zksnarks, so it doesn't need encrypting.

This way, each Bitcoin/Ethereum address and SuperGenius key will have a unique value associated with it- an account key.

For now the proposed interfaces will constitute of a method that receives a private key and a public key string and returns a encrypted message with the signed data and the new derived key for this pair:

```
string GenerateSharedSecret(const private_key &key, const string &sgnus_pub_key_value);
```

The interface on the other side will enable the new key decoding and validate it by verifying the signature:

```
scalar_field_value GetNewKeyFromSecret(const string &secret, const string &signer_key, const string &own_key);
```

The result is a scalar value, that will be the new private key value.

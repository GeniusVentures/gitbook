# Key Derivation Function

This module creates a new derived value from an input data vector. The creation is deterministic and fast and it aims to generate a new value by hashing the input data. The output value rive new keys and consequently addresses.

The input data must map to a relation between a private ECDSA key and a public key value.  &#x20;

```
uint256_t GenerateKDF(const vector<uint8_t> &data);
```

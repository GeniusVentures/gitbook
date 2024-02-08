---
description: The El Gamal scheme is used to provide asymmetric and homomorphic encryption
---

# El Gamal encryption

To enable safe sensitive data communication El Gamal was chosen due to its ability to have homomorphism and its asymmetric nature.

For each input number $$r$$ El Gamal encryption generates a pair of  cypher text data $$C_1C_2$$using the public parameters prime $$p$$, generator $$g$$ and public key value $$x$$. The cypher text is not deterministic, meaning a randomness factor is inserted in the encryption, which increases the security of the encrypted data.&#x20;

The decryption process also uses the public parameters $$p$$ and $$g$$ but needs the private key $$y$$which defines the scheme as asymmetric.&#x20;

El Gamal scheme by default has multiplicative homomorphism, meaning that the encryption of the multiplication of raw data is equal to the multiplication of encrypted data, i.e:

$$C_1C_2(x*y) = C_1C_2(x) * C_1C_2(y)$$

Although the application for this characteristic is not directly useful for this project, it indirectly allows additive homomorphism if we use the input data as exponents, being that multiplication of same base operands result in addition of its exponents, so this result in the following scheme for additive homomorphism:

$$C_1C_2(g^{x+y}) = C_1C_2(g^x) * C_1C_2(g^y)$$

This process has a downside as the resulting decryption will retrieve $$g^{x+y}$$instead of $$x+y$$. To retrieve the original data the ECDLP would have to be solved, which depending on size of $$x$$and $$y$$ is not feasible. However in zkSnarks context we intend to prove the validity of a transaction withou needing to reveal the actual value, thus atending to the project's needs.

For data that doesn't require additive homomorphism there's no need to encode the original input as exponents, meaning the decryption will avoid having to solve the ECDLP. In this project the raw data encryption will also be used on other sensitive data, such as the KDF secret sharing.

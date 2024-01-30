# Pedersen Commitments

### Pedersen Commitments Pairs for Blinding Factors and Values <a href="#pedersen-commitments-pairs-for-blinding-factors-and-values" id="pedersen-commitments-pairs-for-blinding-factors-and-values"></a>

This document provides an overview of an advanced cryptographic concept involving two types of Pedersen commitments that are paired: PCBF (Pedersen Commitment for Blinding Factors) and PCValue (Pedersen Commitment for Values). It explores the mathematical foundation and practical applications of these paired commitments in cryptographic systems, including the use of a zero-based blinding factor in the PCBF during operations on PCValue.

#### 1. Pedersen Commitments <a href="#pedersen-commitments" id="pedersen-commitments"></a>

Pedersen commitments are a cryptographic tool used for committing to a chosen value while keeping it hidden, with the ability to reveal the committed value later. They are widely used in various cryptographic protocols to ensure data integrity and confidentiality.

**1.1 PCBF (Pedersen Commitment for Blinding Factors)**

The PCBF is a type of Pedersen commitment specifically designed to securely handle blinding factors. Blinding factors are random values used in cryptographic commitments to ensure that the actual value remains hidden.

The mathematical representation of a PCBF commitment is expressed as:

where:

*   > &#x20;and  are the public generators of the group

    > &#x20;is the blinding factor

    > &#x20;is the value to be committed

**1.2 PCValue (Pedersen Commitment for Values)**

The PCValue commitment is used to securely commit to actual values such as account balances or transaction amounts. Like PCBF, it utilizes a blinding factor to maintain the confidentiality of the value.

The mathematical representation of a PCValue commitment is expressed as:

where:

*   > &#x20;and  are the public generators of the group

    > &#x20;is the value to be committed

    > &#x20;is the blinding factor

#### 2. Integration of PCBF and PCValue in Cryptographic Systems <a href="#integration-of-pcbf-and-pcvalue-in-cryptographic-systems" id="integration-of-pcbf-and-pcvalue-in-cryptographic-systems"></a>

In advanced cryptographic systems, PCBF and PCValue work together to enhance security. While PCValue commitments secure actual values, PCBF commitments manage the blinding factors, adding an additional layer of security.

**2.1 Mathematical Foundation**

The mathematical foundation of Pedersen commitments relies on the properties of cyclic groups and modular arithmetic. Both PCBF and PCValue leverage these principles to secure data.

**2.2 Updating the PCValue Commitment**

Updating the PCValue commitment involves modifying its value while maintaining the blinding factor associated with the original PCBF. This process differs from the simple addition of  and .

**2.2.1 Updating the Blinding Factor**

To update the blinding factor, the following steps are performed:

*   > Generate a random value: Choose a random value  to act as the new blinding factor component.

    > Create a PCBF with zero blinding factor: Create a temporary PCBF commitment using  as the blinding factor and zero as the value.

    > Update the PCBF containing : Use Pedersen's AddMod operation to add the temporary PCBF commitment to the original PCBF containing . This results in a modified PCBF with the updated blinding factor .

The diagram depicts the process of updating the blinding factor values that will be used in a PCValue commitment using a zero-based blinding factor. It involves generating a random value , creating a temporary PCBF with  and zero as the blinding factor, adding the temporary PCBF to the original PCBF containing , and updating the PCBF value to , which is the new blinding factor for the updated PCValue commitment value , creating a temporary PCBF with  and zero as the blinding factor, adding the temporary PCBF to the original PCBF containing , and updating the PCBF value to , which is the new blinding factor for the updated PCValue commitment value

**2.2.2 Updating the Value**

Once the blinding factor is updated, the PCValue commitment can be updated accordingly:

#### 2.3 Opening the Updated Commitment <a href="#opening-the-updated-commitment" id="opening-the-updated-commitment"></a>

To retrieve the stored value from the updated PCValue commitment, the original creator, who knows , can use it along with  to validate the commitment and decode the value.

Mathematical Equations

The mathematical equations for updating the PCValue commitment are summarized below:

* > Updating Blinding Factor:
* > Updating Value:

#### 2.4 Enhanced Blinding Using Key Derivation Function and Ethereum Public Keys <a href="#enhanced-blinding-using-key-derivation-function-and-ethereum-public-keys" id="enhanced-blinding-using-key-derivation-function-and-ethereum-public-keys"></a>

To further augment the privacy and security aspects of the PCValue commitments, an advanced technique involving a Key Derivation Function (KDF) and dual encryption with Ethereum public keys has been introduced. This method provides an additional layer of security, particularly pertinent in the context of blockchain technology and cryptocurrency transactions.

**2.4.1 Key Derivation Function (KDF)**

A KDF is employed to create a set of sophisticated encryption keys from an initial secret value. This secret value, fundamental in the encryption process, yields robust keys crucial for maintaining transaction privacy and security.

**2.4.2 Dual Encryption Process**

Enhancing the blinding of PCValue commitments involves encrypting the user's Ethereum wallet address, concatenated with a secret value from the KDF. This concatenated string undergoes a two-step encryption process:

*   > First Layer of Encryption: Utilizing the user's public Ethereum key, the first layer of encryption ensures that the data is intrinsically linked to the user's identity within the Ethereum network.

    > Second Layer of Encryption: To bolster security, the same string is also encrypted using a backend or host’s public Ethereum key. This dual-layer approach significantly enhances the commitment's resilience against unauthorized access and potential security threats.

**2.4.3 Application in Initial Blinding Value**

This encrypted value serves as the initial blinding value for the PCValue commitment. By starting with an account balance of zero, it not only secures the commitment but also preserves the confidentiality of the account balance from the outset.

**2.4.4 Consistency with PCBF**

In line with ensuring comprehensive security, the same initial blinding value is employed in the initial PCBF and its commitment value. This harmonization between PCValue and PCBF guarantees that both the blinding factors and the values they safeguard are enveloped within this enhanced privacy framework.

#### Conclusion <a href="#conclusion" id="conclusion"></a>

Pedersen commitments, specifically the paired use of PCBF (Pedersen Commitment for Blinding Factors) and PCValue (Pedersen Commitment for Values), stand as a powerful cryptographic tool in the realm of data security and confidentiality. These commitments allow for secure and verifiable commitment to values while ensuring that only authorized parties can reveal the committed values.

The integration of PCBF and PCValue in cryptographic systems has been further advanced with the introduction of enhanced blinding techniques. The use of a Key Derivation Function (KDF) combined with dual encryption employing Ethereum public keys significantly elevates the security and privacy of these commitments. This innovative approach ensures that both the values (such as account balances) and the blinding factors (which protect these values) are enveloped in a robust layer of privacy.

By encrypting the concatenated string of the user's Ethereum wallet address and a secret KDF value with both the user’s and a backend/host’s public keys, we achieve a dual-layered security mechanism. This not only protects the PCValue commitments from unauthorized access but also maintains the confidentiality of account balances from the onset. The consistency of this enhanced blinding technique across both PCValue and PCBF further strengthens the overall cryptographic system.

In conclusion, the use of paired PCBF and PCValue commitments, complemented with advanced blinding techniques involving KDF and Ethereum public keys, showcases a significant stride in cryptographic innovation. This approach not only fortifies the privacy and security of blockchain applications but also sets a new standard for confidentiality in various cryptographic protocols, including zero-knowledge proofs and anonymous credentials.

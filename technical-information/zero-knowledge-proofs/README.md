# Zero Knowledge Proofs

Proofs in the context of zk-rollups (zero-knowledge rollups) are a form of cryptographic evidence that validates all transactions in a rollup block without revealing the actual data of those transactions. Here’s a simplified breakdown:

> **What Are zk-Rollups?**
>
> zk-Rollups are a type of Layer 2 scaling solution for blockchains like Ethereum. They help in scaling by processing transactions off the main chain (Layer 1) while ensuring the security and decentralization of the network.

### Zero-Knowledge Proofs <a href="#zero-knowledge-proofs" id="zero-knowledge-proofs"></a>

In blockchain, there are several types of zero-knowledge proofs (ZKPs) which vary in their interaction model and cryptographic techniques:​**zk-SNARKs**zk-SNARKs are the most well-known ZKP protocol, valued for their quick verification times and minimal proof sizes. Initially, they required a "trusted setup," posing potential security risks, but newer versions have mitigated these concerns with trustless implementations using Multi-Party Computation (MPC). **Bulletproofs** Introduced as a scalable solution, Bulletproofs' proof sizes increase logarithmically with the number of inputs, improving over linear-sized proofs. They eliminate the need for a trusted setup, enhancing security, although they lack quantum resistance.**Zk-STARKs: The latest ZKP technology, zk-STARKs, offers transparency and quantum resistance** without needing a trusted setup. They are considered more scalable with more straightforward assumptions at the cost of larger proof sizes than zk-SNARKs.​

| Feature        | zk-SNARKs                                 | Bulletproofs                 | zk-STARKs                        |
| -------------- | ----------------------------------------- | ---------------------------- | -------------------------------- |
| Trusted Setup  | Required (traditional), optional (recent) | Not required                 | Not required                     |
| Proof Size     | Small (\~0.2kB)                           | Medium (logarithmic scaling) | Large (\~50kB)                   |
| Quantum Safety | No (traditional), Yes (recent)            | No                           | Yes                              |
| Computational  | Fast proving, very fast verifying         | Slower proving and verifying | Faster proving, slower verifying |
| Transparency   | No (traditional), Yes (recent)            | Yes                          | Yes                              |
| Scalability    | High (with trustless setup)               | High                         | Higher due to simple assumptions |

#### Why we choose zk-SNARKs <a href="#why-we-choose-zk-snarks" id="why-we-choose-zk-snarks"></a>

1. **Efficiency**: zk-SNARKs enable high-speed proof verification, crucial for maintaining performance on a blockchain network where many transactions must be verified quickly.
2. **Compact Proofs**: They generate small proof sizes, making them ideal for blockchains where conserving space is essential for scalability.
3. **Privacy**: zk-SNARKs provide strong privacy guarantees, allowing for the verification of transactions without revealing any underlying sensitive data.
4. **Adoption**: zk-SNARKs have been widely adopted and are supported by many blockchain projects, offering a mature ecosystem for developers.

### zk-SNARK <a href="#zk-snark" id="zk-snark"></a>

A zk-SNARK (Zero-Knowledge Succinct Non-Interactive Argument of Knowledge) is an advanced cryptographic technique that allows someone to prove they possess certain information without revealing what that information is. This proof of knowledge satisfies a known mathematical statement yet maintains the inputs' secrecy. It's a powerful tool for maintaining privacy and security within various digital interactions. The process of verifying a zk-SNARK is designed to be efficient, with computational demands growing very slowly (logarithmically) relative to the complexity of the statement being proved. This efficiency is what gives zk-SNARKs their 'succinct' characteristic.

Furthermore, the verification process does not require any back-and-forth communication between the prover and the verifier. The prover presents their proof to the verifier for validation. When the requirement for succinctness is set aside, and zero knowledge is adjusted to a more lenient standard known as Honest Verifier Zero Knowledge, similar concepts can be seen in digital signature algorithms like ECDSA and EdDSA. These algorithms, derived from the Schnorr Identification Protocol, prove the knowledge of a discrete logarithm without revealing it. While verifying such signatures is not costly and aligns with the non-interactive nature of zk-SNARKs, they do not fulfill the succinctness criterion, a defining feature of zk-SNARKs.​

### Definition of a zk-SNARK <a href="#definition-of-a-zk-snark" id="definition-of-a-zk-snark"></a>

A zk-SNARK involves three core components: a key **generator** (`G`), a **prover** (`P`), and a **verifier** (`V`). The process begins with `G`, which, using a secret parameter _lambda_ and a specific program `C`, \
outputs a pair of keys: a **proving key** (pk) and a **verification key** (vk). These keys, once generated, are public and tied to the program `C.`\
\
Next, the prover `P`, utilizing the proving key `pk`, public inputs `x`, and a secret witness `w`, produces proof `prf` that they know a witness `w,` which conforms to the constraints of program `C.` \
\
Finally, the verifier `V` checks the validity of the proof by executing `V(vk, w.pub(), prf)`, which confirms the truth of the claim if the proof prf is valid.\


<figure><img src="../../.gitbook/assets/Proof System.png" alt=""><figcaption></figcaption></figure>

### Circuit <a href="#circuit" id="circuit"></a>

From a user's perspective, a circuit functions similarly to a program written in a language like Go. It defines the logic or computation you want to prove has been executed correctly. Internally, however, a circuit is not a typical program but a system of algebraic constraints. These constraints represent the steps of the computation, and each one must be satisfied for the overall computation to be considered valid. This unique structure allows zk-SNARKs to prove complex computations efficiently.

#### Purpose of Circuits <a href="#purpose-of-circuits" id="purpose-of-circuits"></a>

A zk-SNARK circuit defines the computations that a prover wants to prove knowledge of without disclosing the underlying data. These circuits play a pivotal role in zk-SNARK protocols, ensuring that the prover can provide convincing evidence of the correctness of their computations while keeping the sensitive data private.

#### Components of a zk-SNARK Circuit <a href="#components-of-a-zk-snark-circuit" id="components-of-a-zk-snark-circuit"></a>

A zk-SNARK circuit consists of several key components:

* **Input Variables**: These are the data that the prover aims to prove knowledge of, often referred to as the witness.
* **Output Variables**: These represent the result of the computation the prover tries to prove.
* **Constraints**: Constraints are mathematical equations that define the rules the computation must adhere to. They ensure that computations are performed correctly.
* **Witness**: The witness comprises the private information known to the prover. It is used in the computation and is kept secret.
* **Public Inputs**: These are pieces of information that are publicly known and are used to validate the proof.

#### Arithmetic Circuits <a href="#arithmetic-circuits" id="arithmetic-circuits"></a>

Arithmetic operations, such as addition, multiplication, and comparison, are frequently used in zk-SNARK circuits to define computations. Here's a simplified example in JavaScript.

```cpp
#include <nil/crypto3/algebra/curves/pallas.hpp>

using namespace nil::crypto3::algebra::curves;

[[circuit]] typename pallas::base_field_type::value_type
    field_arithmetic_example([[private_input]] typename pallas::base_field_type::value_type a,
                             typename pallas::base_field_type::value_type b) {

    return a + b;
}
```

#### Constraints <a href="#constraints" id="constraints"></a>

Constraints in zk-SNARK circuits are crucial for enforcing the correctness of the computation. They are formulated as mathematical equations involving input and output variables. Examples of constraints include equality constraints and inequality constraints.

#### Constraint System <a href="#constraint-system" id="constraint-system"></a>

The entire collection of constraints in a zk-SNARK circuit forms a constraint system, a fundamental element in generating zk-SNARK proofs.

#### Prover and Verifier <a href="#prover-and-verifier" id="prover-and-verifier"></a>

In zk-SNARK protocols, there are two main roles:

* **Prover**: The prover's role is to create a zk-SNARK proof demonstrating knowledge of the correct computation while keeping the witness secret.
* **Verifier**: The verifier's role is to check the validity of the proof provided by the prover without knowing the underlying data.

​

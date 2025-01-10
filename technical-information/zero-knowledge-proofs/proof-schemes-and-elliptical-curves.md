# Proof schemes and Elliptical Curves

Proof schemes, also known as proof systems or protocols, are cryptographic techniques that allow one party (the prover) to convince another party (the verifier) that a specific statement or claim is true without revealing any additional information beyond the statement's truth. There are several proof schemes, each with its characteristics and use cases.\
\
Since we are utilizing [zkLLVM](https://github.com/NilFoundation/zkLLVM) to create cryptographic circuits, it's important to note that it supports multiple proving schemes and Elliptical Curve Cryptography (ECC): Groth16, PlonK and its variants (HyperPlonk, Halo2), and even Nova and its variants (SuperNova, HyperNova).\
\
These schemes can be implemented using a variety of elliptic curves, including BN254, BLS12-381, BLS12-377, BLS24-315, BW6-633, BW6-761, and Pallas and Vesta. To specify the desired proving scheme and the corresponding elliptic curve, we use templates from the [=Nil Crypto3](https://github.com/NilFoundation/crypto3) C++ library.

### Arithmetization of Proofs

Proofs are generated into circuits that perform multiple arithmetization operations using arithmetic functions in what are known as gates of the circuits. Those gates are then connected to form the proof. There are several circuit arithmetization systems, including Rank One Constraint Systems (R1CS), Algebraic Intermediate Representation (AIR), Plonkish arithmetization (PLONK), and Customizable Constraint System (CCS) that can capture R1CS, Plonkish and AIR arithmetization without overhead.

### Choosing an Arithmetization Circuit System <a href="#choosing-an-arithmetization-circuit-system" id="choosing-an-arithmetization-circuit-system"></a>

#### Arithmetization Circuit Systems Considered

**R1CS**: Rank-One Constraint System, is a mathematical construct used to encode polynomial equations in matrices 𝐴, 𝐵, and 𝐶, where each row of the matrices corresponds to a system of equations of the form:

$$
Az * Bz = Cz
$$

> While R1CS is a powerful tool, it has some limitations. One of the main issues is that it does not work with folding schemes.

**AIR:** Algebraic Intermediate Representation (AIR) is the arithmetization procedure used by StarkWare in their virtual machine, CAIRO (CPU AIR)

**PLONKish**: PLONK is an arithmetization system with a universal and continuously updatable trusted setup. This innovation facilitates its use across multiple circuits, ensuring versatility and security. With faster proving time and succinct verification, PLONK stands out as a significant advancement in cryptographic protocols.

**CCS**: Customizable Constraint System is a generalization of R1CS that can simultaneously capture R1CS, Plonkish, and AIR without overheads.

The arithmetization adds significant overhead to the computation time. Using SNARK-friendly operations can increase computation time by nearly two orders of magnitude, and for non-friendly operations, it can be more.

Recently, many different optimizations have been presented to reduce the overhead, such as:

* Lookup tables (PlookUP).
* SNARK-friendly cryptographic primitives (such as [Rescue](https://eprint.iacr.org/2020/1143.pdf?ref=blog.lambdaclass.com), [SAVER](https://eprint.iacr.org/2019/1270.pdf?ref=blog.lambdaclass.com), [Poseidon](https://eprint.iacr.org/2019/458?ref=blog.lambdaclass.com), [Reinforced Concrete](https://eprint.iacr.org/2021/1038.pdf), and [Monoli](https://medium.com/@horizenlabs-tech/introducing-monolith-for-faster-hashing-in-zk-settings-6980f406af0e)[th](https://medium.com/@horizenlabs-tech/introducing-monolith-for-faster-hashing-in-zk-settings-6980f406af0e)[ ](https://medium.com/@horizenlabs-tech/introducing-monolith-for-faster-hashing-in-zk-settings-6980f406af0e)Hashing ).
* Concurrent proof generation.
* Hardware acceleration (such as using GPU or FPGA).

We can also prove that we executed thousands of transactions or operations using recursive proof composition, [proof aggregation](https://blog.zk.link/nova-studies-i-exploring-aggregation-recursion-and-folding-23b9a67000cd), [folding schemes](https://medium.com/veridise/introduction-to-nova-and-zk-folding-schemes-4ef717574484), or [incrementally verifiable computing](https://blog.lambdaclass.com/incrementally-verifiable-computation-nova/).

### Our Proving Scheme's Architecture <a href="#our-proving-schems-architecture" id="our-proving-schems-architecture"></a>

1. **Performance Efficiency**: Performance is critical in blockchain applications, especially those involving frequent transactions or operations that require repeated proving of the same computational logic. We choose C++ and utilize the GPU for efficiency and cross-platform compatibility.\
   \
   **Plonkish Arithmetization** was chosen because it can be highly optimized using PLONK Lookup tables (PLookUp) and optimized for GPU devices. This efficiency is crucial for maintaining fast transaction times and lower computational costs.\
   \
   **Monolith Hashing** was chosen because it is efficient, comparable to SHA3-256 hash rate speed, can be highly optimized for GPU devices, and is highly efficient to implement in PLONK circuits.
2. **Succinct Proofs**: The Plonkish-based proofs generated by ZKLLVM are notably concise, especially when designed to leverage specific elliptic curves like Pallas and Vesta (PaSTA), known for their succinctness and efficiency in zero-knowledge proof systems. The commitment scheme is similar to the Halo2 and is more broadly called a Polynomial Commitment Scheme (PCS).\
   \
   The number of group elements in a PLONK proof can vary depending on the specific implementation details and optimizations applied. However, for a typical PLONK setup, the proof size is generally characterized by a few main components:
   1. **Commitments to the polynomials** used in the protocol are usually represented as points on the elliptic curve.
   2. **Evaluation Points** at which these polynomials are evaluated are also represented as elliptic curve points.
   3. **The Opening Proof** for these polynomial commitments at the evaluation points involve elements from the base and scalar fields of the elliptic curve. \\
3. **Zero-Knowledge Property**: PLONK provides strong zero-knowledge guarantees, allowing the prover to validate the truth of a statement without revealing any underlying data. This is essential in blockchain applications where privacy and confidentiality are paramount, such as in the case of private transactions or confidential contracts.
4. **Security and Soundness**: The cryptographic strength of PLONK, which relies on the hardness of problems on elliptic curves, ensures a high degree of security. This aligns with the need for robust security in blockchain applications, where the integrity and trustworthiness of transactions are critical.
5. **Aggregate/Folding/IVC Proofs:** Incrementally Verifiable Computing (**I**VC) is a technique that allows proving that a function was repeatedly applied to some initial state, producing a sequence of states,\
   \
   PLONK can do IVC using the Pallas and Vesta (PaSTA) Elliptical Curve Pair.
   1. PLONK is used with PaSTA curves defined over a finite field, which were chosen to aggregate proofs similar to the [Halo2 commitment scheme](https://zcash.github.io/halo2/index.html?ref=blog.lambdaclass.com).
   2. Parts of the [Kimchi Proving System](https://minaprotocol.com/blog/kimchi-the-latest-update-to-minas-proof-system) were also adopted to minimize the blockchain's storage requirements.
6. **Compatibility with Ethereum and Other Platforms**: Since zkLLVM can also generate Solidity Smart Contract code for Ethereum Virtual Machines (EVMs) to verify via the Solidity Smart Contract, it can verify the aggregated proofs. The verifier Smart Contract is compatible with major blockchains like Ethereum, which is crucial.

### Final Decision on Proving System

Finally, after all the research, we decided that all these choices led us to use the [Placeholder Prover System](https://nil.foundation/blog/post/placeholder-proofsystem) that the =nil Foundation developed. The Placeholder Prover System is a modular approach to a robust zkSnark proving system, which allowed us to build a fast custom proving system.

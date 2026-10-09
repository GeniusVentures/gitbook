# Technical Deep Dive: How GNUS.ai Works

> **Reviewed October 9, 2026.** This FAQ replaces outdated statements about token rewards, mainnet dates, guaranteed savings, audits, and network consensus. **SuperGenius mainnet implementation is complete, but its public native mainnet has not launched.** GCS and the OpenAI-compatible gateway have specified and in-progress components, not a verified public production service. See [Platform Status](../../about-gnus.ai/release-status.md), [Tokenomics](../../about-gnus.ai/features-and-benefits/tokenomics.md), and [Pricing Methodology](../../about-gnus.ai/features-and-benefits/pricing-methodology.md). Source-level behavior, operational readiness, and public availability are different claims.

### 1. How could participants in emerging markets offset device costs by contributing compute through apps?

GNUS.ai aims to let eligible devices contribute useful processing capacity through applications and SDK integrations. A future public contributor program **may** compensate accepted work in GNUS under published program rules. It is **not** accurate to describe public node earnings, fiat conversion, or device-cost offsets as currently available or guaranteed. Earnings would depend on eligibility, useful work completed, local energy and data costs, token liquidity, applicable law, and the program's payment terms.

The platform targets multiple device classes, but support for a specific phone, console, or operating system requires a compatible SDK/runtime and tests. An integration design is not proof that every device can execute every AI model.

### 2. How does GNUS useful-work processing differ from traditional proof-of-work mining?

GNUS is designed to connect computation to application workloads—such as inference and other processing—rather than requiring every provider to perform the same hash puzzle. **Useful processing does not by itself secure a ledger or prove a result correct.** Consensus, job-result verification, incentives, and settlement have separate roles.

Historical descriptions of an **80% / 10% / 10%** reward split and a **fixed 10% processing burn** must not be treated as current rules. The native [`BurnConfig` source](https://github.com/GeniusVentures/SuperGenius/blob/develop/src/account/BurnConfig.hpp) defines a **100-basis-point (1%) genesis default** and quorum-controlled updates; EVM bridge and token-conversion burns are separate. No default establishes an actual public-network payout rate before activation.

### 3. What scaling problems does GNUS address, and where does GCS fit?

Three distinct responsibilities matter:

- **GCS** plans cognitive work, chooses small specialist Expert Language Models (ELMs), applies memory and privacy policy, and checks answers. It may run locally or privately without sending work to public workers.
- **SuperGenius** owns its native processing queue, processor selection, peer-to-peer transport, trust rules, and GNUS settlement for eligible distributed jobs.
- **EVM token contracts and bridging** move or represent value on supported chains. They do not prove that a particular fiat on-ramp, payment partner, or cross-chain service is available.

The planned GCS-to-SuperGenius ELM bridge specifies **one funded native job with multiple ELM work items**, not a new native scheduler for each expert. The bridge remains specified but unfinished; see [GCS developer bridge](https://gcs.gnus.ai/developer-api-and-compute-bridge/) and [SuperGenius issue #369](https://github.com/GeniusVentures/SuperGenius/issues/369).

### 4. How will GNUS handle varying hardware and unreliable nodes?

The architecture has workload descriptions, processing queues, SDK boundaries, and result-checking components. Hardware limits still matter: a model fitting into device storage does not guarantee that its RAM use, thermal behavior, speed, or accuracy are acceptable. Features such as automatic failover and variable device contribution require end-to-end testing on named devices and workloads.

There is **no published matched-workload evidence here** for a **99%+ uptime guarantee**, universal mobile/console support, or guaranteed privacy from federated learning alone. Do not treat parity checks, cryptographic proofs, and semantic accuracy checks as interchangeable.

### 5. Is GNUS.ai simply a cheaper GPU-cloud provider?

No. The intended product is **a modular cognitive system backed by optional distributed compute**. GCS selects experts, memory, tools, and checks for a request; eligible work may run on devices owned by participants, or entirely within a private or local deployment.

Lower cost is a design goal, **not a demonstrated fixed 70–90% saving** across workloads. Compare matched precision, device utilization, model quality, end-to-end latency, network traffic, and operating costs before making a numerical claim. The [pricing page](../../about-gnus.ai/features-and-benefits/pricing-methodology.md) separates historical node-hour assumptions, the implemented native estimated-work escrow, and a planned ELM-hour rate.

### 6. How are jobs routed, checked, and settled?

GCS decides **what cognitive work** to perform. For eligible distributed execution, SuperGenius chooses processors and schedules native SubTasks. These are not interchangeable with the GCS planning layer. The native general-processing path can quote estimated work and reserve GNUS escrow; the GCS ELM-hour bridge is **not** yet a deployed billing path.

Keep four different forms of checking separate: **ledger consensus** authorizes network state; **execution integrity (EIS)** aims to check whether distributed work was carried out according to its specification; **cognitive verification** evaluates the usefulness or factual quality of an answer; **settlement** accounts for accepted work. Neither equal hashes from different GPU vendors nor a proof that computation ran automatically guarantees the answer is correct. The current [GCS Execution Integrity System design](https://github.com/GeniusVentures/GeniusCognitiveSystem/blob/main/docs/architecture/execution-integrity-system.md) is a specification; cross-hardware conformance evidence must be documented separately.

### 7. How do users, developers, and the token economy benefit?

The aim is to let developers build applications using locally owned, private, or network-provided compute, with an eventual incentive for eligible third-party providers. The native SuperGenius ledger uses **1 GNUS = 1,000,000 Minions** internally ([`TokenAmount.hpp`](https://github.com/GeniusVentures/SuperGenius/blob/develop/src/account/TokenAmount.hpp)); EVM contracts can use different token precisions.

There is **no guaranteed contributor return, token appreciation, margin, or fixed burn-induced price increase**. Historical Monte Carlo simulations and projected token prices were scenarios rather than measured investment outcomes. Buying GNUS does not buy shares in Genius Ventures.

### 8. What protects against Sybil attacks and bad validators?

The current SuperGenius code distinguishes a **genesis-reviewed trusted-peer registry**, changes authorized by that registry's quorum policy, and the separate [`ValidatorRegistry`](https://github.com/GeniusVentures/SuperGenius/blob/develop/src/blockchain/ValidatorRegistry.hpp) for consensus roles and weighted votes. [`TrustedPeerRegistry`](https://github.com/GeniusVentures/SuperGenius/blob/develop/src/trustedpeer/TrustedPeerRegistry.hpp) is **not** equivalent to an unrestricted 'any node votes based on earned reputation' rule. Each threshold applies to its own decision; do not replace the code's distinct policies with a universal 2/3 reputation vote.

These controls form part of a threat model, not proof that Sybil attacks cannot succeed. Earlier claims about device fingerprinting, mandatory IP diversity, guaranteed slashing, or specific DAO voting thresholds need separately verified implementations and policies before being presented as active protections.

### 9. How can a beginner join as a compute provider?

**A general public native-mainnet contributor enrollment and rewards program has not launched.** Check [official platform status](../../about-gnus.ai/release-status.md), published download links, supported-device requirements, and program terms before installing software or committing hardware. Do not rely on old instructions claiming a guaranteed testnet reward, current exchange conversion, or a historical 2025/early-2026 start date.

### 10. Has GNUS.ai been audited, and how are funds protected?

The [Contracts page](../contracts.md) publishes a **Solidproof smart-contract audit dated February 24, 2024**. That report has its own scope and date; it is **not evidence of a completed third-party audit of the entire C++ node, bridge deployment, GCS, or current operational network**. The prior claim of *two* publicly posted third-party contract audits is not supported by the audit listing reviewed here.

Security depends on the specific contract, wallet, key custody, network configuration, and code being run. Neither use of an ERC standard nor references to zero-knowledge proofs establish that all transactions, prompts, or user data are encrypted or private. Additional independent audits, deployment-specific threat models, and published test results remain diligence items.

### 11. Is a dedicated physical GNUS.ai device planned?

The publicly documented direction emphasizes software that uses existing hardware. No current, verified product launch, specifications, price, or availability for a dedicated GNUS device were established in the references reviewed for this FAQ. Future hardware plans, if any, require a separate announcement.

---

**Authoritative references:** [Platform Status](../../about-gnus.ai/release-status.md) · [Tokenomics](../../about-gnus.ai/features-and-benefits/tokenomics.md) · [Pricing Methodology](../../about-gnus.ai/features-and-benefits/pricing-methodology.md) · [Master Architecture](../../technical-information/MASTER_ARCHITECTURE.md) · [GCS architecture](https://gcs.gnus.ai/) · [Contracts and audit](../contracts.md).

*This page describes architecture, stated project decisions, and limits of published evidence. It does not provide legal, tax, or investment advice.*

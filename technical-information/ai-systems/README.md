# AI Systems

**GNUS.ai is both a distributed execution platform and an application platform for modular AI.** It should not be described only as distributed RAG, sharded LLM inference, or generic agents running on GPUs.

- **GCS (Genius Cognitive System)** governs the cognitive request: planning, Semantic Core reasoning, routed Expert Language Models (ELMs), grounding, tools, structured GAML memory, and answer checks.
- **SuperGenius / GNUS** handles eligible distributed processing, network participation, ledger and settlement work. It does not replace the GCS controller, model routing, or memory governor.
- **Applications**, including Genius AI Boss, expose these capabilities to users. GCS may execute locally or on a private network without sending each request to a public swarm.

The pages below cover infrastructure components, including retrieval, storage, pub/sub and retraining design. They are **not** a complete implementation-status inventory of GCS. See the [GCS architecture documentation](https://gcs.gnus.ai/) for the cognitive specifications and the [Master Platform Architecture](../MASTER_ARCHITECTURE.md) for component ownership.

**Release status:** SuperGenius mainnet implementation is complete as of October 2026; its public launch is held for GCS and initial application readiness. See [Platform Status](../../about-gnus.ai/release-status.md).

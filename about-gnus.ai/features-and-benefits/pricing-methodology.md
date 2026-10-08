# GNUS.ai Pricing Methodology and Status

**Pricing-status reference — October 2026.** This page separates historical prices and throughput models from a proposed lightweight-GCS cost assumption. **It is not a rate card, offer of service, approved payout schedule, or production benchmark.** Native SuperGenius mainnet code is complete; public mainnet has **not launched**. The GCS OpenAI-compatible gateway is a planned v1.1 Phase 6 interface, not a live retail API.

## Three different things have been called "compute pricing"

| Source and date | Number | Unit and meaning | Current authority |
| --- | --- | --- | --- |
| Older GNUS cost and xAI-cluster comparisons | **$0.005** | Assumed *node-hour* processing/payout in those historical scenarios | **Historical illustrative assumption**, not a verified active node reward or current API rate |
| October 2026 lightweight GCS planning | **$0.0003** | Proposed compute-only cost per **active external ELM-hour** | **Provisional planning assumption**; not approved API retail price or node reward |
| [GNUS AI Pricing Comparison, Feb 2026](https://github.com/GeniusVentures/gnus-ai-pricing) | e.g. 200 FP32 and 2,200 blended | Modeled **effective TFLOPS per $1/hour**; other modes express cost per 1,000 effective TFLOPS | Comparative **scenario**, not measured network performance or an API billing rate |

The native [SuperGenius `TokenAmount`](https://github.com/GeniusVentures/SuperGenius/blob/develop/src/account/TokenAmount.hpp) also contains a **USD-per-FLOP** estimator based on processed-byte workload estimates and a GNUS/USD price. It uses a completely different unit from node-hours or ELM-hours. Its constants do not establish the public GCS API tariff.

No authoritative, final pricing decision has been identified that supersedes all these references. A new customer price needs an explicit unit definition, performance evidence, what expenses it includes, billing policy, and a published approval.

## The $1 compute comparison: formulas and limits

The separate [pricing comparison](https://github.com/GeniusVentures/gnus-ai-pricing) expresses a GPU's **modeled useful throughput** per unit of hourly spend:

```text
effective_TFLOPS = peak_TFLOPS_at_precision * assumed_utilization

effective_TFLOPS_per_$1_hour
  = effective_TFLOPS / rental_USD_per_hour

USD_per_1000_effective_TFLOPS_hour
  = (rental_USD_per_hour / effective_TFLOPS) * 1000

USD_per_1000_effective_TFLOPS_hour
  = 1000 / effective_TFLOPS_per_$1_hour
```

The February 2026 model uses **60% utilization** for the listed rental GPUs. Its GNUS-side FP32 (200), FP16 (600), FP8 (1,400), adaptive low-bit (3,500), and blended (2,200) values were **supplied modeling inputs**, not network-measured benchmarks. The inverse cost mode is a mathematical transformation of those values, not a new cost measurement.

**Worked model example:** At $2/hour, 67 peak FP32 TFLOPS and 60% utilization, a GPU is assigned `(67 * 0.60)/2 = 20.1` effective TFLOPS per $1/hour. The corresponding modeled cost per 1,000 effective TFLOPS-hours is `1000/20.1 ≈ $49.75`. This does not mean 1,000 real TFLOPs of any precision or workload can be purchased at that price.

Use **the same precision, workload, actual sustained utilization, total billable time, and system boundary** for comparisons. Hardware peak rates, hypothetical node-equivalents, quantization differences, and historical marketplace prices are not interchangeable. End-to-end inference cost also depends on memory, bandwidth, communication, model size, and scheduling.

## Lightweight ELM compute assumption (not a price list)

For GCS architecture planning only, the current suggested **external expert compute-only** assumption is:

```text
external_ELM_cost_USD
  = 0.0003 * SUM(external ELM active seconds / 3600)
```

The expected ordinary cognitive workflow would use **zero to approximately three external ELMs** as needed, not run three dedicated workers continuously. This is an expectation, not a verified or enforced maximum.

Examples using the proposed unit: one external ELM active for one hour = **$0.0003**; three external ELMs each active for one hour = **$0.0009**; three external ELMs each active for one minute = **$0.000015**.

These costs **exclude** potentially chargeable Semantic Core computation, data transfer, memory/retrieval, verification, queuing/retries, operations, node compensation policies, margin, taxes, token conversion, and any minimum charge. If billing is later denominated in GNUS tokens, USD-equivalent conversions and rounding must be specified separately.

The higher-level [GCS OpenAI-compatible API Router](https://gcs.gnus.ai/openai-compatible-api-router-and-gcs-job-queue/) may eventually charge by tokens, requests, subscriptions or resource budgets, but **no one of those retail models is committed here**.

## Historical comparisons and token claims

The [older $0.005/hour comparison](scale-and-cost-efficiency.md) and the [xAI 100k-cluster scenario](gnus.ai-network-vs.-centralized-xai-100k-cluster/README.md) contain historical node counts, GPU price assumptions, and sometimes **fixed 10% burn or token-price projections**. Those are **not current network parameters or financial forecasts**. Current native `BurnConfig` has a **1% genesis default subject to trusted-peer quorum changes**; EVM bridge/conversion burns are distinct. See [Tokenomics](tokenomics.md).

Use [Platform Status](../release-status.md), the [GCS developer bridge](https://gcs.gnus.ai/openai-compatible-api-router-and-gcs-job-queue/), and the [GCS API Router Specification](https://github.com/GeniusVentures/GeniusCognitiveSystem/blob/main/docs/architecture/openai-compatible-api-router-and-gcs-job-queue.md) for release and API-delivery status.

# GNUS.ai Pricing Methodology and Status

**Pricing-status reference — October 2026.** This page distinguishes implemented general-processing GNUS escrow quotes, the owner-set **future ELM-job hourly rate**, and historical compute comparisons. **It is not a rate card, offer of service, approved payout schedule, or production benchmark.** Native SuperGenius mainnet code is complete; public mainnet has **not launched**. The GCS OpenAI-compatible gateway is a planned v1.1 Phase 6 interface, not a live retail API.

## Four different pricing units and contexts

| Source and date | Number | Unit and meaning | Current authority |
| --- | --- | --- | --- |
| Native SuperGenius processing-job escrow | **$5 × 10^-13 per estimated FLOP** ($0.005 per 10 billion estimated FLOPs) | Implemented work estimate, converted to GNUS at the current GNUS/USD price and held in escrow | **Implemented** funding path; underlying work-unit semantics need validation; not an hourly rate or public GCS API tariff |
| Older GNUS cost and xAI-cluster comparisons | **$0.005** | Assumed *node-hour* processing/payout in those historical scenarios | **Historical illustrative assumption**, not a verified active node reward or current API rate |
| Owner-resolved ELM Job Bridging design (2026-08-26) | **$0.0003** | Fixed funding rate per **processing-hour** for a future `elm_processing` job; one pooled budget or separate ELM allocations to be decided | **Agreed engineering rate**, tracked in open [SuperGenius #369](https://github.com/GeniusVentures/SuperGenius/issues/369), **not yet implemented ELM billing or API retail pricing** |
| [GNUS AI Pricing Comparison, Feb 2026](https://github.com/GeniusVentures/gnus-ai-pricing) | e.g. 200 FP32 and 2,200 blended | Modeled **effective TFLOPS per $1/hour**; other modes express cost per 1,000 effective TFLOPS | Comparative **scenario**, not measured network performance or an API billing rate |

The native estimator is **already called during processing-job submission**, not merely a theoretical pricing constant: [`GeniusNode::ProcessImage()`](https://github.com/GeniusVentures/SuperGenius/blob/develop/src/account/GeniusNode.cpp#L3121-L3210) uses [`GetProcessCost()`](https://github.com/GeniusVentures/SuperGenius/blob/develop/src/account/GeniusNode.cpp#L3252-L3300) to fetch the GNUS/USD quote, compute required minions, check available funds, then **call `HoldEscrow()` before enqueuing**. [`TransactionManager`](https://github.com/GeniusVentures/SuperGenius/blob/develop/src/transaction/TransactionManager.cpp#L1087-L1315) handles escrow and results-based payout. Public native mainnet and the future OpenAI-compatible gateway remain separate activation/implementation questions.

## Implemented native processing quote: what $0.005 represents

The [`TokenAmount` constants](https://github.com/GeniusVentures/SuperGenius/blob/develop/src/account/TokenAmount.hpp#L24-L33) implement the following estimate before six-decimal GNUS truncation and a minimum of **one minion (0.000001 GNUS)**:

```text
L = SUM(processing dimensions.block_len values over input model nodes)
estimated_USD = L * 20 assumed FLOPs/unit * (500 / 10^15) USD/FLOP
              = L * 0.00000000001 USD
escrow_GNUS (approximately) = estimated_USD / (USD per GNUS)
```

Thus the source rate is **$0.005 per 10 billion assumed FLOPs**, or per 500 million **assumed byte-like units**. It is **not** a constant $0.005 per hour. The [token amount tests](https://github.com/GeniusVentures/SuperGenius/blob/develop/test/src/account/token_amount_test.cpp) expect 5,242 minions for 500 MiB at $1/GNUS, consistent with truncation.

**Source-unit issue requiring validation:** [`SGProcessingManager::ParseBlockSize()`](https://github.com/GeniusVentures/SGProcessingManager/blob/91021875491925e08c26e1d3ffedbe5815f3871d/src/processingbase/ProcessingManager.cpp#L1242-L1265) sums `dimensions.block_len`, **not measured elapsed hours, total bytes processed, or actual FLOPs**. The [processing JSON guide](https://github.com/GeniusVentures/SGProcessingManager/blob/91021875491925e08c26e1d3ffedbe5815f3871d/doc/processing-json-guide.md) defines that same field as **patch depth** for `texture3D` processing; other processors use patch length. This may make the assumed 20-FLOPs-per-byte factor dimensionally incorrect for some workload types. Validate units and test across chunk count, formats, and model types before reporting a measured per-work rate.

The existing GNUS-denominated **native general-processing job funding** is the base mechanism for the planned ELM extension, not proof that its hourly pricing has been implemented.

**What was decided:** On August 26, 2026, SuperGenius project leadership resolved the conflicting `0.0003 cents/hour` wording to **$0.0003 per processing-hour** in [INGEST-CONFLICTS.md](https://github.com/GeniusVentures/SuperGenius/blob/develop/.planning/INGEST-CONFLICTS.md). The [Phase 13 roadmap](https://github.com/GeniusVentures/SuperGenius/blob/develop/.planning/ROADMAP.md) specifies that exact rate for ELM bridging through existing GNUS escrow and the native queue, while [SGProcessingManager #17](https://github.com/GeniusVentures/SGProcessingManager/issues/17) owns the runtime. Both issues remain open. **The engineering funding rate is decided; the implementation, pooled-versus-per-ELM aggregation, and customer-facing API rate are not.**

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

## Fixed ELM processing-hour design rate (not deployed API pricing)

The canonical engineering decision for **planned** funded `elm_processing` jobs is **$0.0003 per processing-hour**. This is a chosen **native ELM funding rate**, *not* the existing general-processing USD-per-estimated-FLOP quote above, an implemented ELM runtime, or a public OpenAI-compatible API retail price.

```text
planned ELM job escrow, USD-equivalent
  = 0.0003 * funded_processing_hours

estimated GNUS to reserve
  = planned USD-equivalent / market price (USD per GNUS)
    [quote timing, rounding and actual billing policy pending]
```

One API-level request may fund **one** SuperGenius job containing multiple `elms[]` work items. Zero to approximately three external ELMs is an ordinary workload expectation, not a fixed maximum or automatic threefold charge. The planning record permits either **one pooled processing-hour allowance** or **per-ELM hour allocations**; the charging interpretation has not been selected.

For illustration, **one minute of total pooled funded work** costs **$0.000005**. **Only if** three ELMs are allocated and charged one minute each is the compute funding **$0.000015**. These are mathematical illustrations of the planned fixed rate, not transaction receipts, actual marginal cost benchmarks, or customer quotes. Model download is included as work in the owner-approved Phase 13 scope; how to track idle/parallel time, cancellations, overruns and refunds still needs tests and policy.

The future GCS API may add costs for memory, verification, network, operations and margin. It can present token/request/subscription usage to customers, but its final retail price and mapping to native GNUS escrow remain undecided. The [OpenAI-compatible API Router](https://gcs.gnus.ai/openai-compatible-api-router-and-gcs-job-queue/) is planned, not live.

## Historical comparisons and token claims

The [older $0.005/hour comparison](scale-and-cost-efficiency.md) and the [xAI 100k-cluster scenario](gnus.ai-network-vs.-centralized-xai-100k-cluster/README.md) contain historical node counts, GPU price assumptions, and sometimes **fixed 10% burn or token-price projections**. Those are **not current network parameters or financial forecasts**. Current native `BurnConfig` has a **1% genesis default subject to trusted-peer quorum changes**; EVM bridge/conversion burns are distinct. See [Tokenomics](tokenomics.md).

Use [Platform Status](../release-status.md), the [GCS developer bridge](https://gcs.gnus.ai/openai-compatible-api-router-and-gcs-job-queue/), and the [GCS API Router Specification](https://github.com/GeniusVentures/GeniusCognitiveSystem/blob/main/docs/architecture/openai-compatible-api-router-and-gcs-job-queue.md) for release and API-delivery status.

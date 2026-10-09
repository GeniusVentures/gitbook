# Scale and cost-efficiency

The GNUS.ai platform aims to make specialist AI and distributed processing more economical by using capable hardware already owned by participants. That can reduce dedicated capital costs, but actual cost per useful unit of compute depends on **device efficiency, utilization, network overhead, work type, and payment terms**.

GNUS's commercial model includes two different kinds of services: **distributed compute execution** and the planned **GCS OpenAI-compatible cognitive API**. Both can use the network, but API inference may also run locally or inside a private deployment.

**Pricing status (October 2026):** There is **no verified live public native-mainnet tariff or guaranteed percentage saving**. Older comparisons used **$0.005 per node-hour**. SuperGenius leadership has selected **$0.0003 per funded processing-hour for the planned ELM-job bridge** (not yet implemented or a customer API tariff); **whether a job funds one pooled hours budget or separate per-ELM allocations remains undecided**. The implemented generic-processing path instead estimates work and converts its USD quote to GNUS for escrow. These units cannot be treated as equivalent V100 GPU-hours. See [Pricing Methodology and Status](pricing-methodology.md).

## Historical hourly-provider comparison (not current quotes)

This legacy illustrative comparison was written before public mainnet activation. The figures are **not** independently normalized to the same precision, device capability, sustained throughput, or data-center cost coverage, and cannot substantiate a fixed savings guarantee. Review current provider pricing and run matched-workload benchmarks before using the table for procurement.

| Provider                        | Approximate hourly cost for ML training work (V100-equivalent) | Scalability |
| ------------------------------- | -------------------------------------------------------------- | ----------- |
| GNUS.ai                         | $.005                                                          | High        |
| Single personal GPU             | $0.28                                                          | None        |
| Gensyn (projected)              | $0.40                                                          | High        |
| Single GPU in datacenter        | $0.40                                                          | None        |
| GCP spot instances (unreliable) | $0.75                                                          | Medium      |
| AWS spot instances (unreliable) | $0.90                                                          | Medium      |
| Vast.ai                         | $1.10                                                          | Low         |
| Golem Network                   | $1.20                                                          | Low         |
| AWS on-demand                   | $2                                                             | Medium      |
| GCP on-demand                   | $2.50                                                          | Medium      |
| Truebit (+ Ethereum)            | $12                                                            | Low         |
| Ethereum                        | $15,700                                                        | Low         |

#### &#x20; <a href="#protocol-evaluation" id="protocol-evaluation"></a>


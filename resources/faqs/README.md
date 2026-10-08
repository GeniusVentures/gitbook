# FAQS

**What is a GNUS Token?**

GNUS Tokens are tokens used in a unique, secure, smart, and easy-to-use platform that completely disrupts the way businesses do AI/ML Processing. It is the purchasing unit for AI/ML processing requests.

**What blockchain are the GNUS Tokens on?**

GNUS has EVM token contracts, documented under [Contracts](../contracts.md). References to Bitcoin BRC-20, Solana, and Cardano in earlier plans should not be read as evidence of deployment on those networks.

**What benefits do I gain from GNUS Token?**

The initial value of GNUS tokens is for prepurchasing AI/ML processing and will be used as the reserve currency for Games and applications that integrate with the GNUS blockchain. Once the ecosystem is in full swing, GNUS tokens used for AI/ML processing are paid to anybody who has installed the App or is playing a game with the system integrated. Once GNUS is distributed, it can be used for in-app purchases and becomes part of a gaming ecosystem.

**Why are GNUS Tokens multichain?**

GNUS tokens are a bridging mechanism between other Cryptocurrencies and Fiat currency and a bridge to the SGNUS (Super Genius) private blockchain. This allows AI processing payments earned by app and game developers to be converted to any currency.

**Are GNUS Tokens traded on a big exchange?**

This entry previously described an anticipated March 2024 exchange listing and is no longer a reliable statement of current market availability. Confirm current exchange and chain availability through official announcements and contract addresses.

**How do GNUS and SGNUS relate?**

GNUS Tokens are blockchain tokens that are used to open AI/ML requests and act as a payment channel. SGNUS tokens are created and mapped one-to-one for GNUS tokens and are part of a rollup and bridging system that uses zkSnarks. They then enter their very own economic system for fast transaction processing.

**What is the difference between GNUS and SGNUS tokens?**

GNUS token contracts exist on EVM networks, while SGNUS refers to the native SuperGenius network accounting and bridging design. Do not confuse live EVM token contracts with activation of the native public SuperGenius mainnet, which has not launched. See [Contracts](../contracts.md) and [Platform Status](../../about-gnus.ai/release-status.md).

**Why do the GNUS EVM smart contracts burn tokens?**

The EVM contracts use burning for token conversion and cross-chain transfers, **not as the native SuperGenius processing-payout burn**:

- **Minting certain child tokens:** `GNUSNFTFactory.beforeMint` burns an exchange-rate-defined amount of GNUS when minting a direct child token of GNUS.
- **Bridging:** `GNUSBridge.bridgeOut` burns the tokens on the source chain and emits an event for the bridge flow. A source-chain burn in a bridge transfer should not be counted as a permanent reduction in total cross-chain supply without checking the corresponding destination mint.
- **Redemption and controlled burns:** `GNUSBridge.withdraw` burns child tokens when converting them back to GNUS on the same EVM network; the bridge contract also provides a role-restricted GNUS burn function.

These operations serve different purposes and **do not guarantee token-price appreciation**. The descriptions come from [GNUSNFTFactory](https://github.com/GeniusVentures/gnus-ai-contracts/blob/main/GNUSNFTFactory.sol) and [GNUSBridge](https://github.com/GeniusVentures/gnus-ai-contracts/blob/main/GNUSBridge.sol) source; confirm the deployed contract facets and configuration for a specific network using [Contracts](../contracts.md).

**Is the native SuperGenius processing burn the same mechanism?**

No. The native SuperGenius `BurnConfig` governs a separate processing-payout burn. Its current implementation defines a **1% genesis default**, with changes requiring trusted-peer quorum approval. The source does **not** establish a permanent 10% payout burn, nor does a default establish the value used by a particular deployed network. See [Tokenomics](../../about-gnus.ai/features-and-benefits/tokenomics.md) and [Platform Status](../../about-gnus.ai/release-status.md).

**Will this token be considered a security?**

GNUS is intended for network utility, including payment for AI/ML processing. A legal classification cannot be determined from that purpose alone; it depends on the specific offering, transactions, representations, and applicable law. This documentation is not a legal opinion.

**Can I invest in the company by buying these tokens?**

GNUS tokens and equity in Genius Ventures are different instruments. Buying GNUS tokens is not the same as acquiring company shares. Contact Genius Ventures directly for any current securities offering and its applicable documents; older SAFE/SAFT descriptions may no longer apply.

**Would anybody be able to buy your tokens?**

Availability varies by venue and jurisdiction. The intended utility of GNUS tokens for AI/ML processing does not by itself determine their legal status or whether every person may purchase them. Seek qualified legal advice for specific jurisdictions.

**Are you worried about the U.S. crackdown on Cryptocurrencies?**

Not in the slightest. Cryptocurrencies and Cryptotokens have been adopted by major corporations and have grown significantly over the last few years. The Genie is already out of the bottle!

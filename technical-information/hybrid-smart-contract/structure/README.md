# Structure

Structure for the Smart Contract Token/NFT Collection (ERC-1155)

```solidity
struct NFT {
    string name;            // Token/NFT Name
    string symbol;          // Token/NFT Symbol
    string uri;             // Token/NFT URI for metadata
    uint256 exchangeRate;   // Only for withdrawing to GNUS
    uint256 maxSupply;      // Maximum supply of NFTs
    address creator;        // The creator of the token, as an ERC-20 address
    uint128 childCurIndex;  // The current childNFT count created
    bool nftCreated;        // If there is a mapping/token created
}
```

Hierarchical Structure

```
- GNUS Token (ID 0)
  - Game Studio 1 Token (ID 0.1)
    - Game 1 Token (ID 0.1.1)
      - NFT 3 (ID 0.1.1.1)
    - Game 3 Token (ID 0.1.2)
      - NFT 6 (ID 0.1.2.1)
  - App 1 Token (ID 0.2)
  - Solo Game 1 Token (ID 0.3)
    - NFT 1 (ID 0.3.1)
    - NFT 2 (ID 0.3.2)
  - Country 1 Token (ID 0.4)
    - Game Studio 2 Token (ID 0.4.1)
      - Game 2 Token (ID 0.4.1.1)
        - NFT 4 (ID 0.4.1.1.1)
      - Game 4 Token (ID 0.4.1.2)
        - NFT 5 (ID 0.4.1.2.1)
    - App 2 Token (ID 0.4.2)

```

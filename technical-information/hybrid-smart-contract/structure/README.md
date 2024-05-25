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
    - Game 1 Token (ID 1.2)
      - NFT 3 (ID 2.3)
    - Game 3 Token (ID 1.4)
      - NFT 6 (ID 4.5)
  - Assistance App Token (ID 0.6)
  - Solo Game 1 Token (ID 0.7)
    - NFT 1 (ID 7.8)
    - NFT 2 (ID 7.9)
  - Healthcare App Token (ID 0.A)
  - Country 1 Token (ID 0.B)
    - Game Studio 2 Token (ID B.C)
      - Game 2 Token (ID C.D)
        - NFT 4 (ID D.E)
      - Game 4 Token (ID C.F)
        - NFT 5 (ID F.10)
    - ISP Token (ID B.11)
  - Fiance App Token (ID 0.12)

```

# NFT Staking (Staking Program)

Author: Dhruv Patel

Overview
- This repository contains a Solana/Anchor program and TypeScript test harness for NFT staking. The program lets NFT owners stake tokens from a tracked collection to earn time-based rewards.

Key actions
- initialize: Set up the on-chain config account that stores reward parameters and collection tracking.
- create_collection: Register a verified NFT collection (collection-level metadata) so the program can track which NFTs are eligible to stake.
- mint_asset: Mint an NFT in the registered collection (done off-chain or with your standard token-minting flow); the program expects NFTs to be correctly attributed to the collection.
- stake: Lock an eligible NFT into the program’s stake account for a user; staking begins reward accrual based on configured rates.
- claim_rewards: Claim accrued reward tokens (or account balances) for a staked NFT without unstaking it.
- unstake: Unlock the NFT and stop reward accrual; any unclaimed rewards can be claimed before or after unstaking depending on the config.

Reward logic (brief)
- Rewards accrue over time while an NFT is staked. The program stores a per-collection reward rate and uses timestamps to calculate earned rewards since the last claim or stake action.
- Claiming resets the last-claimed timestamp for that stake so future accrual starts after the claim.

Collection staking tracking
- The program maintains collection-level metadata and per-NFT stake records. Only NFTs from a registered collection are eligible to stake; the program tracks which NFTs are currently staked and who owns each stake.

Local development and common commands
- Install JavaScript dependencies with Bun:

```bash
bun install
```

- Build the Anchor program:

```bash
anchor build
```

- Run the TypeScript test suite (Bun test harness):

```bash
bun test
```
Project Structure
staking/
│
├── programs/
│   └── staking/
│       └── src/
│           ├── instructions/
│           ├── state/
│           ├── constants.rs
│           ├── error.rs
│           └── lib.rs
│
├── tests/
│   ├── functional/
│   ├── setup.ts
│   ├── constants.ts
│   └── pda.ts
│
├── migrations/
│   └── deploy.ts
│
├── target/
│
├── Anchor.toml
├── Cargo.toml
├── package.json
├── tsconfig.json
└── README.md

Notes and safety
- The repository keeps Anchor configuration files and program code intact; do not change `Anchor.toml` or the program `Cargo.toml` unless you understand how program IDs and builds are managed.
- This README focuses on the developer workflow for local testing and iteration.

If you want, I can also add brief example commands or a short walkthrough showing how to run the test fixtures and a quick end-to-end stake/claim cycle locally.

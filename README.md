# Acala Network

# Acala audit details
- Total Prize Pool: 36,500 in USDC
  - HM awards: 27,750 in USDC
  - Analysis awards: 1,500 in USDC
  - QA awards: 750 in USDC
  - Judge awards: 3,600 in USDC
  - Lookout awards: 2,400 in USDC
  - Scout awards: $500 in USDC
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2024-03-acala/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts March 22, 2024 20:00 UTC
- Ends April 5, 2024 20:00 UTC

## Publicly Known Issues
_Note for C4 wardens: Anything included in this `Publicly Known Issues` section is considered a publicly known issue and is ineligible for awards._

No publicly known issues

# Overview

The following substrate modules are used by Acala Network to implement staking and earning functionality and are in scope for this audit:

- [Incentives](https://github.com/code-423n4/2024-03-acala/tree/main/src/modules/incentives/): Substrate module for staking LP tokens, keeping track of shares and incentives for staking pools.

- [Rewards](https://github.com/code-423n4/2024-03-acala/tree/main/src/orml/rewards/): Used by the incentives module to calculate and distribute rewards to users.

- [Earning](https://github.com/code-423n4/2024-03-acala/tree/main/src/modules/earning/): Implements a bond/locked token system, which allows users to lock their tokens for a period of time.

## Links

- **Previous audits:** https://github.com/AcalaNetwork/Acala/tree/master/audit
- **Documentation:** https://guide.acalaapps.wiki/staking/aca-staking
- **Website:** https://acala.network
- **Twitter:** https://twitter.com/AcalaNetwork
- **Discord:** https://acala.gg
- **Main Repo:** http://github.com/AcalaNetwork/Acala

# Scope

- [Incentives](https://github.com/code-423n4/2024-03-acala/tree/main/src/modules/incentives/src/lib.rs): Each period, pools will accumulate incentives and rewards are distributed to them from RewardsSource. Each pool can receive multiple incentives. Users can claim rewards from the pool at any time. Deduction rate is configurable and is applied to the rewards when they are claimed. When a user adds liquidity to the pool, they receive shares, and withdrawn rewards are adjusted accordingly so the new user will start with no reward.

- [Rewards](https://github.com/code-423n4/2024-03-acala/tree/main/src/orml/rewards/src/lib.rs): This module contains the base methods for calculating and distributing rewards. It is used by the incentives module to calculate and distribute rewards to users.

- [Earning](https://github.com/code-423n4/2024-03-acala/tree/main/src/modules/earning/src/lib.rs): Users will bond/lock their tokens for a period of time. Unbonding/unlocking is possible by paying a fee/penalty, or requesting to unbond/unlock and waiting for the unbonding period to finish before you can withdraw. The module implements a set of hooks that can be used by other modules (i.e. Incentives) to implement staking.

## Out of scope

The following modules are out of scope for this audit. They are not used by the modules in scope and are not required for the functionality of the protocol. They are included in the repository to make it easier to run the tests.

- [EVM Utility](https://github.com/code-423n4/2024-03-acala/tree/main/src/modules/evm-utility)
- [Stable Asset](https://github.com/code-423n4/2024-03-acala/tree/main/src/modules/stable-asset)
- [Support](https://github.com/code-423n4/2024-03-acala/tree/main/src/modules/support)
- [Tokens](https://github.com/code-423n4/2024-03-acala/tree/main/src/orml/tokens)
- [Traits](https://github.com/code-423n4/2024-03-acala/tree/main/src/orml/traits)
- [Utilities](https://github.com/code-423n4/2024-03-acala/tree/main/src/orml/utilities)


# Additional Context

- This code is deployed to both Karura and Acala
  - Karura Block Explorer: http://karura.subscan.io
  - Karura RPC: wss://karura-rpc.aca-api.network
  - Acala Block Explorer: http://acala.subscan.io
  - Acala RPC: wss://acala-rpc.aca-api.network
- Continious DoS more than 2 hours is considered valid.

## Attack ideas (Where to look for bugs)

- Find a way to unstake bypass the bonding duration
- Find a way to gain more shares than you should
- Find a way to claim more rewards than you should

## Main invariants

- No token minting / burning
- Staker always gets more or equal amount of tokens back

## Scoping Details 

```
- If you have a public code repo, please share it here: https://github.com/AcalaNetwork/Acala 
- How many contracts are in scope?:   3
- Total SLoC for these contracts?:  1135
- How many external imports are there?: 1 
- How many separate interfaces and struct definitions are there for the contracts within scope?: 5 
- Does most of your code generally use composition or inheritance?:   Composition
- How many external calls?:   0
- What is the overall line coverage percentage provided by your tests?: 85
- Is this an upgrade of an existing system?: No
- Check all that apply (e.g. timelock, NFT, AMM, ERC20, rollups, etc.): ERC-20 Token, Non ERC-20 Token, Timelock function
- Is there a need to understand a separate part of the codebase / get context in order to audit this part of the protocol?: No  
- Please describe required context:   
- Does it use an oracle?:  No
- Describe any novel or unique curve logic or mathematical models your code uses: 
- Is this either a fork of or an alternate implementation of another project?:   Yes
- Does it use a side-chain?: 
- Describe any specific areas you would like addressed:
```

# Tests

Refer to [this](https://docs.substrate.io/install/) guide for detailed instructions to setup dev env.

Please ensure you working directory is `./src`

- Build: `cargo build`
- Test: `cargo test`

## Miscellaneous

Employees of Acala Foundation and employees' family members are ineligible to participate in this audit.

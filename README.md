# Acala Network

## Build and test

Refer to [this](https://docs.substrate.io/install/) guide for detailed instructions to setup dev env.

Please ensure you working directory is `./src`

- Build: `cargo build`
- Test: `cargo test`

# Repo setup

## ⭐️ Sponsor: Add code to this repo

- [ ] Create a PR to this repo with the below changes:
- [ ] Provide a self-contained repository with working commands that will build (at least) all in-scope contracts, and commands that will run tests producing gas reports for the relevant contracts.
- [ ] Make sure your code is thoroughly commented using the [NatSpec format](https://docs.soliditylang.org/en/v0.5.10/natspec-format.html#natspec-format).
- [ ] Please have final versions of contracts and documentation added/updated in this repo **no less than 48 business hours prior to audit start time.**
- [ ] Be prepared for a 🚨code freeze🚨 for the duration of the audit — important because it establishes a level playing field. We want to ensure everyone's looking at the same code, no matter when they look during the audit. (Note: this includes your own repo, since a PR can leak alpha to our wardens!)


---

## ⭐️ Sponsor: Edit this `README.md` file

- [ ] Modify the contents of this `README.md` file. Describe how your code is supposed to work with links to any relevent documentation and any other criteria/details that the C4 Wardens should keep in mind when reviewing. ([Here's a well-constructed example.](https://github.com/code-423n4/2022-08-foundation#readme))
- [ ] Review the Gas award pool amount. This can be adjusted up or down, based on your preference - just flag it for Code4rena staff so we can update the pool totals across all comms channels.
- [ ] Optional / nice to have: pre-record a high-level overview of your protocol (not just specific smart contract functions). This saves wardens a lot of time wading through documentation.
- [ ] [This checklist in Notion](https://code4rena.notion.site/Key-info-for-Code4rena-sponsors-f60764c4c4574bbf8e7a6dbd72cc49b4#0cafa01e6201462e9f78677a39e09746) provides some best practices for Code4rena audits.

## ⭐️ Sponsor: Final touches
- [ ] Review and confirm the details in the section titled "Scoping details" and alert Code4rena staff of any changes.
- [ ] Review and confirm the list of in-scope files in the `scope.txt` file in this directory.  Any files not listed as "in scope" will be considered out of scope for the purposes of judging, even if the file will be part of the deployed contracts.
- [ ] Check that images and other files used in this README have been uploaded to the repo as a file and then linked in the README using absolute path (e.g. `https://github.com/code-423n4/yourrepo-url/filepath.png`)
- [ ] Ensure that *all* links and image/file paths in this README use absolute paths, not relative paths
- [ ] Check that all README information is in markdown format (HTML does not render on Code4rena.com)
- [ ] Remove any part of this template that's not relevant to the final version of the README (e.g. instructions in brackets and italic)
- [ ] Delete this checklist and all text above the line below when you're ready.

---

# Acala audit details
- Total Prize Pool: 36,500 in USDC
  - HM awards: 27,750 in USDC
  - Analysis awards: 1,500 in USDC
  - QA awards: 750 in USDC
  - Judge awards: 3,600 in USDC
  - Lookout awards: 2,400 in USDC
  - Scout awards: $500 in USDC
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2024-01-acala/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts January 22, 2024 20:00 UTC
- Ends TBD February 2, 2024 20:00 UTC

## Automated Findings / Publicly Known Issues
_Note for C4 wardens: Anything included in this `Automated Findings / Publicly Known Issues` section is considered a publicly known issue and is ineligible for awards._

[ ⭐️ SPONSORS: Are there any known issues or risks deemed acceptable that shouldn't lead to a valid finding? If so, list them here. ]


# Overview

The following substrate modules are used by Acala Network to implement staking and earning functionality and are in scope for this audit:

- [Incentives](src/modules/incentives/): Substrate module for staking LP tokens, keeping track of shares and incentives for staking pools.

- [Rewards](src/orml/rewards/): Used by the incentives module to calculate and distribute rewards to users.

- [Earning](src/modules/earning/): Implements a bond/locked token system, which allows users to lock their tokens for a period of time.

## Links

- **Previous audits:** https://github.com/AcalaNetwork/Acala/tree/master/audit
- **Documentation:** https://guide.acalaapps.wiki/staking/aca-staking
- **Website:** https://acala.network
- **Twitter:** https://twitter.com/AcalaNetwork
- **Discord:** https://acala.gg
- **Main Repo:** http://github.com/AcalaNetwork/Acala

# Scope

- [Incentives](src/modules/incentives/src/lib.rs): Each period, pools will accumulate incentives and rewards are distributed to them from RewardsSource. Each pool can receive multiple incentives. Users can claim rewards from the pool at any time. Deduction rate is configurable and is applied to the rewards when they are claimed. When a user adds liquidity to the pool, they receive shares, and withdrawn rewards are adjusted accordingly so the new user will start with no reward.

- [Rewards](src/orml/rewards/src/lib.rs): This module contains the base methods for calculating and distributing rewards. It is used by the incentives module to calculate and distribute rewards to users.

- [Earning](src/modules/earning/src/lib.rs): Users will bond/lock their tokens for a period of time. Unbonding/unlocking is possible by paying a fee/penalty, or requesting to unbond/unlock and waiting for the unbonding period to finish before you can withdraw. The module implements a set of hooks that can be used by other modules (i.e. Incentives) to implement staking.

## Out of scope

The following modules are out of scope for this audit. They are not used by the modules in scope and are not required for the functionality of the protocol. They are included in the repository to make it easier to run the tests.

- [EVM Utility](src/modules/evm-utility)
- [Stable Asset](src/modules/stable-asset)
- [Support](src/modules/support)
- [Tokens](src/orml/tokens)
- [Traits](src/orml/traits)
- [Utilities](src/orml/utilities)


# Additional Context

- [ ] Describe any novel or unique curve logic or mathematical models implemented in the contracts
- [ ] Please list specific ERC20 that your protocol is anticipated to interact with. Could be "any" (literally anything, fee on transfer tokens, ERC777 tokens and so forth) or a list of tokens you envision using on launch.
- [ ] Please list specific ERC721 that your protocol is anticipated to interact with.
- [ ] Which blockchains will this code be deployed to, and are considered in scope for this audit?
- [ ] Please list all trusted roles (e.g. operators, slashers, pausers, etc.), the privileges they hold, and any conditions under which privilege escalation is expected/allowable
- [ ] In the event of a DOS, could you outline a minimum duration after which you would consider a finding to be valid? This question is asked in the context of most systems' capacity to handle DoS attacks gracefully for a certain period.
- [ ] Is any part of your implementation intended to conform to any EIP's? If yes, please list the contracts in this format: 
  - `Contract1`: Should comply with `ERC/EIPX`
  - `Contract2`: Should comply with `ERC/EIPY`

## Attack ideas (Where to look for bugs)
*List specific areas to address - see [this blog post](https://medium.com/code4rena/the-security-council-elections-within-the-arbitrum-dao-a-comprehensive-guide-aa6d001aae60#9adb) for an example*

## Main invariants
*Describe the project's main invariants (properties that should NEVER EVER be broken).*

## Scoping Details 
[ ⭐️ SPONSORS: please confirm/edit the information below. ]

```
- If you have a public code repo, please share it here:  
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

*Provide every step required to build the project from a fresh git clone, as well as steps to run the tests with a gas report.* 

*Note: Many wardens run Slither as a first pass for testing.  Please document any known errors with no workaround.* 

## Miscellaneous

Employees of [SPONSOR NAME] and employees' family members are ineligible to participate in this audit.

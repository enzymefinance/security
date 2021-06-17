# Enzyme Bug Report - 5 May 2021

# Summary

- A potential vulnerability in one of the Enzyme Finance smart contracts was identified by Avantgarde
- The vulnerability was fixed, and a new release was deployed.
- The vulnerability has not been exploited, and it does no longer exist.

# Background/Timeline

- On May 5, 2021, the Avantgarde Finance team discovers that withdrawals from certain vaults lead to partial internal transaction failures.
- The team identifies that the failing piece of code is in the `PerformanceFee` contract, and it prevents the payout of performance fees for the affected vaults on share redemption.
- A detailed analysis of the failing piece of code reveals that (apart from a minor correctness issue) a carefully crafted redemption transaction could lead to a situation where the vault manager would be able to pay themselves large amounts of shares as performance fee. This attack could be repeated several times, which would lead to a substantial dilution of share value for depositors.
- The team notifies three members of the Enzyme Council (with an auditing background) as well as the protocol auditors (ChainSecurity), using a secure chat on Keybase.
- After having identified the affected vaults, the Avantgarde Finance team settles all outstanding fees for those vaults in a series of transactions. This is necessary in order to record the most up-to-date performance of the vaults, thereby securing past performance fees for vault managers (in particular vaults that had not seen deposits or withdrawals for a longer period).
- On May 6, 2021, all assets with non-standard decimals are removed from the protocol. After this removal, the bug can no longer be exploited. However, the affected vaults can no longer accept new deposits, and they migrate to a new release.
- The Avantgarde Finance team fixes the bug, and deploys a new release on May 7, 2021. The fix is audited by ChainSecurity.
- The team prepares the Enzyme App and the Enzyme Subgraph to handle migrations. An updated version of the app is released on May 9.
- In order to incentivise migrations and to mitigate the inconvenience caused by the bug, the Enzyme Council subsidies the gas costs of the migrations with 5 MLN per vault.

# Documents

[ChainSecurity Report](chainsecurity-report.pdf)

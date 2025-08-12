## Common missing checks

### Missing staleness check

Oracles can sometimes, for a multitude of reasons, experience stale prices, meaning that when `lastRoundData()` is called, an old, no longer accurate price is returned. This can lead to wrongful liquidations, problems with perpetual pricing, and many more issues depending on the protocol. This can be mitigated by checking the timestamp of the price returned by the oracle

[Example](https://solodit.cyfrin.io/issues/stale-oracle-price-data-not-checked-before-token-operations-may-drain-assets-from-protocol-quantstamp-vusd-stablecoin-markdown)


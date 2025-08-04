## Common missing checks

### Missing staleness check

Oracles can sometimes, for a multitude of reasons, experience stale prices, meaning that when `lastRoundData()` is called, an old, no longer accurate price is returned. This can lead to wrongful liquidations, problems with perpetual pricing, and many more issues depending on the protocol. This can be mitigated by checking the timestamp of the price returned by the oracle

[Example](https://solodit.cyfrin.io/issues/stale-oracle-price-data-not-checked-before-token-operations-may-drain-assets-from-protocol-quantstamp-vusd-stablecoin-markdown)

### Missing sequencer uptime check

When using oracles on a layer two, it's important to ensure the sequencer is actually up, as when the sequencer is down, prices that are in reality stale or extrapolated can pass staleness checks and lead to the same issues mentioned above. The sequencer being down can also lead to other problems, such as giving users who directly interact with the network an unfair advantage. To mitigate this, check for sequencer uptime, for example, by using a specific oracle.

[Example](https://solodit.cyfrin.io/issues/missing-l2-sequencer-uptime-check-in-oracleadapter-cyfrin-none-yieldfi-markdown)

[Further reading on sequencer uptime](https://docs.chain.link/data-feeds/l2-sequencer-feeds)
## Multichain deployment
### Are any addresses hard coded
If any addresses (tokens, pools....) are hard coded and the protocol is deployed on different chains, the addresses will only be correct on one chain, leading to core functionalities failing. 
[Example](https://solodit.cyfrin.io/issues/the-libweth-hardcodes-the-weth-address-which-makes-it-incompatible-on-the-to-deploy-l2-chain-codehawks-beanstalk-the-finale-git)

### `block.number` refers to the L1 block on Arbitrum

When calling block.number, the approximate block number on Mainnet will be returned by Arbitrum, not of the current Arbitrum block. This can lead to problems, especially since the block time on Arbitrum is only a fraction of the block time on Mainnet. To mitigate this use `arbBlockNumber()` instead

[Example](https://solodit.cyfrin.io/issues/incorrect-use-of-l1-blocknumber-on-arbitrum-cantina-none-uniswap-pdf)

### General stuff
### Missing sequencer uptime check

When using oracles on a layer two, it's important to ensure the sequencer is actually up, as when the sequencer is down, prices that are in reality stale or extrapolated can pass staleness checks and lead to the same issues mentioned above. The sequencer being down can also lead to other problems, such as giving users who directly interact with the network an unfair advantage. To mitigate this, check for sequencer uptime, for example, by using a specific oracle.

[Example](https://solodit.cyfrin.io/issues/missing-l2-sequencer-uptime-check-in-oracleadapter-cyfrin-none-yieldfi-markdown)

[Further reading on sequencer uptime](https://docs.chain.link/data-feeds/l2-sequencer-feeds)


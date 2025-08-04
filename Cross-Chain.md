## LayerZero
### Are refunds from` _lzsend` actually send to the right recipient. 
The address of the recipient of any excess gas which is not used by `_lzsend` is passed to the function as a parameter. Often, the `msg.sender` is passed, which isn't always the user or contract that should receive the refund. This can also lead to permanently lost funds if the contract that gets the excess gas refunds doesn't have a withdrawal mechanism.
[Example](https://solodit.cyfrin.io/issues/m-04-layerzero-fee-refunds-misdirected-to-deposit-contracts-pashov-audit-group-none-nexus_2024-11-29-markdown)

## General

### Make sure any tokens used have the same decimals on both/all chains 
Some tokens like `USDC` have different tokens on different chains. Make sure that all tokens either have the same decimals on all chains or are converted correctly. 

[Example](https://solodit.cyfrin.io/issues/h-11-users-will-lose-funds-due-to-token-decimal-mismatches-across-chains-sherlock-lend-git)
## LayerZero
### Are refunds from` _lzsend` actually send to the right recipient. 
The address of the recipient of any excess gas which is not used by `_lzsend` is passed to the function as a parameter. Often, the `msg.sender` is passed, which isn't always the user or contract that should receive the refund. This can also lead to permanently lost funds if the contract that gets the excess gas refunds doesn't have a withdrawal mechanism.
[Example](https://solodit.cyfrin.io/issues/m-04-layerzero-fee-refunds-misdirected-to-deposit-contracts-pashov-audit-group-none-nexus_2024-11-29-markdown)

### Is enough gas provided on the source chain
LayerZero recommends that at least 200k gas should be passed to the send function on the source chain to cover gas on the destination chain. Check that the user or the protocol depending on business logic passes at least that amount. 
[Example](https://solodit.cyfrin.io/issues/h-02-due-to-missing-checks-on-minimum-gas-passed-through-layerzero-executions-can-fail-on-the-destination-chain-code4rena-decent-decent-git)
## General

### Make sure any tokens used have the same decimals on both/all chains 
Some tokens like `USDC` have different tokens on different chains. Make sure that all tokens either have the same decimals on all chains or are converted correctly. 

[Example](https://solodit.cyfrin.io/issues/h-11-users-will-lose-funds-due-to-token-decimal-mismatches-across-chains-sherlock-lend-git)

### Cross chain replay attack
Even when a proper nonce is implemented to make sure each signature can only be used once, an attacker can reuse the message across different chains if the nonce's match and the message itself doesn't contain the chain Id (or the chain specific parameter can be entered arbitrary by the user) or any other value that ensures its chain specific. 
[Example](https://solodit.cyfrin.io/issues/h-01-cross-chain-signature-replay-attack-due-to-user-supplied-domainseparator-and-missing-deadline-check-code4rena-next-generation-next-generation-git)


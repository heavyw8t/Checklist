## Liquidation

### Does the protocol deal with bad debt somehow?
Can a liquidation somehow result in bad debt remaining? If it's now economically viable for a liquidator to liquidate the remaining position, it will remain in the system and cause a loss of funds for either the protocol or other users. Sometimes this can also happen if the remaining positions are very small and the gas cost would be higher than the liquidation reward a liquidator would get. There are many ways to mitigate this, such as insurance or spreading the loss among all users.

[Example](https://solodit.cyfrin.io/issues/m-32-malicious-liquidator-can-intentionally-leave-dust-amount-of-collateral-and-wont-trigger-bad-debt-handling-sherlock-peapods-git)

## Health factor

### Is the health factor calculated at the right time of the transaction? Is it calculated with the before or after values?
In some cases, the health factor is calculated with the wrong values. For example, the collateral gets reduced, but the health factor is accidentally calculated with the old collateral value, or the collateral gets reduced, but then the health factor function itself reduces the collateral again in the calculation, leading to any call failing unless the user has way more collateral than required.

[Example](https://code4rena.com/audits/2025-03-starknet-perpetual/submissions/S-591)
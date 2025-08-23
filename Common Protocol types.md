## Dexes

### Missing slippage protection
When liquidity is added to a pool or a user uses the pool to trade, they should always be able to set some sort of slippage protection, causing the transaction to revert in case they don't get at least a specified minimum amount of LP tokens or of the bought token.
[Example](https://solodit.cyfrin.io/issues/m-15-addliquidity-and-decreaseliquidity-missing-slippage-protection-code4rena-particle-protocol-particle-protocol-git)

## ERC-4626 (Vaults)

### Inflation attack
When a new vault is created, the first depositor can be frontrun by an attacker who will deposit just enough so that the initial depositor's shares will be rounded down to 0, and the attacker can withdraw their one share, now also containing the victim's tokens. This can be mitigated by allowing users to pass a `minSharesOutParameter` or using "dead shares," which are placed in the vault during creation.

[Example](https://solodit.cyfrin.io/?b=false&f=&ff=&i=HIGH&l=&maxf=&minf=&p=1&pc=&pn=&qs=1&r=true&rf=alltime&rs=1&s=inflation+attack&sd=Desc&sf=Recency&t=&u=&ur=true)
[Further reading](https://blog.openzeppelin.com/a-novel-defense-against-erc4626-inflation-attacks)

### Rounding errors
When shares are minted or burned, the protocol should do so in a way that benefits the protocol; otherwise, attackers can use user-benefiting rounding to steal funds from the protocol and users or grief by iterating through the deposit and withdraw functions multiple times

[Example](https://solodit.cyfrin.io/?b=false&f=&ff=&i=HIGH&l=&maxf=&minf=&p=1&pc=&pn=&qs=1&r=true&rf=alltime&rs=1&s=rounding+vault&sd=Desc&sf=Recency&t=&u=&ur=true)


## Lending

### Does the protocol deal with bad debt somehow?
Can a liquidation somehow result in bad debt remaining? If it's now economically viable for a liquidator to liquidate the remaining position, it will remain in the system and cause a loss of funds for either the protocol or other users. Sometimes this can also happen if the remaining positions are very small and the gas cost would be higher than the liquidation reward a liquidator would get. There are many ways to mitigate this, such as insurance or spreading the loss among all users.

[Example](https://solodit.cyfrin.io/issues/m-32-malicious-liquidator-can-intentionally-leave-dust-amount-of-collateral-and-wont-trigger-bad-debt-handling-sherlock-peapods-git)


### Is the health factor calculated at the right time of the transaction? Is it calculated with the before or after values?
In some cases, the health factor is calculated with the wrong values. For example, the collateral gets reduced, but the health factor is accidentally calculated with the old collateral value, or the collateral gets reduced, but then the health factor function itself reduces the collateral again in the calculation, leading to any call failing unless the user has way more collateral than required.

[Example](https://code4rena.com/audits/2025-03-starknet-perpetual/submissions/S-591)
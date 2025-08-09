
## General Stuff

### USDC only has 6 decimals on most chains
Check that the actual decimals of the tokens used are always accounted for, especially in protocols where most or any ERC-20 can be used. Check for hard coded decimals in calculations. 
[Example](https://solodit.cyfrin.io/?b=false&f=&ff=&i=HIGH%2CMEDIUM&l=&maxf=&minf=&p=1&pc=&pn=&qs=1&r=true&rf=alltime&rs=1&s=usdc+decimals&sd=Desc&sf=Recency&t=&u=&ur=true)

### Fee on Transfer tokens reduce the actual received amount
Fee on transfer tokens (FOT) take a small cut of every transfer and burn it or send it to a fee receiver address. This can be done to collect fees or for deflationary purposes. The problem here occurs when instead of checking the actually received amounts, the amount that the users sends is used by the internal accounting. This can lead to either reverts because of insufficient balances or the receiver getting less then they should. This issue is out of scope on some platforms so double check the rules. To mitigate this use the delta of the receiver/contract's token balance before and after the transfer or only whitelist specific ERC-20's.
[Example](https://solodit.cyfrin.io/issues/m-02-incorrect-receipt-token-minting-for-fee-on-transfer-tokens-shieldify-none-multipli-markdown)

## USDT (definitely the most common weird ERC20)

### is `forceApprove` used?
`USTD` will revert when trying to change the approved amount from a non-zero amount to another non-zero amount. The amount always has to be reset to 0, either by actually transferring the whole approved amount or manually. Use `forceApprove` to mitigate this
[Example](https://solodit.cyfrin.io/issues/some-contracts-might-not-work-properly-with-usdt-allowance-openzeppelin-none-across-audit-markdown)

### is a return expected?
`USDT` doesn't return a bool, which means any logic that requires a boolean return value, such as the classic `IERC20().transfer()` function, will revert. Use the `safeERC20` library and its functions to mitigate this issue.

[Example](https://solodit.cyfrin.io/issues/usdt-cannot-be-withdrawn-from-aavev3yieldmanager-cantina-none-level-money-pdf)


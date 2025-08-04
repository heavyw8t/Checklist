## Morpho
### `Morpho.repay` will revert if there is no dept to repay
If `morpho.repay()` is called with 0 shares and 0 assets to repay, for example, if a protocol migrates a position from one router to another and calls the repay function every time without checking if any debt exists. To mitigate this, check if the shares and assets to repay parameters will both be 0 before calling `morpho.repay()`.

[Example](https://github.com/sherlock-audit/2025-06-notional-exponent-judging/issues/674)

## Ethena

### The cool down for withdrawals can be set to 0 which can lead to problems when the protocol expects an asynchronous redeeming process

Usually, a certain cool-down period is set for withdrawals when withdrawing from Ethena. In some cases, this cool-down can be set to zero, which causes any funds to instantly be transferred when withdrawing. The protocol needs to implement a check for this case; otherwise, the user won't receive any tokens when finalizing the withdrawal, as they have already been transferred to the protocol and might even be frozen there permanently if there is no admin withdrawal.

[Example](https://github.com/sherlock-audit/2025-06-notional-exponent-judging/issues/263)

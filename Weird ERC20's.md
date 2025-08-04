## USDT (definitely the most common weird ERC20)

### is `forceApprove` used?
`USTD` will revert when trying to change the approved amount from a non-zero amount to another non-zero amount. The amount always has to be reset to 0, either by actually transferring the whole approved amount or manually. Use `forceApprove` to mitigate this
[Example](https://solodit.cyfrin.io/issues/some-contracts-might-not-work-properly-with-usdt-allowance-openzeppelin-none-across-audit-markdown)


### is a return expected?
`USDT` doesn't return a bool, which means any logic that requires a boolean return value, such as the classic `IERC20().transfer()` function, will revert. Use the `safeERC20` library and its functions to mitigate this issue.

[Example](https://solodit.cyfrin.io/issues/usdt-cannot-be-withdrawn-from-aavev3yieldmanager-cantina-none-level-money-pdf)


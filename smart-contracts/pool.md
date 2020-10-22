# `IPool`

# Configuration Queries

## `isPublicSwap`

```
function isPublicSwap() returns (bool isPublic)
```

Check if swapping tokens and joining the pool is allowed.

## `getSwapFee`

```
function getSwapFee() returns (uint256 swapFee)
```

## `getController`

```
function getController() returns (address controller)
```

Returns the controller address.

# Token Queries

## `getNumTokens`

```
function getNumTokens() returns (uint256 num)
```

Get the number of tokens bound to the pool.

## `getCurrentTokens`

```
function getCurrentTokens() returns (address[] tokens)
```

Get all bound tokens.

## `getCurrentDesiredTokens`

```
function getCurrentDesiredTokens() returns (address[] tokens)
```

Returns the list of tokens which have a desired weight above 0.

Tokens with a desired weight of 0 are set to be phased out of the pool.

## `getTotalDenormalizedWeight`

```
function getTotalDenormalizedWeight()
returns (uint256 totalDenorm)
```

Get the total denormalized weight of the pool.

## `getDenormalizedWeight`

```
function getDenormalizedWeight(
  address token
) returns (uint256 denorm)
```

Get the denormalized weight of a bound token.


## `getTokenRecord`

```
function getTokenRecord(
  address token
) returns (Record record)
```

Get the record for a token bound to the pool.


## `getBalance`

```
function getBalance(
  address token
) returns (uint256 balance)
```

Get the stored balance of a bound token.

## `getMinimumBalance`

```
function getMinimumBalance(
  address token
) returns (uint256 minimumBalance)
```

Get the minimum balance of an uninitialized token.

Note: Throws if the token is initialized.

## `getUsedBalance`

```
function getUsedBalance(
  address token
) returns (uint256 usedBalance)
```

Get the balance of a token which is used in price calculations. If the token is initialized, this is the stored balance; if not, this is the minimum balance.

# Price Queries

## `extrapolatePoolValueFromToken()`

```
function extrapolatePoolValueFromToken()
returns (
  address token,
  uint256 extrapolatedValue
)
```

Finds the first token which is initialized and returns the address of that token and the extrapolated value of the pool in that token.

The value is extrapolated by multiplying the token's balance by the reciprocal of its normalized weight.

## `getSpotPrice`

```
function getSpotPrice(
  address tokenIn,
  address tokenOut
) returns (uint256 spotPrice)
```

Get the spot price for `tokenOut` in terms of `tokenIn`.

## `getSpotPriceSansFee`

```
function getSpotPriceSansFee(
  address tokenIn,
  address tokenOut
) returns (uint256 spotPrice)
```

Get the spot price for `tokenOut` in terms of `tokenIn` ignoring swap fees.

## `getInGivenOut`

```
function getInGivenOut(
  address tokenIn,
  address tokenOut,
  uint256 tokenAmountOut
) returns (uint256 tokenAmountIn)
```

Calculate the amount of `tokenIn` needed to receive `tokenAmountOut` of `tokenOut`.

## `getOutGivenIn`

```
function getOutGivenIn(
  address tokenIn,
  address tokenOut,
  uint256 tokenAmountIn
) returns (uint256 tokenAmountOut)
```

Calculate the amount of `tokenOut` which can be received for `tokenAmountIn` of `tokenIn`.

# Control Actions

## `configure`

```
function configure(
  address controller,
  string calldata name,
  string calldata symbol
)
```

**Summary**

Sets the controller address and the token name & symbol. This saves on storage costs for multi-step pool deployment.

**Notes**

The stored controller address must be zero.

## `initialize`

```
function initialize(
  address[] tokens,
  uint256[] balances,
  uint96[] denorms,
  address tokenProvider,
  address unbindHandler
)
```

**Summary**

Sets up the initial assets for the pool.

**Notes**

Each token added in this function must have a corresponding weight and initial balance. 

`tokenProvider` must have approved the pool to transfer the provided balances of each token.

The provided balance of each token should be worth the token's proportional weight of the pool value.

## `setSwapFee`
```
function setSwapFee(uint256 swapFee)
```

**Summary**

Sets the swap fee.

**Notes**

The swap fee must be between 0.0001% and 10%

## `reweighTokens`

```
function reweighTokens(
  address[] calldata tokens,
  uint96[] calldata desiredDenorms
)
```

**Summary**

This function sets the desired weights for the assets in the pool. It is not time-restricted because the pool controller is responsible for managing the portfolio.

**Notes**

The following requirements are assumptions that are not checked within the pool contract in order to save gas, but are met by the pool controller:
- The total of desired weights should equal the default total weight of 25.
- The number of tokens should be equal to the index size.
- Only the tokens with a desired weight above 0 should be included: tokens which are in the process of being phased out may still be in the pool, but should not be factored into the new weight calculations.

## `reindexTokens`

```
function reindexTokens(
  address[] calldata tokens,
  uint96[] calldata desiredDenorms,
  uint256[] calldata minimumBalances
)
```

**Inputs**

- `address[] tokens` - Underlying tokens the pool should hold.
- `uint96[] desiredDenorms` - Desired weights for each token.
- `uint256[] minimumBalances` - Minimum balance for each token - the number of tokens which is equal to 1/25 of the current pool's portfolio.

These arrays must all have the same length, which should be equal to the index size.

**Summary**

Sets the desired underlying assets for the pool and their target weights, which may or may not include some or all of the current underlying tokens.

**Notes**

Any currently bound tokens which are not provided in the input will be marked for removal (desired weight set to 0). For tokens which are not already bound, the minimum balance will be assigned in the `_minimumBalances` mapping; otherwise, the minimum balance provided is not used.

If a token is provided with a desired weight less than the minimum weight, the weight is replaced with the minimum. This is meant to ensure that the pool maintains the desired index size even if one asset is set to a substantially lower weight than any of the other assets. This will probably never happen given the way that weights are calculated.

## `unbind`

```
function unbind(address token)
```

**Summary**

This function instantly removes a bound token and sends the remaining balance to the pool controller. This is intended to be a last-resort mechanism to handle a quickly crashing token or one which has been found to have a significant vulnerability.

# Liquidity Functions

## `joinPool`

```
function joinPool(
  uint256 poolAmountOut,
  uint256[] calldata maxAmountsIn
)
```

**Inputs**
- `uint256 poolAmountOut` - The number of pool tokens to mint
- `uint256[] maxAmountsOut` - Maximum amounts of underlying tokens to transfer, in the order of the `_tokens` array.

`maxAmountsOut` must have a length equal to `_tokens`.

**Summary**

Mint new pool tokens by providing the proportional amount of each underlying token's balance equal to the proportional pool tokens being minted, e.g. to mint 10 pool tokens when there are 100, the caller must provide 1/10 of each underlying token's balance. For any underlying tokens which are not initialized, the caller must provide the proportional share of the minimum balance for the token rather than the actual balance.

**Notes**

The amount of underlying tokens to transfer for each token can not:
- exceed the corresponding maximum from `maxAmountsOut`
- be 0
- exceed 1/2 the current balance (or minimum balance in the case of uninitialized tokens)

The amount of pool tokens to mint can not be 0.

If any input token is not initialized, its balance will be replaced with the token's minimum balance and its weight will be replaced with the minimum weight [plus a premium determined by the token's distance from the minimum balance](#weight-for-price-calculations). This is only for the purpose of price calculations and is not written to storage.

If any input token is brought above its minimum balance, it will be marked as initialized and its record will be assigned the minimum weight plus a [factor proportional to the amount by which the minimum balance was exceeded](#weight-when-token-is-initialized).

If any input token has a higher desired weight than its real weight and has not been adjusted in the last hour, it will move towards the real weight with a maximum difference of $$\frac{weight \cdot fee}{2}$$. If the token is not initialized and has still not met its minimum balance after the swap, its weight will not be adjusted.

## `joinswapExternAmountIn`

```
function joinswapExternAmountIn(
  address tokenIn,
  uint256 tokenAmountIn,
  uint256 minPoolAmountOut
) returns (uint256 poolAmountOut)
```

**Summary**

Pay `tokenAmountIn` of `tokenIn` to mint at least `minPoolAmountOut` pool tokens.

The pool implicitly swaps `(1- weightTokenIn) * tokenAmountIn` to the other underlying tokens. Thus a swap fee is charged against the input tokens.

**Notes**

`tokenAmountIn` can not:
- be 0
- exceed 1/2 the current balance (or minimum balance in the case of uninitialized tokens) of `tokenIn`

If `tokenIn` is not initialized, its balance will be replaced with `_minimumBalances[tokenIn]` and its weight will be replaced with the minimum weight [plus a premium determined by the token's distance from the minimum balance](#weight-for-price-calculations). This is only for the purpose of price calculations and is not written to storage.

If `tokenAmountIn` brings the real balance above the minimum balance, `tokenIn` will be marked as initialized and its record will be assigned the minimum weight plus a [factor proportional to the amount by which the minimum balance was exceeded](#weight-when-token-is-initialized).

If `tokenIn` has a higher desired weight than its real weight and has not been adjusted in the last hour, it will move towards the real weight with a maximum difference of $$\frac{weight \cdot fee}{2}$$. If `tokenIn` is not initialized and has still not met its minimum balance after the swap, its weight will not be adjusted.

## `joinswapPoolAmountOut`

```
function joinswapPoolAmountOut(
  address tokenIn,
  uint256 poolAmountOut,
  uint256 maxAmountIn
) returns (uint256 tokenAmountIn)
```

**Summary**

Pay up to `maxAmountIn` of `tokenIn` to mint exactly `poolAmountOut`.

The pool implicitly swaps `(1- weightTokenIn) * tokenAmountIn` to the other underlying tokens. Thus a swap fee is charged against the input tokens.

**Notes**

`tokenAmountIn` can not:
- exceed `maxAmountIn`
- be 0
- exceed 1/2 the current balance (or minimum balance in the case of uninitialized tokens) of `tokenIn`

If `tokenIn` is not initialized, its balance will be replaced with `_minimumBalances[tokenIn]` and its weight will be replaced with the minimum weight [plus a premium determined by the token's distance from the minimum balance](#weight-for-price-calculations). This is only for the purpose of price calculations and is not written to storage.

If `tokenAmountIn` brings the real balance above the minimum balance, `tokenIn` will be marked as initialized and its record will be assigned the minimum weight plus a [factor proportional to the amount by which the minimum balance was exceeded](#weight-when-token-is-initialized).

If `tokenIn` has a higher desired weight than its real weight and has not been adjusted in the last hour, it will move towards the real weight with a maximum difference of $$\frac{weight \cdot fee}{2}$$. If `tokenIn` is not initialized and has still not met its minimum balance after the swap, its weight will not be adjusted.


## `exitPool`

```
function exitPool(
  uint256 poolAmountIn,
  uint256[] calldata minAmountsOut
)
```

**Summary**

Burns `poolAmountIn` pool tokens in exchange for the amounts of each underlying token proportional to `poolAmountIn / totalSupply` of the token's balance. The amount of each token transferred to the caller must be greater than or equal to the associated minimum output amount from the `minAmountsOut` array.

**Notes**

`minAmountsOut` must have a length equal to `_tokens`.

The amount of pool tokens to burn can not be 0.

An exit fee is charged if the pool has an exit fee value set. The exit fee is taken from the input pool tokens and transferred to the pool controller prior to calculating the ratio of underlying balances to give the caller.

Tokens may not exit the pool if they are uninitialized. The minimum amount out provided for any uninitialized tokens must be 0.

Unlike other swap & pool token functions, this does not update the weights of any tokens due for a weight decrease.

## `exitswapPoolAmountIn`

```
function exitswapPoolAmountIn(
  address tokenOut,
  uint256 poolAmountIn,
  uint256 minAmountOut
) returns (uint256 tokenAmountOut)
```

**Summary**

Burns `poolAmountIn` pool tokens in exchange for at least `minAmountOut` of `tokenOut`. Returns the number of tokens sent to the caller.

The pool implicitly burns the tokens for all underlying tokens and swaps them to the desired output token. A swap fee is charged against the output tokens.

**Notes**

`tokenOut` must be initialized.

`tokenAmountOut` can not exceed 1/3 of the current balance of `tokenOut`.

If `tokenOut` is due for a weight decrease, its real weight will move toward the desired weight with a maximum absolute difference of $$\frac{weight \cdot fee}{2}$$.

An exit fee is charged if the pool has an exit fee value set. The exit fee is taken from the input pool tokens and transferred to the pool controller prior to calculating the ratio of underlying balances to give the caller.


## `exitswapExternAmountOut`

```
function exitswapExternAmountOut(
  address tokenOut,
  uint256 tokenAmountOut,
  uint256 maxPoolAmountIn
) returns (uint256 poolAmountIn)
```

**Summary**

Burn up to `maxPoolAmountIn` for exactly `tokenAmountOut` of `tokenOut`. Returns the number of pool tokens burned.

The pool implicitly burns the tokens for all underlying tokens and swaps them to the desired output token. A swap fee is charged against the output tokens.

**Notes**

`tokenOut` must be initialized.

`tokenAmountOut` can not exceed 1/3 of the current balance of `tokenOut`.

If `tokenOut` is due for a weight decrease, its real weight will move toward the desired weight with a maximum absolute difference of $$\frac{weight \cdot fee}{2}$$.

An exit fee is charged if the pool has an exit fee value set. The exit fee is taken from the input pool tokens and transferred to the pool controller prior to calculating the ratio of underlying balances to give the caller.


# Token Swaps

## `swapExactAmountIn`

```
function swapExactAmountIn(
  address tokenIn,
  uint256 tokenAmountIn,
  address tokenOut,
  uint256 minAmountOut,
  uint256 maxPrice
) returns (
  uint256 tokenAmountOut,
  uint256 spotPriceAfter
)
```

**Summary**

Trades exactly `tokenAmountIn` of `tokenIn` for at least `minAmountOut` of `tokenOut`. Returns the output amount and the new spot price after the swap, which can not exceed `maxPrice`.

**Notes**

`tokenAmountIn` can not exceed 1/2 of the current balance (or the minimum balance for uninitialized tokens) of `tokenIn`.

`tokenAmountOut` can not exceed 1/3 of the current balance of `tokenOut`.

`tokenOut` must be initialized.

If `tokenIn` is not initialized, its balance will be replaced with `_minimumBalances[tokenIn]` and its weight will be replaced with the minimum weight [plus a premium determined by the token's distance from the minimum balance](#weight-for-price-calculations). This is only for the purpose of price calculations and is not written to storage.

If `tokenAmountIn` brings the real balance above the minimum balance, `tokenIn` will be marked as initialized and its record will be assigned the minimum weight plus a [factor proportional to the amount by which the minimum balance was exceeded](#weight-when-token-is-initialized).

If `tokenIn` has a higher desired weight than its real weight and has not been updated in the last hour, or `tokenOut` has a lower desired weight than its real weight and has not been updated in the last hour, their weights will move up or down (respectively) towards their desired weights by a maximum of $$\frac{weight \cdot fee}{2}$$. If `tokenIn` is not initialized and has still not met its minimum balance after the swap, its weight will not be adjusted.

## `swapExactAmountOut`

```
function swapExactAmountOut(
  address tokenIn,
  uint256 maxAmountIn,
  address tokenOut,
  uint256 tokenAmountOut,
  uint256 maxPrice
) returns (
  uint256 tokenAmountIn,
  uint256 spotPriceAfter
)
```

**Summary**

Trades at most `maxAmountIn` of `tokenIn` for exactly `tokenAmountOut` of `tokenOut`. Returns the actual input amount and the new spot price after the swap, which can not exceed `maxPrice`.

**Notes**

`tokenOut` must be initialized.

If `tokenIn` is not initialized, its balance will be replaced with `_minimumBalances[tokenIn]` and its weight will be replaced with the minimum weight [plus a premium determined by the token's distance from the minimum balance](#weight-for-price-calculations). This is only for the purpose of price calculations and is not written to storage.

If `tokenAmountIn` brings the real balance above the minimum balance, `tokenIn` will be marked as initialized and its record will be assigned the minimum weight plus a [factor proportional to the amount by which the minimum balance was exceeded](#weight-when-token-is-initialized).

If `tokenIn` has a higher desired weight than its real weight and has not been updated in the last hour, or `tokenOut` has a lower desired weight than its real weight and has not been updated in the last hour, their weights will move up or down (respectively) towards their desired weights by a maximum of $$\frac{weight \cdot fee}{2}$$. If `tokenIn` is not initialized and has still not met its minimum balance after the swap, its weight will not be adjusted.

# Other

## `gulp`

```
function gulp(address token)
```

**Summary**

Absorb any tokens which have been sent to the pool that are not represented in the balance.

**Notes**

If `token` is not bound, any tokens sent to the pool will be sent to the pool's `unboundTokenHandler`.

If `token` is bound, the token record's balance will be set to the current balance on the ERC20 token.

If `token` is not initialized and the updated balance is greater than its minimum balance, the token's weight will be set, its minimum balance will be deleted and it will be marked as initialized.

## `flashBorrow`

```
function flashBorrow(
  IFlashLoanRecipient recipient,
  address token,
  uint256 amount,
  bytes calldata data
)
```

**Summary**

Sends `amount` of `token` to `recipient`, then calls `recipient.receiveFlashLoan(data)`. If `amount` of `token` is not repaid with `swapFee * amount` interest, the transaction will revert.

**Notes**

`recipient` must implement the `IFlashLoanRecipient` interface.

`token` must be bound to the pool.

The pool must have at least `amount` of token.

This function uses a reentrancy lock, so the flash loan recipient can not interact with the pool.

If `token` is not initialized and the repayment with the fee brings the token above its minimum balance, the minimum balance will be deleted and the token will be marked as initialized.

# Uninitialized Weight Calculations

Formulae for calculating weights of uninitialized tokens.

## Weight for price calculations

If a token is uninitialized, its weight used for swaps will be set to the minimum weight plus a premium determined by the distance between its real and minimum balances. The premium begins at 10% and decreases linearly as the token gets closer to its minimum balance. The weight used for price calculations with an uninitialized token ($$W_t^u$$) is calculated with:
$$W_t^u = W_{min} \cdot \left(1 + \frac{B_{t}^{min} - B_{t}}{10 \cdot B_{t}^{min}}\right)$$

## Weight when token is initialized

When a token reaches its minimum balance, it is marked as ready and its weight is set. Unlike other weight changes which modify weights by a factor of $$\frac{fee}{2}$$, when a token is becoming initialized its weight will be set to the minimum weight plus a factor proportional to the amount it exceeded the minimum balance. The weight is set to:

$$W_{min} \cdot \frac{1 + \left(B_{t} - B_{t}^{min}\right)}{B_{t}^{min}}$$ where $$B_{t}$$ is the pool's balance in that token including the amount gained in the transaction.
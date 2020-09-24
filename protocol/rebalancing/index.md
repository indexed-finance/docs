# Rebalancing

The typical method for rebalancing a token portfolio is to sell and purchase sufficient amounts of each asset to reach the desired weights. This typically involves trading with on-chain exchanges or using an auction system. Any method of swapping on-chain to rebalance will cause some amount of loss for the pool, potentially quite a lot. On-chain exchanges are illiquid, and auctions on Ethereum [have a history of being exploited](https://forum.makerdao.com/t/black-thursday-response-thread/1433).

Indexed pools rebalance themselves over time by creating small arbitrage opportunities that incentivize traders to gradually adjust token balances and weights. In other words, Indexed pools intentionally create impermanent loss in order to bring token balances in line with their weights. The exact amount lost is a function of the time between weight changes and the amount by which a weight can change each time it is updated, so it can be configured to take a longer time and lose less money for liquidity providers or be faster and lose a bit more.

While this rebalancing process is not instantaneous, it is permissionless, it works for arbitrarily large pools, it is generally more gas efficient and it does not assume that the pool or its controller can access external liquidity to execute rebalances.

## Weight adjustment

In order to rebalance through internal swaps, Indexed uses a *desired weight* ($$D_t$$) parameter which specifies the target weight for an asset. If a desired weight is higher than the actual weight, the pool should increase its balance in that token. If the desired weight is lower than the actual weight, the pool should decrease its balance in that token.

Each pool has a minimum update delay, which by default is set to 1 hour, and a weight change factor, which by default is $$\frac{W_t \cdot fee}{2}$$. 

If a token with a positive weight difference ($$D_t > W_t$$) is swapped into the pool and it has been more than the minimum delay period since its last weight change, the pool will increase that token's weight by either the weight change factor or the token's desired weight, whichever is less.

```js
const weightChangeFactor = swapFee / 2;

updateWeightIn(tokenIn) {
  if (tokenIn.desiredWeight > tokenIn.weight) {
    tokenIn.weight = Math.min(
      tokenIn.desiredWeight,
      tokenIn.weight * (1 + weightChangeFactor)
    )
  }
}
```

If a token with a negative weight difference ($$D_t < W_t$$) is swapped out of the pool and it has been more than the minimum delay period since its last weight change, the pool will decrease that token's weight by either the weight change factor or the token's desired weight, whichever is less.

```js
const weightChangeFactor = swapFee / 2;

updateWeightOut(tokenOut) {
  if (tokenOut.desiredWeight < tokenOut.weight) {
    tokenOut.weight = Math.max(
      tokenOut.desiredWeight,
      tokenOut.weight * (1 - weightChangeFactor)
    )
  }
}
```

As swaps are executed and LP tokens are minted and burned, inbound tokens with desired weight increases (desired > real) and outbound tokens with desired weight decreases (real > desired) automatically adjust their weights, occasionally creating small arbitrage opportunities which move tokens toward their target balances when traders execute on them, thus rebalancing the pool.

**Note:** There are two exceptions to the stated weight adjustment rule:

1. The `exitPool` function, which sends out some amount of every initialized token. In order to minimize gas expenditure, this function does not adjust the weights of outbound tokens.
2. When an uninitialized token becomes ready, the weight can increase beyond the fee factor<sup>[1](#Initialization)</sup>.

## Re-weighing assets

Pools can be re-weighed to adjust the composition of the *current desired tokens* in the pool. The current desired tokens are the underlying tokens in the pool with a desired weight greater than zero. Re-weighing a pool adjusts the target weights of each asset but does not remove or add tokens.

## Re-indexing assets

Pools can be re-indexed to adjust both the underlying tokens and their target weights.

Any current underlying tokens which are not assigned a new target weight in the re-index call will be assigned a target weight of 0 so that they can be gradually removed from the pool. If this occurs for a token which is bound but not initialized, the token will be unbound (see [unbound token handling](./removing-tokens.md#Handling-unbound-tokens)).

New tokens added to the pool must be assigned a minimum balance (see [bootstrapping new tokens](./adding-tokens.md)).
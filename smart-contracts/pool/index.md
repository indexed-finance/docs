
# Summary

The Indexed Pool contract is a fork of the Balancer Pool. The primary changes made to the contracts were intended to enable more dynamic pool management so that assets can be bound, rebound and reweighed gradually and without the need to access other markets. It may be useful to read the Balancer [Whitepaper](https://balancer.finance/whitepaper/) or [documentation](https://docs.balancer.finance/) for additional context.

This contract has been designed in tandem with the pool controller, and some of the assumptions about how the contract should function are only valid given the design of the controller. These assumptions are explicitly stated in the API document and in the contract's natspec comments.

## Deployment
Pools are deployed as delegatecall proxies which point to the implementation address, which is the deployed pool contract. Rather than a constructor, the pool exposes an `initialize` function which must be called in the same transaction as the proxy deployment (otherwise anyone will be able to take control of the pool).

## Tokens
Every token $t$ in the pool has an associated weight $W_t$ and balance $B_t$. A token's normalized weight represents the total value of the pool which is held in the balance of that token, where the normalized weight is the token's weight divided by the total weight. These two values are used to price swaps between tokens - the spot price between token $i$ and token $o$ is given by the formula:

$$
SP_{i}^{o} = \frac{B_i/W_i}{B_o/W_o} \cdot \frac{1}{1-fee}
$$

# Rebalancing
In Balancer, reweighing a token requires that you remove or add sufficient tokens to make the new balance proportional to the new weight, meaning that you need to access some external source of liquidity and handle the rebalancing outside of the pool. In an optimal scenario where the controller has access to unlimited on-chain liquidity at a constant price, this method of rebalancing a pool would result in minimal losses for the liquidity providers; unfortunately, those conditions do not exist on Ethereum. In effect, a dynamic Balancer pool which rebalances on any regular basis must do one of the following: have its own trading system for executing rebalances; use on-chain markets, with some acceptable price parameters for large trades; or trust some centralized entity that can use more liquid external markets to rebalance the pool.

Indexed pools rebalance themselves over time by creating small arbitrage opportunities that incentivize traders to gradually adjust token balances and weights. While this is not instantaneous, it is decentralized, it works for arbitrarily large pools and it does not assume that the pool or its controller can access external liquidity to execute rebalances.

## Weight adjustment
In order to rebalance through internal swaps, Indexed uses a *desired weight* parameter which specifies the target weight for an asset. If the desired weight for a token is higher than the actual weight, the pool will try to increase its balance in that token; if it is lower, the pool will try to decrease its balance in that token.

This assumes that the balance in each asset on the pool is close to the target balance. The target balance for a token is the amount of tokens worth the weighted value of the pool; e.g. if a token has weight 2 out of a total of 10, the target balance is the number of tokens worth 20% of the pool's portfolio. In a rational market, the real balance of a token should always be within `swapFee` of the target balance, as there would be an arbitrage opportunity whenever it moves outside that.

As swaps are executed and LP tokens are minted and burned, inbound tokens with desired weight increases (desired > real) and outbound tokens with desired weight decreases (real > desired) automatically adjust their weights at a maximum frequency of once per hour - the real weight will move towards the desired weight with a maximum absolute difference of $\frac{weight \cdot fee}{2}$. By adjusting weights by half the swap fee (proportional to their existing weights), we create small arbitrage opportunities which move tokens toward their target balances, thus rebalancing the pool.

> Note: The one exception to the previous rule is the `exitPool` function, which sends out some amount of every initialized token. In order to minimize gas expenditure, this function does not adjust the weights of outbound tokens.

Arbitragers can identify when one token is set for an increase and another is set for a decrease, execute a small swap between them to trigger the weight adjustments, then execute a trade that brings the token's spot prices in line with their external prices. The first step creates a spot price difference roughly equal to the swap fee, so if the tokens were already favorably priced relative to each other but unprofitable due to the swap fee, the new price including the swap fee will be favorable to the trader.

The amount of token $i$ ($A_i$) needed to trade against token $o$ such that the spot price changes from $SP_{i}^{o}$ to $SP_{i}^{′o}$ is given by the [in-given-price](https://balancer.finance/whitepaper/#in-given-price) formula from the Balancer whitepaper:

$$
A_i = B_i \cdot \left(\left(\frac{SP_{i}^{′o}}{SP_{i}^{o}}\right)^{\frac{W_o}{W_o + W_i}} - 1\right)
$$

## Bootstrapping new tokens
When a new token is added, the pool does not have any balance in it, which impairs the ability to correctly calculate pricing for token swaps. In order to bootstrap new tokens added to the pool, we use false weight and balance values. Each token record has a `ready` boolean field which indicates whether the token is fully initialized, meaning that the pool has a sufficient balance in the token for its weight.

When the pool is deployed, every token in the initial asset pool must be added with sufficient tokens to cover its weight. After that, when new tokens are added to the pool, an additional value `minimumBalance` must be provided. The minimum balance represents the number of tokens needed for the token to have the minimum weight. The default total weight for the pool is 25, and the minimum weight is 1, so the minimum balance value provided for a new token is the number of tokens worth `1/25` of the pool value. The exact total weight can vary slightly as the result of weight adjustments, but will quickly balance itself assuming a rational market which equally adjusts tokens regardless of the direction of their desired weight changes.

<!-- We approximate this by taking the first token in the pool which is fully initialized, and extrapolating the value of the

$$
\left(\frac{ \sum_k{W_k}}{W_t} \cdot B_t\right)\cdot {EP}_{t}^{e}
$$ -->

Until the new token has reached its minimum balance, two rules are applied:
- The token can not be sent out of the pool.
- For price and trade calculations, the token's balance and weight are replaced with the minimum balance provided when the token was bound and the minimum weight (1/25).

Once the minimum balance is reached, the token is marked as ready, the minimum balance is deleted and the token will be swappable in both directions.
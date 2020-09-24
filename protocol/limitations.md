## Unbound token handling

**Protocol Docs Incomplete**

# Pool Limitations

**Abnormal token implementations**

Tokens that have internal transfer fees or other non-standard balance updates may create arbitrage opportunities. For now, these tokens should not be used in Indexed pools. Indexed pools do not have the same ERC20 restrictions on return values as Balancer pools, as the pool contract uses `SafeERC20`.

**Permanent loss for some liquidity providers due to unbound token handling**

While the selling of a pool's unbound tokens is restricted to a small range around their moving average prices, it is still possible for a liquidity provider to experience permanent loss due to the way that unbound tokens are handled. If an LP exits a pool after a token is removed from the pool, but before its balance is swapped to the other underlying assets, the LP will suffer a loss of around 1% of their pool tokens' value (as 1% is the minimum weight of the pool).

**Swap input amount**

When a token is sold to a pool, the input amount can not exceed half of the pool's current balance in that token. This restriction applies to swaps and single-asset liquidity providing functions, but does not apply to all-asset liquidity providing. This only applies to an individual call to the contract, and can be bypassed with multiple calls.

**Swap output amount**

When a token is purchased from a pool, the output amount can not exceed one third of the pool's current balance in that token. This restriction applies to swaps and single-asset liquidity removal functions, but does not apply to all-asset liquidity removal. This only applies to an individual call to the contract, and can be bypassed with multiple calls.

**Minimum balance**

When a pool is first initialized, it must have a balance of at least 1e6 wei. This does not apply to tokens after the pool is initialized
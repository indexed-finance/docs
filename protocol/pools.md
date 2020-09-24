# Summary

**Protocol Docs Incomplete**

Index pools are multi-asset portfolios that also act as AMMs. The pool contract is designed to be able to radically change the composition of its portfolio without needing to access external liquidity<sup>[*](./removing-tokens.md#selling-unbound-tokens)</sup>.

## Fork Notes

The Index Pool contract is a fork of the [Balancer Pool](https://github.com/balancer-labs/balancer-core/blob/master/contracts/BPool.sol). The primary changes made to the contract were intended to enable more dynamic pool management so that assets can be bound, rebound and reweighed gradually and without the need to access external liquidity.

> It may be useful to read the Balancer [Whitepaper](https://balancer.finance/whitepaper/) or [documentation](https://docs.balancer.finance/) for additional context on the pool contract.

## Deployment

Pools are deployed as delegatecall proxies which point to the implementation address, which is the deployed pool contract. Rather than a constructor, the pool exposes an `initialize` function which must be called in the same transaction as the proxy deployment (otherwise anyone will be able to take control of the pool).

# Tokens
Every token $$t$$ in a pool has an associated weight $$W_t$$ and balance $$B_t$$. A token's normalized weight represents the total value of the pool which is held in the balance of that token, where the normalized weight is the token's denormalized weight divided by the total weight. These two values are used to price swaps between tokens - the spot price between token $$i$$ and token $$o$$ is given by the formula:

$$
SP_{i}^{o} = \frac{B_i/W_i}{B_o/W_o} \cdot \frac{1}{1-fee}
$$

## Pool Types

There are 2 types of pool supported by Indexed:

- **Fixed-Target Pools** - Pools with predetermined values for the weights and desired weights of the underlying assets.
- **Index Pools** - Pools controlled by an approved strategy contract which can completely change a pool's composition.

## Fixed-Target Pools

Fixed target pools do not have a controller and can not be adjusted once they are deployed.

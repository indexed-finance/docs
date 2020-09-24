# Terminology

- **Weight** - The proportion of a pool's total value which a token represents.
- **Denorm** - The denormalized weight value. Solidity does not have good handling for fixed point numbers, so the contracts uses denormalized values to represent token weights.
- **Target Weight** - The weight that a pool's controller has determined a token should eventually have, and which swaps will move the token towards. Used interchangeably with "desired weight".
- **Initialized** - Used to describe whether a pool owns a sufficient amount of a token to cover the minimum weight<sup>[1](./pools/adding-tokens.md)</sup>. **Note:** this is distinct from "pool initialization", which acts in the place of a constructor<sup>[2](./pools/index.md#deployment)</sup>.
- **Portfolio** - The basket of assets held by a pool.
- **Portfolio Composition** - The makeup of a portfolio, particularly with regard to the weights of each token.
- **Underlying Tokens** - The tokens held by a pool.
- **Pool Tokens** - Liquidity provider tokens for a pool. These represent ownership of the underlying assets in a pool.
- **Controller** - The address of the account which is able to modify a token's weights, pause/resume public trading and adjust the swap fee.
- **Index Pool** - A pool contract that is controlled by a DAO-approved management strategy.
- **Fixed-Target Pool** - A pool contract with preset weights and target weights for a particular set of tokens which can not be modified.
- **Rebalance** - To change the composition of a portfolio.
- **Re-weigh** - To re-assign the target weights of only the current underlying tokens in an index pool.
- **Re-index** - To re-assign both the desired tokens and weights of an index pool.
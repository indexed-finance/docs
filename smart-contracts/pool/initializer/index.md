## `PoolInitializer`



Contract that acquires the initial balances for an index pool.

This uses a short-term UniSwap price oracle to determine the ether value of tokens sent to the contract. When users contribute tokens they are credited for the moving average ether value of said tokens.

When all the tokens needed are acquired, the index pool will be initialized and this contract will receive the initial token supply (100).

Once the contract receives the index pool tokens, users can claim their share of the tokens proportional to their credited contribution value.
# `UnboundTokenSeller`

Contract for swapping undesired tokens to desired tokens for an index pool.

This contract is deployed as a proxy for each index pool. When tokens are unbound from a pool, they are transferred to this contract and sold on UniSwap or to anyone who calls the contract in exchange for any token which is currently bound to its index pool and which has a desired weight about zero.

It uses a short-term uniswap price oracle to price swaps and has a configurable slippage rate which determines the range around the moving average for which it will accept a trade.
# Removing Tokens

Tokens are removed from a pool when their weights become lower than the minimum weight. When a token is removed from a pool, it is sent to an 'unbound token handler' contract which handles the remaining tokens in a way that minimizes losses to the liquidity providers.

> **Note**: This does not apply to uninitialized tokens.

Additionally, if the `gulp` function on a pool is called for a token which is not bound to the pool, the pool's balance of that token will be sent to the unbound token handler.

## Handling unbound tokens

Currently, the only contract for handling unbound tokens is [UnboundTokenSeller.sol](../../smart-contracts/token-seller.md). A new unbound token seller contract is deployed as a proxy for each index pool. The contract receives unbound tokens from a pool and sells them for the desired underlying tokens in the pool (tokens with a non-zero target weight).

### **Token Pricing**

The token seller uses the [short term price oracle](../price-oracles.md) to determine the recent moving average prices for tokens being swapped. It is configured with a `premiumPercent` value that gives an advantage to token buyers by reducing the output value it expects for a given input value.

**Example:** if the seller has `premiumPercent = 5` and owns 10 A tokens with an average price of 1 ETH on UniSwap, and someone wants to purchase them for B tokens with an average price of 2 ETH on UniSwap, the contract will accept 4.75 B (worth 9.5 ETH) for 10 A (worth 10 ETH).

### **UniSwap Trades**

Users can call the contract to trigger a UniSwap trade between a token it holds and a token the pool will accept. For UniSwap trades, any output tokens the contract receives beyond the minimum are paid to the caller as a reward for triggering the swap.

### **User Trades**

Users can call the contract to trade with it directly. For these trades, the contract will always take the minimum output or pay the maximum input, depending on whether the user calls to swap an exact input or output amount.
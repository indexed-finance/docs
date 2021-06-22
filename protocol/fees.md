# Fees

We strive to be as transparent as possible in terms of fees charged by our protocol.

Indexed charges two types of fees: [_swap_](#swap-fees) fees and [_exit_](#exit-fees) fees. The majority of users of the Indexed protocol will _not_ pay any of these fees. Specifically, users that simply market buy, hold, and eventually market sell our indices don't pay any fees. There are no streaming/management fees on any of our indices.

With this in mind, let's look at the types fees we _do_ charge.

## Swap fees

Swap fees are paid by traders when they _swap_ assets within index pools. The incentives to do so are either low-slippage token swaps, or profiting from arbitrage opportunities between pools and the open market. These fees accrue to the index holders as a form of passive yield, offsetting impermanent loss (recall that holding Indexed indices is essentially providing liquidity to an underlying AMM balancer pool).

As mentioned above, market buying index tokens incurs no fees. However, when buying large amounts (e.g > $10,000), slippage costs might be significant. Therefore, you might be better off minting the liquidity pool (LP) tokens corresponding to the desired index. Minting does not incur swap fees if you provide all the underlying pool tokens in the weights suggested by the UI, but does if you provide only one of the underlying tokens, or mint via the router using ETH, DAI or USDC. The two latter options can be quite gas intensive, and should only be considered for buys greater than US$10,000.

Similarly, _burning_ indices (see [below](#exit-fees)) to one of their underlying components or to ETH, DAI or USDC also triggers internal swaps, and therefore incurs swap fees.

**Swap fees are 2%**. This might reduce the trading volume with our index pools, but we find this acceptable as we target accuracy in the tracking of sectors rather than trade volume.

## Exit fees

Most index holders exit their positions by simply market selling their index tokens. This incurs _no_ exit fees.

Exit fees are only charged when burning index tokens into their underlying components. This might be warranted if an index is trading at a discount relative to its net asset value. In this scenario, arbitrageurs can buy the index and immediately burn it into its underlying tokens which are then sold at a profit on external markets.

For the sake of addressing any centralization concerns, note that we cannot actually shut down the underlying asset pool. Anyone will always be free to mint or burn any of our indices via the underlying contract, and anyone is able to update the appropriate oracle and adjust weightings in all of our products. Therefore, burning indices is a mechanism by which anyone can _always_ exit their index positions and redeem the underlying assets, regardless of whether liquidity for a given index exists or not in the markets.

**Exit fees are 0.5%** for all our indices. These are generate revenue which is currently routed to the Indexed [treasury](https://etherscan.io/address/0x78a3ef33cf033381feb43ba4212f2af5a5a0a2ea), and soon will start to be distributed to [$NDX](https://www.coingecko.com/en/coins/indexed-finance) token holders via the [upcoming $dNDX token](https://forum.indexed.finance/t/create-dndx-a-dividends-token-for-indexed-fee-revenue/610).

## Summary

The following table summarizes actions which incur fees for users of the Indexed protocol.

| Action                                      | Swap fee | Exit fee | Total fee (%) |
|---------------------------------------------|----------|----------|---------------|
| Minting via a single underlying token       | ✅       | ❌       |             2 |
| Minting via all underlying tokens           | ❌       | ❌       |             0 |
| Minting via router (using ETH, DAI or USDC) | ✅       | ❌       |             2 |
| Burning to a single underlying token        | ✅       | ✅       |           2.5 |
| Burning to all underlying tokens            | ❌       | ✅       |           0.5 |
| Burning via router (to ETH, DAI or USDC)    | ✅       | ✅       |           2.5 |
| Internal trades with the AMM pool           | ✅       | ❌       |             2 |

And here's our we compare to several of the other decentralized index providers on Ethereum:

| Fee type (%) | Indexed Finance (NDX) | Index Coop (INDEX) | PieDAO (DOUGH) | Powerpool (CVP) | Cryptex (CTX) | BasketDAO (BASK) |
|--------------|-----------------------|--------------------|----------------|-----------------|---------------|------------------|
| Entry        | -                     | 0 - 0.1            | -              | 0.1             | -             | 5                |
| Swap         | 2                     | -                  | 0 - 1          | 0 - 0.3         | -             | -                |
| Exit         | 0.5                   | 0 - 0.1            | -              | 0.1             | 1             | 5                |
| Management   | -                     | 0.95 - 1.95        | 0 - 1          | -               | -             | -                |

_(Values accurate to the best of our knowledge as of June 19th, 2021. Sources: documentation of the various protocols, Etherscan)_

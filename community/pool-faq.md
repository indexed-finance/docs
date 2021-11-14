# Index Tokens FAQ

All of our indices are themselves ERC20-compliant Ethereum tokens, with their prices reflected by the weighted performance of their constituents. The strategy for determing weights within a particular index is determined by the [index controller](../protocol/index-controller.md) associated with it.

*Last update: 1 August 2021*

### What Indices Do You Offer?

At present, we have six indices available for purchase, with the following descriptions:

* [DEFI5](https://www.coingecko.com/en/coins/defi-top-5-index) - a hyper-focused index of the most successful large-cap decentralized finance protocols across the Ethereum chain,
* [CC10](https://www.coingecko.com/en/coins/cryptocurrency-top-10-index) - an index combining several popular medium/large-cap protocols, primarily drawn from decentralized finance,
* [ORCL5](https://www.coingecko.com/en/coins/oracle-top-5-index) - an index representing the current market leaders in protocols designed to bring external data onto the blockchain,
* [DEGEN](https://www.coingecko.com/en/coins/degen-index) - a higher risk/reward index of promising Ethereum protocols that have significant room to grow,
* [NFTP](https://www.coingecko.com/en/coins/nft-platform-index) - a collectors index of governance and protocol tokens drawn from both the NFT space and the wider Metaverse
* [FFF](https://www.coingecko.com/en/coins/future-of-finance-fund) - a meta-index providing all-in-one exposure to Bitcoin and Ether (20% each), with the remainder weighted across DEFI5, CC10 and DEGEN using circulating market cap weightings.

### What _Are_ The Index Tokens, Really?

Fundamentally, the index tokens themselves represent fractional ownership of assets in pools maintained by a fork of [Balancer](https://balancer.finance/whitepaper/). Assets within these pools have _target weights_ assigned to them, and differences between the current and target weights (due to price fluctuations) are evened out via arbitrage.

Each index has two 'groupings': the current constituent list - those tokens that are currently _active_ within the associated Balancer pool - and a secondary 'candidate' list of tokens waiting on the sidelines, ready to be switched in if an active member underperforms relative to the others, or if a particular candidate's performance justifies its inclusion.

Periodically, the target weights of members of the pools are recalculated on-chain (dependent on the weighting strategy associated with a given index), and occasional reindexes evaluate the list of all current and potential members to determine if membership of the current list needs to be adjusted due to shifts in performance of all tokens.

We presented a talk about what Indexed pools are and how they operate at EthCC[4] - you can view it [here](https://www.youtube.com/watch?v=TqFveXwjOBM).

### Who Owns The Underlying Assets?

It's worth emphasising that the Indexed DAO itself does *not* control the assets that comprise the indices that we enable. They are kept within the Balancer pools themselves, and ownership of the assets is strictly limited to owners of the index tokens.

### Do You Make Any Guarantees Regarding Funds I Place Into An Index?

In short, no. Indices are superb instruments for gaining exposure to a large segment of a market at once, but they are subject to downturns just as much as any other asset or instrument. As with all crypto assets, do not expose more than you can afford to lose.

## Staking And Rewards

At present, we reward users who provide liquidity to DEXes (i.e. Uniswap, Sushi) in the form of NDX governance tokens, at a rate relative to their share of the relevant liquidity pool.

We have migrated our reward scheme to a fork of Masterchef V2, which will run until mid-2023, emitting 1.5 million NDX via a linearly decreasing emission rate. Details of the rewards program can be found [here](https://ndxfi.medium.com/introducing-the-extended-ndx-liquidity-mining-program-ae30a0470001).

### I Hold {X} - Why Can't I Stake It For Rewards?

The most likely cause of this is that you're trying to stake the 'pure' token (such as ORCL5), rather than the equivalent Uniswap liquidity provider (LP) token, e.g. DEFI5-ETH. However, you _can_ stake certain index tokens 'single-sided': at present, these are DEFI5, CC10 and DEGEN.

If you're unfamiliar with the process of providing liquidity, please read [this article](https://defiprime.com/uniswap-liquidity-pools). Be sure you're absolutely certain what you're doing before you engage in staking.

## Minting And Burning

When minting new index tokens, you have three options:

* Provide each of the underlying tokens within the pool.
* Provide _one_ of the underlying tokens within the pool.
* Use the Mint option on the appropriate page, routing an asset into an underlying component in order to mint.

### What Is This 'Swap Fee'? Do I Have To Pay It?

If you opt for the first option above, you will _not_ have to pay the 2% swap fee - you are providing the underlying assets in the correct amounts, and will not trigger a swap within the pool to rebalance the weightings therein.

In the latter two cases, the swap fee applies. This fee is designed to lessen the impact and frequency of arbitrageurs, and is distributed to liquidity providers of the pool - namely, the existing index token holders. This is how the simple act of holding an index token becomes a form of passive yield, over and above the value gained - or lost - based on the performance of the index assets themselves.

Note that minting is a fairly gas-intensive operation, and is not recommended for small amounts - you may well end up paying as much (or more) in gas than you receive by way of index tokens.

### What About Burning Index Tokens And Burning Fees?

It's possible to 'burn' index tokens either into their underlying components or directly to, e.g. ETH or DAI. This means you can always exit your index positions regardless of the liquidity of the index.

Burning index tokens incurs an exit fee of 0.5% of the amount burned. In practice, these fees do not impact traders who are just market selling index tokens rather than burning them. Rather, they offset the potential profit margins of arbitrageurs (a fractional subset of the overall users of the Indexed protocol) that seek to profit from differences between the net asset value and the market price of the ETF. These fees are a source of revenue for Indexed and have thus far been routed to the Indexed DAO Treasury, pending distribution to NDX holders upon the introduction of staking.

### Why Is The Total Supply Of {X} Always Changing?

The supply of each index token itself is _elastic_ - users of the platform can either mint more by providing the underlying tokens, or burn them back into their underlyings at the current weightings within the pool.

If sufficient amounts of an ETF token are being purchased via locations such as Uniswap, Sushiswap or Quickswap to drive the price over the Net Asset Value of its constituents, arbitrageurs can bring this back into line by minting more tokens and selling them on the marketplace. Likewise, if a token's price has dropped below its NAV, arbitrageurs burn the relevant index token and sell the constituent assets for a profit.

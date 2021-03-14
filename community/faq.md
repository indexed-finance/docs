# Frequently Asked Questions

Hi there, and welcome to the Indexed docs! As this is probably the first page you've clicked on, hopefully we'll be able to answer any initial questions you may have here.

This is an evolving document, and we'll be adding/editing it as questions come to the fore.

If you want to see something added here - come to [our Discord](https://discord.gg/jaeSTNPNt9) and ask us!

Last update: 14th March 2021.

## The Indexed Platform

The purpose of Indexed Finance is to provide financial products that help users invest in the various market sectors or groupings within the cryptocurrency space (primarily on Ethereum, although we intend to eventually branch out to synthetic stocks and wrapped assets across different blockchains).

By providing these instruments, we aim to enable exposure to the wider cryptocurrency market to those who are interested in the cryptocurrency sector but do not have the time or inclination to research which projects are worthy of their attention, or separate the signals from the noise in the wider market. They are intended to act as 'set and forgets' for the more passive investor.


## The [NDX](https://www.coingecko.com/en/coins/indexed-finance) Token

The NDX token is - at present - a pure governance token (as a fork of UNI), intended for people who wish to participate in determining the direction of the Indexed platform as it evolves by way of [voting on proposals](https://www.withtally.com/governance/indexed) brought forward by the DAO (either for or against).

## The Index Tokens [CC10, DEFI5 et al]

All of our products are themselves Ethereum tokens, with their prices reflected by the weighted performance of their constituents. 

### What Are The Index Tokens?

At present, we have four offerings available, with the following target sectors:

* [DEFI5](https://www.coingecko.com/en/coins/defi-top-5-index) - large cap DeFi governance tokens.
* [CC10](https://www.coingecko.com/en/coins/cryptocurrency-top-10-index) - large cap protocol tokens and DeFi governance tokens.
* [ORCL5](https://www.coingecko.com/en/coins/oracle-top-5-index) - medium cap protocol and governance tokens for oracle projects.
* [DEGEN](https://www.coingecko.com/en/coins/degen-index) - [Sigma Program] higher risk protocol and governance tokens.

### But, What _Are_ The Index Tokens?

Fundamentally, the index tokens themselves are Balancer liquidity tokens, representing ownership in a pool comprising the tokens currently within the index. The members of these pools have _target weights_ assigned to them, and differences between the current and target weights (due to price fluctuations) are evened out via arbitrage.

Each index has two 'groupings': the current constituent list - those tokens that are currently _active_ within the associated Balancer pool, and a secondary 'candidate' list of tokens waiting on the sidelines, ready to be switched in if an active member underperforms relative to the others, or if a particular candidate's performance justifies it's inclusion.

Periodically, the target weights of members of the pools are recalculated (dependent on the weighting strategy associated with a given index), and occasional reindexes evaluate the list of all current and potential members to determine if membership of the current list needs to be adjusted due to shifts in performance of all tokens.

At present, our weighting strategies are all based on the square root of market-capitalisations (either fully diluted or circulating). As time goes on, we will introduce a wider range of strategies, enabling a pick-and-mix style of financial instrument creation.

### Who Owns The Underlying Assets?

It's worth emphasising that the Indexed DAO itself does *not* control the assets that comprise the indices that we enable. They are kept within the Balancer pools themselves, and ownership of the assets is strictly limited to owners of the index tokens.


## Staking And Rewards

At present, we reward users who provide liquidity to DEXes (i.e. Uniswap) in the form of NDX governance tokens, at a rate relative to their share of the liquidity pool over a fixed daily emission.

We are in the process of migrating this reward scheme to a fork of Masterchef, as detailed in [this proposal](https://forum.indexed.finance/t/proposal-dynamic-reward-emission-schedule/510) - if adopted, this will set forth a flexible two-year schedule, allowing us to best incentivise those pools that require additional liquidity (with the primary aim being minimal slippage, for the above reason of wanting to ease access to the market for users who are not crypto-native).

However, the simple act of holding the index tokens themselves is a passive investment act, due to the way in which the swap fee for minting index tokens or arbitraging the underlying pools are dissipated: see [this](https://twitter.com/need3lives/status/1369358000763371522) informative thread by a community user.

### Can I Stake NDX Itself?

No, and there are currently no plans to enable this. Incentivising people to lock up NDX in a liquidity pair (i.e. NDX/ETH) in order to earn NDX by way of reward would have the adverse effect of making governance _harder_ for the wider platform, as staked NDX cannot be used to vote.

## Minting And Burning

The supply of each index token itself is elastic - users of the platform can either mint more by providing the underlying tokens, or burn them back into their underlyings at the current weightings within the pool.

When minting new index tokens, you have three options:

* Provide each of the underlying tokens within the pool.
* Provide _one_ of the underlying tokens within the pool.
* Use the Mint Through Uniswap option on the appropriate page, routing an asset into 

### What Is This 'Swap Fee'? Do I Have To Pay It?

If you opt for the first option above, you will _not_ have to pay the 2.5% swap fee - you are providing the underlying assets in the correct amounts, and will not trigger a swap within the pool to rebalance the weightings therein.

In the latter two cases, the swap fee applies. This fee is designed to lessen the impact and frequency of arbitrageurs, and is distributed to liquidity providers of the pool - namely, the existing index token holders. This is how the simple act of holding an index token becomes a form of passive investment.

Note that minting is a fairly gas-intensive operation, and is not recommended for small amounts - you may well end up paying as much (or more) in gas than you receive by way of index tokens.
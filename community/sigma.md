# The Sigma Program

If you've spent any time on our Discord server, or reading our Twitter account, you'll possibly have seen mention of the 'Sigma committee', or 'Sigma pools'.

On this page, we'll quickly explain what the Sigma program aims to do, how it does it, what powers are available to it, and who currently holds the keys.

*Last update: 30 September 2021*

## Introduction

In short: the Sigma committee are responsible for maintaining certain products within the Indexed protocol, and routing liquidity to them where necessary.

The 'core' products that are offered by Indexed - DEFI5, CC10 and ORCL5 - are maintained entirely by the DAO, in that their [controller](https://etherscan.io/address/0xf00a38376c8668fc1f3cd3daeef42e0e44a7fcdb) - the contract that has the power to create pools and adjust membership - is owned by the NDX [Timelock contract](https://etherscan.io/address/0x78a3ef33cf033381feb43ba4212f2af5a5a0a2ea) (the treasury), the admin of which is the Indexed [Governor Alpha contract](https://etherscan.io/address/0x95129751769f99cc39824a0793ef4933dd8bb74b).

The upshot of this is that on-chain governance votes are required to operate these pools (i.e. adding or removing tokens from the asset lists). This is very much as things should be - reweighs and reindexes can be triggered by anyone, but changes need to be approved by protocol governance.

However, in the days of 300+ gwei gas prices, these are expensive changes to make, and they take time to be applied: three days for the on-chain vote, followed by a two-day timelock before they can be executed, assuming they reach quorum (see [Using Your Vote]() for details).

To this end, it was decided via [IIP 4](https://forum.indexed.finance/t/iip-4-sigma-pilot/74) to create a committee of 5 people that can rapidly deploy new products and enact changes to their constituent lists, as well as assign liquidity mining rewards to them, operating via a Gnosis multisig. The people behind the keys are referred to as the Sigma committee as a whole.

Why Sigma? Because it's shorthand for adding things. Sorry.

## The Committee

Here are the current members of the Sigma committee, along with their Discord usernames and Twitter accounts where available.

* Dillon Kellar: @d1ll0n#8888, [@d1ll0nk](https://twitter.com/d1ll0nk)
* Dr Fabio Nery: @fnery#4202, [@0xfnery](https://twitter.com/0xfnery)
* tei: @tei#6148, N/A
* glueeater: glueeater#0638, N/A
* Champagne Pampi: CHAMPAGNE PAMPI#9878, N/A

## Justification

There are two main 'concerns' when having the DAO administer the creation or adjustment of indices against the core controller:

1. The proposer requires 1% of the total supply of NDX (100,000) to do so, and
2. The scoring contract tied to said controller utilizes the square-root FDV method.

If the proposing party wishes to utilize something other than the square-root FDV methodology, the Sigma committee can get around the above on their behalf by deploying a new scoring contract (if it does not exist already) and creating the new index pool against the Sigma controller.

As the Sigma controller is owned by the committee multisig rather than the Indexed Governor Alpha, these 'Sigma pools' can be created and have their token lists adjusted without the minimum token or timelock requirement associated with core pools, subject to a 3/5 vote.

Note that if we wish to create a new index that is maintained by a *separate* party (i.e. protocol X wishes to launch an index that only they control the candidate asset list for), this is possible by launching a new controller that they own. In this light, the Sigma committee is the in-house wing responsible for our community-sourced index products.

## Process

If you have a neat idea for a new index, the way to go about making it real is:

* Create a new thread on [forum.indexed.finance](https://forum.indexed.finance) under the Sigma category.
* Include the following things:
    * The name of the index,
    * A description of it's purpose or market sector,
    * The weighting strategy,
    * Any backtesting or projection analyses you have performed,
    * The starting price for the token (the 'initial index value'),
    * The number of tokens it will actively contain (minimum 3, maximum 10),
    * Criteria for token inclusion (age, market capitalisation),
    * The list of tokens to include at launch (maximum 25),
    * [Optional] If you're capable of making a large initial liquidity commitment, mention this,
    * [Optional] Ideas for an icon/logo.
* The Sigma committee - and wider DAO - will look over the proposal and provide their feedback.

If everything looks good, the committee will deploy the pool for you. If you've requested a novel weighting strategy, this will require some development and testing time from those who are capable of doing so. 

Note that if you provide a list of tokens that is larger than the number to be actively included in the index at any given time, the weighting strategy you define will determine what assets are included at launch. If you want to *guarantee* the inclusion of a given set of tokens, then you should only list as many tokens as there are to be active members.

Examples of successful applications made in this manner are:
  * [The DEGEN Index](https://forum.indexed.finance/t/application-for-the-degen-index/85) ($DEGEN)
  * [The 484 Fund](https://forum.indexed.finance/t/application-for-484-fund-error/583/) ($ERROR) [now deprecated]
  * [The Future Of Finance Fund](https://forum.indexed.finance/t/proposal-the-future-of-finance-fund-fff/625) ($FFF)

## Liquidity Mining

All NDX liquidity mining has been rolled into a single fork of Masterchef V2, which covers both single-sided staking, core pools and Sigma pools.

The details of the liquidity mining program can be found [here](https://ndxfi.medium.com/introducing-the-extended-ndx-liquidity-mining-program-ae30a0470001), and the staking page itself can be found [here](https://indexed.finance/staking) - to ensure that your balances show up correctly, please make sure that your wallet is connected (top-right of the app) and that you're on the Ethereum mainnet.

## The Circuit Breaker

One of the key benefits of deploying index pools via a controller that isn't behind a timelock is the ability to utilize the [circuit breaker](https://github.com/indexed-finance/circuit-breaker).

This is a service - currently running on a handful of DigitalOcean droplets - that monitors the price and supply of each token within a given index pool, and in the event that either of these jumps up or down by some percentage deemed excessive (currently 20% on all Sigma pools) from one block to the next, freezes swaps between assets in any pools that contain said token.

The ability to do this is what prevents an exploit in a single asset token from being used to drain the liquidity of an entire pool - we saw this occur in the [attack on the Roll platform](https://www.coindesk.com/social-tokens-crash-after-a-reported-hack-at-tryroll-wallet), where various social tokens were minted en masse: in the absence of a circuit breaker, an attacker could swap in vast amounts of an exploited token in exchange for unaffected assets.

It is important to note that whilst a circuit break prevents swaps from taking place within a pool, your funds remain accessible at all times. The holders of an index token are _always_ free to burn them back into the underlying assets.

## Composition & Future Purpose

The DAO currently aims to elect a new Sigma committee on a quarterly basis.

As the Indexed protocol evolves, we aim to introduce the ability for Joe Public to create their own index pools using our technology, with the role of Sigma being downgraded to simply maintaining the circuit breaker and enacting asset list updates for existing Sigma pools, rather than acting as reviewers and deployers.
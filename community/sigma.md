# The Sigma Program

If you've spent any time on our Discord server, or reading our Twitter account, you'll possibly have seen mention of the 'Sigma committee', or 'Sigma pools'.

On this page, we'll quickly explain what the Sigma program aims to do, how it does it, what powers are available to it, and who currently holds the keys.

## Introduction

In short: the Sigma program is designed to quickly create innovative products on the Indexed protocol and bring initial liquidity to them.

The 'core' products that are offered by Indexed - DEFI5, CC10 and ORCL5 - are maintained entirely by the DAO, in that their controller is owned by the NDX Timelock contract (the treasury), the admin of which is the NDX GovernorAlpha contract. 

The upshot of this is that on-chain governance votes are required to operate these pools (i.e. adding or removing tokens from the asset lists). This is very much as things should be for our established products - reweighs and reindexes can be triggered by anyone, but changes need to be approved by holders of the protocol.

However, in the days of 300+ gwei gas prices, these are expensive changes to make, and they take time to be applied: three days for the on-chain vote, followed by a two-day timelock before they can be executed, assuming they reach quorum. 

To this end, it was decided via [IIP 4](https://forum.indexed.finance/t/iip-4-sigma-pilot/74) to create a committee of people that can quickly deploy new products and enact changes to their constituent lists, as well as assign liquidity mining rewards to them, operating via a Gnosis multisig. The people behind the keys are referred to as the Sigma committee as a whole.

Why Sigma? Because it's shorthand for adding things. Sorry.

## Justification

There are two main issues with having the DAO as an organization administer the creation of new indices against the core controller:

1. The proposer requires 1% of the total supply of NDX (100,000) to do so, and
2. The scoring contract tied to said controller utilizes the square-root FDV method.

If the proposing party wishes to utilize something other than the square-root FDV methodology, the Sigma committee can get around the above on their behalf by deploying a new controller (if it does not exist already) and creating the new index pool. They'll even pay for the gas needed to do so, because they're stand-up folk.

As newly deployed controllers are owned by the committee multisig rather than the Indexed GovernorAlpha, these 'Sigma pools' can be created and have their token lists adjusted in their infancy without the minimum token or timelock requirement associated with core pools. However, the intent is for ownership of Sigma-created controllers to eventually be handed over to the DAO, where they belong.

This flexibility brings with it both some additional benefits in the form of [Safety Measures](#safety-measures), and some [Security Concerns](#security-concerns) for those worried about centralization, both of which we discuss below.

## Process

{how to request a Sigma pool}

## Liquidity Mining

Separate to the long-term liquidity mining proposal currently being discussed by the DAO, the Sigma committee has 600,000 NDX tokens to allocate as staking rewards for initial liquidity provision on AMMs such as Uniswap.

At the time of writing, 72,500 NDX has been distributed 
## Safety Measures

{talk about the circuit breaker, and that it's a nice thing to have}

## Security Concerns

{detail the powers that the Committee has, and that they can't rug funds}

## The Future

Moving towards a quarterly election focused more on maintaining the circuit breaker and enacting governance requests on controllers that haven't migrated over to GovernorAlpha yet.

Mention that the desire is to increase the democratic nature of index creation so that more people can put things together without having to go through a committee
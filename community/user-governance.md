# Using Your Vote

If you hold NDX tokens, you have a voice when it comes to decisions made by the Indexed protocol as a whole.

In this section, we'll cover the various ways in which you can utilize that voice.

_Last update: 4 October 2021_

## The Overall Process

The Indexed protocol is governed by the Indexed DAO, which is defined as all parties that hold the NDX governance token.

As NDX is a fork of [Compound (COMP)](https://etherscan.io/token/0xc00e94cb662c3520282e6f5717214004a7f26888), this means that we utilize the [Governor Alpha](https://web.archive.org/web/20201205152826/https://compound.finance/docs/governance) module in conjunction with a Timelock contract in order to enable the DAO to implement changes that have popular support.

The life-cycle of a governance proposal is:

* An address with at least 100,000 NDX delegated to themselves puts forward the proposal.
* Members of the Indexed DAO have 3 days to vote for or against the proposal.
* If the proposal receives at least 400,000 votes (and a majority in favour), it is queued.
* After a 2 day timelock, the queued proposal can be executed.

The phrase 'can be executed' above gives away the fact that proposals are code: a transaction (or series of transactions) relating to token transfers, contract upgrades or parameter changes.

## What's Delegation?

The life-cycle above mentions tokens that are 'delegated': this refers to the fact that whilst you might own NDX tokens, you still need to inform the Indexed Governor Alpha who is allowed to cast votes with the weight of those tokens on your behalf. The person who owns NDX and the person who votes with them are frequently the same, which requires a user to simply tell Indexed Governor Alpha that they're self-delegating when they first join the Indexed DAO.

However, casting votes for on-chain proposals involves the expenditure of gas. Even though when you vote, you're only sending a transaction with the identifier of the proposal in question along with a single bit indicating your support or opposition, in periods of high gas prices - or if a protocol puts forward proposals quite frequently - this isn't nothing.

As such, if you prefer, you can delegate your token weight to someone else to vote on your behalf: preferably someone who's active, and who you anticipate will vote the same way you would. It's important to note that delegating does not mean that the delegatee can spend your tokens: they can only vote with them.

## Where Can I Vote Or Delegate?

Indexed has been integrated into the Tally website, which provides wonderfully intuitive support for protocols that utilize either Governor Alpha (or Compound's latest upgrade, Governor Bravo).

[View the Indexed page on Tally here](https://www.withtally.com/governance/indexed).

If there are active proposals, you'll be informed as such under the Proposals section, and from there you can view the associated text of said proposal(s) and cast 'In Favor' or 'Against' votes.

Available on [this dashboard](https://www.withtally.com/governance/indexed/voters) is a list of the largest voters, along with some figures relating to the number of proposals they've voted on and their total delegated votes. From here you can simply click 'Delegate' - the simplest way to go about it if you're new to the process is to just go through Direct Delegation and sign a transaction signalling your intent.

## A Note On Delegating "In Time"

The way that on-chain proposals work is that a particular wallet can only vote with the weight of the tokens delegated to themselves at the block in which a proposal was created.

This means that if you want to vote on an upcoming proposal, you _must_ delegate your tokens - either to yourself or someone else - before the proposal is created. If you have not yet performed any delegation by that time, you _cannot vote_.

Similarly, if you have already delegated your votes, but change the delegatee after a proposal is created, the new recipient will not be able to vote with your weight on that proposal: the right to vote remains with the previous delegatee.

So, if you're new to the Indexed DAO, or you've been a member for a while but haven't delegated yet, it's important that you do so if you wish to exercise your right to vote on-chain.

## Do All Decisions Need To Be Made This Way?

Not all of the topics that the DAO considers require alterations to the protocol, and as such do not require going through the process of proposing and voting on-chain.

A good rule of thumb is that if the question can reasonably be phrased in a way that starts with the world "should", it probably doesn't need to be addressed on chain, especially if the proposer is trying to gauge the appetite of the DAO for a certain move. Examples are:

* *Should* we establish an auction for selling 100,000 NDX to VC firms from the treasury?, or
* *Should* the annual Indexed meetup happen in Miami or Vladivostok?

These are questions that help establish direction, and for these, we utilize [Snapshot](https://docs.snapshot.org/), which enables gasless (free) off-chain polling. 

[View the Indexed Snapshot page here.](https://gov.indexed.finance/#/)

We frequently use Snapshot polls as a *precursor* to putting on-chain proposals forward, as it doesn't cost anything for you to cast votes there. One thing to bear in mind, however, is that Snapshot simply takes a freeze-frame of how many tokens are held by you (or delegated to you) at the creation time of a poll.

Beyond the fact that it's free to interact with, there are two other major benefits to Snapshot: 
* Whereas Governor Alpha proposals are restricted to Yes or No options, Snapshot polls allow the proposer to put forward multiple responses (click [here](https://gov.indexed.finance/#/ndx.eth/proposal/QmcRHDdFqFbPyeJYKq9MDnSbECps6rNYbNk1W3r2g2Z91i) for an example).
* Proposers only require a single NDX token to create a poll rather than the 100,000 NDX required by Governor Alpha, allowing a far wider group of participants to initiate discussions and proposals.

We do not consider Snapshot polls to have the same binding quorum levels as required by Governor Alpha, as Snapshot cannot - by definition of being off-chain - trigger changes to the protocol. Rather, we use Snapshot polls as a gauge for whether or not an on-chain vote would be successful.

## When Can't You Vote?

Leaving to the side the issue of delegating your tokens in time, there is one other common situation where you 'have' NDX tokens, but cannot use them to vote.

When you stake NDX in a liquidity pool, such as NDX/ETH on Uniswap or NDX/BNT on Bancor, the NDX tokens involved are transferred to another address. Neither of these actions have a delegation step as part of the transfer process (as not all tokens on these platforms adhere to the Governor Alpha process), and so tokens that are 'locked up' in this way are ineligible to vote.

If you own NDX tokens, it is worth weighing whether or not you wish to utilize them primarily for their voting capabilities or their ability to earn fees as liquidity.

The core developer team informs the DAO in the [Discord](https://discord.indexed.finance) in advance of any intended proposal submissions, be they on or off-chain, so that those who are staking but may wish to vote have time to exit their positions and delegate appropriately. 

### An Aside: The Best Of Both Worlds

Indexed allows members of the DAO to stake their NDX tokens in exchange for [dNDX](https://etherscan.io/token/0x262cd9adce436b6827c01291b84f1871fb8b95a3), a dividend-bearing variant that is entitled to a pro-rata share of 60% of all protocol revenue. Holders of the NDX token can enter a timelock in exchange for dNDX via the Timelock webpage [here](https://indexed.finance/timelocks), and details about dNDX are available on [this Medium post](https://ndxfi.medium.com/ndx-is-now-a-productive-asset-fa375e3f8db0).

NDX that is entered into a timelock in this way is automatically delegated back to stakers, allowing for both revenue generation and on-chain voting simultaneously. Our Snapshot strategy accounts for both NDX tokens that have been delegated to you _and_ undelegated NDX that is within your wallet, so you can also use these locked tokens to vote off-chain via Snapshot.

## Metagovernance

As the ultimate owners of the [core controller](https://etherscan.io/address/0xf00a38376c8668fc1f3cd3daeef42e0e44a7fcdb#writeProxyContract), the DAO indirectly has voting rights on any protocols with governance power that the core index pools hold tokens for. At the time of writing, there are two tokens that utilize the same governance structure as NDX: COMP and UNI, which are in both DEFI5 and CC10.

[Proposal 4](https://www.withtally.com/governance/indexed/proposal/4) enabled 'metagovernance' of these two tokens, whereby the tokens held by these pools are delegated to metagovernor contracts, and the pool controller can direct these contracts to vote on proposals put forward by these external protocols.

At present, there is no Indexed user interface for intuitively casting metavotes in this manner, but the functionality is available via Etherscan and is being monitored.
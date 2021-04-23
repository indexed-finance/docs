# Using Your Vote

If you hold NDX tokens, you have a voice when it comes to decisions made by the protocol as a whole.

In this section, we'll cover the various ways in which you can utilize that voice, both on and off-chain.

_Last update: 23 April 2021_

## The Overall Process

The Indexed protocol is governed by the Indexed DAO, which is defined to be the group of all parties that hold the NDX governance token.

As NDX is a fork of Compound (COMP), this means that we utilize the Governor Alpha module in conjunction with a Timelock contract in order to enable the DAO to implement changes that have popular support.

The life-cycle of a governance action is therefore as follows:

* An address with at least 100,000 NDX delegated to themselves puts forward a proposal.
* Members of the Indexed DAO have 3 days to vote for or against the proposal.
* If the proposal receives at least 400,000 votes (and a majority in favour), it is queued.
* After a 2 day timelock, the proposal can be executed.

The phrase 'can be executed' above gives away the fact that proposals are code: a transaction (or series of transactions) relating to token transfers or parameter changes.

## What's Delegation?

The life-cycle above mentions tokens that are 'delegated' - this refers to the fact that whilst you might own NDX tokens, you still need to inform Governor Alpha of who is allowed to cast votes with the weight of those tokens on your behalf. The person who owns NDX and the person who votes with them are frequently the same, which requires a user to simply tell Governor Alpha that they're self-delegating when they first join the Indexed DAO.

However, casting votes for proposals necessarily involves the expenditure of gas: it's not much, because you're only sending a transaction with the identifier of the proposal in question along with a single bit indicating your support or opposition, but in periods of high gas prices, or if a protocol puts forward proposals quite frequently, this isn't nothing.

As such, if you prefer, you can delegate your token weight to someone else to vote on your behalf: preferably someone who's active, and who you anticipate will vote the same way you would.

## Where Can I Vote Or Delegate?

Whilst everything described above can, theoretically, be done via Etherscan - Indexed has been integrated into the Tally website, which provides wonderfully intuitive support for protocols that utilize either Governor Alpha (or Compound's latest upgrade, Governor Bravo).

[View the Indexed page on Tally here](https://www.withtally.com/governance/indexed).


## Do All Decisions Need To Be Made This Way?

## When Can't You Vote?

## Metagovernance

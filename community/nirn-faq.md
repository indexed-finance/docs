# Yield Aggregator Vaults FAQ

*Last update: 4 August 2021*

## What Is Nirn, Exactly?

Nirn is a permissionless yield aggregator that optimizes interest rates for lenders across several lending protocols. The central idea is to allocate capital among multiple lending protocols in whatever ratios result in the greatest net interest rate.

Nirn as a _protocol_ supports several assets that can be loaned out via distinct Nirn _vaults_.

Conceptually, Nirn is similar to Yearn's iTokens, Rari's yield pools and Idle Finance; however, it has a number of key distinctions:

Each Nirn vault can split its capital among several lending markets, and does not use permissioned rebalancer accounts to determine how it is split. Instead, optimal allocations can be calculated off-chain by anyone and suggested to the vault contract, which then verifies that the suggested rebalance would increase the vault's net interest rate. This both prevents any reliance on the developers of Indexed and ensures that if a better allocation of capital is possible, anyone can make the vault use it.

## Is There A Whitepaper?

Yes we do! Please enjoy: [Nirn, A Compositional, Extensible and Permissionless Yield Aggregator](https://github.com/indexed-finance/nirn-whitepaper/blob/main/Nirn_Whitepaper.pdf).

Note that as we integrate additional protocols, release the off-chain optimiser and generally improve upon the explanation in the aftermath of the launch, the paper version is liable to change. Changes to the paper are reflected in a version on the front page and a change-log.

## When Would Nirn Be Helpful For Me?

Imagine that you've deposited a significant amount of DAI into Compound. You're happy with the lending APR, and go on with your daily business.

You come back after a while and discover that a lot of capital has followed you into the Compound vault, dragging down your returns to the point where you'd be better off using Aave instead. So, you decide to move your capital.

After you do so, you check the rates again - only to find that Aave's rate of return has decreased, and Compound's has _increased_, to the point where Compound is once again the better bet.

This is down to the fact that - all other things being equal - the amount of capital that is deposited to a lending protocol is inversely proportional to the rates that depositors receive. The act of you moving your funds from Compound to Aave may well have been what tipped the balance (or other people noticed the same thing as you, and similarly migrated funds across).

The 'solution' here is to only move _some_ of your funds over to Aave, and leave the rest in Compound, in such a way as the average of the returns from the two is higher than you being purely in one or the other.

That is where Nirn comes in - if such a rebalancing of funds is possible, you - or _anyone else_ - can propose the change, and put it into effect for everyone within the same vault as you.

Even if your tokens are sitting in cold storage somewhere, the vault rates can be adjusted by any EOA account: you don't have to play around with moving your funds from where they're stored.

## Why Did You Build Nirn? You're An Index Protocol!

This is true, it's in the name. With that said, our goal is to assist with all forms of passive portfolio management.

The core reason that Nirn exists is to ultimately integrate the nTokens provided by the vaults as proxy assets within our [index pools](./pool-faq.md). Most of the assets within our pools - such as the DEFI5 - can be loaned on most protocols, and it is a wasted opportunity for those assets to simply sit in a Balancer pool to act as liquidity.

Nirn is our solution to this: by representing UNI within an index as nUNI (Indexed UNI), tokens such as DEFI5 become _interest-bearing_: they pay YOU, rather than having you pay a streaming or management fee for holding them.

Once we integrate Nirn into our indices, we'll make sure that we aren't building a walled garden: you'll still be able to mint index tokens from the standard asset such as, e.g. UNI, and burn index tokens back into the same. The nToken administration will be dealt with internally.

## How Do I Deposit Or Withdraw?

{We'll fill this one out once the protocol is integrated into our website with some step-by-step instructions: we'll also likely film an Indexed Learn video about this exact topic quite soon. Stay tuned!}

## I Made A Transaction When Depositing, But Nothing Happened?

It's likely that your transaction approved the ability for the selected Nirn vault to transfer your token, rather than actually transferred it. This is a necessary step, and not one we can bundle up into a single action for you.

The 'fix' is simple: execute the transaction again.

## What Assets Can I Deposit Into A Nirn Vault?

The full list of assets that can have Nirn vaults created for them is available [here](../nirn/supported.md).

## Your List Says That The Asset I Want To Stake Is Supported, But I Don't See A Vault!

Just because an asset is supported by Nirn doesn't mean that we've spent the gas to create a vault for it: there are a LOT of tokens captured in the dragnet of the protocols that we support.

In a future version of this document, we'll show you how to launch a new Nirn vault if one doesn't already exist. Alternatively, hop into our Discord and ask us!

## What Happens If A New Lending Protocol Starts Up? Can You Support It?

Provided that someone (either ourselves or some third party) produces a protocol adapter for the new protocol, then yes: we can deploy the new protocol adapter through a vote from the Indexed DAO, register it with the adapter registry, and capture all of its lending markets as available options for Nirn vaults to use.

Similarly, should the DAO choose to, it can vote to remove the protocol adapter and all of its supported markets.

## A New Lending Market Has Opened Up For An Asset On A Supported Protocol. Can We Integrate It?

Yes! This is simple for us to do - one of the requirements of our protocol adapters is the ability to list supported markets. If a new market opens up on an existing protocol, the appropriate protocol adapter can deploy a new token adapter, exposing the vault to the new market.

## The Asset I Want To Lend Only Has A Market On One Protocol. Should I Use Nirn?

In the interests of honesty: no. Nirn vaults charge a default fee of 10% of the yield generated - although this can be changed by the Indexed DAO -, and if there's only ever one protocol that a Nirn vault will use, it's best to simply use that protocol instead.

_However_, if you know that new markets are opening up for your asset on protocols that are supported by Nirn (or there's a new protocol starting up that will: see above), then you _might_ be justified in utilising a Nirn vault. Your mileage may vary!

## What Are The Differences Between The Types Of Rebalancing?

There are three types of rebalancing:

* A 'plain' rebalance,
* A weight rebalance, and
* A weight and adapter rebalance

The first type of rebalance is a rebalance that puts any capital in excess of the current reserve ratio (default 10%) of deposited assets to work through the currently defined protocols at the currently defined weightings.

The latter two are more refined, and involve adjusting the ratios for which capital is deployed to different supported protocols. For most of you reading this, you'll likely only ever invoke a plain rebalance, if at all.

Newly deposited assets sit within a vault as liquid capital until such time as a plain rebalance is called: this is to reduce the average gas cost of a deposit or withdrawal, but it's worth remembering that if you've deposited assets and want to immediately put them to work, you need to subsequently trigger a plain rebalance.

## I'm Not Very Technical - Do I Have To Wait For Someone To Perform A Weight/Adapter Rebalance A Vault For Me?

To start with, yes: if you don't have the technical knowledge to work this out yourself.

However, this won't be the case for long: we'll soon be releasing an off-chain optimiser that can determine whether a rebalancing can be made (and submit one if it can), and you'll be able to run this yourself for your preferred vault/s!

Stay tuned, this page will be updated linking you to the appropriate repository and documentation when it's available!

## I Proposed A Weight/Adapter Rebalance, And It Wasn't Accepted. Why?

The default settings of Nirn vaults are such that these types of rebalance need to produce at least a 5% improvement on the current APR of a vault in order to be considered valid.

If you _have_ got a rebalancing that meets this criteria, it could well be that someone else just performed a rebalance before you: weight/adapter rebalances are only accepted every 60 minutes, in order to reduce the attack surface.

## Why Are All The Vaults Just Using A Single Protocol Right Now?

When a vault is launched, it automatically assigns the entirety of the vault weight to the protocol that has the highest APR at the time of creation.

Depending on how rates evolve (and the amount within a given vault), rebalances may either shift the protocol being utilised, or make use of multiple protocols simultaneously.

## I Deposited/Withdrew X Tokens, And Some Wrapped Tokens Went To The Treasury - Why?

Fees accrued within the vault are transferred to the Indexed Finance DAO upon every deposit or withdrawal.

If you're concerned that you've received 'fewer' nTokens or underlying tokens than you'd expect to have done as a result, you haven't. What the vault has done is inflated the nToken supply (updating the conversion ratios appropriately) and treated the fee claim as a deposit of `fees_due` to a vault with a balance of `balance - fees_due`.

## I Have Other Questions, Help!

If you've got _any_ other questions that you'd like to be answered here, please reach out to us on [Discord](http://discord.indexed.finance/) or by email at [contact@indexed.finance](mailto:contact@indexed.finance).

We want this page to be as helpful as possible, so help us help you!
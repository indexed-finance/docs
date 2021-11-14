# Governance

*Last Update: 9 August 2021*

## Role

The NDX governance organization is responsible for:
- Upgrading proxy implementations as needed.
- Deploying new index pools from the core controller.
- Managing the token categories which indices select from and creating new ones.
- Approving pool controllers that implement new management strategies.
- Setting configuration values such as swap fees.
- Adjusting parameters of Nirn yield aggregator vaults such as fees and reserve ratios.

## NDX Token Distribution

NDX is the governance token for Indexed. The initial supply of 10,000,000 NDX is being distributed as follows:
- 35% is vesting to the NDX treasury over the course of 9 months, beginning March 1, 2021.
- 25% was distributed through liquidity mining to users who staked CC10/DEFI5 index tokens or their Uniswap V2 Ether pair LP tokens (ended March 8th 2021).
- 20% will go to the founders and future contributors of the protocol, subject to vesting periods.
- 15% is set to be distributed through liquidity mining to users who stake index tokens, either single-sided or as liquidity for various DEXes (scheduled to end Q1 2023).
- 5% will be used to reward keepers who update the Uniswap oracle and trigger periodic updates on the pool controller (under development).

As of June 1, 2021 the ability to mint new NDX tokens is available to the DAO.

Minting is restricted to a maximum of 10% of the supply (at the time tokens are minted) and may only occur once every 90 days. NDX governance may also disable minting permanently by changing the minter address from the timelock contract to the null address.

## Early Governance

In order to ensure the security of the project while distribution is underway, the team will retain the ability to create and vote on governance proposals while our tokens are vesting. This will ensure that we are able to respond if security incidents occur prior to the completion of the initial distribution, but all successful proposals will still be subject to the two day time lock.

## Keepers

The 5% allocation for keepers is currently held by the timelock contract and will be transferred once we complete development and testing of the keeper bot and contract. Until then we will trigger the updates ourselves, and anyone else can do so on Etherscan.
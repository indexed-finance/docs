# Governance

## Role

The NDX governance organization is responsible for:
- Upgrading proxy implementations as needed.
- Deploying new index pools.
- Managing the token categories which indices select from and creating new ones.
- Approving pool controllers that implement new management strategies.
- Setting configuration values such as swap fees.

## NDX Token Distribution

NDX is the governance token for Indexed. The initial supply of 10,000,000 NDX will be distributed as follows:
- 20% will go to the founders, investors and future team members, subject to vesting periods.
- 5% will be used to reward keepers who update the Uniswap oracle and trigger periodic updates on the pool controller.
- 25% will be available for liquidity mining between December 22, 2020 and January 21, 2021.
- 20% will be distributed to DeFi users after January 22, 2021.
- 30% will be made available to the NDX treasury over the course of 9 months, beginning March 1, 2021.

After June 1, 2021 the ability to mint new NDX tokens will be available to the governance organization.

Minting is restricted to a maximum of 10% of the supply (at the time tokens are minted) and may only occur once every 90 days. NDX governance may also disable minting permanently by changing the minter address from the timelock contract to the null address.

## Early Governance

In order to ensure the security of the project while distribution is underway, the team will retain the ability to create and vote on governance proposals while our tokens are vesting. This will ensure that we are able to respond if security incidents occur prior to the completion of the initial distribution, but all successful proposals will still be subject to the two day time lock. Additionally, the voting period on the governor contract is temporarily set to a value which corresponds to about 12 hours in blocks; after January 7, 2021, anyone can call a function on the governor to set the voting period to its permanent value, which is closer to 3 days.

## Keepers

The 5% allocation for keepers is currently held by the timelock contract and will be transferred once we complete development and testing of the keeper bot and contract. Until then we will trigger the updates ourselves, and anyone else can do so on Etherscan.

## Liquidity Mining

The initial liquidity mining period will begin on December 22 and continue for 30 days. Users will be able to mine NDX by staking CC10, DEFI5 or the Uniswap LP tokens for their respective WETH pairs. Each pool will receive 625,000 NDX in total.
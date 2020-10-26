# Table of Contents

## Protocol

* [Home](protocol/index.md)
* [Terminology](protocol/terminology.md)
* [Price Oracles](protocol/price-oracles.md)
* [MCapSqrt Strategy](protocol/mcap-strategy.md)
* [Pools](protocol/pools.md)
* [Rebalancing](protocol/rebalancing/index.md)
  * [Bootstrapping new tokens](protocol/rebalancing/adding-tokens.md)
  * [Removing tokens](protocol/rebalancing/removing-tokens.md)
* [Limitations](protocol/limitations.md)

## Smart Contracts

* [IPool.sol](smart-contracts/pool.md)
* [PoolInitializer.sol](smart-contracts/initializer.md)
* [UnboundTokenSeller.sol](smart-contracts/token-seller.md)
* [UniSwapV2PriceOracle.sol](smart-contracts/oracle.md)
* [MarketCapSqrtController.sol](smart-contracts/controller.md)
* [@indexed-finance/proxies](smart-contracts/proxies/proxies.md)
  * [DelegateCallProxyManager.sol](smart-contracts/proxies/DelegateCallProxyManager.md)
  * [DelegateCallProxyManyToOne.sol](smart-contracts/proxies/DelegateCallProxyManyToOne.md)
  * [DelegateCallProxyOneToOne.sol](smart-contracts/proxies/DelegateCallProxyOneToOne.md)
  * [ManyToOneImplementationHolder.sol](smart-contracts/proxies/ManyToOneImplementationHolder.md)
  * [SaltyLib.sol](smart-contracts/proxies/SaltyLib.md)
* [Interfaces](smart-contracts/interfaces/index.md)
  * [IBPool.sol](smart-contracts/interfaces/IBPool.md)
  * [IFlashLoanRecipient.sol](smart-contracts/interfaces/IFlashLoanRecipient.md)

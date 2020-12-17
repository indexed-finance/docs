# Table of Contents

## Protocol

* [Home](protocol/index.md)
* [Terminology](protocol/terminology.md)
* [Governance](protocol/governance.md)
  * [Role](protocol/governance.md#role)
  * [NDX Token Distribution](protocol/governance.md#NDX-Token-Distribution)
  * [Early Governance](protocol/governance.md#Early-Governance)
  * [Keepers](protocol/governance.md#Keepers)
  * [Liquidity Mining](protocol/governance.md#Liquidity-Mining)
* [Security](protocol/security.md)
* [Index Controller](protocol/index-controller.md)
* [Index Pools](protocol/pools.md)
* [Rebalancing](protocol/rebalancing/index.md)
  * [Bootstrapping new tokens](protocol/rebalancing/adding-tokens.md)
  * [Removing tokens](protocol/rebalancing/removing-tokens.md)

## Smart Contracts

* [IndexPool.sol](smart-contracts/pool.md)
* [PoolInitializer.sol](smart-contracts/initializer.md)
* [UnboundTokenSeller.sol](smart-contracts/token-seller.md)
* [MarketCapSqrtController.sol](smart-contracts/controller.md)
* [@indexed-finance/proxies](smart-contracts/proxies/proxies.md)
  * [DelegateCallProxyManager.sol](smart-contracts/proxies/DelegateCallProxyManager.md)
  * [DelegateCallProxyManyToOne.sol](smart-contracts/proxies/DelegateCallProxyManyToOne.md)
  * [DelegateCallProxyOneToOne.sol](smart-contracts/proxies/DelegateCallProxyOneToOne.md)
  * [ManyToOneImplementationHolder.sol](smart-contracts/proxies/ManyToOneImplementationHolder.md)
  * [SaltyLib.sol](smart-contracts/proxies/SaltyLib.md)
* [@indexed-finance/uniswap-v2-oracle](smart-contracts/oracle/IndexedUniswapV2Oracle.md)
* [Interfaces](smart-contracts/interfaces/index.md)
  * [IIndexPool.sol](smart-contracts/interfaces/IIndexPool.md)
  * [IFlashLoanRecipient.sol](smart-contracts/interfaces/IFlashLoanRecipient.md)

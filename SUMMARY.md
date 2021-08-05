# Table of Contents

## Introduction

* [FAQs](community/faq.md)
  * [Index Pools](community/pool-faq.md)
  * [Yield Aggregator Vaults](community/nirn-faq.md)
* [Fees](protocol/fees.md)

## Day-To-Day Operations

* [Using Your Vote](community/user-governance.md)
* [The Sigma Program](community/sigma.md)

## Technical Details

### Index Pool Protocol

* [Terminology](protocol/terminology.md)
* [Governance](protocol/governance.md)
* [Security](protocol/security.md)
* [Index Controller](protocol/index-controller.md)
* [Index Pools](protocol/pools.md)
* [Rebalancing](protocol/rebalancing/index.md)
  * [Bootstrapping New Tokens](protocol/rebalancing/adding-tokens.md)
  * [Removing Tokens](protocol/rebalancing/removing-tokens.md)

### Index Pool Smart Contracts

* [Deployments](smart-contracts/deployments.md)
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

### Yield Aggregator Protocol

* [Supported Assets](nirn/supported.md)

### Yield Aggregator Smart Contracts

* [Deployments](nirn/deployments.md)
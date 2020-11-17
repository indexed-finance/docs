# Indexed Finance

Indexed Finance is a protocol for on-chain financial metrics and portfolio management. Our primary goals are:
- Improving the state of on-chain financial metrics.
- Simplifying risk-managed exposure to the DeFi ecosystem.
- Creating and maintaining DeFi indices that benchmark market performance.
- Creating widely applicable Defi contracts to expand the toolkit available to developers.

## Uniswap Oracle
A major focus of the Indexed project is improving the state of on-chain financial metrics. The first step we've taken towards this goal is the creation of a Uniswap oracle contract capable of tracking historical price trends. It records prices on Uniswap markets at a maximum frequency of once per hour and enables contracts to efficiently query the moving average price of tokens over an arbitrary time period. This oracle is used throughout the other Indexed contracts.

## Defi Indices
Our first DeFi product is a capitalization-weighted index pool controller that tracks specific sectors of the DeFi market and dynamically adjusts pool compositions according to market trends. By combining on-chain price data with preset rules that determine portfolio targets, these funds enable easy exposure to DeFi without introducing bias from asset managers and serve as objective benchmarks of DeFi markets.
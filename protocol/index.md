# Indexed

**Protocol Docs Incomplete**


Indexed is a protocol for passively managed token portfolios. The goal of Indexed is to provide better systems for users to gain exposure to the DeFi marketplace.

Building on previous work by the Balancer team, Indexed portfolios are asset pools that double as AMMs (automated market makers). Tokens in a pool have weights which can be adjusted over time to change the composition of the pool's portfolio. Pools can increase or decrease token weights, add new tokens and remove existing ones with minimal access to external liquidity.

Indexed uses UniSwap price oracles to track financial indicators of various tokens. Different asset management strategies can use these oracles to determine which assets to assign to pools and how to weigh them within a portfolio.

Indexed enables users to create index pools managed by DAO-approved strategy contracts and fixed-target pools which have preset initial and target compositions.

Index pools track particular sectors of the DeFi market (or combinations thereof) using deterministic strategies based on financial indicators. 

<!-- Pool controller contracts set weight targets for the assets in a pool and arbitrageurs balance them through swaps. This results in funds that gain fees from rebalances rather than paying them to external markets, and which can completely change their composition by creating small arbitrage opportunities. -->





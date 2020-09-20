## `MarketCapSqrtController`

This contract implements the market cap square root index management strategy.

Categories are periodically sorted, ranking their tokens in descending order by market cap.

Index pools have a defined size which is used to select the top tokens from the pool's category.

Every 2 weeks, pools are either re-weighed or re-indexed.

They are re-indexed once for every three re-weighs.

Re-indexing involves selecting the top tokens from the pool's category and weighing them by the square root of their market caps.

Re-weighing involves weighing the tokens which are already indexed by the pool by the square root of their market caps.

When a pool is re-weighed, only the tokens with a desired weight above 0 are included.
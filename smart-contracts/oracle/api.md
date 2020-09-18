# `UniSwapV2PriceOracle`

# Price Updates

## `updatePrice` 

```
function updatePrice(
  address token
) returns (bool didUpdate)
```

Updates the latest price observation for a token if allowable.
Note: The price can only be updated once per period, and price
observations must be made at least half a period apart.

## `updatePrices` 

```
function updatePrices(
  address[] tokens
) returns (bool[] updates)
```

Updates the prices of multiple tokens.

# Queries

## `getPriceObservation` 

```
function getPriceObservation(address token, uint256 observationIndex) returns (struct UniSwapV2PriceOracle.PriceObservation)
```

Gets the price observation at `observationIndex` for `token`.
Note: This does not assert that there is an observation for that index,
this should be verified by the recipient.

## `observationIndexOf` 

```
function observationIndexOf(uint256 timestamp) returns (uint256)
```

Gets the observation index for `timestamp`

## `canUpdatePrice` 

```
function canUpdatePrice(address token) returns (bool)
```

Queries whether the price of `token` can be updated.

## `computeAverageAmountOut` 

```
function computeAverageAmountOut(
  address token,
  uint256 amountIn
) returns (uint144 amountOut)
```

Compute the average value in _weth of a given amount
of a token.

## `computeAverageAmountsOut` 

```
function computeAverageAmountsOut(
  address[] tokens,
  uint256[] amountsIn
) returns (uint144[] amountsOut)
```

Compute the average value in _weth of a given amount
of a token. Queries the current cumulative price and retrieves
the last stored cumulative price, then calculates the average
price and multiplies it by the input amount.

## `computeAveragePrice` 

```
function computeAveragePrice(
  address token
) returns (FixedPoint.uq112x112 priceAverage)
```

Returns the UQ112x112 struct representing the average price.
Note: Requires that the token has a price observation between 0.5
and 2 periods old.

## `computeAveragePrices` 

```
function computeAveragePrices(
  address[] tokens
) returns (FixedPoint.uq112x112[] averagePrices)
```



Returns the average market caps for each token.
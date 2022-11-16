# artemis-docs

## Perpetual Protocols

### Questions

* For the `sum_of_sum_of_*` metrics, is this a singular value or time series?
  
### General Information

* dYdX
  * V1 launched 
  * V2 launched
  * V3 launched
  * [Analytics](https://dydx.metabaseapp.com/public/dashboard/5fa0ea31-27f7-4cd2-8bb0-bc24473ccaa3)
* Perp Protocol
  * V1 launched on Ethereum mainnet (2020) then XDIA, 12/2020
  * V2 launched on OP, 11/2021
  * [Optimism contract](https://metadata.perp.exchange/v2/optimism.json)
  * [Analytics](https://dune.com/momir/Perpetual-Protocol-v2)
* GMX
  * V1 launched on Arbitrum and Avalanche late 2021
  * [Avalanche contracts](https://gmxio.gitbook.io/gmx/contracts#avalanche)
  * [Arbitrum contracts](https://gmxio.gitbook.io/gmx/contracts#arbitrum)
  * [Analytics](https://stats.gmx.io/#/)

### Docs

Below is a list of metrics for each protocol including the contract addresses and important notes.

* `sum_of_sum_of_gas`
  * dYdX
  * Perp Protocol
  * GMX
* `sum_of_sum_of_dau`
  * dYdX
  * Perp Protocol
  * GMX
* `sum_of_sum_of_txns`
  * dYdX
  * Perp Protocol
  * GMX
* `sum_of_sum_of_percent_of_total_gas`
  * dYdX
  * Perp Protocol
  * GMX
* `trading_volume`
  * dYdX
  * Perp Protocol
  * GMX
* `insurance_pool`
  * dYdX
  * Perp Protocol
  * GMX
* `fees_generated`
  * dYdX
  * Perp Protocol
  * GMX
* `daily_unique_traders`
  * [Query](https://app.flipsidecrypto.com/velocity/queries/1c1b39a7-2636-4b64-a0cd-7e300da4ca47)
  * Definition
    * `unique_traders` is the number of unique users who enter or exit a perpetual position
    * Does not include liquidity providers
  * Schema
  ```
  [
    {
      day,
      chain,
      protocol,
      unique_traders
    },
    ...
  ]
  ```
  * Protocol notes
    * dYdX
    * Perp Protocol
      * Counts the distinct `from` address when `open_position` or `close_position` method is called on the clearing house contract
      * **NOTE:** If a contract makes a delegate call to the clearing house contract the source contract will not be counted (should be in traces, I think)
    * GMX
      * Counts the distinct  `from` address when a `swap` event is emitted from the router contract
      * Does not consider GLP interaction






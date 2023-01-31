# artemis-docs

## Perpetual Protocols
  
### General Information

* dYdX
  * V1 launched 
  * V2 launched
  * V3 launched
  * [Analytics](https://dydx.metabaseapp.com/public/dashboard/5fa0ea31-27f7-4cd2-8bb0-bc24473ccaa3)
* Perp Protocol
  * V1 launched on Ethereum mainnet (2020) then XDIA, 12/2020
  * V2 launched on OP, 11/2021
  * [Optimism contracts](https://metadata.perp.exchange/v2/optimism.json)
  * [Analytics](https://dune.com/momir/Perpetual-Protocol-v2)
* GMX
  * V1 launched on Arbitrum and Avalanche late 2021
  * [Avalanche contracts](https://gmxio.gitbook.io/gmx/contracts#avalanche)
  * [Arbitrum contracts](https://gmxio.gitbook.io/gmx/contracts#arbitrum)
  * [Analytics](https://stats.gmx.io/#/)

### Metrics

* `gas_used`
  * [Query](https://dune.com/queries/1708025)
  * Definition
    * `gas_used` is the daily sum of gas consumed (in $) for each day and protocols _revelant_ contracts. Note, tokens traded on DEXs are excluded to prevent double counting. Additionally, price feed updates were excluded because they are not a initiated by the main user base.
  * Columns
    * `day`, `chain`, `protocol`, `contract_addr`, `contract_name`, `gas_used` 
  * Protocol notes
    * Perp Protocol
      * Excluded price feeds and vtokens from [this list](https://metadata.perp.exchange/v2/optimism.json)
    * GMX
      * Excluded GMX token and Trader Joe pool from [this list](https://gmxio.gitbook.io/gmx/contracts#avalanche)
* `num_txns`
  * [Query](https://dune.com/queries/1708028)
  * Definition
    * `num_txns` is the daily count of transactions for each day and protocols _revelant_ contracts. Note, tokens traded on DEXs are excluded to prevent double counting. Additionally, price feed updates were excluded because they are not a initiated by the main user base.
  * Columns
    * `day`, `chain`, `protocol`, `contract_addr`, `contract_name`, `num_txns` 
  * Protocol notes
    * Perp Protocol
      * Excluded price feeds and vtokens from [this list](https://metadata.perp.exchange/v2/optimism.json)
    * GMX
      * Excluded GMX token and Trader Joe pool from [this list](https://gmxio.gitbook.io/gmx/contracts#avalanche)
* `trading_volume`
  * [Query](https://dune.com/queries/1668657)
  * Definition
    * `trading_volume` is the nominal USD volume of traded
  * Columns
    * `day`, `chain`, `protocol`, `trading_volume`
  * Protocol notes
    * Perp Protocol
      * Sums the `volume_usd` column from the decoded `perpetual_protocol_v2_optimism.trades` table if `margin_usd > 0`
    * GMX
      * Sums the volume amount when an `IncreasePosition` or `DecreasePosition` event is emitted from the GMX vault contract    
* `fees_generated`
  * [Query](https://dune.com/queries/1668739)
  * Definition
    * `fees_generated` is the USD amount generated from trading fees
  * Columns
    * `day`, `chain`, `protocol`, `fees_generated`
  * Protocol notes
    * Perp Protocol
      * Sums the `fee_usd` column from the decoded `perpetual_protocol_v2_optimism.trades` table
    * GMX
      * Sums the fee amount when an `IncreasePosition` or `DecreasePosition` event is emitted from the GMX vault contract   
* `daily_unique_traders`
  * [Query](https://dune.com/queries/1668423)
  * Definition
    * `unique_traders` is the number of unique users who enter, exit, or adjust a perpetual position
  * Columns
    * `day`, `chain`, `protocol`, `traders`
  * Protocol notes
    * Perp Protocol
      * Counts the distinct `trader` field from the decoded `perpetual_protocol_v2_optimism.trades` table
    * GMX
      * Counts the distinct trader address when an `IncreasePosition` or `DecreasePosition` event is emitted from the GMX vault contract
      * Since GMX is on multiple chains, it's possible that the same address interacts with both chains on the same day thereby creating duplicate users if the traders for each chain are added together. To handle this, there is a separate count for the global GMX traders where chain equals "All".

### Data Considerations

* All tables are ordered by `day` in ascending order
* The `protocol` and `chain` field are **case sensitive**. For example:
  * Protocols
    * GMX
    * Perpetual Protocol
  * Chains
    * Arbitrum
    * Avalanche
    * Optimism
* Any contract addresses are **lower case** and thus not checksum compliant





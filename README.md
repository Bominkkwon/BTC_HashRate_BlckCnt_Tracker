# BTC_HashRate_BlckCnt_Tracker
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1_MLIv2zu_YBIiEDxpDh29fKvs-TI8jXB?usp=sharing)


## Table of Contents
* [Project title](#project-title)
* [Technologies](#technologies)
* [Overview](#overview)
* [Required Libraries](#required-library)
* [Methodology](#methodology)
* [Summary](#summary)







## Project title
BTC - Hashrate and Block Count tracker

## Technologies
[Python](https://www.python.org/downloads/ "Download Python") 3.7.9.

## Overview 
Tracking Bitcoin mining network hashrate(TH/s) (the estimated number of terahashes per second the bitcoin network is performing) and Block Count (the sum count of blocks created that interval that were included in the main (base) chain) using the [community API](https://docs.coinmetrics.io/api/v4) from blockchain data provider CoinMetrics.

## Required Libraries

* [Coin Metrics API v4](https://docs.coinmetrics.io/api/v4)
```python
!pip install coinmetrics
```
* [Plotly](https://plotly.com/python/)

## Methodology

1. Obtaining hashrate and block count data from the community API-- API key is not required when accessing community endpoints.
```python
# Initialize a reference object for the Community API
cm = coinmetrics.Community()

# Obtain `HashRate` and `BlkCnt` data for BTC from 2017-01-01 to 2021-08-18.
asset = "btc"
metric = "HashRate,BlkCnt"
begin_timestamp = "2017-01-01"  # Multiple formats of ISO 8601 are supported
end_timestamp = "2021-08-20"    # Multiple formats of ISO 8601 are supported
asset_data = cm.get_asset_data_for_time_range(asset, metric, begin_timestamp, end_timestamp)
print("data given timerange and metric:\n", asset_data)

```
2. Understanding Coin Metrics API/Asset Metrics

* ``` metric = "HashRate" ```
  * Hash rate is derived from difficulty (DiffMean), the rate at which block came in (BlkIntMean) and depending on the protocols, some other pieces of data. It gives an estimate of how much hash power is mining a given chain.

* ```metric = "BlkCnt" ```
  * Only mainchain (non-orphaned/uncles) blocks are counted.
  * For chains that use median time, the day is defined using it, otherwise, it’s defined using the block’s timestamps.

  This API platform provides a lot of different [asset metrics](https://docs.coinmetrics.io/info/metrics) that the users can use.

## Summary
[Bitcoin hashrate chart](https://chart-studio.plotly.com/~bkplotly/1/#plot)

This chart illustrates the historical data regarding the number of hashes calculated per second. Each mining device contributes to a specific hashrate, and the chart reflects the total hashrate (TH/s) for the entire Bitcoin network. Hashrate is a derivative of difficulty, which considers the rate of incoming blocks and, depending on protocols, incorporates additional data. It provides an estimation of the hash power actively engaged in mining a given blockchain. Notably, the hashrate exhibits constant fluctuations, with instances of significant drops exceeding 50%, such as during China's prohibition of Bitcoin mining in various inland provinces, the most recent being Sichuan from May to June 2021. On June 26, 2021, the hashrate plummeted to 57.47M (TH/s), marking a 52.73% decrease. Remarkably, Bitcoin's SHA256 hashrate rebounded swiftly, increasing by 151.72% the following day.

| Date          | Hashrate (TH/s) | % Hashrate +/- |
|---------------|------------------|-----------------|
| June 24, 2021 | 108.9951M        |                 |
| June 26, 2021 | 57.47014M        | 52.727%         |
| June 27, 2021 | 87.19607M        | 151.724%        |
[BTC_hashrate_data](https://chart-studio.plotly.com/~bkplotly/1/#data)

This data, while suggestive of potential implications on miner behavior and mining pools, reveals the inherent volatility in hashrate, common in mining activities. A temporary disruption in mining power, as observed during the Chinese crackdown, does not offer substantial information beyond indicating a reduction in computing power. It is crucial to recognize that correlation does not necessarily imply causation.

Even if one were to assume that the sole recent network change was the China mining ban, given that a substantial portion of hashrate was concentrated in China, the fluctuation in hashrate alone cannot definitively ascertain the percentage of mining originating from China or gauge its impact. This uncertainty arises from the specific algorithm and its dependence on adjustment methods. While some context on miner activity, like Coin Metrics' ["Miner-exchange Flows,"](https://coinmetrics.io/following-flows-ii-where-do-miners-sell/) or a loose idea of hashrate distribution (mining pools) through coinbase data in transactions (e.g., Blockchain.com's ["Hashrate Distribution"](https://www.blockchain.com/pools) may offer insights, such data is inherently unreliable. Bitcoin miners, driven by strong privacy concerns, can obfuscate their identities, and the technical features of Bitcoin prioritize user and miner privacy. Notably, these miners are unlikely to be long-term Bitcoin holders, as they often sell rewarded Bitcoins to cover costs and for other purposes.

[Block Count Chart](https://plotly.com/~bkplotly/3/)

As miners discontinue their operations, the difficulty of mining a block undergoes adjustment to become more manageable. The targeted rate for Bitcoin mining is deliberately established at one block every 10 minutes. To achieve this, difficulty is recalibrated every 2016 blocks, approximately every two weeks (20160 minutes). This adjustment is based on the performance of the preceding 2016 blocks. During the recent crackdown on Bitcoin mining in China, numerous miners were compelled to go offline, resulting in a temporary reduction in mining computing power. Consequently, the hashrate declined, triggering a rapid downward adjustment in [difficulty](https://btc.com/stats/diff). While such volatility can be disconcerting, it is unlikely to have a significant impact due to the robust technical features and properties of Bitcoin, including preimage resistance, collision resistance, avalanche effects, and puzzle friendliness.

The behavior of the network during this period constitutes a novel scenario. The mining computing power has evolved with the introduction of new technology as additional miners have joined the Bitcoin network, intensifying competition for block rewards. Simultaneously, the current difficulty level is considerably higher than before, rendering the blockchain nearly impervious to rewriting. Notably, Bitcoin adoption has accelerated, surpassing previous rates.

Despite the escalating crackdown on Bitcoin in China since 2013, the cryptocurrency has demonstrated resilience and accrued substantial value since its inception, with expectations of further appreciation over time. Bitcoin's unique incentive system serves as a driving force for miners, motivating them to relocate to different countries to operate their mining rigs. This migration also provides an opportune moment to transition to cleaner power supplies. For Bitcoin miners outside of China, the crackdown presents a unique opportunity—the "great mining migration." A decentralized Bitcoin mining landscape, less concentrated in an authoritarian state, strengthens the overall resilience of the Bitcoin network. This shift attracts new investors, fostering heightened interest in cryptocurrency. The extensive migration opens doors for investors to engage in both facets of Bitcoin's incentive system, further enhancing the cryptocurrency's appeal.



** Disclaimer: This analysis is not financial advice but a data study based on available information. Individuals should conduct their research and seek professional advice before making investment decisions. **

The recent Bitcoin mining migration, prompted by the China mining ban, has raised concerns about network security. However, our research team anticipates long-term benefits. The dispersion of mining power across countries reduces dependence on a single nation, fostering decentralization. Additionally, the shift to countries with cleaner energy sources contributes to a more sustainable network. Despite concerns, the Bitcoin network has mechanisms to withstand disruptions. This information is for informational purposes only, and individuals should seek professional advice for investment decisions.

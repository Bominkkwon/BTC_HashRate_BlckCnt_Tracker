# BTC_HashRate_BlckCnt_Tracker
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1_MLIv2zu_YBIiEDxpDh29fKvs-TI8jXB?usp=sharing)


## Table of Contents
* [Project title](#project-title)
* [Technologies](#technologies)
* [Overview](#overview)
* [Required Libraries](#required-library)
* [Methodology](#methodology)







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


  

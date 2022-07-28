# Title
Humble Tractors NFT KPI

# Summary

Humble tractors’ KPI options are to promote sales of its NFTs on the OpenSea marketplace. The KPI options will track the number of sales at the price request timestamp (contract expiration) through a query to the given humble tractors activity page on OpenSea and verified by screenshots by named trusted users on an open channel in the SuperUMAn DAO and this is converted to a corresponding share from the maximum KPI options payout.

# Ancillary Data Specifications

- Metric: Total number of sales before expiry,
- Endpoint: “https://discord.com/channels/909933079181799524/994957148025012225", 
- Fallback: If cannot access discord link refer to https://discord.com/channels/909933079181799524/994957148025012225,
- Method: "https://github.com/SuperUMAn-DAO/UMIPs/blob/master/Implementations/humble-tractors.md", 
- Key: Total sales,
- Interval: Lookup the total number of sales achieved at or before request timestamp,
- Rounding: 0.

# Implementation

1. Proposers/Voters should check the number of sales at "https://discord.com/channels/909933079181799524/994957148025012225" and https://api.opensea.io/api/v1/collection/humble-tractors/stats
2. Humble Tractors does not have a collection id which makes it difficult to ascertain the number of sales by a certain timestamp.
3. For this reason, the source used as a reference to determine the number of sales will be the median for the first 3 screenshots provided by pre-designated SuperUMAns posted after the request timestamp in "discord link" channel of the SuperUMAn discord. The specific SuperUMAns taking the expiry screenshots will be  @deadcoin#0901, @PVmilihache#8517, @PennyPanda#4443 and @Neondaemon#7190


# Post-Processing

It is intended to deploy the documented KPI options on Polygon using [LSP contract](https://github.com/UMAprotocol/protocol/blob/master/packages/core/contracts/financial-templates/long-short-pair/LongShortPair.sol) with `General_KPI` price identifier approved in [UMIP-117](https://github.com/UMAprotocol/UMIPs/blob/master/UMIPs/umip-117.md). The contracts should use [Linear LSP FPL](https://github.com/UMAprotocol/protocol/blob/master/packages/core/contracts/financial-templates/common/financial-product-libraries/long-short-pair-libraries/LinearLongShortPairFinancialProductLibrary.sol) with the `lowerBound` set to 0 and `upperBound` set to 30. 

500 USDC is set as the collateral, with the KPI linked to NFT sales
Based on the intended ancillary data above, `upperBound` should be set to 30 and lowerbound set to 0 implying the following payouts:

* NFT Sales at or below 10 humble tractors voters should return the value 0 and long KPI option holders would be allocated 0% of collateral and short tokens would be allocated 100% for each token;
* NFT Sales between 11 and 30 (inclusive) voters should return the value 15 and long KPI option holders would be allocated 50% of collateral and short tokens would be allocated 50% for each token;
* NFT Sales at 31 or above voters should return the value 30 and long KPI option holders would be allocated 100% of collateral and short tokens would be allocated 0% for each token;

`collateralPerPair` above is the total locked collateral per KPI options token and is set to 1 USDC


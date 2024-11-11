# T-100 Aviation Data Analysis
The goal of this repository is to provide insightful analysis of aviation data using various Python tools including `numpy` and `pandas`.

## About the data
The primary dataset is the U.S. DOT T-100 data for Q1 & Q2 of 2024. It is publicly available from the [Bureau of Transportation TranStats](https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FMG). There are also various helper tables, sourced also from the Bereau of Transportation. These lookup tables translate T-100 codes into plain text. For example, WAC = 15, corresponds to the region of Rhode Island. All data used can be found in the 📁[`data`](https://github.com/admacpherson/T-100-Aviation-Data/tree/main/data) folder of this repository. 

## Findings

### Load Factor by Carrier

#### Test

|Carrier|Total LF|Domestic LF|International LF|
|-------|--------|-----------|----------------|
|Delta Air Lines Inc.|0.862686|0.864426|0.853418|
|Allegiant Air|0.859050|0.859050|NaN|
|Sun Country Airlines d/b/a MN Airlines|0.856746|0.865843|0.798086|
|American Airlines Inc.|0.843187|0.843864|0.840523|
|United Air Lines Inc.|0.840662|0.851609|0.807783|
|Spirit Air Lines|0.822254|0.828956|0.766056|
|Envoy Air|0.821440|0.823843|0.788894|
|JetBlue Airways|0.818494|0.826618|0.797715|
|Alaska Airlines Inc.|0.817015|0.815006|0.847703|
|Hawaiian Airlines Inc.|0.811663|0.816743|0.760081|
|SkyWest Airlines Inc.|0.804319|0.804277|0.808450|
|Republic Airline|0.794361|0.794361|NaN|
|Southwest Airlines Co.|0.780325|0.778630|0.859099|
|Frontier Airlines Inc.|0.767294|0.770876|0.713395|

As the table shows, in Q1/Q2 of 2024, Delta had the best load factor performance from an overall perspective as well as in the domestic and international categories. Meanwhile Frontier was the worst performer in all three of these categories, though their domestic performance is only slightly below Southwest, which also underperformed relative to other airlines. Along with Republic Airlines, Southwest and Frontier join to be the only 3 carriers with an overall or domestic load factor below 80%. While the legacy carriers are among the top performers in load factor, 2 ULCCs (Allegiant and Sun Country) boast strong results boosted by domestic LF and surpass American and United to claim the #2 and #3 spots respectively. 

# T-100 Aviation Data Analysis
The goal of this repository is to provide insightful analysis of aviation data using various Python tools including `numpy` and `pandas`.

## About the data
The primary dataset is the U.S. DOT T-100 data for Q1 & Q2 of 2024. It is publicly available from the [Bureau of Transportation TranStats](https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FMG). There are also various helper tables, sourced also from the Bereau of Transportation. These lookup tables translate T-100 codes into plain text. For example, WAC = 15, corresponds to the region of Rhode Island. All data used can be found in the 📁[`data`](https://github.com/admacpherson/T-100-Aviation-Data/tree/main/data) folder of this repository. 

## Findings

### Load Factor
The analysis of load factor can be performed along several different variables. Here, we analyze the top performing routes, domestically, internationally, and abroad, as well as total load factor by airline along the same categories.

#### Best & Worst International LF by Route & Airline
|Origin|Destination|Airline|LF|
|------|-----------|-------|---|
|PUJ|BWI|Southwest|0.991429|
|SJD|ORD|American|0.990741|
|PUJ|DFW|American|0.919122|
|...|
|GUM|NGO|United|0.202610|
|NGO|GUM|United|0.202008|
|FLL|PAP|Spirit|0.168975|

Looking at the best and worst performing international routes by load factor, we see that the top 3 are Southwest's Punta Cana, DR to Baltimore, American's Chicago O'Hare to San Jose del Cabo, MX, and American's Dallas-Fort Worth to Punta Cana, DR (American and Punta Cana are also #4 on the list). The worst 3 performers were Spirit's Fort Lauderdale to Port-au-Prince, Haiti, United's Nagoya, Japan to Guam, and United's return flight from Guam to Nagoya. While the Port-au-Prince route's worst-in-class performance is understandable due to the recent political instability and violence in Haiti, it seems that United's GUM-NGO route pairing does not have a lot of demand. While there may be additional considerations, such as Essential Air Service subsidies or network feed, the LF data seem to suggest the route is not independently commercially viable.


#### Overall Load Factor by Carrier
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



## Methodologies

### Load Factor
This analysis focused only on major US carriers as defined by the DOT (carriers with annual revenue >$1B). The data include a classification scheme under the variable `CARRIER_GROUP_NEW`. Filtering this provides a list of major airlines but includes cargo flights as well as commercial. Rather than filter wholesale by airlines, since many airlines perform both passenger and cargo service, I filtered on the flight level to include all flights with at least 1 passenger.
```python
# Filter only major carriers (TranStats category 3)
major_carriers = big_table.loc[big_table['CARRIER_GROUP_NEW'] == 3]
# Filter passenger flights only
major_passenger_flights = major_carriers.loc[major_carriers['PASSENGERS'] > 0]
```
This yielded all commercial passenger flights on major airlines as desired. However, many of the routes listed were not regularly scheduled flights and could thus distort the data with uncharacteristically high or low load factors. To prevent outliers while still preserving the bulk of scheduled flights, I filtered for all route pairings that had been flown at least 10 times by the airline in question.

```python
# Filter flights performed
major_passenger_flights = major_passenger_flights[major_passenger_flights['DEPARTURES_PERFORMED'] > 10]
```
Now, to distinguish between domestic and international flights, the DOT uses a `REGION` category, rather than a straight binary. Accordingly, there are several different values that correspond to international flights, yet only one that corresponds to domestic air travel. We can use this latter value to filter flights as domestic or not domestic (i.e. international). Here I used an anonymous lambda function to create a new column titled "DOMESTIC" that had a value of either `D` for domestic or `I` for international.

```python
major_passenger_flights['DOMESTIC'] = major_passenger_flights['REGION'].apply(lambda x: 'D' if x == 'D' else 'I')
```

Finally, with a complete dataset we could analyze routes by airline and load factor. 


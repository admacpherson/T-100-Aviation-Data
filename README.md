# T-100 Aviation Data Analysis
The goal of this repository is to provide insightful analysis of aviation data using various Python tools including `numpy` and `pandas`.

## About the data
The primary dataset is the U.S. DOT T-100 data for Q1 & Q2 of 2024. It is publicly available from the [Bureau of Transportation TranStats](https://www.transtats.bts.gov/Fields.asp?gnoyr_VQ=FMG). There are also various helper tables, sourced also from the Bereau of Transportation. These lookup tables translate T-100 codes into plain text. For example, `WAC = 15`, corresponds to the World Area Code region of Rhode Island. All data used can be found in the 📁[`data`](https://github.com/admacpherson/T-100-Aviation-Data/tree/main/data) folder of this repository. 

## Findings

### Load Factor
File: [`Load Factor Analysis`](https://github.com/admacpherson/T-100-Aviation-Data/blob/main/Load%20Factor%20Analysis.ipynb) | [Jump to Methodology](https://github.com/admacpherson/T-100-Aviation-Data/blob/main/README.md#load-factor-1)<br><br>
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

Looking at the best and worst performing international routes by load factor, we see that the top 3 are Southwest's Punta Cana, DR to Baltimore, American's Chicago O'Hare to San Jose del Cabo, MX, and American's Dallas-Fort Worth to Punta Cana, DR (American and Punta Cana are also #4 on the list). The worst 3 performers were Spirit's Fort Lauderdale to Port-au-Prince, Haiti, United's Nagoya, Japan to Guam, and United's return flight from Guam to Nagoya. While the Port-au-Prince route's worst-in-class performance is understandable due to the recent political instability and violence in Haiti, it seems that United's GUM-NGO route pairing does not have a lot of demand as its load factor is appoximately only 20%. While there may be additional considerations, such as Essential Air Service subsidies or network feed, the LF data seem to suggest the route is not independently commercially viable.

#### Best & Worst Domestic LF by Route & Airline
|Origin|Destination|Airline|LF|
|------|-----------|-------|---|
|BWI|IAH|Spirit|1.004579|
|BDL|CLT|American|0.996449|
|LAS|BUF|Southwest|0.994006|
|...|
|LAX|GJT|SkyWest|0.111765|
|MCW|ORD|SkyWest|0.106667|
|MCW|ORD|SkyWest|0.104211|

The domestic performance of load factor by route highlights some interesting properties in the data. Spirit's Baltimore to Houston route apparently has a load factor of just over 100%. Though Spirit is known for their cramped planes, the load factors should be contrained to the range of 0-100% - it is impossible to have more passengers than seats. What is likely occuring here is overbooking on the behalf of Spirit. Briefly explained, the practice of overbooking refers to selling more seats than are available, knowing that a certain percentage of passengers are likely to miss their flight. While most US airlines no longer practice overbooking, Spirit is a notable exception and seemingly boosts their load factors using this strategy. 

We also see that 2 of the top 3 routes are long-haul point-to-point routes with destinations that are typically more leisure-oriented. Additionally, we see a leisure-oriented destination (Hartford, CT) connecting to American's hub in Charlotte, NC. Though we cannot draw conclusions from a top 3 sample, the high load factors on these routes suggests additional analysis may be merited to discover a correlation between long-haul leisure destinations and load factor, despite the fact that leisure-oriented carriers tend to rank lower than their legacy counterparts in overall network load factor (see below).

At the bottom of the table, we see small airports served by SkyWest, a regional airline that operates smaller planes on behalf of all 3 legacy carriers (American, Delta, and United). These flights are sold and branded as legacy airline flights, but operated by SkyWest. This is likely why we see MCW-ORD show up twice at the bottom of the table, likely once as an American flight operated by SkyWest and once as a United flight operated by SkyWest. Unsurprisingly, each of the bottom 3 pairings are to minor airports (Mason City, IA and Grand Junction, CO) and are likely supported by the Essential Air Service.

#### Best & Worst LF by Route & Airline (All Routes)
|Origin|Destination|Airline|LF|
|------|-----------|-------|---|
|BWI|IAH|Spirit|1.004579|
|BDL|CLT|American|0.996449|
|LAS|BUF|Southwest|0.994006|
|...|
|LAX|GJT|SkyWest|0.111765|
|MCW|ORD|SkyWest|0.106667|
|MCW|ORD|SkyWest|0.104211|

Interestingly, the overall results (unfiltered to include both domestic and international routes) mirrors the domestic table exactly.

#### Overall Load Factor by Carrier
|Carrier|Total LF|Domestic LF|International LF|
|-------|--------|-----------|----------------|
|Delta Air Lines Inc.|0.862686|0.864386|0.854014|
|Allegiant Air|0.859050|0.859196|0.772746|
|Sun Country Airlines d/b/a MN Airlines|0.856746|0.866856|0.793314|
|American Airlines Inc.|0.843187|0.843518|0.841933|
|United Air Lines Inc.|0.840662|0.850916|0.812517|
|Spirit Air Lines|0.822254|0.828956|0.766056|
|Envoy Air|0.821440|0.823591|0.796062|
|JetBlue Airways|0.818494|0.825273|0.801065|
|Alaska Airlines Inc.|0.817015|0.814979|0.847187|
|Hawaiian Airlines Inc.|0.811663|0.817055|0.755141|
|SkyWest Airlines Inc.|0.804319|0.803651|0.822122|
|Republic Airline|0.794361|0.789418|0.845860|
|Southwest Airlines Co.|0.780325|0.778630|0.859099|
|Frontier Airlines Inc.|0.767294|0.770876|0.713395|

Next we analyze the overall load factor each airline had across its entire network, including breakdowns along domestic and international lines. As the table shows, in Q1/Q2 of 2024, Delta had the best load factor performance from an overall perspective as well as in the domestic and international categories. Meanwhile Frontier was the worst performer in all three of these categories, though their domestic performance is only slightly below Southwest, which also underperformed relative to other airlines. Along with Republic Airlines, Southwest and Frontier join to be the only 3 carriers with an overall or domestic load factor below 80%. While the legacy carriers are among the top performers in load factor, 2 ULCCs (Allegiant and Sun Country) boast strong results boosted by domestic LF and surpass American and United to claim the #2 and #3 spots respectively. 

#### Best LF by Origin

|DEST|City|LF|DEPARTURES PERFORMED|
|---|---|---|---|
|PRG|Prague, Czech Republic|0.937301|83|
|ATH|Athens, Greece|0.926690|1017|
|RFD|Rockford, IL|0.912462|253|
|ARN|Stockholm, Sweden|0.905959|136|
|DOH|Doha, Qatar|0.904475|210|

International cities dominate this list, with 4 of the top 5 being long haul international destinations. The notable exception is RFD, a distant suburb of Chicago served exclusively by Allegiant for passenger service.

#### Best Domestic LF by Origin

|DEST|City|LF|DEPARTURES PERFORMED|
|---|---|---|---|
|RFD|Rockford, IL|0.912462|253|
|LNK|Lincoln, NE|0.897701|772|
|ABE|Allentown/Bethlehem/Easton,PA|0.895144|1013|
|STC|St. Cloud, MN|0.895127|40|
|PVU|Provo, UT|0.892846|585|

Exploring now domestic load factor performance, we see that the top 5 destination airports by load factor all appear to be smaller airports with less commercial service. In fact, 4 of the 5 are located in the Midwest. Nonetheless, only 1 destination - Rockford, Illinois, boasts an average load factor above 90%.

#### Best Domestic LF by Destination
|ORIGIN|City|LF|DEPARTURES PERFORMED|
|---|---|---|---|
|PPG|Pago Pago, TT|0.964628|36|
|MFE|Mission/McAllen/Edinburg, TX|0.909346|2081|
|LNK|Lincoln, NE|0.907876|774|
|LCK|Columbus, OH|0.903170|278|
|PVU|Provo, UT|0.901945|591|

Topping the list of domestic load factor by origin is an airport that's hardly in the United States at all. Pago Pago is the capital of American Samoa, an unincorporated territory of the United States in the southern Pacific Ocean. Though the sample size is small, departures from Pago Pago boast an impressive 96.5% load factor. The rest of the list sees some repeats (Lincoln, Provo) and consists again of small airports. Notably, there are two secondary airports in the list. Columbus LCK provides secondary service to Columbus OH, after CMH, and is exclusively served by Allegiant. Meanwhile Provo PVU serves the Greater Salt Lake City region and is served by Breeze, American Eagle (AA's regional service), and Allegiant. Though the sample size is small,  Allegiant's presence at the top of all three lists suggests their strategy of secondary airports correlates strongly with their ability to fill planes.


## Methodologies

### Load Factor
File: [`Load Factor Analysis`](https://github.com/admacpherson/T-100-Aviation-Data/blob/main/Load%20Factor%20Analysis.ipynb) | [Jump to Analysis](https://github.com/admacpherson/T-100-Aviation-Data/blob/main/README.md#load-factor)<br><br>
This analysis focused only on major US carriers as defined by the DOT (carriers with annual revenue >$1B). The data include a classification scheme under the variable `CARRIER_GROUP_NEW`, which, when filtered, provides a list of major airlines, but includes those with cargo flights as well as passenger service. Rather than filtering wholesale by airlines, since many airlines perform both types of service, filtering flight level to include all flights with at least 1 passenger succinctly excludes all cargo-only flights while ensuring no passenger service is excluded.
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
Now, the data do not include a binary variable to distinguish between domestic and international flights. To do so, we must rely on the origin and destination countries, represented as `ORIGIN_COUNTRY_NAME` and `DEST_COUNTRY_NAME`. Since, by definition of the dataset, every flights either starts or ends in the United States, we can define domestic flights as those where both the origin and destination country are both the United States, and international flights as those where exactly one of those is not the United States. 

```python
if dom_only == True:
        df = df[(df['ORIGIN_COUNTRY_NAME'] == 'United States') & (df['DEST_COUNTRY_NAME'] == 'United States')]
    if int_only == True:
        df = df[(df['ORIGIN_COUNTRY_NAME'] != 'United States') | (df['DEST_COUNTRY_NAME'] != 'United States')]
```

We can also add a column to the data that categorizes each flight in the dataset. Here I used an anonymous lambda function to create a new column titled `DOMESTIC`, with a value of either `D` for domestic or `I` for international.

```python
major_passenger_flights['DOMESTIC'] = major_passenger_flights.apply(lambda row: 'D' if row['ORIGIN_COUNTRY_NAME'] == 'United States' and row['DEST_COUNTRY_NAME'] == 'United States' else 'I', axis=1)
```

Finally, with a complete dataset we can analyze routes by airline and load factor. 

Using the previously defined data frames, it is a simple matter to select the applicable data set (domestic/international/all), include the desired columns, and sort by load factor.

```python
# Select and order specified columns for international flights
mpf_int_abbrv = int_flights.loc[:, ['ORIGIN', 'DEST', 'ORIGIN_CITY_NAME', 'DEST_CITY_NAME','CARRIER_NAME', 'DEPARTURES_PERFORMED', 'SEATS', 'PASSENGERS', 'LF', 'DISTANCE']]
# Sort individual carrier routes by load factor
mpf_int_abbrv.sort_values(by='LF', ascending=False)
```

The next task of this analysis was to calculate each airline's overall load factor. If we want to understand this by overall region, the formula is a fairly simple `groupby` aggregation.

```python
seats_by_carrier = major_passenger_flights.groupby(['CARRIER_NAME', 'DOMESTIC']).agg({'SEATS': 'sum', 'PASSENGERS': 'sum'}).reset_index()
```

However, to understand the load factor overall and by the international/domestic breakdown, we need to implement a more complicated pivot methodology:

```python
# Pivot to create separate columns for each region and metric
pivoted_regions = seats_by_carrier.pivot_table(index='CARRIER_NAME', columns='REGION', values=['SEATS', 'PASSENGERS'], fill_value=0)

# Flatten the MultiIndex in columns and rename columns
pivoted_regions.columns = [f'{metric}_{region}' for metric, region in pivoted_regions.columns]

# Reset index to turn CARRIER_NAME back into a column
pivoted_regions = pivoted_regions.reset_index()
```
This leaves us with 4 new columns: `PASSENGERS_D`, `PASSENGERS_I`, `SEATS_D`, and `SEATS_I`.
Combining the pivot and `groupby`/`agg` methodologies, we implement the following:

```python
# Group by CARRIER_NAME and DOMESTIC, then sum SEATS and PASSENGERS
seats_by_carrier = major_passenger_flights.groupby(['CARRIER_NAME', 'DOMESTIC']).agg({
    'SEATS': 'sum',
    'PASSENGERS': 'sum'
}).reset_index()

# Pivot to create separate columns for Domestic and International regions
pivoted_ID_seats_pax = seats_by_carrier.pivot_table(index='CARRIER_NAME', columns='DOMESTIC', values=['SEATS', 'PASSENGERS'], fill_value=0)

# Flatten the MultiIndex in columns and rename columns
pivoted_ID_seats_pax.columns = [f'{metric}_{region}' for metric, region in pivoted_ID_seats_pax.columns]

# Reset index to turn CARRIER_NAME back into a column
pivoted_ID_seats_pax = pivoted_ID_seats_pax.reset_index()
```

It is then a simple matter to add the load factor calculation.

```python
LF_by_carrier = pivoted_ID_seats_pax
LF_by_carrier['Total LF'] = (pivoted_ID_seats_pax['PASSENGERS_D'] + pivoted_ID_seats_pax['PASSENGERS_I']) / (pivoted_ID_seats_pax['SEATS_D'] + pivoted_ID_seats_pax['SEATS_I'])
LF_by_carrier['Domestic LF'] = pivoted_ID_seats_pax['PASSENGERS_D'] / pivoted_ID_seats_pax['SEATS_D']
LF_by_carrier['International LF'] = pivoted_ID_seats_pax['PASSENGERS_I'] / pivoted_ID_seats_pax['SEATS_I']
```

Finally, we select the columns for display and sort by overall load factor in descending order.
```python
LF_by_carrier = LF_by_carrier.loc[:, ['CARRIER_NAME', 'Total LF', 'Domestic LF', 'International LF']]
LF_by_carrier.sort_values(by='Total LF', ascending=False)
````

To compute the top origins and destinations by load factor, we merely need to aggregate on the applicable variables (`SEATS` and `PASSENGERS` to calculate `LF` and `DEPARTURES_PERFORMED` to keep us aware of the sample size)

```python
# Aggregate seats, pax, and departures by origin airport/city name
flights_by_dest = major_passenger_flights.groupby(['DEST', 'DEST_CITY_NAME']).agg({
    'SEATS': 'sum',
    'PASSENGERS': 'sum',
    'DEPARTURES_PERFORMED': 'sum'
    ''
}).reset_index()
```

We can then calculate our familiar load factor formula and sort and select the relevant columns
```python
# Calculate load factor
flights_by_dest['LF'] = flights_by_dest['PASSENGERS'] / flights_by_dest['SEATS']
# Select columns and sort by load factor (highest to lowest)
flights_by_dest.loc[:,['DEST', 'DEST_CITY_NAME', 'LF','DEPARTURES_PERFORMED']].sort_values(by='LF', ascending=False)
```

Repeating this process for domestic flights, simply requires substituting our data frame and selecting `ORIGIN`/`ORIGIN_CITY_NAME` where applicable:

```python
# Repeat analysis with domestic flights
# Aggregate seats, pax, and departures by origin airport/city name
dom_flights_by_origin = dom_flights.groupby(['ORIGIN', 'ORIGIN_CITY_NAME']).agg({
    'SEATS': 'sum',
    'PASSENGERS': 'sum',
    'DEPARTURES_PERFORMED': 'sum'
}).reset_index()
# Calculate load factor
dom_flights_by_origin['LF'] = dom_flights_by_origin['PASSENGERS'] / dom_flights_by_origin['SEATS']
# Select columns and sort by load factor (highest to lowest)
dom_flights_by_origin.loc[:,['ORIGIN', 'ORIGIN_CITY_NAME', 'LF','DEPARTURES_PERFORMED']].sort_values(by='LF', ascending=False)
```

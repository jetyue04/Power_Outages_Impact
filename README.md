# Power_Outages_Impact

### by Jet Yue and Namitha Vishnupad

# Introduction

Hello! Welcome to our analysis of power outages across the United States. The core of this project's data consists of detailed records of major power outages in the United States, which contains information about the causes of these outages, their duration, the number of people/consumers impacted, and various other socio-economic factors related to the impacted regions. 

Power outages are significant events, and can disrupt daily life, impact economic activities, and potentially pose risks to health and safety - especially ones on larger scales.
<br>

<center><img src = "https://i.ytimg.com/vi/eSmUwjGs738/maxresdefault.jpg" width = 500></center>

We aim to answer the question of finding the characteristics of major power outages with high severity, and whay risk factors an energy company might want to look into when predicting the location/severity of its next major power outage.


And we know it is hard to find a single answer to this question. So, we have narrowed our approach to be slightly more specific, with the following research question:

##### Is there a significant difference in the mean outage duration between major power outages caused by severe weather, and major power outages caused by intentional attacks?

This question aims to uncover whether the nature of the cause of the outage - whether it is natural or human induced, affects the duration of the power outage. The answer could potentially influence how resources are allocated for outage prevention, as well as inform strategies for improving the resilience of power infrastructure.


Before we take a look into our project, here is a brief introduction of what the data is!

The working dataset we are using has <b><span style="color:red">**1534 rows**</span></b> and <b><span style="color:blue">**36 columns**</span></b>. 

Shortly put - this is a lot of data 😬. 

For our approach, we have compiled a list of the data we feel is most relevant to our research question -


- OUTAGE.DURATION: Duration of the power outage in minutes.
- CAUSE.CATEGORY: Primary category of the cause of the outage (e.g., severe -weather, intentional attack).
- OUTAGE.START.DATE: Date when the outage started.
- OUTAGE.RESTORATION.DATE: Date when power was restored.
- CUSTOMERS.AFFECTED: Number of customers affected by the outage.
- U.S._STATE: Location of the outage
- CLIMATE.REGION: Climate region of the outage location.
- ANOMALY.LEVEL: Climate anomaly level during the time of the outage.
- RES.SALES, COM.SALES, IND.SALES: Electricity consumption patterns by residential, commercial, and industrial sectors.
- TOTAL.SALES: Total electricity sales in the affected area.
- PC.REALGSP.STATE: Per capita real Gross State Product.
- POPULATION: Population of the affected area.


# Data Cleaning and Exploratory Data Analysis

In the original dataset, there are several rows in the excel sheet encompassing a description of the data. We removed those rows before importing it into our notebook.

Below, we have displayed the first 5 rows of the original dataset
|   variables |   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | OUTAGE.START.DATE   | OUTAGE.START.TIME   | OUTAGE.RESTORATION.DATE   | OUTAGE.RESTORATION.TIME   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   RES.PRICE |   COM.PRICE |   IND.PRICE |   TOTAL.PRICE |   RES.SALES |   COM.SALES |   IND.SALES |   TOTAL.SALES |   RES.PERCEN |   COM.PERCEN |   IND.PERCEN |   RES.CUSTOMERS |   COM.CUSTOMERS |   IND.CUSTOMERS |   TOTAL.CUSTOMERS |   RES.CUST.PCT |   COM.CUST.PCT |   IND.CUST.PCT |   PC.REALGSP.STATE |   PC.REALGSP.USA |   PC.REALGSP.REL |   PC.REALGSP.CHANGE |   UTIL.REALGSP |   TOTAL.REALGSP |   UTIL.CONTRI |   PI.UTIL.OFUSA |   POPULATION |   POPPCT_URBAN |   POPPCT_UC |   POPDEN_URBAN |   POPDEN_UC |   POPDEN_RURAL |   AREAPCT_URBAN |   AREAPCT_UC |   PCT_LAND |   PCT_WATER_TOT |   PCT_WATER_INLAND |
|------------:|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:-------------------|:--------------------|:--------------------|:--------------------------|:--------------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|------------:|------------:|------------:|--------------:|------------:|------------:|------------:|--------------:|-------------:|-------------:|-------------:|----------------:|----------------:|----------------:|------------------:|---------------:|---------------:|---------------:|-------------------:|-----------------:|-----------------:|--------------------:|---------------:|----------------:|--------------:|----------------:|-------------:|---------------:|------------:|---------------:|------------:|---------------:|----------------:|-------------:|-----------:|----------------:|-------------------:|
|         nan |   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | normal             | 2011-07-01 00:00:00 | 17:00:00            | 2011-07-03 00:00:00       | 20:00:00                  | severe weather     | nan                     |               nan |              3060 |              nan |                70000 |       11.6  |        9.18 |        6.81 |          9.28 | 2.33292e+06 | 2.11477e+06 | 2.11329e+06 |   6.56252e+06 |      35.5491 |      32.225  |      32.2024 |         2308736 |          276286 |           10673 |           2595696 |        88.9448 |        10.644  |       0.411181 |              51268 |            47586 |          1.07738 |                 1.6 |           4802 |          274182 |       1.75139 |             2.2 |      5348119 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |
|         nan |   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | 2014-05-11 00:00:00 | 18:38:00            | 2014-05-11 00:00:00       | 18:39:00                  | intentional attack | vandalism               |               nan |                 1 |              nan |                  nan |       12.12 |        9.71 |        6.49 |          9.28 | 1.58699e+06 | 1.80776e+06 | 1.88793e+06 |   5.28423e+06 |      30.0325 |      34.2104 |      35.7276 |         2345860 |          284978 |            9898 |           2640737 |        88.8335 |        10.7916 |       0.37482  |              53499 |            49091 |          1.08979 |                 1.9 |           5226 |          291955 |       1.79    |             2.2 |      5457125 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |
|         nan |   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | cold               | 2010-10-26 00:00:00 | 20:00:00            | 2010-10-28 00:00:00       | 22:00:00                  | severe weather     | heavy wind              |               nan |              3000 |              nan |                70000 |       10.87 |        8.19 |        6.07 |          8.15 | 1.46729e+06 | 1.80168e+06 | 1.9513e+06  |   5.22212e+06 |      28.0977 |      34.501  |      37.366  |         2300291 |          276463 |           10150 |           2586905 |        88.9206 |        10.687  |       0.392361 |              50447 |            47287 |          1.06683 |                 2.7 |           4571 |          267895 |       1.70627 |             2.1 |      5310903 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |
|         nan |   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | 2012-06-19 00:00:00 | 04:30:00            | 2012-06-20 00:00:00       | 23:00:00                  | severe weather     | thunderstorm            |               nan |              2550 |              nan |                68200 |       11.79 |        9.25 |        6.71 |          9.19 | 1.85152e+06 | 1.94117e+06 | 1.99303e+06 |   5.78706e+06 |      31.9941 |      33.5433 |      34.4393 |         2317336 |          278466 |           11010 |           2606813 |        88.8954 |        10.6822 |       0.422355 |              51598 |            48156 |          1.07148 |                 0.6 |           5364 |          277627 |       1.93209 |             2.2 |      5380443 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |
|         nan |   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | warm               | 2015-07-18 00:00:00 | 02:00:00            | 2015-07-19 00:00:00       | 07:00:00                  | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |       13.07 |       10.16 |        7.74 |         10.43 | 2.02888e+06 | 2.16161e+06 | 1.77794e+06 |   5.97034e+06 |      33.9826 |      36.2059 |      29.7795 |         2374674 |          289044 |            9812 |           2673531 |        88.8216 |        10.8113 |       0.367005 |              54431 |            49844 |          1.09203 |                 1.7 |           4873 |          292023 |       1.6687  |             2.2 |      5489594 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |


As you can see, there is a lot of missing data, and it's not the most interpretable data. So with data cleaning, here are the changes we made -

1. Then, we combined the 'OUTAGE.START.DATE' and 'OUTAGE.START.TIME' columns into a single string for each row, handling missing values by replacing them with empty strings.
2. We then converted the combined date-time strings into datetime objects, coercing invalid entries to NaT values (Not a Time)
3. Only take out columns we are interested in
4. Check for unreasonable values:
    - Duration, Demand Loss and Customer affected should not be 0
    - all other columns's value are checked
    - REPLACE WITH NAN VALUES


In summation: The data cleaning steps transformed raw data into a structured and analyzable format. By filling missing values, combining date and time columns, calculating outage durations, and standardizing categorical data, we ensured that the dataset is ready for meaningful analysis. These steps were essential for achieving accurate and reliable insights into the characteristics and severity of major power outages, ultimately aiding in the identification of risk factors for future outages.

#### The first 5 rows of our cleaned data:

|   YEAR |   MONTH | POSTAL.CODE   | U.S._STATE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | OUTAGE.START        | OUTAGE.RESTORATION   |   OUTAGE.DURATION | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   TOTAL.PRICE |   TOTAL.SALES |   POPPCT_URBAN |   POPDEN_URBAN |   AREAPCT_URBAN |   AVG_DURATION_PER_STATE |
|-------:|--------:|:--------------|:-------------|:--------------|:-------------------|----------------:|:--------------------|:---------------------|------------------:|:-------------------|:------------------------|-----------------:|---------------------:|--------------:|--------------:|---------------:|---------------:|----------------:|-------------------------:|
|   2011 |       7 | MN            | Minnesota    | MRO           | East North Central |            -0.3 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |              3060 | severe weather     | nan                     |              nan |                70000 |          9.28 |   6.56252e+06 |          73.27 |           2279 |            2.14 |                     2760 |
|   2014 |       5 | MN            | Minnesota    | MRO           | East North Central |            -0.1 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |                 1 | intentional attack | vandalism               |              nan |                  nan |          9.28 |   5.28423e+06 |          73.27 |           2279 |            2.14 |                     2760 |
|   2010 |      10 | MN            | Minnesota    | MRO           | East North Central |            -1.5 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |              3000 | severe weather     | heavy wind              |              nan |                70000 |          8.15 |   5.22212e+06 |          73.27 |           2279 |            2.14 |                     2760 |
|   2012 |       6 | MN            | Minnesota    | MRO           | East North Central |            -0.1 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |              2550 | severe weather     | thunderstorm            |              nan |                68200 |          9.19 |   5.78706e+06 |          73.27 |           2279 |            2.14 |                     2760 |
|   2015 |       7 | MN            | Minnesota    | MRO           | East North Central |             1.2 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |              1740 | severe weather     | nan                     |              250 |               250000 |         10.43 |   5.97034e+06 |          73.27 |           2279 |            2.14 |                     2760 |
​


#### Univariate Analysis
For our univariate analysis, we explored the following plots 

<insert data>

#### Bivariate Analysis

For our bivariate analysis, we used a box plot to explore the differences in outage duration caused be different categories. Our choice of picking was between severe weather and intentional attacks, which we have pictured below <inset boxplot>. We see that with severe weather, there appears to be longer outages, both with a higher mean and a greater spread of durations, while intentional attacks tend to have shorter durations and fewer outliers.

We explored a couple more plots for our bivariate analysis, but one of utmost interest to us was to pictographically visualize average power outages across the United States, which we did through a geomap (pictured below). We used median power outages to get a general understanding of the distribution across states in the USA.

<insert geomap>



### Interesting Aggregates
The following pivot table is a breakdown of the average outage duration by different cause categories in different climate regions. It gives  some insight into the power grids across the country, and helps identify what cause category is most significant per climate region

|    | CLIMATE.REGION     |   equipment failure |   fuel supply emergency |   intentional attack |   islanding |   public appeal |   severe weather |   system operability disruption |
|---:|:-------------------|--------------------:|------------------------:|---------------------:|------------:|----------------:|-----------------:|--------------------------------:|
|  0 | Central            |             322     |                 10035.2 |              490.25  |    125.333  |         1410    |          3299.63 |                        2695.2   |
|  1 | East North Central |           26435.3   |                 33971.2 |             2501.11  |      1      |          733    |          4434.82 |                        2610     |
|  2 | Northeast          |             269.75  |                 14629.6 |              264.68  |    881      |         2655    |          4429.9  |                         773.5   |
|  3 | Northwest          |             702     |                     1   |              488.831 |     73.3333 |          898    |          4838    |                         141     |
|  4 | South              |             295.778 |                 17482.5 |              337.667 |    493.5    |         1163.98 |          4391.35 |                         899.385 |
|  5 | Southeast          |             554.5   |                   nan   |              504.667 |    nan      |         2865.4  |          2685.71 |                         180.6   |
|  6 | Southwest          |             113.8   |                    76   |              274.678 |      2      |         2275    |         11572.9  |                         370.375 |
|  7 | West               |             524.81  |                  6154.6 |              886.267 |    214.857  |         2028.11 |          2928.37 |                         363.667 |
|  8 | West North Central |              61     |                   nan   |               47     |     68.2    |          439.5  |          2442.5  |                         nan     |


# Assessment of Missingness 

### NMAR Analysis (TO-DO)


### Missingness Dependency


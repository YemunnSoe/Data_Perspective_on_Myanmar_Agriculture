# Background

In this project, I will utilize data that has been collected for the agriculture sector in Myanmar up until 2016, specifically focusing on the agricultural landscape prior to the occurrence of both the political coup and the COVID-19 pandemic. [(Source: MIMU)](https://themimu.info/5w-maps-and-reports)

2015-2016, economic growth in Myanmar eased to 7 percent amid a supply shock from heavy flooding, a slowdown in new investment flows during an election year, and a more challenging external environment including lower commodity prices affecting Myanmar’s main exports. Agriculture growth decelerated to 2 percent in 2015-2016 compared to 5.6 percent the previous year due to the impact of heavy rains between July and September 2015 causing widespread flooding and landslides. The sector contributed less than 10 percent of overall growth. Although the floods were geographically widespread, major agricultural producing areas were particularly badly hit. Damages from the disaster affected storage facilities with stocks of seeds; animals and livestock; aquaculture facilities and fisheries’ ponds; and fishing equipment. Losses were generated from lower crop production, reduced output of meat and eggs, and contraction in fisheries’ production.

These in turn had knock on effects beyond agriculture in food processing, trading, and transportation services. A combination of all this will have negatively affected household incomes and food inscurity .[(Source: World Bank, Myanmar Economic Monitor May 2016)](https://bit.ly/3BGLvJQ)


![](./Diagrams/1_System_Architecture.png)

> The objective of this project is to utilize existing data to develop an engaging and comprehensive interactive report. The primary focus of this dashboard is the agricultural sector, as it seeks to leverage data to explore different (my) perspectives and approaches. The aim is to create visually compelling and informative representations that offer valuable insights and a glimpse into Myanmar's agriculture sector before the occurrence of the coup and the COVID-19 pandemic.

![](./Diagrams/2_System_Architecture.png)

# Project Deliverables
- National Sector, Sub-sectors Description [(See More)](https://bit.ly/41ZTrAu)
- My Dashboard: Myanmar Agriculture Landscape (2016) [(Click HERE)](https://bit.ly/45gkCK9)
- Ref: MIMU 5W Overview Dashboard [(See More)](https://themimu.info/5w-overview-dashboard)
- Ref: MIMU 5W Village Tract Dashboard [(See More)](https://themimu.info/5W_Dashboard_by_Village_Tract)
- Ref: MIMU Datasets [(See More)](https://themimu.info/baseline-datasets)


### Analytical Approach

![](./Diagrams/Prescriptive_Analytics.png)


# Data modelling
I use pre-aggregated data for this portfolio project. It helps me reduce the amount of data and sensitive information that needs to be processed for analyses or reporting. It involves summarizing or grouping data at a higher level of granularity, such as by week or month, instead of processing every individual record. I use THREE pre-aggregation methods:

Summarizing data by time intervals (daily basics)
Aggregating data by categories (less granularity in dimension data)
Filtering data to exclude irrelevant records (omit sensitive information)

[](./Diagrams/1_Data_Model.png)

### DAX used in this SAMPLE Dashboard

```
CAGR Agri Project 2014-16 = 
VAR Lastyear = 2016
VAR Firstyear = 2014
VAR No_of_Years = 3

VAR Numerator = CALCULATE(SUM('3W'[2016 - Agriculture]))
VAR Denominator = CALCULATE(SUM('3W'[2014 - Agriculture]))

RETURN
    IF(
        ISBLANK(Numerator) || ISBLANK(Denominator),
        BLANK(),
        POWER(DIVIDE(Numerator, Denominator), 1 / No_of_Years) - 1
    )
```
```
Cultivated Land (%) =
IF (
    HASONEVALUE ( Slicer[Crop] ),
    SWITCH (
        VALUES ( Slicer[Slicer Value] ),
        1, SUM ( 'Agriculture-crops'[Harvested Area of Paddy (acres)] ) / SUM ( 'Satellite - Cultivated Land'[Cultivated area (acre)] ),
        2, SUM ( 'Agriculture-crops'[Harvested Area of Cotton (acres)] ) / SUM ( 'Satellite - Cultivated Land'[Cultivated area (acre)] ),
        3, SUM ( 'Agriculture-crops'[Harvested Area of Green Gram (acres)] ) / SUM ( 'Satellite - Cultivated Land'[Cultivated area (acre)] ),
        4, SUM ( 'Agriculture-crops'[Harvested Area of Ground-nut (acres)] ) / SUM ( 'Satellite - Cultivated Land'[Cultivated area (acre)] ),
        5, SUM ( 'Agriculture-crops'[Harvested Area of Maize (acres)] ) / SUM ( 'Satellite - Cultivated Land'[Cultivated area (acre)] ),
        6, SUM ( 'Agriculture-crops'[Harvested Area of Pigeon Pea (acres)] ) / SUM ( 'Satellite - Cultivated Land'[Cultivated area (acre)] ),
        7, SUM ( 'Agriculture-crops'[Harvested Area of Sesame (acres)] ) / SUM ( 'Satellite - Cultivated Land'[Cultivated area (acre)] ),
        8, SUM ( 'Agriculture-crops'[Harvested Area of Sugar-cane (acres)] ) / SUM ( 'Satellite - Cultivated Land'[Cultivated area (acre)] ),
        9, SUM ( 'Agriculture-crops'[Harvested Area of Sun Flower (acres)] ) / SUM ( 'Satellite - Cultivated Land'[Cultivated area (acre)] ),
        10, SUM ( 'Agriculture-crops'[Harvested Area of Urad Pea (acres)] ) / SUM ( 'Satellite - Cultivated Land'[Cultivated area (acre)] ),
        [Total Harvested Area (Acres)] / SUM ( 'Satellite - Cultivated Land'[Cultivated area (acre)] )
    ),
    [Total Harvested Area (Acres)] / SUM ( 'Satellite - Cultivated Land'[Cultivated area (acre)] )
)

```
```
Harvested Acreage =
VAR SelectedCrop =
    VALUES ( Slicer[Slicer Value] )
RETURN
    IF (
        HASONEVALUE ( Slicer[Crop] ),
        SWITCH (
            TRUE (),
            SelectedCrop = 1, SUM ( 'Agriculture-crops'[Harvested Area of Paddy (acres)] ),
            SelectedCrop = 2, SUM ( 'Agriculture-crops'[Harvested Area of Cotton (acres)] ),
            SelectedCrop = 3, SUM ( 'Agriculture-crops'[Harvested Area of Green Gram (acres)] ),
            SelectedCrop = 4, SUM ( 'Agriculture-crops'[Harvested Area of Ground-nut (acres)] ),
            SelectedCrop = 5, SUM ( 'Agriculture-crops'[Harvested Area of Maize (acres)] ),
            SelectedCrop = 6, SUM ( 'Agriculture-crops'[Harvested Area of Pigeon Pea (acres)] ),
            SelectedCrop = 7, SUM ( 'Agriculture-crops'[Harvested Area of Sesame (acres)] ),
            SelectedCrop = 8, SUM ( 'Agriculture-crops'[Harvested Area of Sugar-cane (acres)] ),
            SelectedCrop = 9, SUM ( 'Agriculture-crops'[Harvested Area of Sun Flower (acres)] ),
            SelectedCrop = 10, SUM ( 'Agriculture-crops'[Harvested Area of Urad Pea (acres)] ),
            [Total Harvested Area (Acres)]
        )
    )
```
# Dashboard [(See More)](https://bit.ly/45gkCK9)
![](./Diagrams/1_Dashboard.png)
> This comprehensive overview tab offers valuable insights into the seasonal trends of farming practices, empowering users to effortlessly switch between key metrics. This functionality enables the flexibility to adapt and optimize chat flow and digital campaign strategies, ensuring effective customer reach and engagement.

![](./Diagrams/2_Dashboard.png)
> Within this tab, you will find a comprehensive and detailed analysis of the geographical coverage achieved by our campaign across the entire country. This section also presents an insightful examination of the various types of crops and farming practices that our customers have actively engaged in. It offers a deep and thorough exploration of the performance and effectiveness of AgronomyBot in addressing the challenges faced by farmers. These proactive measures aim to mitigate the occurrence of farming disasters and promote sustainable agricultural practices.

![](./Diagrams/3_Dashboard.png)
> This dashboard section delves into the customer journey (or) funnel, with a specific emphasis on key metrics that provide a deeper understanding of the customer journey, operational efficiency, OPEX, and enables the team to make informed decisions during campaign periods. Moreover, leveraging this knowledge allows us to run prescriptive analysis for setting campaign targets in the upcoming fiscal year.

Since early 2020, Myanmar has faced a series of crises that have had a profound impact on its economy and its people, especially those living in poverty. The country has had to grapple with the COVID-19 pandemic, political and economic unrest following the military coup in February 2021, as well as disruptions in global commodity markets due to the war in Ukraine. These successive crises have taken a significant toll on various sectors, particularly the agri-food industry. Under the successive crises, the agri-food sector has been severely impacted,with huge implications for food and economic security, particularly for the large number of poor people living in rural areas. One the one hand, reduced incomes and higher prices are adversely affecting consumption and food security. On the other hand, rising input prices, especially for fertilizer and fuel, is disrupting agriculture production; many farmers have reduced the use of critical inputs, and in some cases, they are reducing cultivated area. Overall, the agriculture sector contracted by around 10 percent in FY 2021 (World Bank 2021b). It is estimated that paddy area planted in 2021–22 is 7 percent below the average of the past 3 years.".[(Read More About THIS)](https://bit.ly/3LUldK4)
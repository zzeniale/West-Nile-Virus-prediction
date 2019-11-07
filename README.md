### Project 4 - West Nile Virus Prediction
---
    Chenyze | Elaine | Kenrick | Raphael
    
---

West Nile virus (WNV) is the leading mosquito-borne disease in the United States ([CDC, 2009](https://www.cdc.gov/westnile/index.html)). It is a single-stranded RNA virus from the family Flaviviridae, which also contains the Zika, dengue, and yellow fever virus. It is primarily transmitted by mosquitoes (mainly <i>Culex</i> spp.), which become infected when they feed on birds, WNV's primary hosts. Infected mosquitos then spread WNV to people and another animals by biting them. Cases of WNV occur during mosquito season, which starts in the summer and continues through fall ([CDC, 2009](https://www.cdc.gov/westnile/index.html)). 

While WNV is not extremely virulent and only about 1 in 5 people who are infected develop West Nile fever and other symptoms, about 1 out of every 150 infected develop a serious and sometimes fatal illness ([CDC, 2009](https://www.cdc.gov/westnile/index.html)). There is currently no vaccine against WNV.

In view of the recent outbreak of WNV in Chicago, the Chicago Department of Public Health (CDPH) has set up a surveillance and control system to trap mosquitos and test for the presence of WNV. The goal of this project is to use these surveillance data to predict the occurrence of WNV given time, location, and mosquito species. Findings from this project will guide and inform decisions on where and when to deploy pesticides throughout the city, to maximise pesticide effectiveness and minimise spending.

#### Folder Organisation:
---
    |__ code
    |   |__ 01_eda_and_feature_engineering.ipynb   
    |   |__ 02_model_tuning_and_insights.ipynb     
    |__ data
    |   |__ train.csv
    |   |__ test.csv
    |   |__ train_processed.csv
    |   |__ test_processed.csv
    |   |__ weather.csv
    |   |__ spray.csv
    |   |__ mapdata_copyright_openstreetmap_contributors.txt
    |__ images
    |   |__ heatmaps.png
    |   |__ species_count.png
    |   |__ wnv_by_year.png
    |   |__ wnv_distribution.png
    |__ planning_documentation.xlsx
    |__ presentation.ppt
    |__ README.md


#### Summary of Findings & Recommendations
---
<img src="./images/heatmaps.png" width=600 align = center>

<p style="font-size:7px; color:grey;" align='center'>(Occurrences of WNV and mosquito spraying efforts in Chicago from May - Sept in 2007, 2009, 2011, and 2013.)</p>

Using XGBoost (our best performing model), we achieved an ROC_AUC of **0.839** and the following confusion matrix:

|predicted WNV absent|predicted WNV present|
|---|---|---|
|actual WNV absent|2045|444|
|actual WNV present|54|84|

Using the model, we found that WNV is more prevalent under certain conditions. **Week of year** was the top predictor by far for our model, followed by day of year, 10-days rolling sum of daylight hours, <i>Culex restuans</i>, and 10-days rolling mean of average temperature. This means that WNV is most likely to occur during certain weeks of the year (in August), and therefore spray efforts should be concentrated during this period. Location was not a strong predictor in our model, suggesting that WNV clusters may be transient, occurring where best conditions emerge. 

After conducting a cost-benefit analysis, we found that the money saved from reducing WNV cases would at most fund about 300 - 500 sprays. However, as the current datasets do not substantially point to a significant impact from spraying, more evidence (from a better designed spraying regime) are needed for a more concrete recommendation. For example, spraying efforts could be concentrated at the beginning of August so that there would be enough time to observe if mosquito numbers decline, in the relative absence of other confounding factors (such as temperature). 


#### Data Dictionary
---

|Feature|Type|Dataset|Description|
|---|---|---|---|
|Id            |int      |train.csv/test.csv |ID number of the record
|Date           |datetime      |train.csv/test.csv |date the WNV test is performed
|Address      |datetime |train.csv/test.csv| approximate trap address; sent to GeoCoder
|Species         |str      |train.csv/test.csv| mosquito species in trap
|Block         |str      |train.csv/test.csv| block number of address
|Street        |str      |train.csv/test.csv| street of address
|Trap          |str    |train.csv/test.csv| ID number of the trap
|AddressNumberAndStreet|str|train.csv/test.csv| approximate address retrieved from GeoCoder
|Latitude            |float|train.csv/test.csv| latitude retrieved from GeoCoder
|Longitude            |float|train.csv/test.csv| longitude retrieved from GeoCoder
|AddressAccuracy      |int|train.csv/test.csv| accuracy of information returned from GeoCoder
|NumMosquitos        |int      |train.csv/test.csv| number of mosquitoes in a sample
|WnvPresent           |int      |train.csv/test.csv| whether or not WNV is present in a sample (1 = present; 0 = absent)
|Date |datetime |spray.csv| date of spray
|Time         |datetime      |spray.csv| time of spray
|Latitude|float|spray.csv| latitude of spray
|Longitude        |float|spray.csv| longitude of spray
|Station  |int|weather.csv| weather station (1 or 2)
|Date     |datetime|weather.csv| date of measurement
|Tmax     |int|weather.csv| maximum daily temperature (F)
|Tmin     |int|weather.csv| minimum daily temperature (F)
|Tavg  |int|weather.csv| average daily temperature (F)
|Depart     |int|weather.csv| departure from normal temperature (F)
|Dewpoint    |int|weather.csv| average dewpoint (F)
|WetBulb  |int|weather.csv| average wet bulb
|Heat     |int|weather.csv| heating degree days
|Cool  |int|weather.csv| cooling degree days
|Sunrise     |int|weather.csv| time of sunrise (calculated)
|Sunset     |int|weather.csv| time of sunset (calculated)
|CodeSum     |str|weather.csv| code of weather phenomena 
|Depth     |int|weather.csv| unknown
|Water1  |int|weather.csv| unknown
|SnowFall     |int|weather.csv| snowfall (inch)
|PrecipTotal     |str|intweather.csv| total daily rainfall (inch)
|StnPressure     |int|weather.csv| average atmospheric pressure (inch Hg)
|SeaLevel     |int|weather.csv| average sea level pressure (inch Hg)
|ResultSpeed  |float|weather.csv| resultant wind speed (mph)
|ResultDir     |int|weather.csv| resultant wind direction (degrees)
|AvgSpeed     |int|weather.csv| average wind speed (mph)



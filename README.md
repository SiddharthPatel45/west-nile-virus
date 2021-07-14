# West Nile Virus Analysis

Project 4 of General Assembly Data Science Immersive done in a group in July 2021.

## Overview
West Nile Virus(WNV) is most commonly spread to humans through infected mosquitos. Around 20% of people who become infected with the virus develop symptoms ranging from persistent fever to serious neurological illnesses that can result in death. In 2002, the first human cases of WNV were reported in Chicago. By 2004 the City of Chicago and the Chicago Department of Public Health (CDPH) had established a comprehensive surveillance and control program that is still in effect today.

Every week from late spring through the fall, mosquitos in traps across the city are tested for the virus. The results of these tests influence when and where the city will spray airborne pesticides to control adult mosquito populations.

Project based on: https://www.kaggle.com/c/predict-west-nile-virus/overview

### Problem Statement

**Due to the recent epidemic of West Nile Virus in the Windy City, the data science team at Disease And Treatment Agency was tasked to derive an effective plan to deploy pesticides throughout the city. Using various weather conditions, locations, spray attempt and infected mosquitos, we will be using various classification models to obtain the best model that can predict the WNV in Chicago. Test set with the highest ROC AUC score would be used as the final model. Evaluation and cost-benefit analysis would be conducted to see if benefit of spraying outweighs the cost of spraying.**

---

## Executive Summary

## Data Dictionary
Train and Test dataset:
|Feature|Description|
|---|---|
|Id| the id of the record|
|Date| date that the WNV test is performed |
|Address| approximate address of the location of trap. This is used to send to the GeoCoder |
|Species| the species of mosquitos|
|Block| block number of address|
|Street| street name|
|Trap| id of the trap|
|AddressNumberAndStreet|approximate address returned from GeoCoder|
|Latitude, Longitude| latitude and longitude returned from GeoCoder|
|AddressAccuracy| accuracy returned from GeoCoder|
|NumMosquitos| number of mosquitoes caught in this trap|
|WnvPresent| presence of West Nile Virus in these mosquitos. 1 means WNV is present, and 0 means not present|

Spray dataset:
|Feature|Description|
|---|---|
|Date| date that the spray was performed|
|Time| time that the spray was performed |
|Latitude| latitude of area that was sprayed |
|Longitude| longitude of area that was sprayed |

Weather dataset:
|Feature|Description|
|---|---|
|Station| place where weather dataset was collected at|
|Date| time that the weather data was collected |
|Tmax| maximum temperature (degree fahrenheit) |
|Tmin| minimun temperature (degree fahrenheit) |
|Tavg| average temperature (degree fahrenheit) |
|Depart| departure from normal (degree fahrenheit) |
|DewPoint| average dew point (degree fahrenheit) |
|WetBulb| average wet bulb (degree fahrenheit) |
|Heat| heating day (base = 65 F)|
|Cool| cooling day (base = 65 F) |
|Sunrise| time of sunrise (24-hour)|
|Sunset| time of sunset (24-hour)|
|CodeSum| weather phenomena |
|Depth| depth of snow (inches) |
|Water1| snow/ice of water equivalent (1800 UTC) |
|SnowFall| snowfall (inches) |
|PrecipTotal| total precipitation (inches) |
|StnPressure| average station pressure (HG) |
|SeaLevel| average sea level pressure (HG) |
|ResultSpeed| resultant wind speed (miles per hour) |
|ResultDir| resultant direction of wind speed (degrees) |
|AvgSpeed| average speed of wind (miles per hour) |


combined_cleaned dataset (train + weather):
|Feature|Description|
|---|---|
|date| date of data observation |
|latitude| latitude returned from GeoCoder |
|longitude| longitude returned from GeoCoder |
|wnv_present| presence of West Nile Virus in these mosquitos. 1 means WNV is present, and 0 means not present|
|species_ohe| 0 - All other species, 1 - Culex Restuans, 2 - Culex Pipiens/Restuans, 3 - Culex Pipiens |
|tmax| maximum temperature (degree fahrenheit) |
|tmin| minimun temperature (degree fahrenheit) |
|tavg| average temperature (degree fahrenheit) |
|depart| departure from normal (degree fahrenheit) |
|dew_point| average dew point (degree fahrenheit) |
|wet_bulb| average wet bulb (degree fahrenheit) |
|heat| heating day (base = 65 F)|
|cool| cooling day (base = 65 F) |
|precip_total| total precipitation (inches) |
|stn_pressure| average station pressure (HG) |
|sea_level| average sea level pressure (HG) |
|result_speed| resultant wind speed (miles per hour) |
|result_dir| resultant direction of wind speed (degrees) |
|avg_speed| average speed of wind (miles per hour) |
|daylight| average speed of wind (miles per hour) |
|bc| patches weather type |
|br| mist weather type |
|dz| drizzle weather type |
|fg| fog weather type |
|fg+| heavy fog weather type |
|fu| smoke weather type |
|gr| hail weather type |
|hz| haze weather type |
|mi| shallow weather type |
|ra| rain weather type |
|sn| snow weather type |
|sq| squall weather type |
|ts| thunderstorm weather type |
|vc| vicinity weather type |
|year| year of data observation |
|month| month of data observation |
|week| week of data observation |
|day| day of data observation |

The project planning document can be found [here](https://docs.google.com/spreadsheets/d/1r5826I6BlhGzuFMtSM7oJ68pLHUEUJlhdhEZntUghWI/edit#gid=1386834576).

## Conclusion and Recommendations

### Contents

The contents of this notebook are as follows:

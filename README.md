# West Nile Virus Analysis

Project 4 of General Assembly Data Science Immersive done in a group in July 2021.

## Introduction

West Nile Virus (WNV) is most commonly spread to humans through infected mosquitos. Around 20% of people who become infected with the virus develop symptoms ranging from persistent fever to serious neurological illnesses that can result in death. In 2002, the first human cases of WNV were reported in Chicago. By 2004 the City of Chicago and the Chicago Department of Public Health (CDPH) had established a comprehensive surveillance and control program that is still in effect today.

Every week from late spring through the fall, mosquitos in traps across the city are tested for the virus. The results of these tests influence when and where the city will spray airborne pesticides to control adult mosquito populations.

Project based on: https://www.kaggle.com/c/predict-west-nile-virus/overview


### Problem Statement

**Due to the recent epidemic of West Nile Virus in the Windy City, the data science team at Disease And Treatment Agency was tasked to derive an effective plan to spray pesticides throughout the city.

Using various weather conditions and time lags, we will be analysing classification models to obtain the best model that can predict the presence of WNV in Chicago, which the department can use to plan spray.

---

### Executive Summary

The purpose of this project is to identify key areas in the city that are prone to virus and provide solutions to current problems and future prevention measures. The dataset is made available throught the kaggle competition, and using the years 2007, 2009, 2011 and 2013, we are asked to predict the presence of the virus for years 2008, 2010, 2012 and 2014. Additionally, we are given weather and some spray data.

The training data has two columns that the test does not, which can be our potential target variables $-$ _NumMosquitos and WnvPresent_. It also contains the coordinates for the traps and species of mosquitos in the trap. There are a number of traps placed across the city which trap mosquitoes to determine if the area has West Nile Virus or not. However, we found these traps to be inconsistently placed throughout the years and there is no benchmark as to how many mosquitos a trap is supposed to capture. Additionally our research showed other weather conditions that can affect the breeding and lifecycle of mosquitos, such as relative humidity and amount of daylight, which were some of the features we engineered.

From our exploratory data analysis, we observed that the WNV was promininetly found in 3 species, 'Culex Pipiens', 'Culex Pipiens/Restuans' and 'Culex Restuans', and mostly in 'Culex Pipiens/Restuans'.

As this is a a binary classification problem, we used a myriad of models such as Logistic Regression, tree based models like Extra Trees and Random Forest, and boosted models like AdaBoost and XGBoost classifiers and picked our best model based on the highest 'ROC-AUC' score obtained on the validation set to predict the test set. Our best model was the XGBoost model with an 'ROC-AUC' score of 0.75 on the validation set and 0.695 as our kaggle score.

The most common metric for classification problems is accuracy. But some times, accuracy can give a fake sense of success, especially when measured on highly unbalanced classes like in this project. Thus, we can look at other widely used metric, ROC-AUC, which can give us more information because it plots true positive rate vs false positive rate. Intuitively, it explains how good the model is at separating the two classes. In this project, it is crucial to reduce the number of observations that are predicted to not have the virus when they actually have. To maximise the help we can provide to the city authorities, it is imperative that we don't miss many sites which might have the virus.

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


combined_cleaned dataset (train + weather) & test_cleaned (test + weather):
|Feature|Description|
|---|---|
|date| date of data observation |
|latitude| latitude returned from GeoCoder |
|longitude| longitude returned from GeoCoder |
|wnv_present | presence of West Nile Virus in these mosquitos. 1 means WNV is present, and 0 means not present|
|species_label_1.0| CULEX PIPIENS/RESTUANS |
|species_label_2.0| CULEX PIPIENS |
|species_label_3.0| Other mosquito species |
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
|daylight| length of daylight (mins) |
|r_humid| measure of the water vapor content of air (%) |
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
|tavg_10, tavg_14, tavg_28| avg temperature (10, 14, 28 lag days) |
|precip_total_10, precip_total_14, precip_total_28| precipitation (10, 14, 28 lag days) |
|r_humid_10, r_humid_14, r_humid_28| relative humidity (10, 14, 28 lag days) |
|week| week of data observation |


The project planning document can be found [here](https://docs.google.com/spreadsheets/d/1r5826I6BlhGzuFMtSM7oJ68pLHUEUJlhdhEZntUghWI/edit#gid=1386834576).

## Conclusion and Recommendations

In summary, we were tasked to create a best model that can predict the WNV. From our data cleaning, EDA and feature engineering processes, we established the best features that can help us to best predict WNV. We also explored some feature interactions and feature rolling values from the past, based on research.

The best model is the XGBoost Classifier that churned out the highest validation ROC AUC scores and a score of 0.695 on kaggle on the test dataset. Although it has a low recall, it was a better model over the Bagging Classifier model as it allows us to look at the important features that best predict the WNV and aid us in our cost benefit analysis and providing recommendations to reduce the impact of the virus.

Spraying could not be definitively proven to be useful or not from the EDA, based on the data alone as not enough information is available for it. But, as our CBA suggests that the investments in spraying could be better used in other places, so we can recommend that the city department look at the other means like, campaigning and spreading awareness among its people. Since past weather is a major factor, other ways can be looked at to prevent the rise of mosquito population and thus the spread of the WNV.

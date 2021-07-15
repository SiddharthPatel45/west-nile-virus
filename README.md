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
|year| year of data observation |
|month| month of data observation |
|week| week of data observation |
|day| day of data observation |

The project planning document can be found [here](https://docs.google.com/spreadsheets/d/1r5826I6BlhGzuFMtSM7oJ68pLHUEUJlhdhEZntUghWI/edit#gid=1386834576).

## Conclusions and Recommendations

The XGBoost Classifier performed the best among all the variety of models tried, in terms of ROC-AUC score. As mentioned before, this score is a good predictor of how well the model is able to separate the two classes. However, using XGBoost is quite resource intensive, and similar results can be obtained using other models like Random Forest and AdaBoost at significantly faster rate. Some of the weather parameters suspected to be useful in predicting the presence of WNV turned out to be quite strong predictors for the different models, like the average temperature, location, precipitation, year and month. The latter two shows that there is a seasonality in the occurence of virus and relevant steps can be taken in advance to stop the spread of the virus.

Although no significant evidence was found for spray data and its effect on controlling the mosquito population, it is recommended that the city authorities conduct regular sprays across the city when the "virus season" arrives. The benefits of spray inhibiting the mosquito population far outweigh the costs of not doing it. Since past weather is a major factor, other ways can be looked at to prevent the rise of mosquito population and thus the spread of the WNV.

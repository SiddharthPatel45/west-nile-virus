# West Nile Virus Analysis

Project 4 of General Assembly Data Science Immersive done in a group in July 2021.

## Overview
West Nile Virus(WNV) is most commonly spread to humans through infected mosquitos. Around 20% of people who become infected with the virus develop symptoms ranging from persistent fever to serious neurological illnesses that can result in death. In 2002, the first human cases of WNV were reported in Chicago. By 2004 the City of Chicago and the Chicago Department of Public Health (CDPH) had established a comprehensive surveillance and control program that is still in effect today.

Every week from late spring through the fall, mosquitos in traps across the city are tested for the virus. The results of these tests influence when and where the city will spray airborne pesticides to control adult mosquito populations.

Project: https://www.kaggle.com/c/predict-west-nile-virus/overview
### Problem Statement

**Due to the recent epidemic of West Nile Virus in the Windy City, the data science team at Disease And Treatment Agency was tasked to derive an effective plan to deploy pesticides throughout the city. Using various weather conditions, locations, spray attempt and infected mosquitos, we will be using various classification models to obtain the best model that can predict the WNV in Chicago. Test set with the highest ROC AUC score would be used as the final model. Evaluation and cost-benefit analysis would be conducted to see if benefit of spraying outweighs the cost of spraying.**

---

## Executive Summary

## Data Dictionary
|Feature|Description of train and test dataset|
|---|---|
|Id| the id of the record|
|Date| date that the WNV test is performed|
|Address| approximate address of the location of trap. This is used to send to the GeoCoder |
|Species| the species of mosquitos|
|Block| block number of address|
|Street| street name|
|Trap| Id of the trap|
|AddressNumberAndStreet|approximate address returned from GeoCoder|
|Latitude, Longitude| Latitude and Longitude returned from GeoCoder|
|AddressAccuracy| accuracy returned from GeoCoder|
|NumMosquitos| number of mosquitoes caught in this trap|
|WnvPresent|whether West Nile Virus was present in these mosquitos. 1 means WNV is present, and 0 means not present|

## Conclusion and Recommendations

### Contents

The contents of this notebook are as follows:

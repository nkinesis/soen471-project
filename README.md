# SOEN 471 project
Predicting costs of fire incidents

# Project Summary
Firefighting is an important public service, and keeping track of its costs is fundamental for governments around the world. In this project, we create a model to predict the cost of firefighting operations based on [London Fire Brigade Incidents](https://www.kaggle.com/datasets/jonbown/london-fire-brigade-incidents), containing data from 2009 to 2022. We join it with [London Weather Data](https://www.kaggle.com/datasets/emmanuelfwerr/london-weather-data) from 1979 to 2021. We use the files "lfb_incident.csv" (from London Fire Brigade Incidents) and "london_weather.csv" (from London Weather Data). We join both files by date, ignoring fire incidents from 2022 since we have no weather data for them. After joining, we obtain a dataset with 1,286,617 fire incidents. We use this dataset to train a decision tree and a random forest, using the implementations provided by sklearn and XGBoost. We chose these methods because they work well with [tabular data](https://ieeexplore.ieee.org/abstract/document/9393908). We use five input features: 1) month of call (categorical, 1 to 12), 2) building type (categorical), 3) number of fire pumps attending the incident, 4) number of hours the fire pumps worked, 5) mean daily temperature (Cº). Our output feature is the fire pumps' notional cost. This cost was originally expressed in pounds (numerical), but we converted it to categories, divided in intervals of 100 pounds. For example, all records with cost >= 0 and cost < 100 belong to category 1. All records with cost >= 100 and cost < 200 belong to category 2, and so on. This goes up until 1000. Records with costs larger than 1000 belong to category 11. We validate and compare the models produced with both libraries to understand which provides better prediction accuracy. In practice, the model we describe in this project could be useful for fire departments to estimate operation cost as soon as the receive a call for a fire incident.

# Dataset
We will use the [London Fire Brigade Incidents](https://www.kaggle.com/datasets/jonbown/london-fire-brigade-incidents) dataset which can be found on Kaggle. It contains detailed fire incident reports between 2009 and 2022 provided by the LFB (London Fire Brigade) from England. 

We will join this fire incident date with [London Weather Data](https://www.kaggle.com/datasets/emmanuelfwerr/london-weather-data), which contain daily mean temperature and other weather information from 1979 to 2021.

## Features
We use the files "lfb_incident.csv" (from London Fire Brigade Incidents) and "london_weather.csv" (from London Weather Data) to create our own dataset and then train our decision tree. Here is a brief description of the features and examples:

| **Feature**       | **Type**    | **Description**                                                    | **Example**              |
|-------------------|-------------|--------------------------------------------------------------------|--------------------------|
| DateOfCall        | Categorical | Date of call to fire dept (we kept the month only)                 | 12                       |
| PropertyType      | Categorical | Description of the place where the fire happened                   | House - single occupancy |
| NumPumpsAttending | Integer     | Number of pumps used in the incident. Number of firefighters = number of pumps multiplied by five                  | 3                        |
| PumpHoursRoundUp  | Integer     | Time spent at incident by pumps, rounded up to nearest hour        | 1                        |
| mean_temp  | Float     |  Mean temperature in degrees Celsius (°C)        | 2.8                        |
| Notional Cost (£) | Categorical     | Time spent multiplied by notional annual cost of a pump, in pounds. Originally in pounds, we converted this feature from numerical to categorical. For more information, please read the [Cost categories](#cost-cat) section | 1                      |

## <a name="cost-cat"></a> Cost categories
Most records in the dataset have costs lower than 1000 pounds. So we divide the categories in ranges of 100. For example, all records with cost >= 0 and cost < 100 belong to category 1. All records with cost >= 100 and cost < 200 belong to category 2, and so on. This goes up until 1000. Records with costs larger than 1000 belong to category 11.

# Model implementation
We will use the implementation of decision trees provided by [scikit-learn](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html#sklearn.tree.DecisionTreeClassifier). We will also use [xgboost](https://xgboost.readthedocs.io/).

# Model evaluation
We will divide the row in the dataset between training (66.6%) and testing (33.3%). We will use cross-validation.

# Installation
(TODO) For the final version of this README, we will describe our local setup so the experiments can be reproduced. We will add the requirements.txt and other instructions.
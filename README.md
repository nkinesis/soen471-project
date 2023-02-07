# SOEN 471 project - Predicting costs of fire incidents
In this work, we will predict the cost of firefighting operations based on data about fire incidents from LFB (London Fire Brigade). We also take weather data into consideration. We will use this data to train a decision tree model, and use methods such as bagging and boosting to improve prediction accuracy.

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
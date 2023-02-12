# SOEN 471 project
Predicting Fire Incident Costs in London UK with Decision Trees and Random Forests.

# Project Summary
Firefighting is one of the most cost demanding domain of the public safety sector in terms of after damage and preventive measures. Nonetheless, it is a fundamental public service for many governments of the world, and keeping track of its cost can benefit both the firefighters working at the heart of the action and the government bodies planning preventive measures and investments.
<br><br>
In this project, we aim to create a model that can predict the cost of firefighting operations in London, UK, based on two datasets: 
<li>London Fire Brigade Incidents ("lfb_incident.csv"), containing London's fire incident data from 2009 to 2022
<li>London Weather Data ("london_weather.csv" ) containing London's weather information from 1979 to 2021
<br><br>
To standardize the data values, we join both CSV files by date, ignoring fire incident records from 2022 and the weather recrods from 1979 to 2008 since there were no corresponding records in both datasets. The final dataset contains 1,286,617 fire incident and respective weather records in total. Based on this dataset, we will train two models that work well with tabular data: 
<li>a decision tree model 
<li>a random forest model
<br><br>
We will implement them with different Python libraries, such as <i>scikit-learn</i> and <i>XGBoost</i>, and evaluate to determine the best model in terms of <b>prediction accuracy</b>.
<br>
<br>
We use five features as the input values of our models: 
<br>1) month of the fire incident report call 
<br>2) building type 
<br>3) number of fire pumps attending the incident
<br>4) number of hours the fire pumps worked (h)
<br>5) mean daily temperature (Cº) 
<br><br>
Our output feature is the fire pumps' notional cost in pound sterling(£). The cost value was recorded as a continuous numerical variable, but we converted it to categorical variable, dividing and categorizing the numerical value in intervals of 100£. For example, all records of cost between 0.00 and 100.00£ would fall under the category 1, all records with cost between 100.01 and 200.00£ would fall under the category 2, and so on. All records with costs larger than 1000.01£ will fall under the category 11. 
<br><br>
In practice, the model we describe in this project could help estimate the operation cost of fire deparments as soon as a call for a fire incident is made.
<br>

# Dataset
<li> [London Fire Brigade Incidents](https://www.kaggle.com/datasets/jonbown/london-fire-brigade-incidents), from 2009 to 2022.
<li>[London Weather Data](https://www.kaggle.com/datasets/emmanuelfwerr/london-weather-data), from 1979 to 2021.

## Features
We join files "lfb_incident.csv" (from [London Fire Brigade Incidents](https://www.kaggle.com/datasets/jonbown/london-fire-brigade-incidents?select=lfb_incident.csv)) and "london_weather.csv" (from [London Weather Data](https://www.kaggle.com/datasets/emmanuelfwerr/london-weather-data?select=london_weather.csv)) by date. Here is a brief description of the features and examples:

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
- We will divide the row in the dataset between training (66.6%) and testing (33.3%).
- We will use cross-validation.

# Installation
(TODO) For the final version of this README, we will describe our local setup so the experiments can be reproduced. We will add the requirements.txt and other instructions.

# Firefighting cost prediction with tree-based models

Firefighting is one of the most cost-demanding domains of the public safety sector in terms of after-damage and preventive measures. Nonetheless, it is a fundamental public service and keeping track of its cost can benefit both the firefighters working at the heart of the action and the government bodies which manage them.

Therefore, in this project, we answer the following research questions:
1. Is it possible to predict the notional cost of firefighting operations using tree-based models?
2. Which tree-based model provides the best prediction accuracy?
3. What features correlate more or less strongly with the notional cost?

To answer these questions, we use public data from London (UK), which can be found on Kaggle: 
- [London Fire Brigade Incidents](https://www.kaggle.com/datasets/jonbown/london-fire-brigade-incidents) ("lfb_incident.csv"), containing fire incident data from 2009 to 2022.
- [London Weather Data](https://www.kaggle.com/datasets/emmanuelfwerr/london-weather-data) ("london_weather.csv"), containing weather information from 1979 to 2021.

We join both CSV files by date, ignoring fire incidents from 2022 and weather records from 1979 to 2008 since there are no matching records in both datasets. The final dataset contains 1,286,617 rows. We use this dataset to train three tree-based models that work well with tabular data: 
- decision tree 
- random forest
- boosted tree

As for the algorithms, we use the following implementations provided by the Python libraries scikit-learn and XGBoost:
- [sklearn.tree.DecisionTreeClassifier](http://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html)
- [sklearn.ensemble.RandomForestClassifier](http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)
- [xgboost.XGBClassifier](https://xgboost.readthedocs.io/en/stable/python/python_api.html)

We use five features as the inputs of our models: 
1. month of the fire incident report call 
2. building type 
3. number of fire pumps attending the incident
4. number of hours the fire pumps worked
5. mean daily temperature (Cº) 

Our output feature is the fire pumps' notional cost in pound sterling (£). The cost value was originally a continuous numerical variable, but we converted it to a categorical variable, dividing and categorizing the numerical value in intervals of £100. For example, all records of cost between £0.00 and £100.00 fall under category 1, all records of cost between £100.01 and £200.00 fall under category 2, and so on. All records with costs larger than £1000.01 fall under category 11. 

Finally, we evaluate to determine the best model in terms of **prediction accuracy**. In practice, the model we describe in this project could help estimate the operation cost of fire departments as soon as a call for a fire incident is made.

# Detailed feature description

| **Feature**       | **Type**    | **Description**                                                    | **Example**              |
|-------------------|-------------|--------------------------------------------------------------------|--------------------------|
| DateOfCall        | Categorical | Date of call to fire dept (we kept the month only)                 | 12                       |
| PropertyType      | Categorical | Description of the place where the fire happened                   | House - single occupancy |
| NumPumpsAttending | Integer     | Number of pumps used in the incident. Number of firefighters = number of pumps multiplied by five                  | 3                        |
| PumpHoursRoundUp  | Integer     | Time spent at incident by pumps, rounded up to nearest hour        | 1                        |
| mean_temp  | Float     |  Mean temperature in degrees Celsius (°C)        | 2.8                        |
| Notional Cost (£) | Categorical     | Time spent multiplied by notional annual cost of a pump, in pounds. Originally in pounds, we converted this feature from numerical to categorical.| 1                      |

# Model evaluation
We divide the rows in the dataset between training (66.6%) and testing (33.3%).We use hyperparameter tuning and cross-validation. Average f1-scores are:
- Random forest: 0.78
- Decision tree: 0.77
- Boosted tree: 0.77

# Installation
- (TODO) For the final version of this README, we will describe our local setup so the experiments can be reproduced. 
- (TODO) Add the requirements.txt and other instructions.

# 🚗 What drives the price of a car?

## Introduction
This is a  data-driven project that analyzes 426,000+ used cars data to predict prices and optimize dealership inventory decisions. We used the CRISP-D framework to analyze the data and then used it to identify a most suitable model using advanced regression techniques. We identified a model base don Ridge Regression and fine tuned the hyperparameters to achieve a error rate of 0.26 and also gathered valuable insights from the data that can drive decisions related to stocking the inventory to optimize sells.

![Kurt](https://github.com/shirishswate/CarPricePrediction-assignment-11/blob/main/images/kurt.jpeg)

## 🔍 Methodology: CRISP-DM Framework
![CrispDM](https://github.com/shirishswate/CarPricePrediction-assignment-11/blob/main/images/crisp.png)

Following the CRISP-DM methodology, we systematically performed following steps:
1. Understanding the business objectives
2. Understanding the data characteristics
3. Preparing data for modeling
4. Developing predictive models
5. Evaluating the model  performance
6. Deployment of the insights and the choosen model.

## 🎯 Business Understanding
### Problem Statement
In order to maximize profits, Use car dealers have to prepare strategy in following areas
- Optimal pricing 
- Inventory management
- Understanding what drives the value of the goods
- Managing competition

In order to address the above concers, this project is developed with following goals.
1. Identify key factors tha influence price.
2. Develop an accurate model to identify right price for the cars based on key features.
3. Provide actionable insights on what factors must be considered for inventory optimization

## Understanding the data characteristics a.k.a Data Analysis
* Price and odometer features were skewed, and hence converted to a logarithmic scale to provide a normal distribution.
* We found records with missing data, those were replace with the mean/median values of the corresponding features.
* Outliers were removed by considering data between 10 - 99.9 percentile.
* During the data understanding step, it was observed that the used car records are dominated by handful of brands. This is evident from the following chart

![ChatManufacturer](https://github.com/shirishswate/CarPricePrediction-assignment-11/blob/main/images/cars_manu.png)
* Next we looked at the best price performers base don "Fuel Type", "Condition of the car", "Transmission Type", "Manufacturer" "Paint color" and "Drive Type". Following charts shoe the price relation to hese categorical features. 

![ChatFuelType](https://github.com/shirishswate/CarPricePrediction-assignment-11/blob/main/images/box_fuel_type.png)

![ChatCondition](https://github.com/shirishswate/CarPricePrediction-assignment-11/blob/main/images/box_condition.png)

![ChatTransimmisionType](https://github.com/shirishswate/CarPricePrediction-assignment-11/blob/main/images/box_transmission_type.png)

![ChatManufacturer](https://github.com/shirishswate/CarPricePrediction-assignment-11/blob/main/images/box_manufactureres.png)

![ChatPaintColor](https://github.com/shirishswate/CarPricePrediction-assignment-11/blob/main/images/box_paint.png)

![ChatDriveType](https://github.com/shirishswate/CarPricePrediction-assignment-11/blob/main/images/box_drive_type.png)


## Preparing data for modeling

This step involved using the cleaned data to prepaer for modeling. 
* We converted categorical features to numerical representations using ColumnTransformers.
* Nominal categorical features were encoded using OneHotEncoder
* Ordinal catagorical features were converted using Ordinal encoder.
* Numerical features were scaled using StandardScaler. This ensured, the magnitude of the feature does not disproportionately affect the coeficient during regularization step.
* After the categorical features were encoded and numerical features were scaled, correlaion matrix was created, to see which feature are more co-related to the price (price log in this case). Below correlation chart show this.

![ChatCorr](https://github.com/shirishswate/CarPricePrediction-assignment-11/blob/main/images/corr.png)


## Developing predictive models
After the data was cleaned and preped, we developed three model options. In all these options the pre-process step is the same. In order to make these models easily reproducible, we decided to use Pipelines. Following three Pipelines were developed. Each Pipeline had pre-processer as first step whihc included Data preparation encoders mentioned in the abopve section. 
* Simple Linear Regression - This Pipeline consists of following steps
    * Pre-processing
    * Simple Linear Regression model.
* Polynomial Features  - This Pipeline consists of following steps
    * Pre-processing
    * Adding Polynomial features with degree= 2. This degree value was identified to be optimal by trying out multiple degree values and comparing the Mean Squared Error.
    * Simple Linear Regression model
* Ridge Regression - This Pipeline consists of following steps
    * Pre-processing
    * Adding Polynomial features with degree= 2. This degree value was identified to be optimal by trying out multiple degree values and comparing the Mean Squared Error.
    * Ridge Regression model - We identified Ridge regression as the optimal model with Alpha hyperparameter value as 10, using GridSearch Cross Validation method. In this we compared Lasso regression model as well.

## Evaluating the model  performance
Model evaluation techniques were used at three stages. 
* For Polynomial feature addition step as part of data preparation.
* Identifying the hyperparameter alpha for the Ridge and Lasso regression model.
* Selecting the best model with least testing error based on the mean squared error  and Root mean squared error methods.

Following table lists the MSEs and RMSEs calculated for each of the model options on the test data ( which is 20% data set aside from the training set).

| Model | MSE | RMSE |
|-------|-----|-----|
| Linear Regression | 0.3689 | 0.6074 |
| Polynomial Features (d=2) | 0.2659 | 0.5157 |
| Ridge Regression (alpha=10) | 0.2624 | 0.5122 |

Following chart shows the predictions from each model against he actual values.

![ChatPredict](https://github.com/shirishswate/CarPricePrediction-assignment-11/blob/main/images/scatter_pred_comp.png)

## Deployment of the insights and the choosen model.
Based on the above analysis and model evaluation, best model was selected as Ridge Regression with alpha = 10. This Pipeline was fitted with the training set ( which is 80% of the data). Coefficients of each feature were captured and insights were developed. FOllowing are the observations and recommendations. 

### Observations

* Age (Model Year) - Newer cars sell for higher price.
* Number of cylinders - Cars with more number of cylinders tend to sell at higher price. Higher number of cylinders is an indication of higher engine power. This infers that drivers are attracted to cars with higher engine power.
* Odometer reading - Cars with lower odometer reading tend to sell for higher price.
* Transmission type - It is also observed that drivers prefer certain type of transmissions over others. Especially "Automatic" transmission is preferred by drivers over others the most.
* Fuel type - Cars that run on Disel fuel are favored the most by drivers followed by electric , gas and hybrid in that order.
* Car type - When it comes to the tupe of a car, "Sedan" is liked the most followed by "Coupe", "pickup" and then "Van"
* Cars from certain Manufacturer's are favored by drivers. The most favored being "Toyota" followed by "Fiat", "Ram" and "Lincoln"

### Recommendations

* Focus on newer cars with low mileage. This will attract buyers who are looking for used but relatively new cars.
* To attract drivers who are looking for engine power, focus on bigger cars.
* Buyers who care about fuel expenses, will get attracted to cars that run on Disel, Electric and Hybrid. Focus on cars that run on these fuels types, and are more fuel efficient.
* Focus on "Sedan" type cars more, followed by "Coupe", "Pickups" and "Vans",
* Try to stock up on cars from fast selling Brands such as "Toyota", "Fiat" and "Ram".
* Aditionaly, usng the model developed above, implement a feature based pricing strategy to price the cars at a right point to maximize the chances of sell.

[Link to notebook](https://github.com/shirishswate/CarPricePrediction-assignment-11/blob/main/prompt_II.ipynb)

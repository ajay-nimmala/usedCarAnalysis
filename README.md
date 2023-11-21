
### Business Understanding

The data task is to perform exploratory data analysis on a dataset containing information on 426K cars. The dataset includes 18 columns, including information on the car's region, price, year, manufacturer, model, condition, cylinders, fuel, odometer, title status, transmission, VIN, drive, size, type, paint color, and state. The goal is to identify the key drivers of used car prices by analyzing the relationships between these variables and the price of the car. This will involve analyzing data, cleaning, and preprocessing of the data based on the analysis. Followed by, statistical analysis techniques such as correlation analysis and regression modeling. The results of the analysis will be used to provide clear recommendations to the client on what consumers value in a used car.


Vehicles dataset that was provided as a csv file was loaded as a dataframe. Following is the data model for the data.

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 426880 entries, 0 to 426879
Data columns (total 18 columns):
 id   Column        Non-Null Count   Dtype  
---  ------        --------------   -----  
 0   id            426880 non-null  int64  
 1   region        426880 non-null  object 
 2   price         426880 non-null  int64  
 3   year          425675 non-null  float64
 4   manufacturer  409234 non-null  object 
 5   model         421603 non-null  object 
 6   condition     252776 non-null  object 
 7   cylinders     249202 non-null  object 
 8   fuel          423867 non-null  object 
 9   odometer      422480 non-null  float64
 10  title_status  418638 non-null  object 
 11  transmission  424324 non-null  object 
 12  VIN           265838 non-null  object 
 13  drive         296313 non-null  object 
 14  size          120519 non-null  object 
 15  type          334022 non-null  object 
 16  paint_color   296677 non-null  object 
 17  state         426880 non-null  object 
dtypes: float64(2), int64(2), object(14)


### Exploratory Data Analysis

- Dropped null values from the dataset. Then looked for duplicates, there were none.
- Converted categorical columns in the dataset to numeric ones by factorizing to run a quick correlation of the data. Followed by plotting a heatmap, which gave a very high level overview of the correlation of features with price.
- Ran different plots to analyze all features in the dataset. Observations and subsequent actions are listed in Data Preperation section.
- Initial analysis clearly showed that price of cars is not normally distributed and was heavily skewed on the higher price. This would have an impact of overfitting if we did not clean up/normalizee the data. Data needed to be normalized.

### Data Preperation
- Normalized the data by computing 1st and 3rd quantile of the data based on price.
- Year - Has the 2nd highest correlation with price (0.25) based on heatmap. But upon closer look, only 3.7% of data is from before 2000 and hence that data will be deleted.
- Fuel - Has the highest correlation with price (0.36) based on heatmap. Gas and Diesel cover for 98.5% of the data and hence remaining all will be categorized as other
- Cylinder - 4, 6 and 8 cyclinder vehicles comprise of 97% of the data and hence remaining data will be moved under other.
- Title_Status - 97% of overall vehicles have clean title status. Moving rest of the data under other
- Condition - Between Excellent, Like New and Good cover for ~98% data and hence moving remaining fields under other.
- Transmission - 94% of records are Automatic and hence moved remaining records under other category
- Created a new column for vehicle age, which is computed based on year of manufacture.

- After cleaning up the data, dropped unwanted (year, id, region, title_status, transmission and year) columns.

### Updating Categorical Columns and creating training/test data sets.

- Split the prepared data into features (X) and target (y).
- Creating training and test data sets from original data set, with a split of 70/30
- Categorical Columns and Numerical Columns to encode the data so that categorical values will be converted to numericals using category_encoders and then scaled so that they can be used for ML operations can be performed


## Modeling
- Once final dataset is ready, ran three different machine learning models, Linear Regression, Sequential Feature Selection and Ridge Regression. Cross validated the results using MSE and MAE. Plotted the graphs to understand visually.

### Evaluation of Models
Based on the evaluation of the three models, the Ridge Regression model with an alpha value of 10.0 appears to be the best model for predicting used car prices based on the given features. It has the lowest MSE and MAE on the test data, indicating that it is the most accurate of the three models. 

The Sequential Feature Selection model has the highest MSE and MAE on both the training and test data, indicating that it is the least accurate of the three models. 

The Linear Regression model performs reasonably well, but not as well as the Ridge Regression model.

The Ridge Regression model also has the advantage of being able to handle predictions based on relationship between multiple features, which is a common issue in linear regression models. The Ridge Regression model achieves this by adding a penalty term to the cost function that shrinks the coefficients of highly correlated features towards zero.

Based on the coefficients of the Ridge Regression model, it appears that the manufacturer of the car is the most important feature for predicting used car prices, with Acura, BMW, and Cadillac having positive coefficients and Buick, Chrysler, and Dodge having negative coefficients. Other important features include the odometer reading, vehicle age, and fuel type.

Therefore, it is recommended to use the Ridge Regression model with an alpha value of 10.0 for predicting used car prices based on the given features. 

However, it is important to note that there may be other factors that could affect the accuracy of the model, such as data quality, feature selection, and model tuning. Therefore, it is recommended to continue monitoring the performance of the model and making improvements as necessary to ensure its accuracy and reliability.

## Final Results & Recommendations

- Manufacturer of the car is an important feature for predicting used car prices. Acura, BMW and Cadillac have a positive correlation with price. Buick, Chrysler and Dodge have negetive correlation with price.

### Other important features that have a high correlation with price are
- Odometer reading
- Vehicle Age (Total no of years since the car is manufactured)
- Fuel Type
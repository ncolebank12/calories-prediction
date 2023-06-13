Exploratory data analysis for this dataset can be found [here](https://ncolebank12.github.io/recipe-ratings/)

# Framing the Problem

In this analysis, I will be examining how the calories of recipes can be best predicted. Since calories are a continuous variable, this will be a regression prediction problem. 

The response variable is the first element in the 'nutrition' column, as this value corresponds to the calories for the recipe. I am interested to see what factors in this dataset influence the number of calories besides the macronutrient information (since this data can be used to directly calculate the number of calories in a recipe). 

The metric I will be using to evaluate the quality of the model is the Root Mean Square Error (RMSE). This will be best in comparing the baseline model to the final model as it will show the average deviation between the actual and predicted calories. Since it is difficult to evaluate a regression model's quality solely on the RMSE, I will also calculate the R^2 to see how much the predictor variables explain variation in the predicted values.

The information that would be known at the time of prediction for predicting calories would be all columns except those pertaining to reviews. This is because the reviews information only comes after the calories of a recipe is decided and published. Therefore the columns 'rating', 'review', and 'avg_rating' will be ignored in this investigation.

# Baseline Model

For the baseline model, I decided to create two features from the 'tags' and 'n_steps' column. Since 'n_steps' is a numerical column, I passed it through the model as is. 

Since the 'tags' column is categorical, I had to encode it. Due to the structure of the 'tags' column, one-hot encoding could not be used as there can be multiple tags in one row. A workaround for this is the scikit-learn CountVectorizer object, which takes in a column of lists (generated by splitting the 'tags' column), and essentially performs one-hot encoding using the entire set of possible tags as the different features. 

With the ColumnTransformer object, I set remainder='drop' so that these were the only features used, with n_steps being 'quantitative' and and 'tags' being nominal.

I decided to use the LinearRegression object as the model at the end of the pipeline (which consists of a ColumnTransformer applying the transformations outlined above and the model itself).

After fitting the model to the training data, these were the results for the R-squared and RMSE values:
|           | Training Data | Test Data |
|-----------|---------------|-----------|
| R-squared | 0.113         | 0.100     |
| RMSE      | 590.263       | 635.378   |

As illustrated by these results, this baseline model is not a good predictor of calories. Only about 10% of the variance explained by the predictors, and the average deviation from the actual values is about 600 calories, which is way off since most recipes are in the 0-2,000 calorie range.

# Final Model

# Fairness Analysis

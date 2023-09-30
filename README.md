 # Prediction-of-Product-Sales

by Peter Tran |  hdtran103@gmail.com
-------------------------------------------
[Link to the Data (.csv)](https://drive.google.com/file/d/1syH81TVrbBsdymLT_jl2JIf6IjPXtSQw/view)\
[Source of the Data](https://datahack.analyticsvidhya.com/contest/practice-problem-big-mart-sales-iii/)

### With these graphs and models, we can predict future product sales for our clients.

## Data Dictionary
Explanation of the various columns in the Dataset
![Data Dictionary](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/Data%20Dictionary%20(80%25).png)

## Item MRP by Outlet Sales
- Here we can see that as the price of the item goes up, the total return goes up as well
  - Less of those products are sold, but the higher price makes up the difference
![Item MRP by Outlet Sales](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/Item%20MRP%20by%20Outlet%20Sales.png)

## Sales by Item Type
- We can see that 'Fruits and Vegetables' has the most sales followed closely by 'Snack Foods'
![Sales by Item Type](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/Sales%20by%20Item%20Type.png)

## Comparing Outlet Type, Size, and Location Type by Sales
- This plot is broken up into the 3 Tiers of Outlet_Location_Type with a hue of Outlet_Size
- It shows the Outlet_Type by Item_Outlet_Sales
- We can see that there are much more Medium stores
- We can also see that Tier 3 stores have the most variety of Outlet_Type
- We can then see that Supermarket Type1 is in every Tier and has all Outlet_Sizes including the Missing ones
![Outlet Type, Size, and Location Type by Sales](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/Comparing%20Outlet%20Type%2C%20Size%2C%20and%20Location%20Type%20by%20Sales.png)

## Model Evaluation
The Decision Tree is the better model to use when predicting Item Sales.

From the Metrics Score, we can see that the Mean Absolute Error for the Decision Tree is lower by about 70 rupees. The Root Mean Squared Error is also lower for the Decision Tree, meaning that there are less outliers throwing off the weight of our model.

Looking at the Percentage of Error, we can also see that the Linear Regression model will be off, on average, by 36.87% while the Decision Tree will be off by 33.85%. We'll have less error with the Decision Tree.
***
# Project 1 - Revisited

## LinearRegression Most Important Coefficients
![linreg_coefficients](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/linreg_coefficients.png)

### Interpret Top 3 Most Impactful Feature Models

  -  'Outlet_Type_Supermarket Type1':
        If Outlet_type Supermarket Type 1"" == 1, then the product is sold at that type of store and the product will generate that much more revenue.

  -  'Outlet_Identifier_OUT027':
        If the Outlet Identifier is OUT027, this also increases our value of interest. (like sales or customer visits) but by about 901 units. So, it has the second strongest effect.

  -  'Outlet_Type_Supermarket Type3':
        If the Outlet Type is Supermarket Type 3, increase our value of interest by about 900.794(or 901 units), just like the effect of the supermarket with ID 'OUT027'. So these two features share the same level of effect, which make them equally important in our analysis.

- The most impactful features are object type

    - The different types of supermarkets and their unique IDs, and understanding the city and its people better, we can make smarter guesses about how well each supermarket might do in terms of sales.



## RandomForest Feature Importances

### Default Importances
![rf_default_importances](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/rf_default_importances.png)

#### Top 5 Most Important Default Features
    - 'Item_MRP'
    - 'Outlet_Type_Grocery Store'
    - 'Item_Visibility'
    - 'Item_Weight'
    - 'Outlet_Identifier_OUT027'

### Permutation Importances
![rf_perm_importances](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/rf_perm_importances.png)

#### Top 5 Most Important Permutation Features:
    - 'Item_MRP'
    - 'Outlet_Type_Grocery Store'
    - 'Item_Visibility'
    - 'Item_Weight'
    - 'Outlet_Identifier_OUT027'    

- Same features as Default Importance, but, in this case, the features are valued higher in importance compared to the Default
### Differences:

The comparison interesting insights:
- 'Item_Visibility' is ranked lower (5th instead of 3rd) in SHAP.
- 'Outlet_Type_Supermarket Type 3' replaces 'Item_Weight' (ranked 4th) in SHAP.
- 'Outlet_Identifier_OUT027' is ranked higher (3rd instead of 5th) in SHAP.

***
# Project 1 - Revisited Part 2: Explaining Models with SHAP

## Summary Bar Plot RandomForestRegressor
![summary_bar_plot_rf_reg](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/summary_plot_bar_rf_reg.png?raw=true)
- The Summary Bar Plot shows the average magnitude of SHAP values for each feature.
  - The higher the bar, the more impact the feature has on the model's predictions.
  - In this case, `Item_MRP` has the highest influence, followed by `Outlet_Type_Grocery Store`, and `Outlet_Identifier_OUT027`.


### Comparison with RandomForest Regressor Feature Importance

#### Default Feature Importances
![rf_default_importances](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/rf_default_importances.png) 

#### Permutation Feature Importances
![rf_perm_importances](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/rf_perm_importances.png)

#### Differences
- Default and Permutation Importances have the same top 5 features

- SHAP Plot Summary differs in that:
    - 'Item_Visibility' is ranked lower (5th instead of 3rd)
    - 'Outlet_Type_Supermarket Type 3' takes the place of 'Item_Weight' (ranked 4th)
    - 'Outlet_Identifier_OUT027' is ranked higher (3rd instead of 5th)

 ## Summary Dot Plot RandomForestRegressor
 ![summary_plot_dot_rf_reg](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/summary_plot_dot_rf_reg.png?raw=true)

 ### Summary Dot Plot Interpretation

### Interpret Top 3 Feature Models:
1. **Item_MRP**:
    - A higher Item's MRP (redder dots) correlates with increased sales predictions (dots move to the right).
      
2. **Outlet_Type_Grocery_Store**:
    - Being a Grocery Store (red/true) typically results in lower predicted sales (dots move to the left).
      
3. **Outlet_Identifier_OUT027**:
    - Being Outlet OUT027 (red/true) significantly boosts predicted sales (dots move to the right).


***
# Local Explanations
- Comparing 'High' and 'Low' sale stores using SHAP and LIME provides valuable insights into the differing factors influencing sales figures between well-performing and not-so-well-performing stores.
- Features like 'Item_MRP', 'Outlet_Type', and 'Outlet_Identifier' emerge as pivotal variables in determining sales outcomes.
- These local insights, when juxtaposed with global interpretations, contribute to a nuanced understanding of feature impacts on sales predictions.


## SHAP Local Force Plot

### High Sales
![force_plot_high_sales](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/force_plot_high_sales.png)
- Significant 'push' towards the right indicating higher sales
    - Major features:
        - 'Item_MRP'
        - 'Item_Visibility'
        - 'Item_Weight'
        
- Only one feature pushing left (lower sales):
    - 'Outlet_Type_Supermarket Type3'
 
### Low Sales
![force_plot_low_sales](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/force_plot_low_sales.png)
- Significant 'push' to the left (lower) indicating lower sales
    - Major features:
        - 'Outlet_Type_Grocery Store'
        - 'Item_MRP'        
        
- Seems to be no features pushing right (higher sales)

## Lime Tabular Explanation

### High Sales
![lime_high_sales](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/lime_high_sales.png?raw=true)
- Predicted Value is 6693.23 where True Value is 8323.8316

- Interpreting our Features with the 'negative' and 'positive' bar chart
    - Positive (higher sales) include:
        - 'Outlet_Type_Grocery Store' (not a Grocery Store)
        - 'Item_MRP' (greater than 180.25 at 219.35)
    - Negative (lower sales) include:
        - 'Outlet_Identifier_OUT027' (not this Outlet)
        - 'Outlet_Type_Supermarket Type3' (not this Outlet Type)
    - Even though the Feature Names are cutoff, they can be seen in the bottom graph (Feature/Value)
 
### Low Sales
![lime_low_sales](https://github.com/hdtran103/Project-1-Prediction-of-Product-Sales/blob/main/Data/lime_low_sales.png)
- Predicted Value is 63.42 where True Value is 36.62

- Interpreting our Features with the 'negative' and 'positive' bar chart
    - Negative (lower sales) include:
        - 'Outlet_Type_Grocery Store' (is a Grocery Store)
        - 'Item_MRP' (less than or equal to 90.72 at 35.22)
        - 'Outlet_Identifier_OUT027' (is not this Outlet)
        - 'Outlet_Type_Supermarket Type3' (is not this Outlet Type)
    - Positive (higher sales) include:
        - 'Item_Type_Seafood' (is not this Item Type)
        - 'Outlet_Identifier_OUT045' (is not this Outlet)
    

### Lime Tabular Explanation:
#### High Sales:
- **Predicted Value:** 6693.23 
- **True Value:** 8323.8316

#### Low Sales:
- **Predicted Value:** 63.42 
- **True Value:** 36.62


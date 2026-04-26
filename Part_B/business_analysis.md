B1. Problem Formulation
(a)

This problem can be framed as a supervised machine learning regression problem.
The target variable is items_sold, which represents the number of items sold in a store during a promotion period.

The input features can include:

store size
location type (urban, semi-urban, rural)
promotion type
competition density
customer activity (like footfall)
time-based features such as month or festival

This is a regression problem because the output is a continuous numeric value (number of items sold). The goal is to predict how many items will be sold under different conditions.

(b)

Using total sales revenue can be misleading because it depends on product prices, which may vary across stores and promotions. For example, a high revenue value might come from selling fewer expensive items.

On the other hand, items sold directly measures customer response to a promotion. It shows how effective a promotion is in increasing demand.

This reflects an important principle in machine learning:
 the target variable should closely match the actual business objective.
In this case, the goal is to increase sales volume, not just revenue.

(c)

Instead of using one global model, we can use a segmented modelling approach.

For example:

build separate models for urban, semi-urban, and rural stores
OR
include store-specific features and interaction terms

This is better because different stores behave differently. A promotion that works in an urban area may not work in a rural area. So, this approach helps capture those differences and improves prediction accuracy.






B2. Data and EDA Strategy
(a)

The data comes from four tables: transactions, store attributes, promotions, and calendar.

These tables can be joined using common keys such as:

store_id
promotion_id
date

The final dataset should have one row per store per month.

Before modelling, we need to aggregate the data. For example:

total items sold per store per month
average basket size
number of transactions
promotion used in that month

This ensures that the data is in a consistent format for modelling.

(b)

Before building a model, I would perform the following EDA:

Distribution of items sold
→ to check if the data is skewed or has outliers
Promotion type vs items sold (bar chart)
→ to see which promotions perform better
Correlation heatmap
→ to understand relationships between variables
Time trend (items sold over months)
→ to identify seasonality or trends

These insights help in feature engineering. For example:

if seasonality exists → include month feature
if some promotions perform better → model can learn this pattern
(c)

If 80% of data has no promotion, the model may become biased and learn that “no promotion” is the default case.

To handle this:

we can balance the dataset using sampling techniques
or give more importance (weights) to promotion cases
or ensure proper representation during training

This helps the model learn the actual impact of promotions.







B3. Model Evaluation and Deployment
(a)

Since the data is time-based (monthly data over 3 years), we should use a time-based split.

For example:

first 2.5 years → training
last 6 months → testing

A random split is not suitable because it mixes past and future data, which can lead to data leakage.

Evaluation metrics:

RMSE → measures average prediction error (penalises large errors more)
MAE → gives average absolute error (easy to interpret)

Lower values indicate better performance.

(b)

Feature importance helps us understand which factors influence the model’s decision.

For example:

in December → festivals and high demand may make loyalty points effective
in March → discounts may work better due to lower demand

We can explain to the marketing team that the model is considering:

seasonality
customer behaviour
promotion effectiveness

This helps build trust in the model.

(c)

For deployment:

Save the trained model using tools like joblib or pickle
Every month, prepare new data in the same format
Pass this data into the saved model to get predictions

For monitoring:

track prediction errors over time
compare predicted vs actual sales
if performance drops → retrain the model

This ensures the model stays accurate over time.
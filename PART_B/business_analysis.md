===========B1 = PROBLEM FORMULATION ===========

A)  the problem is to predict how many item will be sold when a perticular promotion use for marketing so we can find which protion gives the highest sales for the perticulat area.

and our target variable is our item sold base on this we will predict  which promothion should we use for perticular area 

and our input features are the store size, location type, footfall, competition density, customer demographics, promotion. so we will use these feature to analys the data and do predict 

this is the regresion type of ml problem bacuase we are predicting numirical value


this is regresion problem because the output is in numerical value(item sold) so model predict quantity rathan classifying into categories



B)  Revenue cannot be use as a indicator since there is a wide variation among promotions regarding prices Discounts and complimentary offers can lower revenues even if the sales of the product increase Thus the use of the revenue indicator is problematic due to the mixing of price and number of units sold in its calculation.
the number of items sold reflects customers reactions to the promotion It provides exact information on the number of units bought by customers during the promotion

The target attribute must directly reflect the true aim of the problem and it must not get influenced by any external factors

C)  Rather than relying on a global model a segmented modeling technique can be employed whereby each store type (such as urban, semi-urban, and rural) will have its own model.
It is superior since depending on the location of a particular store there may be unique behavior of customers consumer preferences and competition. This will affect the global model's results making it unreliable.


==============B2 = DATA AND EDA STRATEGY=============

A)  The four tables are joined using common keys. The transactions table is the main table and is joined with store attributes using store id with promotion details using promotion type and with the calendar table using transaction_date.
The final dataset is at the store-month level where one row represents one store for one month.
Before modelling aggregations are performed such as summing items sold to get monthly sales aggregating footfall or transactions and including calendar features like weekends and festivals Store attributes remain unchanged.


B)  Histogram of items sold: To see the skewness in the data and any potential outliers Outliers or data skewness can be handled based on this
Type of promotion vs items sold (bar plot): To see the performance of various promotions Helps us understand which promotion affects sales.
Heatmap of numerical features: To see if there are any relations among the numeric variables and items sold Will help in selecting relevant features for modeling.
Trends in items sold (line graph): To see trends or seasonality if any in the sales Helps us develop time series features.


C)  If there are no promotions in 80% of cases, then there is data imbalance in such cases. The model might be skewed toward “there’s no promotion” and the learning effect of each promotion might be missed by the model.

There are ways to handle such an imbalance issue. These include methods of resampling, where we would either oversample the promotions or undersample no promotions.


============B3 = MODEL EVALUATION AND DEPLOYMENT=============


A)  Since the time feature is present in our data (36 consecutive monthly values) a chronological train-test split needs to be applied thus earlier data points will be utilized as a training sample while newer ones will serve as a test sample.

A randomized splitting of the dataset is not suitable since it violates the time ordering and will lead to leakage meaning future data will impact past prediction results causing unreasonable model performance.

The following performance metrics can be considered:

RMSE (Root Mean Squared Error): reflects total error and punishes larger errors. In our case RMSE would illustrate how much error is made when we make our predictions regarding the number of items sold making it crucial to avoid significant forecasting errors.
MAE (Mean Absolute Error): reflects the average prediction error. MAE is straightforward and easy to understand since it simply gives us the average difference between actual and predicted sales.

These performance metrics can be useful in evaluating how well the algorithm predicts sales making it relevant for choosing promotions and inventory management.

B)  To find out why the model provides contradictory recommendations for the same store in different months I would conduct an analysis of feature importance in the model.

Feature importance reveals which predictors (such as month seasonality type of promotion or customer behavior) have the greatest impact on prediction I will look at how the features of month period of festivities and customer demand differ from December to March.

For instance the month of December can have a high level of demand because of festivities and holidays and therefore it may be more efficient for the model to suggest Loyalty Points Bonus while Flat Discount is expected to produce higher results in March.

In order to explain this to the marketing department, I would point out that:
The models predictions are not random but based on seasonality and customer behavior which are determined by features such as time and demand trends.

C)  The model after training is saved using libraries such as joblib or pickle such that it can be used in future without the need to train again.

Each month, fresh data is obtained for the 50 stores (information about stores, possible promotions, calendar information, etc). The data is prepared using the same techniques as used during training (scale and encode) and input to the trained model for making predictions about the most suitable promotion for each store.

For monitoring purposes, predictions from the model are compared against actual sales values whenever new data becomes available. RMSE and MAE are measured periodically. Any significant increase in these errors signifies poor model performance.

In such instances, retraining needs to be done with the most up-to-date data.
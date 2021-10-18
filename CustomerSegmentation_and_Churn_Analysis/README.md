## Customer Segmentation and Churn Prediction 

- **Objective:** To create useful customer segments from shopping data study the factors which contribute to customer churn.

- **Results:** Provided three customer segments using a hierarchical clustering model with distinct behavioral patterns that also posessed unique demographic difference that allow the segments to be generalized and applied to customers for whom there is no transaction data.   Modeled churn and explored SHAP values with feature importance in order to provide key insights and recommendations for reducing churn.


File Organization: 

- Code
  - 01 - Creating Household-centered data views
  - 02 - Creating Aggregate dataframe of Household data for segmentation
  - 03 - Customer Segmentation Data Wrangling
  - 04 - Exploratory Data Analysis
  - 05 - Customer Segmentation Pre-processing and Training
  - 06 - Cluster Modeling
  - Churn Prediction & Analysis
  - README.md

- Data
  - Aggregate_Customer_Data
  - Cleaned_Customer_Data
  - Correlation_Thresholds
  - Cust_seg
  - Cust_seg_categorical
  - Cust_seg_numerical
  - Trimmed_Data
  - campaign_desc.csv
  - campaign_table.csv
  - causal_data.csv
  - coupon.csv
  - coupon_redempt.csv
  - dunnhumby - The Complete Journey User Guide.pdf
  - hh_demographic.csv
  - product.csv
  - transaction_data.csv
  - README.md
-  Documents
  - README.md
- README.md

## Customer Segmentation Approach:

- The provided data set included some demographic information, but all transactional and marketing information needed to be amalgamated into a household centered
view for clustering, I did this by aggregating data using SQL queries and appending to the data set. 

- After creating the data view I realized that about 30% of households had any demographic information, and decided the limit clustering to those households for which I had demographic information
 
- Prior to applying clustering algorithms to the data, I decided to compare at least two different models and use whichever model provided the most distinct clusters for customer segmentation


### Models Used:

- I then decided to visualize clusters for the K-Means algorithm using various values for K and comparing using the silhouette score and elbow method, as well as visualizing clusters for Agglomerative clustering via dendogram.  Ultimately I ended up using the Agglomerative clusters since they presented more distinct results for analysis and insights. 

- Generally speaking, the K-Means model found the most distinct clusters at K = 9, however 9 clusters is not manageable for from a customer segmentation standpoint.  The next best clusters for the model occured at K = 4, however the structure of these clusters were much less distinct.  

- Agglomerative modeling provided good structure to the data, with the most defined clusters occuring with three clusters: 

     ![image of agglomerative dendogram](https://github.com/NickD-Dean/Springboard/blob/0bf0e49098a1d924d9db1759ed1db2def231f1aa/CustomerSegmentation_and_Churn_Analysis/Documents/Dendrogram.png)


### Model Selection: 

- More important than the structure to the data uncovered by the clustering models was their usefulness for segmenting customers, which necessitates both a need for distinct demographic traits as well as behavioral differences; the Agglomerative model provided this better than the K-means model did.

- Both models uncovered the same key differences along demographic lines, overwhelmingly hosuehold size, marital status, and childrearing status were the most important differences between clusters regardless of algorithm used or the number of clusters used: 

     ![image of household size with clusters](https://github.com/NickD-Dean/Springboard/blob/0bf0e49098a1d924d9db1759ed1db2def231f1aa/CustomerSegmentation_and_Churn_Analysis/Documents/Household%20Size.png)
     
- However, the Agglomerative model revealed the subtle differences in spending and transaction behavior between the clusters in a way that the K-means model did not.  You can see below that the average loyalty discount, as well as maximum manufacturer rebate (coupons that the product manufacturer pays for rather than the grocery store) are distinct for the Agglomerative model, while these were nearly identical for the K-means model. 

    ![image of the avg loyalty disc](https://github.com/NickD-Dean/Springboard/blob/0bf0e49098a1d924d9db1759ed1db2def231f1aa/CustomerSegmentation_and_Churn_Analysis/Documents/Avg%20Loyalty%20Discount.png)
    
    ![image of the max manufacturer rebate](https://github.com/NickD-Dean/Springboard/blob/0bf0e49098a1d924d9db1759ed1db2def231f1aa/CustomerSegmentation_and_Churn_Analysis/Documents/Max%20Manu%20Rebate.png)

- You can see this 'distinctness' difference between the clusters created by either algorithm when visualized under PCA in 3-dimensions:

    ![image of K-means clusters](https://github.com/NickD-Dean/Springboard/blob/0bf0e49098a1d924d9db1759ed1db2def231f1aa/CustomerSegmentation_and_Churn_Analysis/Documents/K-means%20clusters.png)
    
    ![image of Agglo clusters](https://github.com/NickD-Dean/Springboard/blob/0bf0e49098a1d924d9db1759ed1db2def231f1aa/CustomerSegmentation_and_Churn_Analysis/Documents/Agglomerative%20Clusters.png)
    
    
### Customer Segmentation Results

- I ultimately chose to work with the agglomerative lusters sinc ethey provided the best structure to the data.  The resulting customer segments were as follows:

1. **A0:** (Red cluster in above plot) This is the largest cluster that the Agglomerative model produced. It's overwhelmingly made up of  single-person households which are poorer on average than those belonging to another cluster. This cluster also has the largest group of households between the ages of 45 and 54 years old, almost half of the households in this cluster belong to that group.  This cluster is the most recent purchasers, who typically have the smallest average sales value, smallest discounts, and the smallest basket size. "Frequent low volume customers"


2. **A1:** (Grey cluster in above plot)This is the smallest cluster, and also is the youngest cluster with most of its households made up of people between the age of 25 and 44. This cluster is also the only cluster to be made up of households with children, and not a single member has fewer than 3 members. Finally, this is the wealthiest cluster on average.  A1 has the largest average discount (coupon, loyalty, or rebate), as well as the most coupons redeemed and the highest average sales value as well as highest total value. "High value, high discount"


3. **A2:** (Orange cluster in above plot)The final cluster is exclusively made up of 2-person households with no children. Generally speaking this cluster is older on average than the other two, with the largest number of households over the age of 65. Additionally, this cluster is generally poorer on average than cluster A1, however it has the largest number of households earning over 150k.  This cluster is the one which has shopped the least recently, but has the second highest loyalty discount. Generally speaking it seems to follow the behavior trends of A0, but with less magnitude (frequent but low value discounts). "High interval shoppers"


## Churn Modeling Approach:

Prior to analyzing churn using machine learning I needed to settle on a definition of churn.  I decided to visualize how much of the customer base would be labelled as 'churned' under different definitions.  These are listed and visualized below: 

1. Churn is allowing 30 days (1 month) to pass without visiting one of the grocery stores (This infers that a customer has shopped 2 times at a different grocery chain without returning to the chain being examined).


2. Churn is no longer shopping from this brand of grocery chain 1 year after the first active day (This limits churn to those who are never 'resurrected').


3. Churn is allowing 90 days to pass without visiting one of the grocery stores (This infers that a customer shopped 6 times at a different chain, and would capture the behavior which I personally exhibit).


4. Some other definition of churn based on patterns noticed in the data.

![image of churn definition](https://github.com/NickD-Dean/Springboard/blob/0bf0e49098a1d924d9db1759ed1db2def231f1aa/CustomerSegmentation_and_Churn_Analysis/Documents/Churn%20Def%20Plot.png)


I ultimately chose to work with definition # 3 for churn.  This resulted in 6.84% of households being labeled as churn. 


### Models Selection:


- I was primarily focused on the recall score for the churn class.  This measures the ratio of correct churn predictions to the total number of churned customers in the data set.   Since the goal is to use machine learning to understand which qualities of a household are the most indicative of churn, this will be the best metric for evaluating models.


- I chose which models to test using the sci-kit learn website’s best practices diagram. Ultimately the models I tested  were: Linear SVC, KNN, SVC, Random Forest, and Gradient Boosting.


- Only the Random Forest, KNN, and Gradient Boosting predicted any households as churned.  Of those only the Gradient Boosting model had a minority class recall score over 0.3.


- My Gradient Boosting model correctly predicted 44% of the true churned households, far better than any other model, and also produced the highest overall accuracy of 95%.  I used this model with it's feature_importances as well as the shapley values to better understand the model and the insights it provided.

### Churn Results: 

- Below I've plotted the feature importances and shap summary plot for the Gradient Boosting model. 

![Feature Importance](https://github.com/NickD-Dean/Springboard/blob/95b6215a711ed17b97613a955d903d09690d4a6d/CustomerSegmentation_and_Churn_Analysis/Documents/Feature_importance.png)

![Shap Summary](https://github.com/NickD-Dean/Springboard/blob/95b6215a711ed17b97613a955d903d09690d4a6d/CustomerSegmentation_and_Churn_Analysis/Documents/Shap_summary.png)


Using the above plots, as well as the previous exploratory analysis I made several recommendations: 


1. Firstly, provide more and larger coupons in the mailing advertisements.  Higher maximum coupon discounts are associated with reduced churn probability, as well as a higher frequency of purchasing products that were advertised in the mailer.


2. Secondly, increase the size of ‘utility’ items sold in the store in order to increase the average shopping lag (one of the best predictors of churn) of customers.  For instance, selling a 24 ct pack of paper towels rather than a 16 ct pack.  These kinds of utility items can influence households to shop with a larger period of time in between trips and are products that are simply convenient to purchase anywhere.  If a customer needs toilet paper they’re going to purchase it regardless of the amount you sell. 


3. Find ways to increase loyalty program participation, since an increased loyalty discount is heavily correlated (correlation coefficient of 0.82) with increased average sales value for a household.  Strategies used by other grocery chains for this purpose include pricing techniques such as 'instant markdown' or visually contrasting normal vs loyalty prices.


4. No household redeemed more than 4 percent of their coupons unless Type A campaigns were less than 50% of the campaigns sent to them.  Type A campaigns are tailored based upon past purchasing behavior, and based on the churn analysis a higher number of unique products is associated with an increased ‘stickiness’ for a household.  I recommend using Type A campaigns to offer coupons for new products based on past purchases, or to reduce the number of Type A campaigns overall.


5. Lastly, study further the customers who purchased a high percentage of products on display. Were the products they purchased on display cheaper than other similar products they have purchased? Why is it that purchasing goods marketed in one way causes the model to predict a customer as churned, while purchasing goods marketed via mail as retained?  Understanding how marketing efforts influence different households in different ways - particularly in the context of customer segmentation - will better enable targeted efforts to reduce churn. 




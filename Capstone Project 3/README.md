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
- 
- Prior to applying clustering algorithms to the data, I decided to compare at least two different models and use whichever model provided the most distinct clusters for customer segmentation


### Models Used:

- I then decided to visualize clusters for the K-Means algorithm using various values for K and comparing using the silhouette score and elbow method, as well as visualizing clusters for Agglomerative clustering via dendogram.  Ultimately I ended up using the Agglomerative clusters since they presented more distinct results for analysis and insights. 

- Generally speaking, the K-Means model found the most distinct clusters at K = 9, however 9 clusters is not manageable for from a customer segmentation standpoint.  The next best clusters for the model occured at K = 4, however the structure of these clusters were much less distinct.  

- Agglomerative modeling provided good structure to the data, with the most defined clusters occuring with three clusters: 

![image of agglomerative dendogram](https://raw.githubusercontent.com/NickD-Dean/Springboard/main/Capstone%20Project%203/Documents/Dendrogram.png)


### Model Selection: 



### Customer Segmentation Results

## Churn Modeling Approach:

### Models Used:

### Model Selection: 

### Churn Results: 

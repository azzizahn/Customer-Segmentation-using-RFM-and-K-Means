# Customer-Segmentation-using-RFM-and-K-Means

* Dataset Overview: This dataset contains information related to customer personality. It has various attributes including customer personal data, products, promotion, and place of transaction that contains information about number of purchases made from different places. This dataset has 29 columns. 
* Dataset: Customer Personality Analysis (https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis)
* Analysis Process:
# 1. Data Preparation
Before analyzing data, the first step that we usually do is data preparation. In this data preparation, we will gathering, assessing, and cleaning data. Here's the result from data preparation:
# a. Data Assessment
| Data Assessment |  Cleaning |
| :---            |           ---: |
| There are 24 missing values in 'Income'      |  Imputation using median    |
| No duplicated data        |  -      |
| There is an inaccurate value in the 'Dt_Cus tomer' data type       |  Convert the data type into datetime     |
| Outliers were found in some features, but there is one extreme value in a specific feature         |  handling missing value using IQR |

# b. Feature Engineering
In this step, we will creating new features such as: 
| Feature Engineering |
| :---             |
|Age: 2024 (this year) - Year_Birth|
|Children: Kidhome + Teenhome|
|Age_Desc: Grouping age based on the categories|
|Seniority: 2024 (this year) - Dt_Customer|
|Promotion: AcceptedCmp1 + AcceptedCmp2 + AcceptedCmp3 + AcceptedCmp4 + AcceptedCmp5|
|Frequency: NumDealsPurchases + NumWebPurchases + NumCatalogPurchases + NumStorePurchases|
|Monetary: MntWines + MntFruits + MntMeatProducts + MntFishProducts + MntSweetProducts + MntGoldProds|

# 2. RFM Analysis
From RFM analysis, we can gain information such as:
 -  **Gold** customer has the lowest recency, highest frequency and lowest monetary. This indicates their loyalty as customers, it's reflected in their frequent product purchases and short transaction periods.
 -  **Silver** customer has  low recency, low frequency, and low monetary. This indicates their loyalty too. Despite having the low monetary value, they have a high frequency of purchases and engage in transactions over relatively short periods.
 -  **Bronze** customer has moderate recency, low frequency, and high monetary. They may not make frequent purchases, but when they do, they contribute to the high value of their transactions.
 -  **Platinum** customer has the highest recency, low frequency, and higher monetary. Their frequent is small and long transaction periods, but when they do, they contribute to the high value of their transaction.
  
# 3. K-Means Clustering
In clustering, number of cluster (k) is important thing, so we should decide it from the beginning. For the optimal number of cluster, I'm using Elbow Method.
![Elbow](https://github.com/azzizahn/Customer-Segmentation-using-RFM-and-K-Means/assets/148351338/893d0102-0935-4f68-a04c-e212a0d6ae32)
From the plot above, we know that the optimal number of clusters (k) is 4. So, we're gonna use k = 4. And here's information that we gained from the clustering:
 -  **Cluster 0**  has low recency, low frequency and lowest monetary. This might indicate that they are new customers because the low recency and monetary.
 -  **Cluster 1** customer has the highest recency, low frequency, and low monetary. Customer in this cluster can be categorized as at-risk customer because they have higher recency than the previous cluster while their frequency and monetary remain almost the same.
 -  **Cluster 2** customer has high recency, high frequency, and the highest monetary. Customer in this cluster can be categorized as top spenders customer because of their significant spending
 -  **Cluster 3** customer has the lowest recency, highest frequency, and high monetary. Customer in this cluster can be categorized as loyal customer. It's reflected in their frequent transactions with high monetary amounts
 ![Income vs Monetary](https://github.com/azzizahn/Customer-Segmentation-using-RFM-and-K-Means/assets/148351338/9faf9ed2-a73f-437b-b48f-130e912af0fd)
From the scatter plot above, we can see that when the income higher, the monetary will go higher too. Cluster 0 and 1 on the left side with monetary that mostly under 500. Meanwhile cluster 2 and 3 on the right side with monetary upper than 500. 
We also can gain information from the other feature beside RFM using this cluster.
-  Promotion
![Promotion](https://github.com/azzizahn/Customer-Segmentation-using-RFM-and-K-Means/assets/148351338/d5f081a5-951f-47c0-b829-9e92d1d981d4)
From the plot, we can see that most of customer accepted the offer in the 1st campaign and cluster 0 is leading the bar, which means that most of customer who accepted the offer in the 1st campaign is from cluster 1. If cluster 0 is new customer then it's possible that they interested in the 1st campaign and being the new customer. The monetary also low, it's possible again because it's their first time purchasing the product. And if we see it further, cluster 2 and 3 keep accepting the offer until the fourth. It can be categorized as loyal customer. 
-  Marital Status and Children
![Marital and Children](https://github.com/azzizahn/Customer-Segmentation-using-RFM-and-K-Means/assets/148351338/58518cde-3174-4abb-89de-697b7d08ae04)
Married and having one children has the highest number comparing to others. Cluster 0 and 1 still leading the bar. 
-  Age Description and Number of Website Visit Last Month
![Age desc and web visit](https://github.com/azzizahn/Customer-Segmentation-using-RFM-and-K-Means/assets/148351338/ae3a7fe9-7fbe-4756-b391-a43f7c80af87)
From the old categories, we can see that old customer leading the bars. From the description, old customer is a customer who older than 45 years old. On the other side, from the web visits number last month cluster 0 and 1 mostly visits the web more than 5 times, meanwhile cluster 2 and 3 mostly under than 5 times. It might be cluster 2 and 3 only visit the web when they're already has a wishlist or target meanwhile cluster 2 and 3 still exploring the web.
# 4. Recommendation
-  For cluster 0, I think we should reduce the email letter frequency and personalized reccomendation based on the history. We also can add special offer and discounts for them.
-  For cluster 1, I think we should add the email letter frequency to add their engagement. We also can send them a form to asking their thought about us. So, we can know and analysis the reason why they're not engage with us in a long time. Add special offer and discount to the email letter too.
-  For cluster 2, I think we can send them the newest product based on their transaction history and something new that they never think of before.
-  For cluster 3, I think we should add the email letter frequency and send them the newest product based on their transaction or somethink new for them to explore.

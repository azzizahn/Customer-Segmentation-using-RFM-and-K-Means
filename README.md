# Customer-Segmentation-using-RFM-and-K-Means

Dataset Overview:
Dataset: Customer Personality Analysis (https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis)
Analysis Process:
# 1. Data Preparation
Before analyzing data, the first step that we usually do is data preparation. In this data preparation, we will gathering, assessing, and cleaning data. Here's the result from data preparation:
# a. Data Assessment
| Data Assessment |  Right-aligned |
| :---            |           ---: |
| There are 24 missing values in 'Income'      |  Imputation using median    |
| No duplicated data        |  -      |
| There is an inaccurate value in the 'Dt_Cus tomer' data type       |  Convert the data type into datetime     |
| Outliers were found in some features, but there is one extreme value in a specific feature         |  handling missing value using IQR |

# b. Feature Engineering
In this step, we will creating new features such as: 
|Age: 2024 (this year) - Year_Birth|
|Children: Kidhome + Teenhome|
|Age_Desc: Grouping age based on the categories|
|Seniority: 2024 (this year) - Dt_Customer|
|Promotion: AcceptedCmp1 + AcceptedCmp2 + AcceptedCmp3 + AcceptedCmp4 + AcceptedCmp5|
|Frequency: NumDealsPurchases + NumWebPurchases + NumCatalogPurchases + NumStorePurchases|
|Monetary: MntWines + MntFruits + MntMeatProducts + MntFishProducts + MntSweetProducts + MntGoldProds|

# 2. RFM Analysis
From RFM analysis, we can gain information such as:
  a. **Gold** customer has the lowest recency, highest frequency and lowest monetary. This indicates their loyalty as customers, it's reflected in their frequent product purchases and short transaction periods.
  b. **Silver** customer has  low recency, low frequency, and low monetary. This indicates their loyalty too. Despite having the low monetary value, they have a high frequency of purchases and engage in transactions over relatively short periods.
  c. **Bronze** customer has moderate recency, low frequency, and high monetary. They may not make frequent purchases, but when they do, they contribute to the high value of their transactions.
  d. **Platinum** customer has the highest recency, low frequency, and higher monetary. Their frequent is small and long transaction periods, but when they do, they contribute to the high value of their transaction.
  
# 3. K-Means Clustering
In clustering, number of cluster (k) is important thing, so we should decide it from the beginning. For the optimal number of cluster, I'm using Elbow Method.
![Elbow](https://github.com/azzizahn/Customer-Segmentation-using-RFM-and-K-Means/assets/148351338/893d0102-0935-4f68-a04c-e212a0d6ae32)
From the plot above, we know that the optimal number of clusters (k) is 4. So, we're gonna use k = 4. And here's information that we gained from the clustering:
  a. **Cluster 0**  has low recency, low frequency and lowest monetary. This might indicate that they are new customers because the low recency and monetary.
  b. **Cluster 1** customer has the highest recency, low frequency, and low monetary. Customer in this cluster can be categorized as at-risk customer because they have higher recency than the previous cluster while their frequency and monetary remain almost the same.
  c. **Cluster 2** customer has high recency, high frequency, and the highest monetary. Customer in this cluster can be categorized as top spenders customer because of their significant spending
  d. **Cluster 3** customer has the lowest recency, highest frequency, and high monetary. Customer in this cluster can be categorized as loyal customer. It's reflected in their frequent transactions with high monetary amounts
 ![Income vs Monetary](https://github.com/azzizahn/Customer-Segmentation-using-RFM-and-K-Means/assets/148351338/9faf9ed2-a73f-437b-b48f-130e912af0fd)
From the scatter plot above, we can see that when the income higher, the monetary will go higher too. Cluster 0 and 1 on the left side with monetary that mostly under 500. Meanwhile cluster 2 and 3 on the right side with monetary upper than 500. 
We also can gain information from the other feature beside RFM using this cluster.
a. Promotion
![Promotion](https://github.com/azzizahn/Customer-Segmentation-using-RFM-and-K-Means/assets/148351338/d5f081a5-951f-47c0-b829-9e92d1d981d4)
From the plot, we can see that most of customer accepted the offer in the 1st campaign and cluster 0 is leading the bar, which means that most of customer who accepted the offer in the 1st campaign is from cluster 1. If cluster 0 is new customer then it's possible that they interested in the 1st campaign and being the new customer. The monetary also low, it's possible again because it's their first time purchasing the product. And if we see it further, cluster 2 and 3 keep accepting the offer until the fourth. It can be categorized as loyal customer. 
b. Marital Status and Children
![Marital and Children](https://github.com/azzizahn/Customer-Segmentation-using-RFM-and-K-Means/assets/148351338/58518cde-3174-4abb-89de-697b7d08ae04)
Married and having one children has the highest number comparing to others. Cluster 0 and 1 still leading the bar
c. Age Description and Number of Website Visit Last Month
![Age desc and web visit](https://github.com/azzizahn/Customer-Segmentation-using-RFM-and-K-Means/assets/148351338/ae3a7fe9-7fbe-4756-b391-a43f7c80af87)

# 4. Recommendation

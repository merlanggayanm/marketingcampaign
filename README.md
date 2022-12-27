# Predict Customer Personality to Boost Marketing Campaign by Using Machine Learning
By processing historical marketing campaign data to improve performance and target the right customers so they can transact on the company's platform, from this data insight our focus is to create a cluster prediction model to make it easier for companies to make decisions.

## Dataset
---
Download dataset [here](https://drive.google.com/file/d/19TUlAkMBRQi4MKfimeYBxCrFSeYk0ZGr/view)

## Conversion Rate Analysis Based on Income, Spending, and Age
---
### Feature Engineering
Made some feature changes as follows:
1. `Total Children` = `Kidhome` + `Teenhome`
2. `Age` = 2022 – `Year_Birth`
3. `Age_Category` = `Age` < 16 (Children), `Age` < 30 (Youth Adults), `Age` < 45 (Middle-aged Adults), `Age` > 45 (Old-aged Adults)
4. `Total_Spend` = `MntCoke` + `MntFruits` + `MntMeatProducts` + `MntFishProducts` + `MntSweetProducts` + `MntGoldProds`
5. `Total_Purchase` = `NumDealsPurchases` + `NumWebPurchases` + `NumCatalogPurchases` + `NumStorePurchases`
6. `Total_Acc_Cmp` = `AcceptedCmp1` + `AcceptedCmp2` + `AcceptedCmp3` + `AcceptedCmp4` + `AcceptedCmp5`
7. `Conversion_Rate` = `Total_Purchase` / `NumWebVisitsMonth`

### Exploratory Data Analysis
![Google Drive Image](https://drive.google.com/uc?export=view&id=1gr0zImgRgLfE8N_targ6O_GUyYFjQaO6)
`Conversion_Rate` has a strong positive correlation with `Income` and `Total_Spend` where these columns also have a fairly strong correlation with `campaigns` so that they have greater potential to respond to campaigns.

![Google Drive Image](https://drive.google.com/uc?export=view&id=1f-bShXsp7EJnJJGA0-dd66VJ0XIR4PhQ)
The higher a person's `Income`, the higher the `Conversion_Rate`. With a high `Conversion_Rate`, the success of marketing is also high.

![Google Drive Image](https://drive.google.com/uc?export=view&id=1Fo9n0ScTOYyocqNxO8D__VEfRSPYekoA)
The higher a person's `Total_Spend`, the higher the `Conversion_Rate`. With a high `Conversion_Rate`, the success of marketing is also high.

![Google Drive Image](https://drive.google.com/uc?export=view&id=127mzenxpFoXPPiiY5TCB4oWDes3_7SOc)
There is no correlation between `Age_Category` and `Conversion_Rate`. Therefore, all people, both young and old can be used as marketing targets.

## Data Cleaning and Preprocessing
---
### Handling Missing Value
There is 1 column that has a Null/NaN value, namely `Income` of 24 rows. The column is filled based on the description of each column. Therefore, the `Income` column will be filled with the median value of that value.

### Handling Duplicated Data
There are no duplicate rows.

### Drop Columns
Dropping columns that are not needed in the modeling process, such as
`Unnamed: 0`, `ID`, `Year_Birth`, `Dt_Customer`, `Z_CostContact`, `Z_Revenue`, `Kidhome`, `Teenhome`, `MntCoke`, `MntFruits`, `MntMeatProducts`, `MntFishProducts`, `MntSweetProducts`, `MntGoldProds`, `NumDealsPurchases`, `NumWebPurchases`, `NumCatalogPurchases`, `NumStorePurchases`, `AcceptedCmp1`, `AcceptedCmp2`, `AcceptedCmp3`, `AcceptedCmp4`, `AcceptedCmp5`, `Age`.

### Feature Encoding
Make changes to the object data type to numeric type by using Label Encoding and One Hot Encoding as follows:
1. Label Encoding: `Education` (SMA : 0, D3 : 1, S1 : 2, S2 : 3, S3 : 4) and `Age_Category` (Children : 0, Youth Adults : 1, Middle-aged Adults : 2, Old-aged Adults : 3).
2. One Hot Encoding: `Marital_Status`.

### Feature Standarization
Perform transformation on the current data value in the same range in each column for numeric data.

## Data Modeling
---
### Elbow Method of K-means Clustering
![Google Drive Image](https://drive.google.com/uc?export=view&id=10qwAdharDt5JgFxXs0mGtC4Y_XjJMEjU)
By using the Elbow Method, the largest percentage decrease lies in the number of clusters 3 and 4. Here, 4 clusters are selected.


<p align="center">
  <img width="460" height="300" src="https://drive.google.com/uc?export=view&id=1HYJau0LNwv4l5aOr5LqXWn2VfwksG29f">
</p>

Clustering evaluation using the Silhouette Score obtained the highest score at number 3. However, the results of the evaluation with the number of clusters based on the Elbow Method were still relatively high.

## Customer Personality Analysis for Marketing Retargeting
---
### Cluster Summary
1. Risk of Churn
- This group is the group with the largest number of users, more than 1000 people, dominated by Old-aged Adults (> 45 years).
- In terms of income and expenses, this group has the smallest income and expenses each month, amounting to IDR 3.5 million and IDR 100 thousand respectively.
- This group still rarely makes transactions when visiting the website.

2. Low Spander
- This group is the group with the lowest number of users compared to other groups which are dominated by Middle-aged Adults (30-45 years) and Old-aged Adults (> 45 years).
- In terms of income and expenditure, this group has higher income and expenditure than the 'Risk of Churn' each month which is IDR 4.5 million and IDR 700 thousand respectively.
- This group is classified as the 'Risk of Churn' in terms of transactions.

3. Middle Spander
- This group is dominated by Middle-aged Adults (30-45 years) and Old-aged Adults (> 45 years).
- This group has the second largest total income and expenses compared to other groups, which are IDR 6.6 million and IDR 1 million respectively.
- There is an increase in the conversion rate of this group compared to 'Risk of Churn' and 'Low Spander'.

4. High Spander
- This group is dominated by Old-aged Adults (> 45 years).
- In terms of income and expenses, this group has the highest income and expenses each month, amounting to IDR 8 million and IDR 1.5 million respectively.
- This group is the group that has the largest conversion rate to buy our products.

### Recommendation
1. Keep monitoring the transactions and retention of the High Spender group. Focus on improving service so that these groups do not churn.
2. For the Mid Spender group, further analysis can be carried out on how to increase transactions by providing more personal recommendations and deeper analysis of how to optimize promos in this segment and keep shopping on our platform.
3. For the Low Spender and Risk to Churn groups, further analysis can also be carried out on how to increase the conversion rate.

# Quantium-Chips-Analysis
## 1. Business Objective
A leading supermarket partnered with Quantium to uncover **data-driven insights** to grow their **chips sales**. At the time, they lacked a clear understanding of customer purchasing behaviors, which made it challenging to design **targeted marketing campaigns** or test new store layouts effectively.  

This project bridges that gap by:  

- 🔍 **Analyzing purchase and transaction data** to uncover customer buying patterns.  
- 🏷️ **Segmenting customers with RFM analysis** (Recency, Frequency, Monetary) to identify high-value customer groups.  
- 🧪 **Designing an A/B testing plan** to select the best trial and control stores for a new store layout experiment.  

By turning raw data into actionable insights, this analysis helps the client **understand customers better, personalize marketing efforts, and boost sales and revenue in the chips category**. 

## 2. Data Overview & Preprocessing
### 2.1 Data Summary
There are two datasets, **Transaction Data** and **Purchase Behaviour** Data for this project. 
- **Transaction Data** contains **264258** rows

|Column             | Desctiption                               |
|-------------------|-------------------------------------------|
|`DATE`             | Transaction Date **Date**                 |
|`STORE_NBR`        | Unique Store Identifier **Integer**       |
|`LYLTY_CARD_NBR`   | Unique Loyalty Card Identifier **Integer**|
|`TXN_ID`           | Transaction Identifier **Integer**        |
|`PROD_NBR`         | Unique Product Identifier **Integer**     |
|`PROD_NAME`        | Name of Product **String**                |
|`PROD_QTY`         | Product Quantity **Integer**              |
|`TOT_SALES`        | Total Sales **Float**                     |

- **Purchase Behaviour Data** contains **72637** rows

|Column             | Desctiption                               |
|-------------------|-------------------------------------------|
|`LYLTY_CARD_NBR`   | Unique Loyalty Card Identifier **Integer**|
|`LIFESTAGE`        | The Lifestage of Customers **STRING**     |
|`PREMIUM_CUSTOMER` | The Types of Customers  **STRING**        |

### 2.2 Outlier Removal
To mitigate the impact of extreme values, we applied the interquartile Range (IQR) method to detect and remove extreme outliers from our dataset. 




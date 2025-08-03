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

|Column             | Description                               |
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

|Column             | Description                               |
|-------------------|-------------------------------------------|
|`LYLTY_CARD_NBR`   | Unique Loyalty Card Identifier **Integer**|
|`LIFESTAGE`        | The Lifestage of Customers **STRING**     |
|`PREMIUM_CUSTOMER` | The Types of Customers  **STRING**        |

### 2.2 Outlier Removal
To mitigate the impact of extreme values, we applied the **Interquartile Range (IQR) method** to detect and remove extreme outliers from our dataset. 

The left plot visualizes the distribution **before** outlier removal, where extreme values distort the scale and obscure underlying patterns. After applying the **Interquartile Range (IQR) method** to remove **578** extreme records, the distribution becomes more compact and symmetric.

<p align="center">
  <img src="https://github.com/zedli123/Quantium-Chips-Analysis/blob/main/Quantium/BeforeOutlier.png?raw=true" width="400"/>
  <img src="https://github.com/zedli123/Quantium-Chips-Analysis/blob/main/Quantium/AfterOutlier.png?raw=true" width="400"/>
</p>

> **Insight:** This preprocessing step ensures that our analysis and modeling are **less influenced by anomalies** and more accurately reflect the typical purchasing behavior of the majority of customers.

## 3. Exploartory Analysis
### 3.1 Holiday Season Trend
As shown in the left plot, **December had the highest total sales** of the year. To understand this trend, I examined the daily sales in December more closely.

The right plot reveals a **noticeable spike in sales leading up to Christmas**, followed by **no sales on Christmas Day**, likely due to store closures.

I also examined the daily sales in **November** to explore whether there was a similar upward trend leading up to Thanksgiving. However, there appears to be **no noticeable spike in sales prior to the Thanksgiving like Christmas**.

<p align="center">
  <img src="https://github.com/zedli123/Quantium-Chips-Analysis/blob/main/Quantium/totalsalesbymonth.png?raw=true" width="250"/>
  <img src="https://github.com/zedli123/Quantium-Chips-Analysis/blob/main/Quantium/totalsalesbymonthnov.png?raw=true" width="250"/>
  <img src="https://github.com/zedli123/Quantium-Chips-Analysis/blob/main/Quantium/totalsalesbydaysindec.png?raw=true" width="250"/>
</p>

> **Insight:** Sales significantly increased during the holiday season, peaking just before Christmas, highlighting a strong seasonal demand pattern.

### 3.2 Overview of Sales and Quantity Per Transaction

After taking a look at the holiday sales trends, I put together a table with some basic stats to give us a better sense of how chips were selling overall. These numbers also provide a helpful snapshot before diving deeper into the analysis.

| Metric                                 | Value |
|----------------------------------------|-------|
| **Average sales per transaction**      | 7.32  |
| **Minimum sales per transaction**      | 1.50  |
| **Maximum sales per transaction**      | 29.60 |
| **Average quantity per transaction**   | 1.90  |
| **Minimum quantity per transaction**   | 1     |
| **Maximum quantity per transaction**   | 7     |




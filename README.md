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
|`LIFESTAGE`        | The Lifestage of Customers **String**     |
|`PREMIUM_CUSTOMER` | The Types of Customers  **String**        |

### 2.2 Outlier Removal
To mitigate the impact of extreme values, we applied the **Interquartile Range (IQR) method** to detect and remove extreme outliers from our dataset. 

The left plot visualizes the distribution **before** outlier removal, where extreme values distort the scale and obscure underlying patterns. After applying the **Interquartile Range (IQR) method** to remove **578** extreme records, the distribution becomes more compact and symmetric.

<p align="center">
  <img src="https://github.com/zedli123/Quantium-Chips-Analysis/blob/main/Quantium/BeforeOutlier.png?raw=true" width="400"/>
  <img src="https://github.com/zedli123/Quantium-Chips-Analysis/blob/main/Quantium/AfterOutlier.png?raw=true" width="400"/>
</p>

> **Insight:** This preprocessing step ensures that our analysis and modeling are **less influenced by anomalies** and more accurately reflect the typical purchasing behavior of the majority of customers.

## 3. Exploartory Analysis
### 3.1 Overview of Sales and Quantity 

I put together a table with some basic stats to give us a better sense of how chips were selling overall. These numbers also provide a helpful snapshot before diving deeper into the analysis.
 
| Metric                                 | Value       |
|----------------------------------------|-------------|
| **Average sales per transaction**      | $7.32       |
| **Minimum sales per transaction**      | $1.50       |
| **Maximum sales per transaction**      | $29.60      |
| **Average daily sales**                | $5,279      |
| **Average quantity per transaction**   | 1.90 packs  |
| **Minimum quantity per transaction**   | 1 pack      |
| **Maximum quantity per transaction**   | 7 packs     |
| **Average daily quantity sold**        | 1,379 packs |

### 3.2 Holiday Season Trend
As shown in the left plot, **December had the highest total sales** of the year. To understand this trend, I examined the daily sales in December more closely.

The right plot reveals a **noticeable spike in sales leading up to Christmas**, followed by **no sales on Christmas Day**, likely due to store closures.

I also examined the daily sales in **November** to explore whether there was a similar upward trend leading up to Thanksgiving. However, there appears to be **no noticeable spike in sales prior to the Thanksgiving in November like Christmas**.

<p align="center">
  <img src="https://github.com/zedli123/Quantium-Chips-Analysis/blob/main/Quantium/totalsalesbymonth.png?raw=true" width="250"/>
  <img src="https://github.com/zedli123/Quantium-Chips-Analysis/blob/main/Quantium/totalsalesbymonthnov.png?raw=true" width="250"/>
  <img src="https://github.com/zedli123/Quantium-Chips-Analysis/blob/main/Quantium/totalsalesbydaysindec.png?raw=true" width="250"/>
</p>

> **Insight:** Sales significantly increased during the holiday season, peaking just before Christmas, highlighting a strong seasonal demand pattern.
>

### 3.3 Comparison Across Brands and Pack Size

#### Top Selling Brand
Kettle is the top-performing chip brand, generating approximately **$390,239** in total revenue — nearly **double** that of the second-best-selling brand. It alone contributes to **21% of total chip sales**, making it the most critical brand to prioritize for restocking.

The top four brands — **Kettle**, **Doritos**, **Smiths**, and **Pringles** — together account for just over **50% of total chip revenue**, highlighting their overall importance in driving sales.

On the other hand, the **French Fries** and **Burger** brands each contribute less than **1%** of total revenue, indicating a relatively minor role in overall performance.

#### Most Popular Pocket Size
The most popular packet size is **175g**, contributing to **27%** of total chip revenue.  

This is followed by the **150g** size, which accounts for **17%**, and the **134g** size, contributing **10%** of total revenue.

These three sizes alone make up over half of the total chip sales, indicating a strong customer preference for medium-sized chip packets.

<p align="center">
  <img src="https://github.com/zedli123/Quantium-Chips-Analysis/blob/main/Quantium/totalsizebybrands.png?raw=true" width="400"/>
  <img src="https://github.com/zedli123/Quantium-Chips-Analysis/blob/main/Quantium/totalsizebypacksize.png?raw=true" width="400"/>
</p>

## 4.Customer RFM Analysis

This table gives a quick summary of customer behavior by lifestage using three key metrics:

- **Recency**: How many days since the last purchase  
- **Frequency**: Average number of transactions per customer  
- **Monetary**: Total chip sales from each group  

| Lifestage                 | Avg. Recency (days) | Avg. Frequency | Total Sales ($) |
|---------------------------|---------------------|----------------|-----------------|
| OLDER SINGLES/COUPLES     | 182.65              | 3.73           | 402,426.75      |
| OLDER FAMILIES            | 182.02              | 4.97           | 352,467.20      |
| RETIREES                  | 181.89              | 3.36           | 366,470.90      |
| MIDAGE SINGLES/COUPLES    | 181.87              | 3.45           | 184,751.30      |
| YOUNG SINGLES/COUPLES     | 181.86              | 2.52           | 260,405.30      |
| YOUNG FAMILIES            | 181.59              | 4.75           | 316,160.10      |
| NEW FAMILIES              | 179.88              | 2.71           | 50,433.45       |

#### What This Tells Us
- **Older Singles and Couples** spend the most on chips overall — even more than retirees and families. This suggests that older individuals might buy chips more often or in larger amounts, possibly for convenience or personal enjoyment.

- **Families (both older and younger)** shop the most frequently. They come back more often than singles or couples, likely because chips are a regular household snack.

- **New Families** stand out as an under-engaged group. They buy less often and spend less overall, which might mean they’re newer customers or just not as interested in chips. This could be a good group to target with promotions or tailored campaigns.

- **Overall**, the data gives us a clearer picture of who the top chip buyers are — and where there might be room to grow. It highlights some interesting differences between life stages and shows how this kind of segmentation can help tailor marketing and inventory decisions.





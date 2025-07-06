# Python-RFM-Analysis-SuperStore-Global-Retail-Company

**Author:** Mai Ngoc Chau (Chann)

**Date:** 2025-05-26

**Tool used:** Python (Google Colab)

## 📑 Table of Contents
- [📌 Background & Overview](#-background--overview)
- [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)
- [⚒️ Process](#-process)
- [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)


## 📌 Background & Overview
### **Context:**

SuperStore is a <b>global retail company</b>, offers a wide variety of products, including <b>groceries, household goods, electronics, clothing, and more.</b>

On the occasion of Christmas and New Year, the Marketing department wants to <b>launch customer appreciation campaigns and exploit potential customer groups</b>. However, because the data this year is too large, it is not possible to manually segment as before.

The Data Analysis department is asked to support customer segmentation, using the <b>RFM model</b>. Previously, the team could do it on Excel, but now it is necessary to build an automatic segmentation process using Python to accommodate large data volumes.

### **Objectives:**
This project will use transacstional dataset to:
*   Build an **RFM-based customer segmentation**
*   Segment into 11 RFM segments: Champions, Loyal, Potential Loyalists, New Customers, Promising, Need Attention, About To Sleep, At Risk, Cannot Lose Them, Hibernating, Lost
*   Advice for Marketing & Sales: **which groups to focus on, and which metrics to base on (R/F/M)**
*   Additional analysis into customer segments insights
*   **Recommendations on how to launch marketing campaign to the right customer segment**

### **Who is this project for:**
* Data analysts & business analysts
* Sales, Marketing decision-makers, team leaders, managers.

## 📂 Dataset Description & Data Structure

### Data source
* Source: The data was provided by the SuperStore Sales Department, or Sales system.
* Size: 1 table, 541909 rows, 8 columns
* Format: .xlsx file

### Data Structure & Relationships
**1. Tables Used:**

This is a transactional dataset which contains all the transactions occurring between 01/12/2010 and 09/12/2011. The company mainly sells unique **all-occasion gifts**. Many customers of the company are wholesalers.

Table name: ecommerce retail.xlsx

**2. Table Schema & Data Snapshot:**

| Column      | Description |
| ----------- | ----------- |
| InvoiceNo   | Invoice number. Nominal, a 6-digit integral number uniquely assigned to each transaction. If this code starts with letter 'C', it indicates a cancellation.|
| StockCode   | Product (item) code. Nominal, a 5-digit integral number uniquely assigned to each distinct product.|
| Description | Product (item) name. Nominal.|
| Quantity    | The quantities of each product (item) per transaction. Numeric.|
| InvoiceDate |Invoice Date and time. Numeric, the day and time when each transaction was generated.|
| UnitPrice   |Numeric, Product price per unit in sterling.|
|CustomerID   |Nominal, a 5-digit integral number uniquely assigned to each customer.|
|Country      | Country name. Nominal, the name of the country where each customer resides.|
     
**Preview data**
| InvoiceNo | StockCode | Description | Quantity | InvoiceDate | UnitPrice | CustomerID | Country |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 536365 | 85123A | WHITE HANGING HEART T-LIGHT HOLDER | 6 | 2010-12-01 08:26:00 | 2.55 | 17850.0 | United Kingdom |
| 536365 | 71053 | WHITE METAL LANTERN | 6 | 2010-12-01 08:26:00 | 3.39 | 17850.0 | United Kingdom |
| 536365 | 84406B | CREAM CUPID HEARTS COAT HANGER | 8 | 2010-12-01 08:26:00 | 2.75 | 17850.0 | United Kingdom |
| 536365 | 84029G | KNITTED UNION FLAG HOT WATER BOTTLE | 6 | 2010-12-01 08:26:00 | 3.39 | 17850.0 | United Kingdom |
| 536365 | 84029E | RED WOOLLY HOTTIE WHITE HEART. | 6 | 2010-12-01 08:26:00 | 3.39 | 17850.0 | United Kingdom |

## ⚒️ Process
### ✅ Summary
**1. EDA Process Summary**
- <b>Load data:</b> The data covers over 541,000 transaction lines from 2010 to 2011, belonging to an online retail company primarily operating in the UK.
- <b>Check data type:</b>
  - Change ['CustomerID'] from float to int
  - Identify 2 columns with abnormal values (['Quantity'] and ['UnitPrice'] < 0) --> Most of the negative ['Quantity'] values ​​belong to canceled orders, so it is necessary to classify successful orders and canceled orders. There are only 2 rows where ['UnitPrice'] < 0.
- <b>Identify missing values:</b> There are missing values in 2 columns: ['CustomerID'] & ['Description'] --> drop missing in ['CustomerID'], ignore ['Description'].
- <b>Identify duplicates:</b> 5192 duplicates found --> drop

**2. RFM Analysis Summary**
- **RFM Classification**
  - Create an RFM (Recency, Frequency, Monetary) table for each customer.
  - RFM is calculated in 2011-12-31 --> Recency is calculated the gap between the latest purchase date and 2011-12-31
  - Recency then is converted into negative values for better cohensive analysis.
  - Frequency is the total times purchase for each customer
  - Monetary is the total amount that a customer spent
  - Apply customer clustering into 11 RFM groups: Champions, Loyal, Lost,...
- **Explore which metrics should we focus on? R, F or M?**
  - Check distribution of Recency, Frequency, Monetary by histogram
  - Check correlation of R-score, F-score, M-score
  - Check AVG Monetary by Recency and Frequency
  - Scatterplot between R, F & M
- **Visualize to understand customer segmentation:**
  - Customer Segment Distribution
  - Total Revenue by Customer Segment (Millions)
  - Treemap of Customer Segments in countries
  - Evaluate R, F & M in each customer segment
    
### ✅ Visualize Result 
**1. Explore which metrics should we focus on?**

![img1](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/R-F-M%20Distribution.png)
![img2](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/1.2.frequency%20dist.png)
![img3](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/1.3.monetary%20dist.png)

![img4](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/Correlation%20heatmap%20between%20R%2CF%20and%20M.png)

![img5](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/3.%20avg%20money%20by%20frequency.png)
![img6](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/4.%20avg%20money%20by%20recency.png)
![img7](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/5.%20scatter%20plot%20MR.png)
![img8](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/6.%20scatter%20MF.png)

&rarr; F_score and M_score have the strongest correlation.

&rarr; Scatter plot shows that although there is hardly a clear correlation between F and M, there are some data points indicating customer who purchases many times still contribute less money.

&rarr;  The marketing department should focus on F & M metrics.

**2. Visualize to understand customer segmentation**

![img9](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/7.%20customer%20segment%20distribution%20and%20revenue%20per%20segment.png)
![img10](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/8.%20customer%20distribution%20and%20revenue%20combined.png)

- **Champions are the most prominent customer group:** They generate the highest revenue (~$3,521 million) and have the highest number of customers (~82,617)
- **Hibernating customers are the second largest in number (~81,235)**, but only generate $124 million, indicating that this group is of low value and should be considered for “awakening”.
- Groups such as At Risk and Loyal, although smaller in number, contribute much more revenue than other groups → potential to be nurtured into Champions.
- The Lost group has a high number of customers but low revenue → likely to be customers who have left or are not active for a long time.

![img11](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/9.Recency%20Treemap%20of%20Customer%20Segments%20in%20UK.png)
![img12](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/10.%20Recency%20Treemap%20of%20Customer%20Segments%20in%20Ger.png)
![img13](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/11.%20Recency%20Treemap%20of%20Customer%20Segments%20in%20FR.png)

Based on the three treemaps, it can be seen that **Champions is the highest revenue group in France, Germany and the UK**, with a particularly strong presence in the UK. Meanwhile, **Loyal and At Risk play a significant role in France and Germany but are less prominent in the UK**. 

**Germany has a more even distribution** of spend across groups than the other two countries, while the **UK relies more heavily on its most loyal customers**. The Need Attention group also has a significant presence in Germany, suggesting the potential for recovery if nurtured properly. 

These differences suggest that customer retention strategies need to be tailored to each market.

Respectively, purchase frequency among segments is quite like the revenue contributed.

![img14](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/12.%20Frequency%20Treemap%20of%20Customer%20Segments%20in%20UK.png)
![img15](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/13.%20Frequency%20Treemap%20of%20Customer%20Segments%20in%20Ger.png)
![img16](https://github.com/Channpate/Python-RFM-Analysis-SuperStore-Global-Retail-Company/blob/ae40b92580c6999f2934a5b2530e87f3cca1f0b7/Visual%20Chart/14.%20Frequency%20Treemap%20of%20Customer%20Segments%20in%20France.png)



## 🔎 Final Conclusion & Recommendations

1.   The <b>“Champions” and “Loyal”</b> customer groups are contributing a large portion of revenue and have made frequent purchases recently. They are brand lovers and have the ability to spread the word. --> Organize gratitude programs (VIP incentives, gifts) for Champions and Loyal.
2.   Groups like **“At Risk”, “Lost” or “Hibernating”** are customers who used to interact, but are now quiet. Some of them may have forgotten about us, or are waiting for a reason to come back. --> Need a call to action: Send personalized emails and limited-time promotions to activate your At Risk, Lost group.
3. The chart shows that **high spenders are also recent buyers – and vice versa**. This further confirms that retaining existing customers is much more valuable than acquiring new ones.
For high spenders, continue to nurture them: prioritize service, reward points, or personalize product recommendations.
4. The data shows that SuperStore’s three largest markets are the UK, the Netherlands and Germany – and customer behaviour is different in each.
* In the UK, there are a lot of “Champions” and “Loyals” → This is a market ripe for a loyalty programme.
* In Germany, there are a lot of “Hibernating” → Try a focused reactivation campaign, perhaps with a small gift.
* In the Netherlands, there are a lot of “Potential Loyalists” → This is a potential place to convert new customers into loyal customers if nurtured properly.

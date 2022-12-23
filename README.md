## Customer Segmentation with RFM/Clustering Techniques & Association Rule Mining with Apriori Algorithms

![banner](/images/banner.jpg)


## INTRODUCTION

### This project is divided into two parts :

a) **Finding customer segments through RFM techniques and comparing segment with ML clustering techniques — K-Means, Hierarchical and DB Scan**. - Combine the purchasing data, demographics and location data with RFM, K-means and Market basket Analysis to help retailers to break down large customer profiles into much smaller segments and to gain insights into granular behavior of customers. The results of this part can be used for developing a **targeted marketing** strategy for the company.

b) **Association Rule mining  -** Finding item sets that are bought frequently together using association rule analysis (Apriori Analysis). The results could be used for developing a shopping cart **recommendation system** or **store layout planning**.

## DATA OVERVIEW AND PREPROCESSING

*File : OnlineRetail.ipynb*

- The [Dataset](https://archive.ics.uci.edu/ml/machine-learning-databases/00352/) used in the analysis is the Online Retail transnational data which contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail.
- The company mainly sells unique all-occasion gifts. Many customers of the company are wholesalers.
- The file has 541909 observations and 8 variables (Invoice No, Stock Code, Description, Quantity, Invoice Date, Unit Price, Customer ID, Country)
- On observing the data summary, the minimum values of quantity and unit price are negative meaning that some transactions were returns.
- On checking further for few more conditions like:
       a) Quantity < 0 & Unit Price < 0   —  0 rows
       b) Quantity < 0 | Unit Price = 0  —  1336 rows
       c) Quantity == 0 | Unit Price < 0   — 0 rows
- I removed negative and zero unit price, negative quantity rows, rows with null customer ID
- Removed duplicate item descriptions, and credit card transactions.
- At the end of cleaning, 133359 rows were left.

## APPROACH

### Clustering and Customer Segmentation 

[*File : CustomerSegmentRFM&Clustering.ipynb*](https://nbviewer.org/github/saniya-k/Market-Basket-Analysis/blob/master/CustomerSegmentRFM%26Clustering.ipynb
)

1. Engineered features - day_since (Recency), Frequency (number of transactions), Monetary value (total invoice price) for each customer ID.
2. Using binning generated R_score, F_score and M_score and aggregated RFM_score.
3. Used this [link](https://www.r-bloggers.com/2019/07/customer-segmentation-using-rfm-analysis/) to assign customer type based on RFM score. Results :

![customer_segments](/images/customer_segments.png)

 ![rfm_3d](/images/rfm_segments.png)

 4. Transformed and standardized variables.

 5. Used elbow plots, silhouette plots to find best k value. K- means clustering was giving the best results at k=3 and better separation than Hierarchical and DB-Scan clustering.

6. Used snake plots to compare RFM segments and K-means segments. 

### Association Analysis

[*File : OnlineRetail.ipynb*](https://nbviewer.org/github/saniya-k/Market-Basket-Analysis/blob/master/OnlineRetail.ipynb)

1. Found the top 3 countries by transactions, subset the data to these 3 countries only.
2. Used Apriori algorithm to find frequent itemset and rules.
3. Found top 5 rules for each country and used networkx library to draw the top  rules e.g.:

![france_top5](/images/france_top.png)

## CONCLUSION & LIMITATIONS

- People in cluster 1 are generating highest profit value whereas people in cluster 0 are generating least value. Further consumer analysis using consumer demographic data can be done to increase profitability across all clusters and to develop marketing strategy to enhance consumer experience for people in cluster 0.
- The Apriori algorithm is a computationally expensive task, hence was done country wise. FP growth might have given better results for the entire geographic domain where the retailer sells.
- For Association rule mining, the goal was to identify rare definitive combinations of items thus low support and high lift thresholds values were taken to highlight cross selling opportunities in highest selling regions.
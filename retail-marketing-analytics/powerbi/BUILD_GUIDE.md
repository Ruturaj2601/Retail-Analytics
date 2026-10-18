# Power BI build guide

1. **Load** (Get data > Text/CSV): `data/processed/cleaned_retail_sales.csv`, `customer_segments.csv`, `customer_clv.csv`, `monthly_kpis.csv`, and `reports/cohort_retention.csv`.
2. **Types** (Transform data): Order_Date, Ship_Date, First_Purchase, Last_Purchase = Date. Revenue, Profit, Monetary, CLV_Simple = Fixed decimal.
3. **Model**: Dim_Date[Date] -> cleaned_retail_sales[Order_Date]; customer_segments[Customer_ID] 1 -> * cleaned_retail_sales[Customer_ID]; customer_clv[Customer_ID] 1 -> 1 customer_segments[Customer_ID]. Single direction.
4. **Theme**: View > Themes > Browse for themes > `FinanceTheme.json`. **Measures**: paste each line of `measures.dax`.
5. **Pages**
| Page | Visuals |
|---|---|
| Executive overview | Cards: Total Revenue, Total Profit, Profit Margin %, Total Orders, AOV, Customers. Line: Dim_Date[Month] x Total Revenue + Total Profit. Bar: Product_Category x Total Revenue. Map or bar: Region x Total Revenue. Slicers: Segment, Region, Date |
| Customers | Bar: customer_segments[Customer_Segment] x RFM Customers. Clustered column: Cluster_Name x RFM Customers and VIP Revenue Share %. Scatter: Recency (x), Frequency (y), size Monetary. Matrix heatmap from cohort_retention (unpivot M0..M13 columns in Power Query) |
| Products | Treemap: Product_Category > Product_Sub_Category x Total Revenue. Table: top products by revenue |
| Value | Cards: Median CLV, Mean CLV, Churn Rate %, Repeat Customer Rate %. Column: CLV_Category x Median CLV |
6. **Checks**: Total Revenue 1,078,671 | Total Profit 198,275 | Orders 10,000 | Customers 1,986 | Median CLV 2,341 | Churned (180+ days) 216 | Repeat Customer Rate 96.3%.

# Customer_Segmentation-and-outliers_analysis using RFM model

The purpose of this project is to conduct a Customer Segmentation Analysis for an Online retail company. Customer segmentation is performed by developing a RFM Model. RFM (Recency, Frequency, Monetary) analysis is a behavior-based approach grouping customers into segments. It groups the customers on the basis of their previous purchase transactions. In this analysis the customer segment was divided into 9 distinct groups. The analysis will help in determining which customers segments should be targeted in order to enhance sales revenue for the company. 


## Objective

•	Customer Segmentation Analysis for an Online Retail Company using the RFM (Recency, Frequency, Monetary) Model

•	This segmentation enables the company to identify high-value customers, re-engage inactive ones, and tailor marketing strategies to maximize customer retention and sales revenue.

## Data Exploration

Initial steps in deriving insights involve cleaning and exploring the dataset. 

Key issues identified:

    Null values in the CustomerID column.
    Negative values in the Quantity column.
    InvoiceNo includes letters such as ‘A’ and ‘C’ along with digits.
    StockCode contains non-numeric values and inconsistent formats.

## Data Cleaning


Steps taken for data preparation:

    Creating a deep copy of the dataset to preserve the original 
    After converting the Invoice column to string, using the regex match, filtering only the invoice having 6 digits 
    Filtered StockCode to keep entries that are either 5 digits or contain valid suffixes like PADS.
    Dropped all the null values of the customer ID column
    Filtered out transactions with non-positive prices.
    Post-cleaning, retained 77% of the original dataset for clustering analysis.

## Feature Engineering

To implement RFM-based clustering:

    Created SalesLineTotal = Quantity × Price.
    Aggregated by CustomerID:
        *Monetary: Sum of SalesLineTotal
        *Frequency: Count of unique InvoiceNo
        *Recency: Difference between max invoice date and each transaction date
    Histograms showed Monetary and Frequency are skewed.
    Boxplots revealed many outliers, likely high-value customers.
    Outliers were separated into a different DataFrame using 1.5 * IQR and preserved for later merging.
    3D scatter plots were created for RFM features.
    Used StandardScaler to normalize RFM data.

## KMeans Clustering

    Ran a loop over range(2, 13) to find optimal K using Inertia.
    Elbow plot indicated potential at K = 4 or 5.
    Used Silhouette Score to validate clustering quality.
    Final K chosen: K = 4
    Visualized clusters using:
       3D scatter plot
       Violin plots for RFM metrics across clusters

## Outliers Clustering

    Separated outliers:
        MonetaryValue_only_outliers
        Frequency_only_outliers
    Removed overlapping customers between outlier groups
    Assigned labels -1, -2, -3 (negative labels indicate outliers)
    Merged all outlier clusters into outliers_cluster_df
    Combined outliers and core clusters labels into a final DataFrame and exported

    

## Visualisation
    
    Created bar plot for cluster labels vs value counts
    Used twin axes to overlay average RFM values per cluster using a line plot

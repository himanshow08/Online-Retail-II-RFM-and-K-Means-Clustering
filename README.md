# Customer Segmentation for E-Commerce

---

## 1. Problem Statement & Business Goal

### Problem Statement
Retail and e-commerce businesses often struggle with one-size-fits-all marketing strategies, leading to inefficient ad spend and low customer engagement. A data-driven approach is necessary to categorize customers based on their behavior, allowing for personalized campaigns and targeted retention efforts.

### Business Goal
The primary objective of this project is to build a customer segmentation model using K-Means clustering. The model segments customers based on RFM (Recency, Frequency, Monetary) metrics and other key behavioral features (Average Order Value, Average Basket Size, Product Diversity) to achieve the following:
* Identify high-value customers for loyalty programs.
* Target "at-risk" customers with reactivation campaigns.
* Personalize product recommendations.
* Optimize marketing spend by focusing on the right segments.

---

## 2. Dataset Source

This project uses the **Online Retail II Dataset** from the UCI Machine Learning Repository, made available on Kaggle.

* **Source Platform:** Kaggle
* **Full Citation:** UCI/Kaggle. (n.d.). *Online Retail II [Dataset]*. Retrieved from: `https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci`
* **Data Content:** This dataset contains transactional data from 2009 to 2011 for a UK-based online retailer.

---

## 3. Project Workflow & Analysis Summary

The project is contained within the `online_retail_loader.ipynb` notebook and follows these steps:

1.  **Data Acquisition:** The dataset is loaded directly from Kaggle using the `kagglehub` API to ensure reproducibility.
2.  **Data Cleaning:** The raw data was extensively cleaned by:
    * Dropping rows with missing `Customer ID`s (essential for segmentation).
    * Removing duplicate transactions.
    * Handling `Quantity` and `Price` issues by removing returns (invoices starting with 'C') and non-positive values.
    * Filtering out non-product `StockCode` entries (e.g., 'POST', 'M', 'ADJUST').
3.  **Feature Engineering:** Transaction-level data was aggregated to the customer level to create 6 key features as defined in the proposal:
    * `Recency`: Days since the customer's last purchase.
    * `Frequency`: Total number of unique invoices.
    * `Monetary`: Total money spent by the customer.
    * `Avg_Basket_Size`: Average number of items per transaction.
    * `Avg_Order_Value`: Average monetary value per transaction.
    * `Product_Diversity`: Count of unique products purchased.
4.  **Data Transformation:** To prepare the data for K-Means clustering, the highly skewed features were first normalized using a **log transformation** (`np.log1p`) and then scaled using `StandardScaler`.
5.  **Modeling (Phase 3):**
    * **K-Means Clustering** was applied.
    * The **Elbow Method** (WCSS), **Silhouette Score**, and **Davies-Bouldin Score** were used to find the optimal $k$.
    * **$k=4$** was chosen as the final model, as it provided the most distinct and actionable business segments, balancing statistical metrics with high interpretability.
6.  **Segment Analysis (Phase 3 Results):**

---

## 4. Tools & Libraries

This project uses Python 3 and relies on the following key libraries. A `requirements.txt` file is included for easy environment setup.

* `kagglehub`: For data acquisition.
* `pandas` & `numpy`: For data manipulation and feature engineering.
* `scikit-learn` (sklearn): For `StandardScaler`, `KMeans`, and evaluation metrics.
* `matplotlib` & `seaborn`: For data visualization (EDA and cluster analysis).

---

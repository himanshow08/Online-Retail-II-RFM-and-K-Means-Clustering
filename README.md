# Customer Segmentation for E-Commerce

---

## 1. Problem Statement & Business Goal

### Problem Statement
[cite_start]Retail and e-commerce businesses often struggle with one-size-fits-all marketing strategies, leading to inefficient ad spend and low customer engagement[cite: 41]. [cite_start]A data-driven approach is necessary to categorize customers based on their behavior, allowing for personalized campaigns and targeted retention efforts[cite: 43].

### Business Goal
[cite_start]The primary objective of this project is to build a customer segmentation model using K-Means clustering[cite: 45]. [cite_start]The model segments customers based on RFM (Recency, Frequency, Monetary) metrics and other key behavioral features (Average Order Value, Average Basket Size, Product Diversity) to achieve the following [cite: 45, 49-53]:
* Identify high-value customers for loyalty programs.
* Target "at-risk" customers with reactivation campaigns.
* Personalize product recommendations.
* Optimize marketing spend by focusing on the right segments.

---

## 2. Dataset Source

This project uses the **Online Retail II Dataset** from the UCI Machine Learning Repository, made available on Kaggle.

* [cite_start]**Source Platform:** Kaggle [cite: 56]
* **Full Citation:** UCI/Kaggle. (n.d.). *Online Retail II [Dataset]*. Retrieved from: `https:
* [cite_start]**Data Content:** This dataset contains transactional data from 2009 to 2011 for a UK-based online retailer[cite: 55].

---

## 3. Project Workflow & Analysis Summary

The project is contained within the `online_retail_loader.ipynb` notebook and follows these steps:

1.  [cite_start]**Data Acquisition:** The dataset is loaded directly from Kaggle using the `kagglehub` API to ensure reproducibility[cite: 70].
2.  [cite_start]**Data Cleaning:** The raw data was extensively cleaned by[cite: 71]:
    * Dropping rows with missing `Customer ID`s (essential for segmentation).
    * Removing duplicate transactions.
    * Handling `Quantity` and `Price` issues by removing returns (invoices starting with 'C') and non-positive values.
    * Filtering out non-product `StockCode` entries (e.g., 'POST', 'M', 'ADJUST').
3.  [cite_start]**Feature Engineering:** Transaction-level data was aggregated to the customer level to create 6 key features as defined in the proposal [cite: 45-48, 73]:
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
    * **$k=3$** was chosen as the final model, as it provided the most distinct and actionable business segments, balancing statistical metrics with high interpretability.
    .
6.  **Segment Analysis (Phase 3 Results):**
    The $k=3$ model yielded three clear customer personas:
    * **Cluster 1 (High-Value Champions):** (1,779 customers) Very recent, highly frequent, and highest spending.
    * **Cluster 2 (At-Risk Mid-Value):** (2,472 customers) Lapsed (235 days recency) but with good historical value.
    * **Cluster 0 (Lapsed Low-Value):** (1,602 customers) Deeply lapsed (320 days recency) and low spending.

---

## 4. Tools & Libraries

This project uses Python 3 and relies on the following key libraries. A `requirements.txt` file is included for easy environment setup.

* `kagglehub`: For data acquisition.
* `pandas` & `numpy`: For data manipulation and feature engineering.
* `scikit-learn` (sklearn): For `StandardScaler`, `KMeans`, and evaluation metrics.
* `matplotlib` & `seaborn`: For data visualization (EDA and cluster analysis).

---

## 5. How to Run

1.  **Set up the environment:**
    * Ensure you have Python 3 installed.
    * Install the required libraries:
        ```sh
        pip install -r requirements.txt
        ```
    * Make sure you have a `kaggle.json` API token in the correct location (e.g., `~/.kaggle/kaggle.json`) for `kagglehub` to authenticate.

2.  **Run the Notebook:**
    * Open `online_retail_loader.ipynb` in Jupyter Notebook, VS Code, or Google Colab.
    * Run all cells sequentially from top to bottom.

3.  **Deliverables:**
    * `online_retail_loader.ipynb`: The main notebook containing all analysis (Phases 1-3).
    * `Project_Proposal_Phase-1.pdf`: The approved project proposal.
    * `requirements.txt`: List of library dependencies.
    * `README.md`: This file.
    * (Phase 4 deliverables - Dashboard & PPT - will be added here upon completion).

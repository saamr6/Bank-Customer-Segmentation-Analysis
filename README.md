# Bank-Customer-Segmentation-Analysis
A project performing customer segmentation on the Bank Churn dataset using K-Means clustering.

## 1. Project Overview

This project analyzes a bank churn dataset to understand the key characteristics of different customer groups. The final goal is to use an unsupervised machine learning algorithm (K-Means) to segment customers into distinct clusters based on their banking behavior and demographics.

The analysis is conducted in a Jupyter Notebook and follows this workflow:
* Data Cleaning and Preparation
* Feature Scaling
* Clustering Model Building (K-Means)
* Determining the Optimal Number of Clusters
* Cluster Profiling and Analysis

## 2. Dataset

The dataset used includes the following key columns:
* `CreditScore`
* `Geography` (France, Spain, Germany)
* `Gender` (Male, Female)
* `Age`
* `Tenure` (Number of years as a customer)
* `Balance` (Bank balance)
* `NumOfProducts` (Number of products a customer has)
* `HasCrCard` (1 if yes, 0 if no)
* `IsActiveMember` (1 if yes, 0 if no)
* `EstimatedSalary`
* `Exited` (The churn variable: 1 if they left, 0 if they stayed)

*Note: `Exited` was not used to build the clusters (as K-Means is unsupervised), but was used *after* clustering to analyze the churn behavior of each segment.*

## 3. Analysis and Clustering Workflow

The analysis and modeling process revealed several key steps and insights:

**Step 1: Data Preparation**
Categorical features (`Geography`, `Gender`) were converted into numerical format using one-hot encoding. Unnecessary columns (`CustomerId`, `Surname`) were dropped.

**Step 2: Feature Scaling**
K-Means is sensitive to the scale of features. Therefore, all features were scaled using `StandardScaler` from scikit-learn. This ensures that features like `Balance` do not dominate features like `Age` or `NumOfProducts`.

**Step 3: Determining Optimal Clusters (K)**
The **Elbow Method** and **Silhouette Score** were calculated for a range of cluster numbers. Based on these metrics, $k=6$ was chosen as the optimal number of clusters, providing a good balance between cluster separation and a meaningful number of segments.

## 4. Clustering Model and Results

A K-Means model was trained to group the customers into 6 distinct clusters.

**Model: K-Means Clustering**
* **Purpose:** To partition customers into $k$ distinct, non-overlapping groups. The algorithm groups data points based on their feature similarity (Euclidean distance).
* **Result:** The model successfully segmented customers into 6 clusters with highly distinct profiles.

**Key Cluster Insights:**

* **Insight 1: Gender as a Primary Splitter:** The model found `Gender` to be a major differentiating feature. Clusters 1 & 2 were 100% Female, while Clusters 3, 4, & 5 were 100% Male. Cluster 0 was mixed.

* **Insight 2: Identification of "Loyal" Segments:**
    * **Cluster 4 (Loyal Males):** This group has the lowest churn rate in the dataset at only **7.8%**.
    * **Cluster 2 (Loyal Females):** This group also shows high loyalty with a low churn rate of **15.9%**.

* **Insight 3: Identification of "At-Risk" Segments:**
    * **Cluster 1 (High-Risk Females):** This segment has a very high churn rate of **33.2%**.
    * **Cluster 5 (High-Risk Males):** This male segment is also a high churn risk, with an `Exited` rate of **31.0%**.

* **Insight 4: The "High-Product" Segment:**
    * **Cluster 0 (Mixed Gender, High-Product Users):** This group is unique for having a significantly higher average number of products (`product_per_year` of 2.04). Their churn rate is moderate at **18.3%**.

## 5. Tools Used

* **Python 3**
* **Jupyter Notebook**
* **Pandas:** For data manipulation and analysis.
* **NumPy:** For numerical operations.
* **Matplotlib / Seaborn:** For data visualization.
* **Scikit-learn (sklearn):** For building and evaluating the clustering model (`KMeans`, `StandardScaler`, `silhouette_score`).

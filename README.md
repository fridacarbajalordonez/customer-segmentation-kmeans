# Customer Segmentation & Clustering Analysis

## Project Overview

This project develops an end-to-end customer segmentation analysis using **Python and K-Means clustering** to identify distinct customer profiles based on purchasing behavior, income, campaign responsiveness, and digital engagement.

The analysis follows a complete data science workflow, from exploratory data analysis and data cleaning to feature engineering, clustering evaluation, customer profiling, and business recommendations.

The final solution identifies **four customer segments** and translates their characteristics into targeted, data-driven strategies.

---

## Objectives

* Explore customer demographics, purchasing behavior, campaign responses, and digital engagement.
* Clean and preprocess the dataset to improve data quality.
* Engineer meaningful features for customer segmentation.
* Select relevant variables while reducing redundant information.
* Compare different K-Means clustering solutions.
* Evaluate clusters using both statistical and business-oriented criteria.
* Profile the resulting customer segments.
* Translate the findings into actionable business recommendations.

---

## Dataset

The project uses the **Customer Personality Analysis** dataset, containing customer demographic information, product spending, campaign responses, and purchase channels.

The original dataset contains **2,240 customers and 29 variables**, grouped into four main categories:

### People

* Year_Birth
* Education
* Marital_Status
* Income
* Kidhome
* Teenhome
* Dt_Customer
* Recency

### Products

* MntWines
* MntFruits
* MntMeatProducts
* MntFishProducts
* MntSweetProducts
* MntGoldProds

### Promotion

* NumDealsPurchases
* AcceptedCmp1–5
* Response

### Place

* NumWebPurchases
* NumCatalogPurchases
* NumStorePurchases
* NumWebVisitsMonth

---

## Methodology

The analysis was structured into the following stages:

### 1. Exploratory Data Analysis

The dataset was examined to understand:

* Dataset structure and variable types
* Numerical distributions and descriptive statistics
* Categorical variables
* Missing values
* Correlations between numerical variables
* Customer demographics
* Purchasing behavior
* Campaign acceptance
* Purchase channels and digital engagement

EDA was used to identify potential data quality issues and guide the feature engineering process.

---

### 2. Data Cleaning & Preprocessing

The following data quality issues were addressed:

* Missing values in `Income`
* Duplicate records
* Incorrect data types
* Invalid birth years
* An invalid income value
* Inconsistent marital-status categories

Marital-status categories such as `Alone`, `Absurd`, and `YOLO` were consolidated into `Single`.

Invalid values were treated as missing and subsequently imputed using the median of the cleaned dataset.

After preprocessing, the analysis was performed on **2,216 customers**.

---

### 3. Feature Engineering

Several variables were created to better represent customer behavior:

| Feature                    | Description                                             |
| -------------------------- | ------------------------------------------------------- |
| `Age`                      | Customer age based on the dataset reference year        |
| `Total_Children`           | Total number of children and teenagers in the household |
| `Total_Spending`           | Total spending across all product categories            |
| `Total_Campaigns_Accepted` | Total number of accepted marketing campaigns            |
| `Total_Purchases`          | Total purchases across web, catalog, and store channels |

These engineered variables provided more interpretable measures for clustering than the original variables individually.

---

### 4. Feature Selection

The initial candidate feature set included:

* `Age`
* `Income`
* `Total_Children`
* `Total_Spending`
* `Total_Campaigns_Accepted`
* `Total_Purchases`
* `NumWebVisitsMonth`

`Total_Purchases` was excluded from the final model because it was highly correlated with `Total_Spending` (approximately **0.82**).

Keeping both variables would introduce redundant information and place excessive weight on purchasing behavior.

The final feature set was:

```text
Age
Income
Total_Children
Total_Spending
Total_Campaigns_Accepted
NumWebVisitsMonth
```

---

### 5. Feature Scaling

Because K-Means is distance-based, the selected features were scaled before clustering.

Both `StandardScaler` and `RobustScaler` were considered.

**RobustScaler** was selected because several variables, particularly income and spending, are skewed and contain valid extreme observations. Robust scaling reduces the influence of these observations while preserving meaningful customer differences.

---

## K-Means Clustering

Several K-Means models were evaluated using:

```python
KMeans(
    n_clusters=k,
    random_state=42,
    n_init=10
)
```

Values of **k = 2 through 10** were initially explored.

Candidate models with **k = 2, 3, 4, 5, and 6** were compared using:

* Inertia and the Elbow Method
* Overall Silhouette Score
* Cluster-level Silhouette Scores
* Cluster size distribution
* Centroid distances
* Cluster interpretability
* Business usefulness

### Model Selection

The final model uses **k = 4**.

Although k = 2 produced the highest overall silhouette score, it resulted in a broad and unbalanced segmentation. Higher values of k introduced additional clusters but also increased complexity and, in some cases, produced smaller or less clearly separated groups.

The k = 4 solution provided the best overall balance between:

* Statistical quality
* Cluster balance
* Separation
* Interpretability
* Business usefulness

Therefore, k = 4 was selected as the final segmentation solution.

---

## Final Customer Segments

The final model identified four customer segments:

| Cluster | Segment                                      | Customers | Share |
| ------- | -------------------------------------------- | --------: | ----: |
| **C0**  | Young Digital Low-Value Customers            |       711 | 32.1% |
| **C1**  | High-Value Low Campaign Acceptance Customers |       728 | 32.9% |
| **C2**  | Premium Campaign-Responsive Customers        |       196 |  8.8% |
| **C3**  | Family-Oriented Low-Value Customers          |       581 | 26.2% |

### Cluster 0 — Young Digital Low-Value Customers

* Younger customers
* Lower income
* Low total spending
* Few children
* High website activity
* Very low campaign acceptance

**Business opportunity:**
Use digital channels and accessible products to increase conversion and gradually increase customer value.

---

### Cluster 1 — High-Value Low Campaign Acceptance Customers

* Higher income
* High total spending
* Few children
* Low campaign acceptance
* Lower website activity

**Business opportunity:**
Focus on customer loyalty and personalized experiences rather than relying heavily on discounts or promotional campaigns.

---

### Cluster 2 — Premium Campaign-Responsive Customers

* High income
* Highest spending levels
* Few children
* Strong campaign responsiveness
* Moderate digital activity
* Smallest segment

**Business opportunity:**
Prioritize retention through personalized campaigns, premium products, exclusive access, VIP programs, and special experiences.

---

### Cluster 3 — Family-Oriented Low-Value Customers

* Older customers
* Moderate income
* More children
* Low spending
* High website activity
* Very low campaign acceptance

**Business opportunity:**
Use family-oriented bundles and online promotions to increase purchase frequency and average spending.

---

## Business Recommendations

The segmentation suggests that customers should not be approached using a one-size-fits-all strategy.

### Customer Value

Higher-value customers should be approached primarily through:

* Loyalty strategies
* Personalized communication
* Exclusive products and experiences
* Retention initiatives

### Growth Opportunities

Lower-value segments present opportunities to increase:

* Purchase frequency
* Average spending
* Digital conversion
* Engagement with online channels

### Campaign Strategy

Campaign responsiveness differs substantially between segments. Promotional strategies should therefore be adapted according to each customer's previous response behavior instead of applying the same level of discounting to everyone.

### Segment-Specific Strategy

| Segment | Main Strategy                                            |
| ------- | -------------------------------------------------------- |
| **C0**  | Digital conversion and accessible products               |
| **C1**  | Loyalty, premium products, and personalized experiences  |
| **C2**  | Retention, VIP benefits, and exclusive offers            |
| **C3**  | Family-oriented bundles and increased purchase frequency |

---

## PCA Visualization

Principal Component Analysis was used to visualize the six-dimensional feature space in two dimensions.

The first two principal components explained approximately:

* **PC1:** 45.55%
* **PC2:** 20.39%
* **Total:** 65.93%

The PCA projection provides a useful visual representation of the clustering structure, although some overlap remains.

This is expected because K-Means was trained using the complete six-dimensional feature space, while PCA represents only two dimensions.

Therefore, PCA was used primarily as a **visualization and diagnostic tool**, rather than as the criterion for selecting the final number of clusters.

---

## Key Findings

* Customer behavior can be segmented using a combination of demographic, financial, purchasing, campaign, and digital-engagement variables.
* Spending and income were important dimensions for distinguishing customer value.
* Campaign responsiveness identified a relatively small but highly valuable customer segment.
* Digital engagement was particularly relevant for lower-value customer groups.
* Household composition helped distinguish family-oriented customers from other segments.
* Removing highly correlated features helped avoid redundant information in the clustering model.
* The final four-cluster solution provided a practical balance between statistical evaluation and business interpretability.

---

## Technologies & Libraries

**Programming**

* Python

**Data Analysis**

* Pandas
* NumPy

**Visualization**

* Matplotlib
* Seaborn

**Machine Learning**

* Scikit-learn
* K-Means
* RobustScaler
* PCA
* Silhouette Analysis

**Environment**

* Jupyter Notebook
* Git / GitHub

---

## Project Workflow

```text
Raw Dataset
     ↓
Exploratory Data Analysis
     ↓
Data Cleaning
     ↓
Feature Engineering
     ↓
Feature Selection
     ↓
Feature Scaling
     ↓
K-Means Modeling
     ↓
Model Evaluation
     ↓
Cluster Profiling
     ↓
Business Recommendations
```

---

## Conclusion

This project demonstrates an end-to-end approach to **customer segmentation using unsupervised machine learning**.

Rather than focusing solely on clustering performance, the analysis combines statistical evaluation with customer profiling and business interpretation. The resulting four segments provide a practical framework for differentiating customer strategies according to **customer value, campaign responsiveness, household characteristics, and digital engagement**.

The project highlights how machine learning can be used not only to identify patterns in customer data, but also to translate those patterns into actionable business insights.

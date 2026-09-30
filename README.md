# Customer Segmentation & Clustering Analysis

## Overview

This project uses **Python and K-Means clustering** to segment customers based on their demographics, purchasing behavior, campaign responses, and digital engagement.

The goal was to identify meaningful customer groups and use their characteristics to develop specific business recommendations.

---

## Dataset

The project uses the **Customer Personality Analysis** dataset from Kaggle.

The original dataset contains **2,240 customers and 29 variables**, including:

* Customer demographics
* Income and household information
* Spending across product categories
* Marketing campaign responses
* Web, catalog, and store purchases
* Monthly website visits

After cleaning the data, **2,216 customers** were used for the final analysis.

---

## Analysis

The project follows this workflow:

1. Exploratory Data Analysis
2. Data Cleaning
3. Feature Engineering
4. Feature Selection
5. Feature Scaling
6. K-Means Clustering
7. Model Evaluation
8. Customer Profiling
9. Business Recommendations

### Feature Engineering

The following features were created:

* `Age`
* `Total_Children`
* `Total_Spending`
* `Total_Campaigns_Accepted`
* `Total_Purchases`

After analyzing correlations and business relevance, the final features used for clustering were:

```text
Age
Income
Total_Children
Total_Spending
Total_Campaigns_Accepted
NumWebVisitsMonth
```

`Total_Purchases` was excluded because it was highly correlated with `Total_Spending`, which would introduce redundant information into the model.

### Scaling

Both `StandardScaler` and `RobustScaler` were evaluated.

**RobustScaler** was selected because the dataset contains skewed variables and valid extreme values, particularly in income and spending.

---

## K-Means Model

Different values of **k** were tested and evaluated using:

* Elbow Method
* Overall Silhouette Score
* Cluster-level Silhouette Scores
* Cluster size
* Centroid distances
* Interpretability
* Business usefulness

The final model uses **4 clusters**.

Although k=2 had the highest overall silhouette score, it produced a much broader and less balanced segmentation. The k=4 solution provided a better balance between clustering quality, cluster size, interpretability, and business usefulness.

---

## Customer Segments

| Cluster | Segment                                      | Customers |     % |
| ------- | -------------------------------------------- | --------: | ----: |
| C0      | Young Digital Low-Value Customers            |       711 | 32.1% |
| C1      | High-Value Low Campaign Acceptance Customers |       728 | 32.9% |
| C2      | Premium Campaign-Responsive Customers        |       196 |  8.8% |
| C3      | Family-Oriented Low-Value Customers          |       581 | 26.2% |

### C0 — Young Digital Low-Value Customers

Lower income and spending, younger customers, and relatively high website activity.

**Recommendation:** focus on digital conversion, accessible products, and online offers.

### C1 — High-Value Low Campaign Acceptance Customers

Higher income and spending, but low campaign acceptance and lower website activity.

**Recommendation:** focus on loyalty, premium products, and personalized experiences rather than heavy discounting.

### C2 — Premium Campaign-Responsive Customers

High income and spending with significantly higher campaign responsiveness. This is the smallest segment.

**Recommendation:** prioritize retention through personalized campaigns, exclusive products, VIP programs, and special experiences.

### C3 — Family-Oriented Low-Value Customers

Larger households, lower spending, and relatively high website activity.

**Recommendation:** use family-oriented bundles and online promotions to increase purchase frequency and spending.

---

## PCA Visualization

PCA was used to visualize the six-dimensional feature space in two dimensions.

The first two components explained **65.93% of the total variance**:

* PC1: 45.55%
* PC2: 20.39%

The PCA plot is used for visualization and interpretation, while the clustering itself was performed using the full feature space.

---

## Key Findings

* Customer value is strongly differentiated by income and spending behavior.
* Campaign responsiveness identifies a small but high-value customer segment.
* Digital engagement is particularly relevant for lower-value segments.
* Household composition helps distinguish family-oriented customers.
* Different customer groups require different approaches rather than a single strategy.

---

## Tools

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook
* Git / GitHub

---


## Conclusion

This project applies K-Means clustering to identify customer segments and connects the results with practical business recommendations.

The final four-cluster solution provides a useful way to differentiate customers based on **value, campaign responsiveness, household characteristics, and digital engagement**.

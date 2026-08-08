# Customer Segmentation using K-Means & Hierarchical Clustering

## 📌 Project Overview
This project applies *unsupervised machine learning* techniques to segment mall customers based on their behavioral and demographic attributes. Using the *Mall Customer Segmentation Dataset, it implements and compares **K-Means Clustering* and *Hierarchical (Agglomerative) Clustering* to identify distinct customer groups by *Annual Income* and *Spending Score*. These segments can support data-driven, targeted marketing strategies.

---

## 🎯 Objectives
- Perform exploratory data analysis (EDA) to understand customer demographics and spending behavior
- Validate observed patterns using statistical hypothesis testing
- Segment customers using K-Means and Hierarchical Clustering
- Determine the optimal number of clusters using the Elbow Method and Dendrograms
- Evaluate and compare clustering performance using the Silhouette Score

---

## 📊 Dataset
*Source:* Mall Customer Segmentation Dataset (Kaggle)

| Column | Description |
|---|---|
| CustomerID | Unique identifier for each customer |
| Gender | Male / Female |
| Age | Customer's age |
| Annual Income (k$) | Customer's annual income in thousands |
| Spending Score (1-100) | Score assigned based on customer spending behavior |

- *200 rows, 5 columns*
- No missing values, no duplicate records

---

## 🔍 Exploratory Data Analysis
- *Univariate analysis*: Histograms and box plots for Age, Annual Income, and Spending Score
  - Age: right-skewed, majority between 30–50 years, no significant outliers
  - Annual Income: right-skewed with one high-income outlier (~$140k)
  - Spending Score: approximately symmetric, no outliers
- *Categorical analysis*: Gender distribution (Female slightly higher than Male)
- *Bivariate analysis: Scatter plots of Annual Income vs Spending Score and Age vs Spending Score revealed **5 visually distinct customer groups*, with no strong linear correlation across the population
- *Gender-based comparison*: Age, Income, and Spending Score distributions are nearly identical across genders

---

## 🧪 Hypothesis Testing

| Test | Variables | Purpose | Result |
|---|---|---|---|
| One-Way ANOVA | Age groups vs Spending Score | Compare means across 3+ groups | p < 0.05 → significant difference in spending score across age groups |
| Pearson Correlation | Annual Income vs Spending Score | Test linear relationship between two continuous variables | p = 0.89 → no significant linear correlation |
| Independent t-test | Annual Income by Gender | Compare means across 2 groups | p = 0.43 → no significant difference in income between genders |

These tests validate that customer segments are *not explained by a simple linear trend or gender*, supporting the need for clustering to uncover non-linear group structure.

---

## 🤖 Clustering Methodology

### Features Used
Annual Income (k$) and Spending Score (1-100) — selected based on EDA showing clear visual groupings, and standardized using StandardScaler since clustering relies on distance metrics.

### K-Means Clustering
- Optimal K determined via the *Elbow Method* (WCSS vs. K) → *K = 5*
- Model: KMeans(n_clusters=5, init='k-means++', random_state=42, n_init=10)
- *Silhouette Score: 0.55*

### Hierarchical Clustering
- Linkage method: *Ward*
- Dendrogram used to visually confirm the optimal number of clusters → *5 clusters*
- Model: AgglomerativeClustering(n_clusters=5, affinity='euclidean', linkage='ward')
- *Silhouette Score: 0.5538*

---

## 📈 Results

Both algorithms independently converged on the *same 5 customer segments*:

| Segment | Annual Income | Spending Score | Description |
|---|---|---|---|
| 1 | High | Low | High earners, cautious spenders |
| 2 | High | High | High earners, high spenders (target segment) |
| 3 | Mid | Mid | Average income, average spending |
| 4 | Low | High | Budget-conscious but high spenders |
| 5 | Low | Low | Low income, low spending |

### Model Comparison

| Metric | K-Means | Hierarchical (Ward) |
|---|---|---|
| Silhouette Score | 0.55 | 0.5538 |

The two scores are nearly identical, with Hierarchical Clustering marginally ahead. This near-agreement across two fundamentally different clustering approaches (centroid-based vs. connectivity-based) indicates the 5-segment structure is a *robust, genuine pattern in the data* rather than an artifact of a single algorithm.

---

## 🛠️ Tech Stack
- *Language:* Python
- *Libraries:* pandas, numpy, matplotlib, seaborn, scipy, scikit-learn

---

## 🚀 Key Takeaways
- Demonstrated the full unsupervised learning workflow: EDA → statistical validation → feature scaling → optimal K selection → clustering → evaluation
- Applied both centroid-based (K-Means) and hierarchical (Agglomerative) clustering, cross-validating results using the Silhouette Score
- Translated cluster outputs into actionable customer segments relevant for *targeted marketing strategy*


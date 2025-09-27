# Clustering of Customer Segments

## WalletUp Fintech Startup - Unsupervised ML project
This project addresses a semester assignment for the course "Clustering Methods," focused on segmenting banking customers for 
WalletUp—a fintech startup offering AI-driven digital banking services. The task involves applying unsupervised machine learning techniques 
to identify and profile customer segments from a provided CRM dataset. The goal is to uncover distinct behavioural archetypes and recommend 
target groups for WalletUp’s marketing strategy, balancing innovation with the traditional bank’s concern for preserving long-standing client 
relationships. The analysis includes exploratory data analysis (EDA), experimentation with clustering algorithms, validation, and strategic recommendations, all implemented using the R programming language.

The project is divided into 4 notebooks, following this sequence:
1. EDA
2. Data Preparation and Cluster Validation
3. Clustering models
4. Interpretation of results

## EDA
During the EDA, I inspected the customer data by viewing its dimensions, structure and summary statistics. Then I checked for NULL values, outliers and performed additional descriptive analysis by distributing
customers in different age groups and comparing them based on various attributes, such as Income and Mortgage.

## Data Preparation and Cluster Validation

- **Data Selection:**  
  Behavioural attributes were extracted from the raw dataset to create `behavioral_data`. All selected columns contain numeric values related to customer behaviour such as
  Internet traffic, mortgage volume, spending, investment, visits, and digital activity.

- **Data Scaling:**  
  The behavioural data were scaled using the `scale()` function to normalise values and enhance model performance. A fixed seed (`set.seed(123)`) was used to ensure reproducibility.

- **Distance Calculation:**  
  Euclidean distance was computed on a random sample of 1000 scaled data points to assess the spread and cohesion of data points, indicating underlying cluster structures.

### Cluster Validation

- **Visual Inspection:**  
  Principal Component Analysis (PCA) revealed approximately 6 visible groups, suggesting potential natural clusters in the data.

- **Hopkins Test:**  
  Statistical testing with Hopkins' statistic (value ≈ 0.9999) indicates a strong tendency for clustering rather than random distribution, supported by a statistically significant p-value (~0).

- **Optimal Number of Clusters:**  
  Multiple methods were employed to determine the best cluster count:
  - **Elbow Method:** Focuses on cluster compactness.
  - **Silhouette Method:** Evaluates how well each point fits within its cluster.
  - **Gap Statistic:** Compares variance within clusters against a null reference.
  - **NbClust Package:** Provides a majority-rule consensus, suggesting 7 clusters as optimal, with some support for 4 clusters.

  The number of clusters likely falls between 6 and 8, with 7 being the most supported choice. Visual methods also indicate smoothing around 5 clusters, highlighting some flexibility in cluster count decisions.

## Clustering
**Models Used:**
1. KMEANS (with 6 and 7 clusters)
2. KMEDOIDS (PAM) (with 6 and 7 clusters)
3. CLARA (with 6 and 7 clusters) - suitable for large datasets, sample subsets and applies PAM
4. Hierarchical KMEANS (with 6 and 7 clusters) - hybrid approach combining hierarchical and k-means
5. Gaussian Mixture Models (GMM) - probabilistic model treating clusters as Gaussian distributions
6. DBSCAN - density-based clustering, good for arbitrary shapes and anomaly detection

**Validation Measures:**
- Dunn’s index: Values above 0.3 indicate good cluster separation.
- Average Silhouette Width: Values above 0.5 indicate good clustering quality.
- Average Within-Cluster Distance: Lower values indicate higher homogeneity within clusters.
- Average Between-Cluster Distance: Higher values indicate better separation between clusters.
- Pearson-Gamma: Values close to 1 indicate a strong relationship between distance and clustering.

**Final Decision:**
- Most models performed best with 6 or 7 clusters, consistent with prior analysis.
- The 7-cluster solutions generally had slightly better validation scores.
- However, the final choice was the 6-cluster solution using the CLARA algorithm (clara_res1), as it was computationally efficient, robust to outliers (using medoids based on medians), and produced distinct and consistent segments based on socio-demographic characteristics.
- This choice balances model performance with practical marketing considerations like strategy and budget.

In summary, several clustering methods were evaluated with internal validation metrics showing strong and comparable results, mostly around 6-7 clusters. 
The CLARA method with 6 clusters was selected as the best compromise for customer segmentation in this project.

## Interpretation and analysis of customer segments
In the interpretation notebook, I first assigned a cluster number to all objects in the dataset. Once I knew each customer cluster affiliation, I could interpret the clusters based on the different attributes.
**Financial characteristics**
- Credit Volume
- Stocks
- App logins
- Time spent on Online Banking
- Bitcoins
- NFT
- Social media channels followed
- Branch visitations
Then I performed a similar analysis on socio-demographic attributes, so I can build my customer segments. You can see charts for:
- Age
- Income
- Household size
- Internet traffic

Once I had gathered and analysed all this information about the customers in each cluster, I created the **Customer Personas** table. This table helped me in giving my personal recommendation for a 
marketing campaign strategy. The recommendation is to prioritise targeting "Risky Investor" and "Innovative Investor" segments as early adopters, 
while also pursuing the "Established & Open" group and large "Young Professionals" base through digital campaigns, avoiding the financially unstable "Indebted" group, 
and approaching "Mature Traditionalists" through offline channels due to their lower digital engagement.

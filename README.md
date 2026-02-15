**District-Level Clustering & Inequality Modeling in Aadhaar Data**

**Overview:**
This project analyzes large-scale Aadhaar enrollment and biometric update data (~1.5 million records) to identify structural inefficiencies across districts using unsupervised learning and statistical inequality modeling.

The goal is to:
Cluster districts based on operational performance
Quantify intra-district inequality at the pincode level
Provide data-driven insights for system optimization

**Dataset:**
Merging Data: Twelve Excel files (approximately 500,000 rows each) were categorized into three groups and
merged to create three final datasets of enrollment, biometric updates and enrollment updates.
Normalization: Standardized text formats by applying trimming and Title Casing.
Correction Mapping: Utilized a dictionary map to rectify over 60 variations into 36 official States/UTs,
addressing both typos and contextual errors.
Anomaly Handling: Eliminated invalid placeholder data (for instance, a State listed as '100000').
Strict Deduplication: Employed logic to remove duplicates only when Date, State, District, Pincode, and
Metrics were identical, ensuring the preservation of detailed local data

**Feature Engineering:**
To ensure meaningful clustering and avoid skewness effects, the following features were engineered:

**1) Log Enrollment:** Enrollment distribution was heavily skewed.
To stabilize variance:

**X1​=log(1+Ed​)**
Where: Ed = Total enrollment in district 𝑑
This prevents high-population districts from dominating clustering.

**2) **Update Efficiency****=**X2​=Ud/Ed**
Where:
Ud = Total biometric updates (Age 5–17)
Ed = Total enrollment
This measures operational effectiveness in converting enrollment into updates.

**3) Pincode-Level Inequality (Coefficient of Variation)**
To quantify intra-district enrollment concentration:
CV = σ(Pd,i​)​/μ(Pd,i​)

Where:
Pd,i = Enrollment in pincode i within district d
σ = Standard deviation
μ = Mean

The Coefficient of Variation (CV) was chosen because it is:
Scale-independent
Comparable across districts
Sensitive to concentration patterns
High CV indicates enrollment concentration in few pincodes.

**Clustering Methodology**
Algorithm: K-Means

Districts were clustered using K-Means on standardized features.
K-Means partitions data into k clusters by minimizing within-cluster variance:

$$\min \sum_{i=1}^{k} \sum_{x \in C_i} ||x - \mu_i||^2$$
Where:
* $C_i$ = Cluster $i$
* $\mu_i$ = Centroid of cluster $i$
* $||x - \mu_i||^2$ = Squared Euclidean distance

The objective is to create compact and well-separated clusters.

**Selection of K**
The optimal number of clusters was selected using : Elbow Method
WCSS=∑(∣∣x−μ∣∣)^2


We selected K at the point where additional clusters resulted in diminishing variance reduction.
Silhouette Score: S= b-a/max(a,b)

Where:
a = Intra-cluster distance
b = Nearest-cluster distance
K = 4 provided a balance between compactness and separation.

**Key Insights**
High enrollment does not guarantee high update efficiency.
District-level averages can mask severe pincode-level concentration.
Inequality modeling reveals structural distribution gaps.
Redistribution simulation reduced inequality by ~25%.

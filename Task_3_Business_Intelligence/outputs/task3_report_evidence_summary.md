# Tasks 2 and 3 - evidence summary (verify before using in your own report)

- Dataset: 489 shares from 11 GICS sectors; original observation date 2024-12-31.
- Two independent feature matrices: mean weekly return + weekly beta; R + F + log1p(M).
- Recency transformed using log1p: True; no winsorisation; all inputs standardised within each matrix.
- Searched k=2..8; seeded KMeans uses n_init=30; Ward uses Euclidean distance and Ward linkage.

## Selected k and silhouettes
- RiskReturn Ward: k=5, silhouette=0.3120, minimum cluster size=36, fallback=False
- RiskReturn KMeans: k=2, silhouette=0.3858, minimum cluster size=144, fallback=False
- RFM Ward: k=2, silhouette=0.4030, minimum cluster size=96, fallback=False
- RFM KMeans: k=2, silhouette=0.4157, minimum cluster size=102, fallback=False

## Agreement between solutions (Adjusted Rand Index)
- Ward_Risk versus KMeans_Risk: ARI=0.1483
- Ward_RFM versus KMeans_RFM: ARI=0.8904
- Ward_Risk versus Ward_RFM: ARI=0.0062
- KMeans_Risk versus KMeans_RFM: ARI=0.0365

## RFM correlation (Pearson; raw R, raw F, log1p M)
- R vs F: -0.3461
- R vs log1p(M): 0.1531
- F vs log1p(M): 0.0128
- Removing Monetary (same shares, same Ward k=2, freshly scaled R/F): ARI=0.7896

## Sector composition and stakeholder use
- Use exported sector-composition plots to describe which sectors are represented in each cluster.
- Risk-return groupings describe historical average weekly performance and index beta; RFM groupings describe volume-event recency/frequency and estimated traded value.
- Use these profiles to monitor activity, investigate unusual changes and support portfolio screening, not to claim diversification or future returns.

## Required cautions
- Using 2026 constituents for 2021-2024 introduces survivorship/membership-selection bias.
- Beta is historical systematic sensitivity and does not quantify covariance among all share pairs.
- Adjusted-price series, corporate actions, incomplete/zero-volume observations and large price jumps require documented review.
- Correlated features may give repeated emphasis to trading activity but correlation alone cannot prove dominance.
- Close × Volume is approximate turnover, not realised profit, market cap or executable liquidity; spreads and price impact are missing.
- Clusters are DESCRIPTIVE and cluster numbers have no ordinal meaning.
- Reports must explain when RFM and RF-only Ward memberships differ; rely on ARI plus original-unit profiles, not label numbers.

## Output files to cite
`four_baseline_cluster_profiles_original_units.csv`, `sector_composition_*.png`, `rfm_correlation_pearson.csv`, `monetary_removal_original_unit_profiles.csv`, `proposed_data_mart_diagram.png`.
# Tactical Role Clustering in the Premier League

This project uses unsupervised machine learning to cluster Premier League players into broad tactical roles based on attacking and ball-progression statistics.

Traditional soccer positions such as defender, midfielder, and forward do not always describe how a player actually contributes during a match. This project explores whether per-90 player statistics from the Premier League 2024/25 season can reveal tactical profiles beyond listed position labels.

## Project Overview

The main research question is:

**Can Premier League players be grouped into meaningful tactical roles using attacking and ball-progression statistics rather than only traditional position labels?**

The final clustering model identifies three broad tactical groups:

- Defensive / Low-Attacking Involvement
- Goal-Scoring Forwards
- Creative / Progressive Hybrid Attackers

## Dataset

Dataset: **FBref Premier League 2024/25 Player Stats Dataset**  
Source: Kaggle, compiled by Siddhraj Thakor

The dataset contains season-level Premier League player statistics, including player information, squad, position, minutes played, goals, assists, expected goals, expected assisted goals, progressive carries, progressive passes, and progressive receptions.

The dataset is **not included** in this repository. Please download it from the original Kaggle source.

To reproduce the analysis:

1. Download the CSV file from Kaggle.
2. Rename the file to:

```text
fbref_PL_2024-25.csv
```

3. Place the CSV file in the same folder as the notebook.
4. Run the notebook from top to bottom.

## Methods

The project uses the following workflow:

1. Load and inspect the dataset with pandas.
2. Filter out players with fewer than 600 minutes played.
3. Create per-90 progression features.
4. Standardize selected features using `StandardScaler`.
5. Perform exploratory data analysis using Matplotlib and seaborn.
6. Apply K-Means clustering as the main unsupervised learning model.
7. Compare K-Means with Agglomerative Clustering.
8. Use PCA to visualize the clusters in two dimensions.
9. Interpret the resulting clusters as tactical player roles.

## Features Used for Clustering

The final clustering features are:

- Goals per 90
- Assists per 90
- Non-penalty expected goals per 90
- Expected assisted goals per 90
- Progressive carries per 90
- Progressive passes per 90
- Progressive receptions per 90

## Main Findings

The K-Means model produced three interpretable tactical groups:

1. **Defensive / Low-Attacking Involvement**  
   Players with low attacking output and lower attacking progression values. This group also includes goalkeepers because the selected features focus on attacking and progression rather than goalkeeper-specific actions.

2. **Goal-Scoring Forwards**  
   Players with the highest goals per 90 and non-penalty expected goals per 90.

3. **Creative / Progressive Hybrid Attackers**  
   Players with stronger creative and ball-progression profiles, including higher assists, expected assisted goals, progressive carries, progressive passes, and progressive receptions.

The results suggest that unsupervised learning can be a useful exploratory tool for identifying broad attacking and progression-based player profiles beyond traditional position labels.

## Model Comparison

K-Means was compared with Agglomerative Clustering using the same scaled feature matrix and the same number of clusters.

| Model | Number of Clusters | Silhouette Score |
|---|---:|---:|
| K-Means | 3 | 0.388 |
| Agglomerative Clustering | 3 | 0.205 |

K-Means was kept as the main model because it produced a higher silhouette score and more interpretable tactical groupings.

## Repository Contents

```text
.
├── tactical_role_clustering.ipynb
├── final_report.pdf
├── requirements.txt
├── README.md
└── figures/
    ├── eda_position_counts.png
    ├── eda_minutes_distribution.png
    ├── eda_correlation_heatmap.png
    ├── kmeans_evaluation.png
    ├── final_pca_roles.png
    └── tactical_role_heatmap.png
```

## Requirements

Install the required Python packages with:

```bash
pip install -r requirements.txt
```

The main libraries used are:

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- jupyter

## How to Run

After installing the required packages and downloading the dataset:

```bash
jupyter notebook tactical_role_clustering.ipynb
```

Then run all notebook cells from top to bottom.

## Limitations

This project focuses on attacking and ball-progression statistics. Because of that, it is better at separating attacking roles than distinguishing defensive roles, goalkeeper roles, pressing profiles, or team-specific tactical systems. The dataset also covers only one Premier League season, so the results may change if multiple seasons are included.

## Future Work

Possible extensions include:

- Adding defensive, pressing, and goalkeeper-specific metrics
- Comparing multiple Premier League seasons
- Testing other unsupervised methods such as DBSCAN or Gaussian Mixture Models
- Comparing the clusters with expert-defined tactical roles
- Separating goalkeepers before clustering

## Author

Sumit Shrestha  
CS490/590 — Intensive Python for Data Science  
Spring 2026

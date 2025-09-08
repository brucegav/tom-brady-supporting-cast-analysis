#Project Overview
Tom Brady Supporting Cast Analysis

- a data analysis of Tom Brady's career statistics measured against composite scoring of his offensive and defensive supporting casts (by season)
- the questions to be answered are 
	1. how truly valuable was Tom Brady in terms of his teams' successes?  
	2. Was the Patriots dynasty a product of an all-time great QB or elite supporting casts, or both? 
	3. How do Brady's supporting casts match up against other elite contemporary QBs (Manning, Brees, Mahomes, etc.)

	
#Technical Details
* Data source: NFL play-by-play data and roster data (2001-2024) from nfl-data-py
* Technologies used: Python, pandas, numpy, scipy, matplotlib, scikit-learn, Jupyter Lab
* Methodologies: Z-scoring, composite metrics, value above replacement calculations, Random Forests, K- Means clustering, Principal Component Analysis, Regression analysis, time series analysis

#Project Structure
```python
├── data/
│   ├── raw/           # Original collected data
│   ├── processed/     # Cleaned and z-scored data
│   └── final/         # Analysis-ready datasets
├── scripts/           # Data collection and processing scripts
├── notebooks/         # Jupyter analysis notebooks
└── results/           # Visualizations and findings
```

#Key Findings (work in progress)
* custom QB metric created and validated against professional EPA metric (r=0.888)
* analysis covers 1,860 qualified QB seasons across 24 NFL seasons
* supporting cast quality measured across 4 position groups using z-scored metrics



#Skills Demonstrated
* sports analytics and statistical modeling
* NFL domain expertise
* statistical methodology and validation
* data visualization (matplotlib)
* large dataset processing and aggregation
* machine learning models

 
# NFL Quarterback Archetypes via K-Means Clustering

Identifying distinct QB playing styles from NFL performance data using unsupervised machine learning. 

**Presented at the [Connecticut Sports Analytics Symposium (CSAS) 2026](https://statds.org/events/csas2026/), University of Connecticut**

---

## Key Findings

K-means clustering (k=4) applied to 204 QB-seasons (2019–2024) identified four statistically distinct archetypes:

| Archetype | Defining Trait | Example QBs | n |
|---|---|---|---|
| 🔵 **Pocket Passer** | High passing volume, elite efficiency | Mahomes, Burrow, Brady | 85 |
| 🟠 **Game Manager** | Low volume, conservative, limited stats | Mac Jones, Devlin Hodges | 48 |
| 🟢 **Gunslinger** | High attempts, high interceptions | Herbert, Heinicke, Howell | 47 |
| 🔴 **Dual Threat** | Elite rushing + solid passing | L. Jackson, Murray, Allen | 25 |

All 10 one-way ANOVA tests were significant at p < 0.001. The most notable result: **Pocket Passers and Dual Threats show no significant difference in QBR** (p = 0.9439), meaning elite efficiency is achievable through fundamentally different styles.


---

## Data

Data was sourced from **[Pro Football Reference](https://www.pro-football-reference.com/)**.

To reproduce the dataset:
1. Go to [PFR Season Passing Stats](https://www.pro-football-reference.com/seasons/NFL-passing-statistics.htm) and export CSVs for seasons 2019–2024
2. Do the same for [Rushing Stats](https://www.pro-football-reference.com/seasons/NFL-rushing-statistics.htm)
3. Place both files in the `data/` folder

**Inclusion criteria:** QBs with ≥ 100 pass attempts *or* ≥ 20 rush attempts in a season. Mid-season team trades are handled using the totals rows PFR provides.

---

## How to Run

### Requirements

```
python >= 3.9
pandas
numpy
scikit-learn
matplotlib
scipy
jupyter
```

Install dependencies:

```bash
pip install pandas numpy scikit-learn matplotlib scipy jupyter
```

### Running the analysis

```bash
quarto render code/archetype_qb.qmd
```

Run cells top to bottom. The notebook covers:
1. Data loading and merging
2. Preprocessing and imputation
3. Standardization and PCA
4. K-means clustering (elbow + silhouette selection)
5. Archetype profiling and visualization
6. ANOVA and Tukey HSD validation

---

## Methods Summary

- **Features:** 43 passing and rushing metrics per QB-season
- **Preprocessing:** Z-score standardization via `StandardScaler`; mean imputation for QBR, median for longest rush
- **Dimensionality reduction:** PCA (~90% variance retained at 10 components)
- **Clustering:** K-means with k-means++ initialization; k=4 selected via elbow method and silhouette score (0.208)
- **Validation:** One-way ANOVA across all 10 key metrics; Tukey HSD post-hoc for pairwise comparisons

---

## Future Work

- **Temporal tracking** of archetype changes within individual QB careers
- **Predictive modeling** — do archetypes predict playoff success, contract value, or career longevity?
- **Richer features** — incorporate Next Gen Stats (air yards, time-to-throw, CPOE) and EPA-based metrics

---

## Citation

If you use this work, please cite:

```
Tamhane, S. (2026). Identifying NFL Quarterback Archetypes via K-Means Clustering.
Connecticut Sports Analytics Symposium (CSAS), University of Connecticut.
```

---

## Author

**Shubhan Tamhane** — Undergraduate Data Science Student, University of Connecticut  
[github.com/ShubhanTamhane1](https://github.com/ShubhanTamhane1)

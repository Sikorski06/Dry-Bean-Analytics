# Dry-Bean-Analytics — Learning and Development Roadmap

## Working agreement

1. Keep completed work intact; prefer small corrections and new cells rather than rewriting notebooks.
2. Student writes analytical code first; assistant provides theory, hints, review and specific corrections. Codex may review/debug, not replace learning.
3. Write notebook explanations in English. Assistant supplies **raw Markdown inside fenced `md` blocks**, directly pasteable into Jupyter Markdown cells. Explain purpose before code and evidence-based findings after code.
4. Use Pandas for labeled tabular analysis, NumPy for arrays/vectorization/numerical computations, Seaborn/Matplotlib for visual analysis. Cover the full breadth of course topics, not just what is convenient for the main dataset.
5. After each section: assess correctness, interpret findings, ask conceptual questions, run notebook top-to-bottom, and commit a meaningful Git change. Preserve raw data and document data provenance.

## Verified progress from uploaded notebook

File: `notebooks/01_data_exploration.ipynb` (uploaded copy named `01_data_exploration.ipynb`).

- [x] Introduction and dataset loading with `pandas`, `numpy`, `pathlib.Path`, `pd.read_excel`.
- [x] Shape, `select_dtypes`, column types and unique `Class` values.
- [x] Class counts and percentages; missing values per column (`df.isna().sum()`).
- [x] `loc`/`iloc`, basic filtering, median threshold, sorting and `groupby`.
- [x] Classwise Area mean/median and Perimeter min/max/std; Area five-measure aggregation using `agg`.
- [ ] Section 6: descriptive statistics: the heading exists but no implementation yet.
- [ ] Complete analytical interpretations of current tabular results; presently mostly short headings.

**Data observed:** 13,611 rows; 16 numerical inputs; 7 classes; no missing values in the uploaded notebook output.

**Minor follow-up review items (do not redo whole section):** `df.iloc[:9]` selects 9 rows rather than 10; in Perimeter summary, `rename(columns={"Area": "Min"})` does not rename the current `Perimeter` column; `rename(..., inplace=True)` triggers a deprecation warning in the user's environment. Consecutive Jupyter expressions ordinarily show only the last display unless `display()` or `print()` is used.

## Phase A — Main research narrative

### M1. Dataset understanding and manipulation — CURRENT, finishing
- Cover Series/DataFrame, shapes/dtypes, indexing, boolean filtering, sorting, `groupby` and `agg`.
- Complete existing Markdown commentary with verified insights.
- Tiny corrections to `iloc` and Perimeter heading.
- No new standalone notebook required.

### M2. Descriptive statistics + NumPy — NEXT
- Continue in existing notebook Section 6.
- Mean, median, mode, range, variance, sample vs population std (`ddof`), Q1/Q3, IQR, percentiles and coefficient of variation.
- Global vs per-class summaries; statistics with `groupby` and `agg`.
- **Add NumPy explicitly:** `Series.to_numpy()`, `ndarray`, `shape`, `ndim`, `dtype`, indexing/masks, `np.mean`, `np.median`, `np.var`, `np.std`, `np.percentile`, `np.quantile`, `np.isnan`, `np.nanmean`; explain NaN behavior, `ddof=0/1` and axis.
- Practice vectorization, broadcasting, `reshape`, `concatenate`, `copy` versus view and basic matrix operations in supplementary array tasks based on actual bean features (not necessarily all in the main research notebook).
- First exercises already assigned: global Area mean/median/variance/std; quartiles/IQR; per-class CV; grouped table including IQR; compare std vs CV rankings; add Pandas vs NumPy comparison.

### M3. Data quality and missing values — PRiAD 2 + colloquium task 1
- Original bean dataset is complete, so create a separate **reproducible corrupted copy** using a fixed random seed; never overwrite raw data.
- Count missing cells, per column and per row; classes, class frequencies, feature count, observation count; `isna`, `notna`, `dropna`, `fillna` and implications of different approaches.
- Write missing-count utility returning per-row and per-column counts, echoing PRiAD 2 exercise.
- Examine before/after distributions and class retention.

### M4. Univariate data visualization — PRiAD 3 + colloquium task 2
- Line/bar/horizontal bar, histograms (`bins`, overlaid groups, KDE), class-specific distribution comparisons, box/violin/swarm plots.
- Match graph to question; distinguish spread, skewness, outliers and class overlap.
- Write reusable visualization/summary function for arbitrary numeric feature(s) and class column (PRiAD 3 exercise).
- Explain why feature with high variance is not automatically a strong class discriminator.

### M5. Relationships and multivariate EDA — PRiAD 2/3 + colloquium task 3
- Covariance versus Pearson correlation (including signs and scale); `corr`, `cov`, `np.corrcoef`, `np.cov`, heatmaps and scatter/pair plots.
- Compare overall and within-class relationships, assess which feature distributions best separate classes.
- Demonstrate Anscombe's quartet: similar summary statistics can conceal different patterns.

### M6. Feature redundancy and discriminative power — colloquium task 4
- Identify correlated/near-duplicate feature pairs and evaluate within- vs between-class separation.
- Candidate methods: classwise descriptive statistics/plots and interpretable numerical comparisons; treat feature importance methods beyond PRiAD as optional and clearly label them.
- Do not equate high feature-feature correlation with irrelevance or feature-target correlation with categorical separability.
- State reasoned removal/retention proposals with caveats.

## Phase B — Full PRiAD material (supplementary notebooks, topic-first)

### M7. Time series + combining tables — PRiAD 1 and 3
- Another suitable dataset: historical currency exchange rates, or source files if available.
- `concat`, `merge`, date parsing/index, resampling, `shift`, rolling/yearly/monthly summaries and line/bar charts; discuss aggregation over time.
- Keep supplementary notebooks separate from Dry Bean's central research story.

### M8. Text analysis — PRiAD 2
- Use a lawful, suitable literary text and reproduce exercises on counting words/characters, summary statistics and per-chapter comparisons.

### M9. Image/raster + deeper NumPy — PRiAD 1 and 3
- `scikit-image` loading, pixel arrays, RGB and alternative color spaces (HSV, YUV), channel slicing and color/grayscale histograms.
- NumPy shape/axes/slicing/masks/copying applied to images.

### M10. Colloquium simulations and review — PRiAD_kolos
- Task 1 (3 pts): observations, number of classes, per-class sizes, feature count, missing count, clean copy.
- Task 2 (4 pts): feature variability overall and by class, and appropriate visualizations.
- Task 3 (4 pts): feature correlations and which attributes distinguish classes, with graphics.
- Task 4 (4 pts): identify redundant features with numerical evidence AND class separability analysis.
- Practice on original simulated `make_classification` data and one unseen dataset; do not copy old answers.
- Check whether the previous-year notebook's wording about data prior to missing-value corruption is internally consistent; validate the actual dataset used for each task.

## Suggested repository evolution (not all at once)

```text
Dry-Bean-Analytics/
├── data/
│   ├── raw/
│   └── processed/
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_data_quality.ipynb
│   ├── 03_visual_exploration.ipynb
│   ├── 04_feature_relationships.ipynb
│   ├── 05_feature_redundancy.ipynb
│   └── supplementary/
│       ├── time_series.ipynb
│       ├── text_analysis.ipynb
│       ├── image_analysis.ipynb
│       └── numpy_experiments.ipynb
├── src/                      # Only as reusable functions emerge
├── reports/                  # Figures and evidence-based final findings
├── requirements.txt
├── .gitignore
├── README.md
└── ROADMAP.md
```

## Progress review cadence

After each completed milestone, update this file's checkpoint, completed items, results, issues and next exercise. This roadmap is the durable source of truth if a new chat does not recover the full previous context.

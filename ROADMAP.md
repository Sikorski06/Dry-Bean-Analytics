# Dry-Bean-Analytics — Learning and Development Roadmap

**Audit checkpoint:** 2026-11-13  
**Sources checked:** `PRiAD 0`, `PRiAD 1`, `PRiAD 2`, `PRiAD 3`, `PRiAD_kolos`, `01_data_exploration(1).ipynb`, `02_data_cleaning.ipynb`, and previous `ROADMAP.md`.  
**Next exercise:** Exercise 9 — feature-distribution visualization in `notebooks/03_visual_exploration.ipynb`.

## Working agreement

1. Preserve finished analytical work. Apply small fixes to incorrect cells; add new cells/notebooks for new topics.
2. Student writes analytical code first; the assistant provides theory, focused hints, code review, statistical interpretation, and colloquium-style questions. Codex can debug or review, not write practice solutions.
3. Use **English Markdown cells** before each analysis (objective/method) and after it (verified findings/limitations). Provide Markdown as raw fenced `md` text.
4. Prioritize PRiAD colloquium tasks **and** complete syllabus coverage across PRiAD 0–3. Use Pandas for labeled data, NumPy for arrays, Matplotlib/Seaborn for graphics.
5. Run every notebook top-to-bottom in a fresh kernel before committing. Keep data provenance documented and meaningful Git commits.

## Verified progress from latest uploads

### `01_data_exploration(1).ipynb` — main data exploration

- [x] Read Excel using Pandas and `Path`; examine shape, dtypes, column names, class frequencies and null values.
- [x] Use `loc`, `iloc`, filtering, sorting, `groupby` and `agg`.
- [x] Compute Area/Perimeter class summaries; mean, median, variance, standard deviation, quartiles, IQR, coefficient of variation, and ranking comparisons.
- [x] Compare selected NumPy and Pandas statistics, including sample standard deviation with `ddof=1`.
- [x] Use `to_numpy`, `shape`, `ndim`, `size`, `dtype`, Boolean masks, standardization, `np.where`, `column_stack` and `reshape`.
- [ ] Fix `iloc[:9]` when ten rows were intended; fix `rename(columns={'Area':'Min'})` on the Perimeter table (actual column is `Perimeter`).
- [ ] Add clear numeric interpretations/Markdown conclusions to the current notebook; use `display()` when multiple outputs should be visible.
- [ ] Deeper NumPy practice: creating arrays with `arange/linspace/logspace/zeros/ones`, indexing/axes, `dot`, `diag`, cumulative operations, `concatenate/hstack/vstack`, `save/load/loadtxt/savetxt`, and views vs copies (can be done later).

### `02_data_cleaning.ipynb` — missing-value handling

- [x] Inject reproducible ~5% cell-level missingness into numeric features only (`default_rng(42)`).
- [x] Count missing cells and incomplete rows; compute per-column missing percentages.
- [x] `dropna`, global mean imputation, global median imputation, class-specific median imputation.
- [x] Compare observation retention, Area mean/median/std/CV and changes, and class distribution TVD.
- [x] Actual saved outputs: **10,828** missing cells; **7,558** rows with any missing feature; **6,053** complete rows remain (**44.4714%**); deletion TVD **0.0072**.
- [ ] Correct Markdown interpretations: class-median imputation has smallest *absolute Area mean change among the cleaning methods* (**+0.0256%**), not global median imputation (**−0.8353%**); class-median also has smallest absolute Area std change among the cleaning methods (**−0.0713%**). The corrupted dataset is a reference condition, not a cleaning strategy.
- [ ] Update wording: class composition changed **slightly** after deletion (TVD **0.0072**), not exactly zero; replace bracketed placeholders and `table .` with precise values.
- [ ] Correct erroneous comment that `.loc` cannot edit DataFrames: assignment via `.loc[...] = ...` is supported.
- [ ] Add explicit check that imputed datasets have zero missing values; compare `Perimeter` and `Eccentricity` in addition to `Area` (helpful for stronger conclusions).
- [ ] Implement the exact PRiAD 2 exercise: a reusable function returning two missing-count vectors/dictionaries (one per row, one per column). Do this as a short follow-up, not a full rewrite.
- [ ] Restart kernel, **Run All**, confirm no failures, and commit.

## Syllabus coverage audit

Notation: **Covered** = present in submitted project code; **Partial** = some practice but identifiable gaps; **Open** = not implemented in submitted project notebooks.

| Course source | Covered | Partial / still to practice | Planned location |
|---|---|---|---|
| **PRiAD 0: Python foundations** | Imports, functions/lambda as a Pandas aggregator, loops/dictionaries; user already knows fundamentals | Conditional logic, `try/except`, standalone functions: quick refresher only if needed | Throughout |
| **PRiAD 0: NumPy** | Arrays from DataFrames, dtype/shape, masking, vectorized arithmetic, z-score, `where`, stacking, reshaping, `mean/std/var/quantile` | Array creation (`zeros`, `ones`, `arange`, `linspace`, `logspace`), `np.dot`, matrices, cumulative operations, array IO, `np.concatenate`, copies/views | Supplementary `numpy_experiments.ipynb` and feature analysis |
| **PRiAD 1: Series/DataFrames** | Read Excel, column access, DataFrame inspection, loc/iloc, filtering/sorting, grouping | Standalone `Series`, explicit indexing/reindexing, `pd.Categorical`, `describe`, other source formats | Small focused cells + supplementary |
| **PRiAD 1: joining and time series** | Some `groupby`, per-class analyses | `concat`, `merge`, dates/date index, resampling, `shift`, yearly change, `idxmin/idxmax`, CSV/Excel import variants | `time_series.ipynb` |
| **PRiAD 1: raster/image** | No direct image exercises yet | `skimage.io.imread`, grayscale, RGB, HSV/YUV, channel separation, pixel arrays | `image_analysis.ipynb` |
| **PRiAD 2: missing values** | Detection, deletion, global and group imputation, comparison | Missing-count **function**, multi-feature evaluation, `isnull/notnull` equivalences | Finish `02_data_cleaning.ipynb` in small patches |
| **PRiAD 2: univariate statistics** | Mean, median, variance, std, quartiles, IQR, CV, class summaries | Mode/range/`describe`, robustness to skew/outliers, interpret means on different distribution shapes | Finish when creating visualizations |
| **PRiAD 2: dependence** | Not implemented | Covariance and correlation, global vs per-class, feature comparisons, scatterplots and heatmaps | `04_feature_relationships.ipynb` |
| **PRiAD 2: text** | Not implemented | Per-book/section word counts, text lengths, descriptive statistics | `text_analysis.ipynb` |
| **PRiAD 3: basic charts** | Not implemented | Line, grouped/stacked bar, horizontal bar, sorting before plotting, `cumsum` | `03_visual_exploration.ipynb` + `time_series.ipynb` |
| **PRiAD 3: univariate charts** | Not implemented | Histograms, bin selection, KDE, comparing class distributions, box/violin/swarm | **Next: `03_visual_exploration.ipynb`** |
| **PRiAD 3: multivariate charts** | Not implemented | Scatter and pair plots (with `hue`), class overlap, interpretable feature pairs | `04_feature_relationships.ipynb` |
| **PRiAD 3: advanced examples** | Not implemented | Reusable plot + per-class-statistics function for arbitrary numeric DataFrame; image histogram; Anscombe's quartet | Visual notebook + image notebook |

The course notebooks contain further **specific dataset exercises** (`iris`, `dane1`–`dane11`, currencies, passenger counts, `mtcars`, text, images). We will practice representative exercises or their equivalent while retaining the distinction between core statistical methods and dataset-specific examples. If preparing for exact lab tasks, use the source datasets when available.

## Colloquium coverage (`PRiAD_kolos` — 15 points)

- **Task 1 — 3 points:** observation/class/feature counts, per-class sizes, missing values, drop incomplete records — **covered as individual operations**, but needs an independent timed simulation and a reusable missing-count function.
- **Task 2 — 4 points:** compare variability globally and within classes with appropriate plots and written interpretation — **numerical part covered; graphical interpretation open**.
- **Task 3 — 4 points:** inter-feature correlation and features separating classes, with plots — **open**.
- **Task 4 — 4 points:** redundant features based both on mutual similarity and class separability — **open**.

## Roadmap, ordered by next learning value

### M1 — Data exploration and manipulation — MAIN CODE COMPLETE, DOC REVIEW PENDING

Keep original analysis; fix two indexing/column-name issues and add evidence-based Markdown findings.

### M2 — Descriptive statistics and NumPy — CORE COMPLETE, SUPPLEMENT PENDING

Core measures and NumPy array operations implemented. Future: mode/range/`describe`, matrix operations and copying/view semantics.

### M3 — Data cleaning — IMPLEMENTED, FINAL QA PENDING

Complete missing-count function, verify imputed null counts, correct narrative conclusions; optional two-feature comparison, then Run All + commit.

### M4 — Statistical visualization — **NEXT**

Create `notebooks/03_visual_exploration.ipynb`. Learn Matplotlib/Seaborn and compare `Area`, `Perimeter`, `Eccentricity` overall and by class with histograms, KDE, boxplots and violin plots. Include `bins` experiments; interpret spread, overlap, outliers, imbalance. Then line/bar/stacked/barh and a generic feature/class plotter. Directly addresses colloquium Task 2.

### M5 — Correlation and multivariate relationships

Use covariance, Pearson coefficients, `corr`, `cov`, `np.corrcoef`, `np.cov`, heatmaps, scatter/pair plots and Anscombe quartet. Identify candidate class-separating features. Directly addresses Task 3.

### M6 — Redundant and discriminating features

Evaluate high feature-feature correlation, feature-specific class separation and evidence for dropping/retaining attributes; distinguish correlation from usefulness. Directly addresses Task 4.

### M7 — Time series and combining tables

Use currency/market or passenger dataset; `merge/concat`, dates, `resample`, `shift`, growth in absolute/relative terms; temporal line/bar charts. Cover PRiAD 1 and 2 examples.

### M8 — Text analysis

Analyze a legally reusable full text or supplied text; per-section word/character distributions and descriptive statistics.

### M9 — Image processing and deeper NumPy

Pixel array manipulation, color space conversion and histograms. Complete array creation, concatenation, matrix algebra, file IO and copy/view exercises that don't fit the research narrative.

### M10 — Timed colloquium simulation

Independently solve all four original task types on a fresh dataset produced with `make_classification`, including answers in Markdown. Review performance and weaknesses, then redo on an unseen dataset. No reliance on previous solutions.

## Exercise 9 — next practical assignment

**Notebook:** `notebooks/03_visual_exploration.ipynb`

1. Write an introduction explaining the research question: *Which morphological attributes help distinguish dry-bean varieties?*
2. Use the original complete `df`, **not** the artificially corrupted dataset, for initial plots.
3. Draw an overall histogram of `Area` using at least **three bin counts**; explain what changes when `bins` changes.
4. Compare Area distributions **between classes** (histograms and/or KDE) with a legend; note that raw counts can be affected by class imbalance.
5. Create **boxplots** and **violin plots** for `Area` by `Class` and interpret medians, IQR, spread, potential outliers and overlap.
6. Repeat one distribution comparison for **Perimeter** and **Eccentricity**; discuss which seems more discriminative and why.
7. Add concise Markdown conclusions supported by the plots, not just code execution.

**Help available when coding:** `matplotlib.pyplot`, `seaborn.histplot`, `seaborn.boxplot`, `seaborn.violinplot`; learn parameters `x`, `hue`, `bins`, `stat`, `common_norm`, and appropriate figure sizing. Student attempts implementation first; assistant reviews.

## Git workflow and repository layout

```text
Dry-Bean-Analytics/
├── data/{raw,processed}/
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_visual_exploration.ipynb   # NEXT
│   ├── 04_feature_relationships.ipynb
│   ├── 05_feature_redundancy.ipynb
│   └── supplementary/{time_series,text_analysis,image_analysis,numpy_experiments}.ipynb
├── src/                              # Add only when reusable code emerges
├── reports/
├── README.md
├── ROADMAP.md
├── requirements.txt
└── .gitignore
```

After correcting known notebook issues and completing the current milestone: **restart kernel, Run All, inspect saved outputs, commit with meaningful message, and push**. GitHub state was not verified in this audit; statuses are based on uploaded notebooks only.

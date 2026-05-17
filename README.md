# Mpox-narrative-surveillance
Beyond Early Warning: A Validated Multi-class Classifier for Concurrent Mpox Narrative Surveillance on Social Media
Overview
This repository contains the code, labeled datasets, and full report for our Harvard Extension School Data Science Capstone project, completed in May 2026 in collaboration with the University of Montreal Mpox research program.
We developed and validated an automated multi-class narrative classification framework for monitoring Mpox-related public discourse on Meta (Facebook) and X (Twitter) — analyzing 600,000+ posts spanning January 2022 through March 2026.
Classified weekly signals were integrated with three external epidemiological anchors:

CDC Daily Mpox Case Counts
CDC National Wastewater Surveillance System (NWSS) viral load data
GDELT global media event metrics


Team
NameRoleRoshini JayasankarProject Lead · Formal Analysis · Annotation · WritingHumphrey LimMethodology · Annotation Framework · Formal AnalysisKevin HuangSoftware · Validation · Data Curation · VisualizationSuong DoanConceptualization · Formal Analysis · Visualization
Sponsoring Scientist: Dr. Bouchra R. Nasri — University of Montreal
Technical Advisor: Muthu Venkataraman
Capstone Faculty: Bruce Huang · Stephen F. Elston — Harvard Extension School

Key Findings

Fear/anxiety discourse on X preceded CDC case reporting by 3–4 weeks — the most consistent early signal identified across the analysis window
Stigma tracks media and news cycles, not biological transmission — stigma correlated positively with CDC cases (ρ = +0.48) but negatively with wastewater viral load (ρ = −0.43), confirming it is a social signal, not an epidemic one
Meta and X serve structurally different roles — X is enriched in stigma (19.8%), misinformation (14.7%), and fear/anxiety (10.2%); Meta is dominated by neutral (29.4%) and outbreak (24.6%) content
Outbreak and stigma retain significant associations with CDC case counts after controlling for total post volume (partial ρ = +0.40 and +0.36 respectively)
Misinformation lags behind case peaks — it rises after the outbreak is established, not before


Methods
Data Sources
SourceVolumeWindowMeta (Facebook) — via Meta Content Library83,395 English postsJan 2022 – Mar 2026X (Twitter)549,107 US-filtered postsJun 2022 – Dec 2024CDC Daily Mpox Case CountsNational weekly aggregatesFull windowCDC NWSS Wastewater184 weeksAug 2022 – Dec 2024GDELT Events + GKG193–194 weeksFull window
8-Class Narrative Schema
core_disease · fear_anxiety · misinformation · neutral · outbreak · stigma · unclear_other · vaccine_treatment
Annotation Pipeline
Two-stage Champion-Challenger pipeline with four human annotators:

2,390 gold-labeled posts (1,117 Meta + 1,273 X)
Inter-annotator agreement: κ = 0.87 (Meta) · κ = 0.73 (X)
Threshold to proceed: κ = 0.70

Champion Models
PlatformModelMacro-F1AccuracyMetaModernBERT0.8070.834X (Twitter)Twitter-XLM-RoBERTa Large0.7530.833
Statistical Analysis

Partial Spearman correlation controlling for total post volume
Cross-source pairwise correlations across 5 sources
Lead-lag analysis (±8 week window, Spearman CCF)
Bootstrap confidence intervals · Permutation-based p-values


Repository Structure
mpox-narrative-surveillance/
│
├── README.md
│
├── report/
│   └── Mpox_Capstone_Project_Report.pdf
│
├── data/
│   ├── weekly_signals/          ← aggregated weekly class counts (no post text)
│   └── labeled/                 ← gold-labeled benchmark datasets
│
├── notebooks/
│   ├── 01_eda/                  ← exploratory data analysis
│   ├── 02_annotation/           ← champion-challenger pipeline
│   ├── 03_modeling/             ← classifier training and evaluation
│   └── 04_signal_analysis/      ← cross-source integration and lead-lag
│
├── src/
│   ├── classifiers/             ← ModernBERT and XLM-RoBERTa training scripts
│   ├── annotation/              ← champion-challenger pipeline code
│   └── analysis/                ← spearman, lead-lag, partial correlation
│
└── outputs/
    ├── model_cards/             ← model cards (Appendix VII)
    └── figures/                 ← all report figures

Note: Raw post text from Meta and X is not included in this repository in compliance with Meta Content Library terms of use and X data policies. Aggregated weekly signal files (counts and labels only) are available in /data/weekly_signals/.


Reproducibility
Classifier training and inference were executed on Apple workstations using PyTorch 2.x. Statistical analyses used Python 3.10 with pandas, NumPy, statsmodels, and SciPy.
To replicate the Meta analysis, independent Meta Content Library research access is required. Retrieval criteria are documented in Section 3.1.1 of the full report.

Data & Privacy

Post text was used for classifier training and inference only — never sent to any external API
All downstream analysis used aggregated counts, labels, and metadata — no raw post text
Individual users were not tracked or identified
Meta Content Library data will be deleted on termination of access per platform terms


Report
The full capstone report is available in the /report directory.
Citation:

Lim, H., Huang, K., Jayasankar, R., & Doan, S. (2026). Beyond Early Warning: A Validated Multi-class Classifier for Concurrent Mpox Narrative Surveillance on Social Media. Harvard Extension School Capstone Report.


Status
ComponentStatusFull Report✅ CompleteGold-Labeled Datasets✅ AvailableWeekly Signal Data✅ AvailableAnnotation Pipeline Code🔄 Coming SoonClassifier Training Code🔄 Coming SoonAnalysis Notebooks🔄 Coming Soon
Code and notebooks are being finalized and will be added shortly.

Acknowledgements
This project was completed as part of the Data Science Capstone course for the Master of Liberal Arts in Extension Studies, Harvard University. The team thanks the University of Montreal Mpox research program, Meta Platforms for research access through the Meta Content Library, and the United States Centers for Disease Control and Prevention for maintaining publicly accessible Mpox case-count data.

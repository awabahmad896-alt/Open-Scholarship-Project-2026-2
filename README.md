# Frontiers of Memory: A Data Geography Analysis of Roman Imperial Heritage

This project analyses how the digital representation of the Roman Empire varies across modern national institutions, using metadata harvested from the Europeana open heritage platform. The central research question is: **which countries act as the primary digital custodians of Roman Imperial heritage, and how does metadata quality differ between them?**

---

## Research Question

How does the digital representation of the Roman Empire vary across modern national institutions, and which countries act as the primary digital custodians of this heritage?

---

## Dataset

The dataset is sourced from the Europeana API ([https://api.europeana.eu](https://api.europeana.eu)), utilizing the "rich" profile to extract extensive metadata regarding cultural heritage objects tagged with "Roman Empire". The data covers records contributed by European national and regional institutions with no fixed time restriction on the objects themselves. Access was obtained programmatically via the Europeana REST API using cursor-based pagination. The dataset is subject to Europeana's terms of use; individual records may carry varying licenses depending on the contributing institution (see [https://www.europeana.eu/en/rights](https://www.europeana.eu/en/rights)).

---

## Repository Structure

```text
Open-Scholarship-Project-2026-2/
├── data/
│   ├── raw/               # Raw CSV as downloaded from the Europeana API, unchanged
│   └── processed/         # Cleaned and enriched CSV used for analysis
├── notebooks/
│   └── 01_reproducible_workflow.ipynb   # Main notebook (run top to bottom)
└── README.md

Workflow
1. Repository Exploration
The Europeana platform (https://www.europeana.eu) was identified as the primary open heritage repository for this project. Europeana aggregates digitised cultural heritage objects from European institutions and provides open API access with structured metadata.

2. Dataset Collection
The Europeana REST API was queried with the search term "Roman Empire" using the "rich" metadata profile. A cursor-based pagination loop was used to extract all available records. The raw response was saved as a CSV to data/raw/. After evaluating coverage and metadata quality, the dataset was narrowed to 47,157 records with 9 usable columns, reducing the original 631-column schema.

3. Research Questions
The dataset's country, dataProvider, and completeness fields directly address the research question by allowing comparison of record volume and metadata quality across contributing nations and institutions.
4. Workflow Plan
Data Access: Query the Europeana REST API and save raw CSV to data/raw/.

Selection & Cleaning: Flatten the data, handle unhashable list-type fields, filter to 9 key columns, handle missing values, and save the result to data/processed/.

Enrichment: Engineer a quality_category variable by mapping completeness scores (0–10) to categorical tiers (low / medium / high). Shorten titles to title_short for memory efficiency.

Analysis & Visualisation: Group by country and dataProvider to calculate record volume and average completeness. Generate bar charts comparing top European providers.

Archiving: Maintain version control via GitHub.

5. AI Implementation
See Generative AI Use Declaration below.

6. Enrichment
Two new variables were engineered during processing:

quality_category: derived from completeness by binning scores into low (0–3), medium (4–6), and high (7–10) tiers.

title_short: a truncated version of the original title field, created to reduce memory usage.
Raw data was not modified; all transformations were applied in the notebook and saved to data/processed/.
7. Analysis & Interpretation
Records were grouped by country and provider to compare digital custodianship patterns. Visualisations show which nations and institutions contribute the most records and which have the highest average metadata completeness. Initial interpretation suggests significant concentration among a small number of Western European providers, with metadata quality varying considerably across countries.
Variable,Description,Values / Units
country,Modern nation-state hosting the data provider,Country name (string)
dataProvider,Holding institution or museum name,Institution name (string)
language,ISO language code of the metadata record,"ISO 639 code (e.g., en, de, fr)"
type,Object classification,"TEXT, IMAGE, VIDEO, SOUND, 3D"
completeness,Metadata richness score assigned by Europeana,Integer scale 0–10
quality_category,Engineered tier based on completeness score,"low (0–3), medium (4–6), high (7–10)"
year,Temporal era indicator from metadata,Year or era string
title_short,Truncated record title for memory efficiency,String (engineered from original title field)
score,Europeana query relevance ranking at ingestion,Float
Metadata Guide
Source: Europeana (https://api.europeana.eu)

Collection: Objects tagged with the query term "Roman Empire" via the REST API, "rich" profile

Coverage: European cultural heritage institutions; no fixed date range on the objects; records collected in 2026

Geographical scope: European national and regional institutions

Main entities represented: Digitised cultural heritage objects (texts, images, artefacts) associated with the Roman Empire

Method of access: Europeana REST API, cursor-based pagination, programmatic download

License / terms: Europeana terms of use apply; see https://www.europeana.eu/en/rights. Individual records carry institution-specific licenses.

Ethical considerations: The dataset consists of institutional metadata about historical objects. No personal data is included. The category "Roman Empire" is a curatorial label applied by contributing institutions and may reflect particular historiographical traditions in how Roman heritage is framed and preserved.

Environment & Reproducibility
Language: Python 3

Main tools: Jupyter Notebook, pandas, requests, matplotlib, seaborn

Dependencies (also listed in requirements.txt):

requests

pandas

matplotlib

seaborn

jupyter

To reproduce:

Install dependencies: pip install -r requirements.txt

Open notebooks/01_reproducible_workflow.ipynb

Run all cells from top to bottom

No OS-specific assumptions. Tested on Python 3.10+.

Ethics & Limitations
The dataset is derived from institutional metadata and contains no personal or sensitive data.

Records are limited to what Europeana member institutions have chosen to digitise and tag. This introduces selection bias: wealthier or more digitally active institutions are likely overrepresented.

The search term "Roman Empire" is a curatorial label; coverage depends on how individual institutions have indexed their collections, which varies.

Missing values in year, language, and type fields were present in a portion of records and were retained or dropped depending on the analysis step (documented in the notebook).

This analysis reflects the state of Europeana's holdings at the time of data collection (2026) and may not generalise to the full landscape of Roman heritage digitisation globally.

Generative AI Use Declaration
Implementation: AI was used strictly as a technical coding partner to handle JSON schema flattening logic, column memory optimisations, and pagination loop error handling. No historical analysis, target variable definitions, or interpretations were machine-generated.

Risks considered: AI-generated code was reviewed manually before use. No AI output was accepted without verification against the actual data structure.

Prompt example: "Act as a senior pandas data engineer. Optimise a cursor-pagination loop to extract 47k nested records, truncate sparse object schemas from 631 down to 9 target columns, and output a memory-safe dataframe under 25MB."

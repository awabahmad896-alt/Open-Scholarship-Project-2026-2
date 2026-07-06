# Frontiers of Memory: A Data Geography Analysis of Roman Imperial Heritage

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20836645.svg)](https://doi.org/10.5281/zenodo.20836645)

**Open Scholarship Project 2026**

This project analyses how the digital representation of the Roman Empire varies across modern national institutions, using metadata harvested from the Europeana open heritage platform. 

---

## Research Question

**How does the digital representation of the Roman Empire vary across modern national institutions, and which countries act as the primary digital custodians of this heritage?**

---

## Repository Structure

* **`data/`** 
  * `raw/` — Raw CSV as downloaded from the Europeana API, unchanged.
  * `processed/` — Cleaned and enriched CSV used for analysis.
* **`docs/`** — Added rules to block hidden Jupyter checkpoint files.
* **`notebooks/`** 
  * `01_reproducible_workflow.ipynb` — Main notebook (run top to bottom).
* **`outputs/`** — Saved analysis visualisations and charts.
* **`report/`** 
  * `project_report.md` — Project report documentation.
* **`.gitignore`** — Rules for Git to ignore local background files.
* **`README.md`** — Project documentation guide.
* **`requirements.txt`** — Software environment dependencies layout.

---

## Dataset & Licensing

The dataset is sourced from the [Europeana API](https://api.europeana.eu), utilizing the "rich" profile to extract extensive metadata regarding cultural heritage objects tagged with "Roman Empire". The data covers records contributed by European national and regional institutions with no fixed time restriction on the objects themselves. 

**Licensing & Access:** The dataset is subject to Europeana's terms of use; individual records may carry varying licenses depending on the contributing institution (see [Europeana Rights](https://www.europeana.eu/en/rights)). Access was obtained programmatically via the REST API using cursor-based pagination. 

The cleaned dataset used for this analysis is permanently archived on Zenodo and can be accessed via the DOI badge above.

---

## Workflow

### 1. Repository Exploration
The Europeana platform (https://www.europeana.eu) was identified as the primary open heritage repository for this project. Europeana aggregates digitised cultural heritage objects from European institutions and provides open API access with structured metadata.

### 2. Research Questions & Data Mapping
The dataset's `country`, `dataProvider`, and `completeness` fields directly address the research question by allowing a direct comparison of record volume and metadata quality across contributing nations and institutions.

### 3. Dataset Collection
The Europeana REST API was queried with the search term "Roman Empire". A cursor-based pagination loop was used to extract all available records to `data/raw/`. After evaluating coverage, the dataset was narrowed to 47,157 records with 9 usable columns, significantly reducing the original 631-column schema.

### 4. Workflow Plan
* **Selection & Cleaning:** Flatten the data, handle unhashable list-type fields, filter key columns, handle missing values, and save to `data/processed/`.
* **Enrichment:** Engineer a `quality_category` variable by mapping `completeness` scores (0–10) to categorical tiers (low/medium/high). Shorten titles to `title_short` for memory efficiency. Raw data was never modified; all transformations happen in the notebook.
* **Analysis:** Group by `country` and `dataProvider` to calculate record volume and average completeness. Generate comparative bar charts.

---

## Data Dictionary

The processed dataset (`data/processed/`) consists of 47,157 rows and 9 columns:

| Variable | Description | Values / Units |
|---|---|---|
| `country` | Modern nation-state hosting the data provider | Country name (string) |
| `dataProvider` | Holding institution or museum name | Institution name (string) |
| `language` | ISO language code of the metadata record | ISO 639 code (e.g., `en`, `de`, `fr`) |
| `type` | Object classification | `TEXT`, `IMAGE`, `VIDEO`, `SOUND`, `3D` |
| `completeness` | Metadata richness score assigned by Europeana | Integer scale 0–10 |
| `quality_category` | Engineered tier based on completeness score | `low` (0–3), `medium` (4–6), `high` (7–10) |
| `year` | Ingestion, digitization, or publication year provided by the museum | Year string (e.g., `2006`) |
| `title_short` | Truncated record title for memory efficiency | String |
| `score` | Europeana query relevance ranking at ingestion | Float |

---

## Metadata Guide

* **Source:** Europeana (https://api.europeana.eu)
* **Collection:** Objects tagged with "Roman Empire" via the REST API, "rich" profile.
* **Coverage:** European cultural heritage institutions; collected in 2026.
* **Geographical scope:** European national and regional institutions.
* **Entities represented:** Digitised cultural heritage objects (texts, images, artefacts) associated with the Roman Empire.
* **Method of access:** Programmatic download via REST API and cursor-based pagination.
* **Ethical considerations:** The dataset consists of institutional metadata about historical objects. No personal data is included. "Roman Empire" is a curatorial label applied by contributing institutions and reflects specific historiographical traditions.

---

## Environment & Reproducibility

**Language:** Python 3  
**Main tools:** Jupyter Notebook, pandas, requests, matplotlib, seaborn  

To regenerate the entire project, run the main notebook from top to bottom. No OS-specific assumptions; tested on Python 3.10+.

1. Install dependencies: `pip install -r requirements.txt`
2. Open `notebooks/01_reproducible_workflow.ipynb`
3. Run all cells from top to bottom. It will query the API, clean the data, and produce the visualisations.

---

## Ethics & Limitations

* **Coverage bias:** The dataset only includes institutions that contribute to Europeana. Many important holders of Roman Imperial heritage (especially outside Western Europe, or those lacking digital infrastructure) are absent, meaning wealthier institutions are overrepresented.
* **Search term bias:** Results depend entirely on the keyword "Roman Empire" appearing in the metadata. Objects described using regional, non-English, or highly specific terms may be missed entirely.
* **Completeness score:** The `completeness` metric is Europeana's internal measure. It does not reflect scholarly or archival quality, only how many metadata fields were populated.
* **Temporal scope:** The `year` field is sparsely populated and inconsistently formatted. Many institutions input their digitization or publication year rather than the object's historical era, limiting temporal analysis.
* **Missing values:** Missing values in `year`, `language`, and `type` fields were present and retained or dropped depending on the specific analysis step (documented in the code).
* **Snapshot in time:** This analysis reflects the state of Europeana's holdings at the time of data collection (2026) and may not generalise to the global landscape of Roman heritage digitisation.

---

## Generative AI Use Declaration

* **Implementation:** AI was used strictly as a technical coding partner to handle JSON schema flattening logic, column memory optimisations, and pagination loop error handling. No historical analysis, target variable definitions, or interpretations were machine-generated.
* **Risks considered:** AI-generated code was reviewed manually before use. No AI output was accepted without verification against the actual data structure.
* **Prompt example:** *"Act as a senior pandas data engineer. Optimise a cursor-pagination loop to extract 47k nested records, truncate sparse object schemas from 631 down to 9 target columns, and output a memory-safe dataframe under 25MB."*

# Frontiers of Memory: A Data Geography Analysis of Roman Imperial Heritage

## Research Question
How does the digital representation of the Roman Empire vary across modern national institutions, and which countries act as the primary digital custodians of this heritage?

## Dataset
The dataset is sourced from the Europeana API, utilizing the "rich" profile to extract extensive metadata regarding cultural heritage objects tagged with "Roman Empire".

## Workflow Plan
1. **Data Access:** Query the Europeana REST API to extract raw JSON metadata and save it to the `data/` folder.
2. **Selection & Cleaning:** Flatten the JSON, handle unhashable lists, filter for key metadata columns (country, provider, completeness), and handle missing values.
3. **Analysis & Visualisation:** Group data by `country` and `provider` to calculate volume and average completeness scores, and generate charts to compare top European providers.
4. **Archiving:** Maintain version control via GitHub and ensure all notebooks are reproducible.
##  Data Appendix & Variables (TIER Section 5)
The optimized target dataset consists of 47,157 rows and 9 core columns selected to fit within strict resource thresholds:
* `country`: Modern nation-state hosting the data provider.
* `dataProvider`: Holding institution/museum name.
* `language`: ISO metadata language code.
* `type`: Object classification (e.g., TEXT, IMAGE).
* `completeness`: Metadata richness metric (Scale 0-10).
* `quality_category`: Custom engineered quality tier mapped from completeness scores.
* `year`: Temporal era indicator.
* `title_short`: Shortened record title optimized for memory layout.
* `score`: Ingestion query relevance ranking.

##  Generative AI Use Declaration 
* **Implementation:** AI was utilized strictly as a technical layout partner to handle JSON schema flattening logic, column memory optimizations, and pagination loop error boundaries. No historical analytics, target variables, or interpretations were machine-generated.
* **Prompt Framework Example:** "Act as a senior pandas data engineer. Optimize a cursor-pagination loop to extract 47k nested records, truncate sparse object schemas from 631 down to 9 target columns, and output a memory-safe dataframe under 25MB."

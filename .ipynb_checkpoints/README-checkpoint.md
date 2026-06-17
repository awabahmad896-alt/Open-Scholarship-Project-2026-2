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

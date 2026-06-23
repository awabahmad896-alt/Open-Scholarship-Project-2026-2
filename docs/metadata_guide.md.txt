# Metadata Guide

## Data Source
- **Platform:** Europeana  
- **API:** Europeana REST API v2  
- **URL:** https://api.europeana.eu/record/v2/search.json  
- **Profile used:** `rich`  
- **Query term:** "Roman Empire"

## Coverage
- **Geographic scope:** European national institutions (any country represented in Europeana)  
- **Temporal scope:** All historical periods tagged with "Roman Empire" metadata; data collected in 2026  
- **Record count:** 47,157 records after filtering

## Main Entities
Cultural heritage objects (physical and digital artefacts) held by European institutions, described via standardised Europeana metadata.

## Method of Access
Data was collected via the Europeana REST API using cursor-based pagination. Raw JSON/CSV responses were saved to `data/raw/` and then flattened and filtered in the notebooks.

## License & Terms of Use
Europeana metadata is made available under the Creative Commons CC0 1.0 Universal Public Domain Dedication. Individual object rights vary by record and are indicated in the `edmRights` field. See: https://www.europeana.eu/en/rights

## Ethical & Contextual Notes
This dataset reflects which European national institutions have chosen to digitise and share Roman Imperial heritage via Europeana. Countries with larger digitisation budgets or longer museum traditions are likely over-represented. The framing of objects as "Roman Empire" heritage is itself a curatorial and political choice — materials from regions once under Roman rule are often catalogued primarily through a Western European lens. Results should be interpreted as a snapshot of *digital custodianship*, not of historical significance or cultural ownership.
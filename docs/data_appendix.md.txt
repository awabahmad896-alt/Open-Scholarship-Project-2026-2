# Data Appendix

## Dataset: Roman_Empire_Europeana_Clean.csv

**Location:** `data/processed/`  
**Rows:** 47,157  
**Columns:** 9

| Variable | Description | Values / Units |
|---|---|---|
| `country` | Modern nation-state hosting the data provider | ISO country name (string) |
| `dataProvider` | Name of the holding institution or museum | String |
| `language` | Language of the metadata record | ISO 639-1 code (e.g. `en`, `de`, `fr`) |
| `type` | Object classification | `TEXT`, `IMAGE`, `VIDEO`, `SOUND`, `3D` |
| `completeness` | Europeana metadata richness score | Integer, scale 0–10 |
| `quality_category` | Custom quality tier derived from `completeness` | `low` (0–3), `medium` (4–6), `high` (7–10) |
| `year` | Temporal era indicator derived from record metadata | Integer or string (e.g. `1st century CE`) |
| `title_short` | Record title truncated for memory efficiency | String, max ~80 characters |
| `score` | Relevance score assigned by Europeana API at ingestion | Float |

## New Variables Created During Processing
- **`quality_category`**: Mapped from `completeness` using threshold binning.  
- **`title_short`**: Truncated from the original `title` field to reduce memory footprint.
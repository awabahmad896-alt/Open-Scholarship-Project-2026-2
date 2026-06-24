# The Art of Making Data Speak: Digital Custodianship of the Roman Empire

## 1. Introduction
The digital representation of historical artifacts is rarely neutral. As cultural institutions digitize their collections, biases emerge regarding which nations have the resources to process, host, and describe this heritage. This project investigates the digital custodianship of the Roman Empire by extracting and analyzing metadata from the Europeana REST API. By bridging sociological inquiry with computational data analysis, this report aims to uncover the patterns and metadata biases present among modern European nations.

## 2. Reproducible Workflow: From Local Environment to Remote Repository
To ensure total transparency and adherence to the TIER (Teaching Integrity in Empirical Research) protocol, the entire workflow was designed to be seamlessly reproducible from a local machine to a web-based GitHub repository.

### Local Setup and Execution
1. **Environment Initialization:** The project relies on a strict set of Python dependencies (`pandas`, `requests`, `matplotlib`, `seaborn`), locked within a `requirements.txt` file to prevent version conflicts across different machines.
2. **Automated Pipeline:** The core engine is a single Jupyter Notebook (`01_reproducible_workflow.ipynb`). When executed top-to-bottom on a local laptop, it automatically contacts the Europeana API, handles pagination to extract 47,157 raw records, processes the JSON into a flattened pandas DataFrame, and engineers new analytical features.
3. **Relative Pathing:** All data ingestion and output generation utilize the `os` and `pathlib` libraries to map relative directories (e.g., `../data/raw/`). This ensures the code runs flawlessly on any local machine without relying on hardcoded personal computer paths.

### Version Control and Web Deployment
Uploading a large-scale data project to GitHub required careful repository management to adhere to web hosting limits:
* **Managing Big Data:** The raw, unlimited extraction file exceeded GitHub's 100MB file limit. To resolve this, the `data/raw/` directory was targeted via a `.gitignore` file, while a blank `.gitkeep` anchor was used to preserve the folder structure on the remote server without uploading the massive CSV.
* **State Management:** Local Jupyter checkpoints (`.ipynb_checkpoints/`) were systematically ignored to keep the repository history clean.
* **Final Push:** Once the local notebook generated the clean datasets (`data/processed/`) and visualisations (`outputs/`), the lightweight, processed assets were committed and pushed to the remote GitHub main branch, providing a fully audited, open-access research repository.

## 3. Data Processing and Feature Engineering
The raw JSON data from Europeana is heavily nested and often inconsistent. The cleaning phase involved flattening lists into strings and handling missing variables. Crucially, two specific data engineering decisions were made:
* **Quality Categorization:** A custom variable (`quality_category`) was engineered to translate Europeana's numerical `completeness` score into accessible tiers: High (Rich Metadata), Medium, and Low (Minimal Data).
* **Geographic Sanitization:** Ambiguous data provider tags, such as records generically labeled as "Europe" rather than a sovereign nation-state, were programmatically dropped from the final dataset to ensure an accurate comparative analysis between modern nations.

## 4. Visual Analysis

### 4.1 The Volume Story: Who Dominates the Database?
![Volume Analysis](../outputs/01_volume_by_country.png)
*Observation:* The volume chart reveals a stark geographic imbalance. Romania overwhelmingly dominates the dataset in total volume (exceeding 15,000 records), followed by Germany, Greece, and Austria. This highlights a fundamental bias in digital humanities: the sheer volume of the online narrative is heavily skewed toward specific national archives rather than being evenly distributed.

### 4.2 The Quality Story: The Paradox of Quantity
![Completeness Analysis](../outputs/02_completeness_by_country.png)
*Observation:* High volume does not equate to high utility. This chart measures the average metadata richness for the top contributing nations. Romania, despite being the #1 contributor by volume, has an average completeness score near zero. Conversely, nations like Hungary, the Czech Republic, and Spain maintain nearly perfect completeness scores, suggesting a focus on meticulous cataloging over sheer mass uploading.

### 4.3 Media Dominance over Technological Diversity
![Media Type Analysis](../outputs/03_media_type_by_country.png)
*Observation:* The media type breakdown reveals a lack of technological diversity across the board. Rather than a gap in advanced technologies like 3D modeling or video (which are entirely absent in the top 10), the data shows a universal reliance on flat images. Germany and Greece also show substantial volumes of digitized text, but the overall digital representation of the Roman Empire remains overwhelmingly 2D.

### 4.4 The "Junk Data" Ratio
![Quality Distribution](../outputs/04_quality_distribution.png)
*Observation:* Utilizing the custom `quality_category` variable, this 100% stacked bar chart exposes the ratio of high-quality metadata to minimal or "junk" data. It vividly confirms the quantity paradox: Romania's massive dataset is almost entirely comprised of "Low (Minimal Data)" records lacking historical context. In contrast, institutions in Hungary, France, Austria, and Italy provide almost exclusively High-Quality metadata, proving that true open scholarship relies on deep curation, not just data dumping.

## 5. Conclusion
This project successfully demonstrates a fully automated, reproducible data science pipeline. Beyond the technical execution, the analysis confirms that digital archives like Europeana are deeply influenced by the operational realities of the institutions that upload them. The data reveals a clear tension between mass digitization (seen in Romania's high-volume, low-quality uploads) and meaningful metadata curation (seen in Hungary's low-volume, highly detailed records).
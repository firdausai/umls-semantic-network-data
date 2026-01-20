# UMLS Semantic Network (CSV & Parquet)

This repository contains dataset exports of the **UMLS Semantic Network**, available in both **CSV** and **Parquet** formats.

These files provide a machine-readable reference for the high-level categories (Semantic Types) and relationships (Semantic Relations) used to classify concepts within the [Unified Medical Language System (UMLS)](https://www.nlm.nih.gov/research/umls/index.html) Metathesaurus.

## About the Data

The [UMLS Semantic Network](https://uts.nlm.nih.gov/uts/umls/semantic-network/root) is one of three Knowledge Sources developed by the National Library of Medicine (NLM). It provides a consistent categorization of all concepts represented in the UMLS Metathesaurus.

The network consists of:
1.  **Semantic Types:** Broad categories (e.g., "Disease or Syndrome", "Clinical Drug", "Organism").
2.  **Semantic Relations:** Relationships that exist between these types (e.g., "treats", "causes", "location_of").

## File Contents

The repository includes the following files:

### 1. Semantic Types
*   **Files:** `UMLS Semantic Network - type.csv`, `umls_semantic_network_type.parquet`
*   **Description:** Defines the nodes in the Semantic Network.

| Column | Description |
| :--- | :--- |
| `semantic_type` | The name of the category (e.g., "Disease or Syndrome"). |
| `definition` | A text description of what the type encompasses. |
| `identifier` | The unique Type Unique Identifier (TUI) (e.g., "T047"). |
| `note` | Additional usage notes or guidelines for assigning this type. |

### 2. Semantic Relations
*   **Files:** `UMLS Semantic Network - relation.csv`, `umls_semantic_network_relation.parquet`
*   **Description:** Defines the edges/relationships available in the Semantic Network.

| Column | Description |
| :--- | :--- |
| `semantic_relations` | The name of the relationship (e.g., "treats", "part_of"). |
| `definition` | A text description of the relationship's meaning. |
| `identifier` | The unique identifier for the relation (e.g., "T154"). |
| `note` | Context on how the relationship is applied. |

## Usage Examples

### Python (Pandas)

You can easily load these datasets using Python and Pandas. The Parquet format is recommended for faster I/O and preserved data types.

```python
import pandas as pd

# Load Semantic Types (Parquet)
types_df = pd.read_parquet('umls_semantic_network_type.parquet')

# View the definition of "Disease or Syndrome" (T047)
disease_type = types_df[types_df['identifier'] == 'T047']
print(disease_type[['semantic_type', 'definition']])

# Load Semantic Relations (CSV)
relations_df = pd.read_csv('UMLS Semantic Network - relation.csv')

# Find all relations regarding "treatment"
treatment_rels = relations_df[relations_df['semantic_relations'].str.contains('treat', case=False)]
print(treatment_rels)
```

## Data Accuracy
Please note that these files were copy-pasted by hand. If you encounter any errors or inconsistencies, please **create an issue** in this repository so it can be fixed.

## Source and Attribution

This data was sourced from the **National Library of Medicine (NLM)** Unified Medical Language System (UMLS).

*   **Source URL:** [https://uts.nlm.nih.gov/uts/umls/semantic-network/root](https://uts.nlm.nih.gov/uts/umls/semantic-network/root)
*   **Publisher:** U.S. National Library of Medicine

## License & Disclaimer

**Please Note:** The UMLS Semantic Network and Metathesaurus are subject to the **UMLS Metathesaurus License**. 

*This repository provides these files for educational and ease-of-access purposes and is not officially affiliated with the NLM.*

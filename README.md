# Dataset Profiling and LLM-Based Interpretation

This project implements an automated pipeline for dataset profiling and high-level interpretation using a locally deployed Large Language Model (LLM).

The workflow is designed to produce a structured, machine-readable summary of a dataset and then generate concise, actionable insights in natural language, without relying on external APIs or cloud-based services.

---

## Project Structure

```
dataset-profiling-and-llm-interpretation
│
├── src/
│    ├── dataset_profiling.ipynb
│    ├── llm_insights.py # LLM-based interpretation script
│    ├── processed_data.json # Dataset profiling output (JSON)
│    ├── dataset_interpretation.txt # LLM-generated interpretation
│    └──data/
│         └── data.csv # Input dataset
└── README.md
```
---

## Overview

The project is divided into two clearly separated stages:

### 1. Dataset Profiling (Deterministic Analysis)

A Jupyter Notebook performs an automated, dataset-agnostic exploratory analysis and generates a structured JSON report containing:

- Global dataset metadata (size, memory usage, duplicated rows, missing value ratios)
- Per-column statistics and summaries
- Detection of potential data quality issues (missing values, constant columns, zero variance)
- Identification of index and identifier columns
- Basic preprocessing recommendations (e.g. scaling, encoding, exclusion)

The output of this stage is a reproducible and interpretable profiling artifact (`processed_data.json`).

---

### 2. LLM-Based Interpretation (Analytical Reasoning)

A standalone Python script (`llm_insights.py`) consumes the profiling JSON and queries a **locally hosted LLM** (via Ollama) to generate:

- A concise executive summary of the dataset
- Identification of relevant risks (data quality, outliers, leakage, sparsity)
- Concrete and technically actionable preprocessing recommendations

The LLM is used strictly for **interpretation and reasoning**, not for computing statistics.  
All numerical analysis is performed beforehand in the profiling stage.

The final output is a human-readable text report (`dataset_interpretation.txt`).

---

## Requirements

- Python 3.10+
- `pandas`
- `requests`
- A local LLM runtime (Ollama recommended)

---

## Example of Local LLM Setup (Ollama)

1. Install llama3.1 using the bash comand `ollama pull llama3.1`
2. Verify the server is running using `ollama run llama3.1`

---

## Usage
1. Generate the profiling JSON running the notebook `dataset_profiling.ipynb`. This will produce the file processed_data.json
2. Run the pyhton file using `python llm_insights.py`. This will generate a plain text file `dataset_interpretation.txt`. Make sure to install the local LLM model before this step.

---
## Intended Use Cases:
- Initial dataset assessment
- Data quality validation
- Feature engineering planning
- Pre-ML exploratory analysis
- Reproducible reporting pipelines

---

## Notes

This project is intended as an analytical tooling example rather than a production-grade data validation framework.
However, its modular design allows easy extension with additional quality rules, alternative models, or structured output formats.

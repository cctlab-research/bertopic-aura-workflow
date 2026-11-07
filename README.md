# BERTopic Theme Alignment: AURA Workflow

This repository contains the Python code for BERTopic modeling and computational theme alignment used in the AURA study. The interview data and human usefulness rating materials are not included in this repository.

## Repository files

```text
notebooks/
    BERTopic_model_2.ipynb
    model_2_gateA-Copy1.ipynb
README.md
environment.yml
LICENSE
```

The first notebook runs BERTopic and saves the topic-level results. The second uses those results to compare the topics with human-coded themes. `environment.yml` lists the packages needed to run the notebooks.

## Setup

Clone the release repository from the CCT Lab GitHub:

```bash
git clone https://github.com/cctlab-research/bertopic-aura-workflow.git
cd bertopic-aura-workflow
```

Create and activate the Conda environment:

```bash
conda env create -f environment.yml
conda activate genai-nursing
```


## Input files

Create a `data/` folder in the repository directory and place the following CSV files in it. These files must be supplied separately; they are not part of the release.

| File | Expected columns | Purpose |
| --- | --- | --- |
| `processed_EV.csv` | `speaker`, `text` | Interview text from the GenAI demonstration section |
| `processed_NE.csv` | `speaker`, `text` | Interview text from the nursing education section |
| `processed_NP.csv` | `speaker`, `text` | Interview text from the nursing practice section |
| `human_sentences.csv` | `doc_id`, `lvl1`, `lvl2`, `sentence_text` | Human-coded sentences with document identifiers and theme labels |
| `theme_list.csv` | `lvl1`, `lvl2`, `include_ge_30` | Human-coded theme list and the indicator used to select themes for the analysis |

Each row in the three `processed_*.csv` files should contain a speaker identifier and its associated interview text. In `human_sentences.csv`, `doc_id` must follow the document-naming format expected by the alignment notebook so that it can match sentences to speakers. The `lvl1` and `lvl2` columns are used to match the human-coded sentences with the theme list. Only themes marked `include_ge_30` are retained for alignment.

Create an `Outputs/` folder before running the notebooks. This is where the code saves its generated files. Neither `data/` nor `Outputs/` is included in the code release.

## Running the notebooks

Run the notebooks in this order:

1. **`BERTopic_model_2.ipynb`** — Loads the processed interviews, creates text chunks, fits BERTopic, and saves topic assignments, representative documents, and topic centroids.
2. **`model_2_gateA-Copy1.ipynb`** — Loads the topic outputs and human-coded files, aligns sentences with topic assignments, and calculates the theme-to-topic similarity results.

The second notebook reads `topic_assignment.csv`, `semantic_chunks_docids.csv`, `topic_top_words.csv`, and `topic_centroids.csv` from `Outputs/`, so the first notebook must be run before it.

The BERTopic notebook also contains an OpenAI-based topic-labeling step. If you use it, you can supply your own API key.


## Code Contributions

This code was developed by Temitope Eyinla as part of the CCT Lab research project led by Dr. Chau Tong.

## Please Cite

Tong, C., Eyinla, T., & Bautista, J. R. (2026). Comparing BERTopic outputs with human-coded themes: The Alignment and Usefulness Rating Audit (AURA) workflow for qualitative analysis. *International Journal of Qualitative Methods*. https://doi.org/10.1177/16094069261486252

## License

This code is licensed under the MIT License - see the [License](LICENSE) file for details.

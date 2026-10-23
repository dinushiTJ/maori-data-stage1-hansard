# Māori Data Identification in NZ Hansard (Stage 1)

[![Hugging Face datasets](https://img.shields.io/badge/Hugging%20Face-Datasets-FFD21E?logo=huggingface&logoColor=black)](https://huggingface.co/collections/dinushiTJ/mdf-nz-hansard-datasets)
[![Stage 2 repository](https://img.shields.io/badge/GitHub-Stage%202-181717?logo=github&logoColor=white)](https://github.com/dinushiTJ/maori-data-stage2-research-commons)
[![Google Colab](https://img.shields.io/badge/Google%20Colab-Notebooks-F9AB00?logo=googlecolab&logoColor=white)](https://colab.research.google.com/)
![Python](https://img.shields.io/badge/Python-3-3776AB?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebooks-F37626?logo=jupyter&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini-2.5%20Flash-8E75B2?logo=googlegemini&logoColor=white)
[![EmbeddingGemma](https://img.shields.io/badge/Model-EmbeddingGemma-4285F4?logo=google&logoColor=white)](https://huggingface.co/google/embeddinggemma-300M)
![Source: Hansard](https://img.shields.io/badge/Source-NZ%20Hansard-00247D)

Research code for finding and classifying Māori data in the debates of the New Zealand Parliament, published as Hansard.

The pipeline scrapes Hansard transcripts and splits each one into sections. An LLM labels every section as **Māori-related** (`maori_origin`), **not Māori-related** (`non_maori_origin`) or **irrelevant**. The labelled data is then used to fine-tune and evaluate an embedding-based classifier built on [EmbeddingGemma](https://huggingface.co/google/embeddinggemma-300M).

## Related repositories

This repository is part of the University of Waikato Māori Data Findability Project. The project is split into stages, and each stage has its own repository:

| Stage | Repository | Source |
|---|---|---|
| Stage 1 | [maori-data-stage1-hansard](https://github.com/dinushiTJ/maori-data-stage1-hansard) (this repository) | New Zealand Parliament debates (Hansard) |
| Stage 2 | [maori-data-stage2-research-commons](https://github.com/dinushiTJ/maori-data-stage2-research-commons) | University of Waikato Research Commons |

Stage 2 applies the same approach to research theses and papers, using the `maori_origin` and `non_maori_origin` labels (no `irrelevant` label). It also adds baselines, Gemma-3-4B fine-tuning, checks against other LLM providers and full-text evidence extraction.

## Notebooks

The notebooks are in `notebooks/` and are numbered in the order they should be run. They were written for Google Colab.

| Notebook | What it does |
|---|---|
| `03_hansard_scraping` | Downloads Hansard transcripts (2012 onwards) |
| `04_datapoints_prep` | Splits each transcript into sections |
| `05_llm_classification` | Labels each section with Gemini |
| `06_prepared_dataset_analysis` | Explores and filters the labelled dataset |
| `07_synthetic_data_generation` | Generates training triplets for the embedding model |
| `08.0`–`08.3` | Fine-tunes EmbeddingGemma, runs zero-shot inference and trains a classifier head |
| `08.4_evaluation` | Evaluates and compares the models |

## Running

Open a notebook in [Google Colab](https://colab.research.google.com/) and run the cells in order. Each notebook installs its own dependencies.

The notebooks need these Colab Secrets:

- a Hugging Face token, for the models and datasets
- a Weights & Biases key, for logging training runs

The Gemini steps also need a Google Cloud project with Vertex AI enabled.

## Data

The datasets are too large to include in this repository. Notebook 03 downloads the raw transcripts again, and each later notebook reads the output of the step before it.

The published datasets are in the [MDF NZ Hansard Datasets](https://huggingface.co/collections/dinushiTJ/mdf-nz-hansard-datasets) collection on the Hugging Face Hub.

## Authors

All authors are at the School of Computing and Mathematical Sciences, University of Waikato, Hamilton, New Zealand.

| Name | Email | ORCID |
|---|---|---|
| Dinushi Jayasinghe | [dinushi.jayasinghe@waikato.ac.nz](mailto:dinushi.jayasinghe@waikato.ac.nz) | [![ORCID](https://img.shields.io/badge/ORCID-0009--0005--6042--9137-A6CE39?logo=orcid&logoColor=white)](https://orcid.org/0009-0005-6042-9137) |
| Paul T. Brown | [paul.brown@waikato.ac.nz](mailto:paul.brown@waikato.ac.nz) | [![ORCID](https://img.shields.io/badge/ORCID-0000--0001--7501--3971-A6CE39?logo=orcid&logoColor=white)](https://orcid.org/0000-0001-7501-3971) |
| Nick Lim | [nick.lim@waikato.ac.nz](mailto:nick.lim@waikato.ac.nz) | [![ORCID](https://img.shields.io/badge/ORCID-0000--0003--4690--5780-A6CE39?logo=orcid&logoColor=white)](https://orcid.org/0000-0003-4690-5780) |

## Acknowledgements

The debate transcripts come from [Hansard](https://hansard.parliament.nz/), the official record of the New Zealand Parliament, published by the Office of the Clerk / Parliamentary Service. All rights in the Hansard content stay with the New Zealand Parliament. See the [parliament.nz copyright terms](https://www.parliament.nz/en/footer/copyright/) for how the content may be reused.

# Tokenization and Data Preparation for LLM Fine-tuning

A Jupyter notebook demonstrating how to tokenize text data and prepare instruction datasets for Large Language Model (LLM) fine-tuning using Hugging Face Transformers and Datasets libraries.

## Overview

This notebook covers:
- Tokenization basics (encoding, decoding, padding, truncation)
- Loading datasets from Hugging Face Hub
- Formatting instruction datasets with prompt templates
- Tokenizing datasets for model training
- Splitting data into train/test sets

**Note:** This notebook focuses on data preparation only - it does not include the actual model fine-tuning step.

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/AminAbd/Finetune_LLM.git
   cd Finetune_LLM
   ```

2. **Create and activate virtual environment**
   ```bash
   python -m venv venv
   venv\Scripts\activate  # Windows
   # or
   source venv/bin/activate  # macOS/Linux
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

## Usage

1. **Launch Jupyter Notebook**
   ```bash
   jupyter notebook
   ```

2. **Open the notebook**
   - Open `tokenization_data_prep.ipynb`
   - Run cells sequentially

## Dataset

The notebook uses the **Lamini Docs** dataset:
- **1,400 question-answer pairs**
- Loaded from Hugging Face: `kotzeje/lamini_docs.jsonl`
- [Dataset link](https://huggingface.co/datasets/kotzeje/lamini_docs.jsonl)

## Notebook Sections

1. **Tokenization Examples** - Encoding, decoding, padding, and truncation techniques
2. **Dataset Loading** - Load dataset from Hugging Face Hub
3. **Data Formatting** - Create prompt templates and format question-answer pairs
4. **Dataset Tokenization** - Apply tokenization to the entire dataset
5. **Data Splitting** - Split dataset into train/test sets (90/10 ratio)

## Dependencies

- `transformers` - Hugging Face Transformers
- `datasets` - Hugging Face Datasets
- `pandas` - Data manipulation
- `torch` - PyTorch
- `jupyter` - Jupyter Notebook

See `requirements.txt` for full list with versions.

## Resources

- [Hugging Face Transformers Documentation](https://huggingface.co/docs/transformers)
- [Hugging Face Datasets Documentation](https://huggingface.co/docs/datasets)
- [Pythia Model](https://huggingface.co/EleutherAI/pythia-70m)

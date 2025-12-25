# Finetune LLM

A comprehensive guide and implementation for fine-tuning Large Language Models (LLMs) using Hugging Face Transformers and Datasets libraries.

## Overview

This project demonstrates how to:
- Load and preprocess instruction datasets from Hugging Face
- Tokenize text data using transformer tokenizers
- Prepare datasets for fine-tuning with proper formatting
- Split datasets into training and testing sets
- Fine-tune language models on custom datasets

## Features

- **Dataset Loading**: Load datasets directly from Hugging Face Hub (no manual download needed)
- **Tokenization**: Complete tokenization pipeline with padding and truncation
- **Data Preprocessing**: Format instruction-following datasets with question-answer pairs
- **Model Support**: Uses EleutherAI/pythia-70m as the base model (easily customizable)
- **Multiple Datasets**: Includes examples for various datasets (Lamini docs, Taylor Swift, BTS, etc.)

## Prerequisites

- Python 3.8+
- Jupyter Notebook or JupyterLab
- pip or conda package manager

## Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Finetune_LLM
   ```

2. **Create a virtual environment** (recommended)
   ```bash
   python -m venv venv
   ```

3. **Activate the virtual environment**
   
   On Windows:
   ```bash
   venv\Scripts\activate
   ```
   
   On macOS/Linux:
   ```bash
   source venv/bin/activate
   ```

4. **Install required packages**
   ```bash
   pip install transformers datasets pandas torch
   ```
   
   Or install Jupyter for notebook support:
   ```bash
   pip install jupyter transformers datasets pandas torch
   ```

## Usage

1. **Launch Jupyter Notebook**
   ```bash
   jupyter notebook
   ```
   
   Or JupyterLab:
   ```bash
   jupyter lab
   ```

2. **Open the notebook**
   - Open `finetune1.ipynb` in Jupyter
   - Run the cells sequentially to understand each step

3. **Dataset Selection**
   - The notebook uses `kotzeje/lamini_docs.jsonl` by default
   - You can modify the dataset path in the notebook to use different datasets:
     - `lamini/lamini_docs`
     - `lamini/taylor_swift`
     - `lamini/bts`
     - `lamini/open_llms`

## Dataset

The project primarily uses the **Lamini Docs** dataset, which contains:
- **1,400 question-answer pairs**
- Topics related to Lamini's LLM Engine documentation
- Structured in JSONL format with "question" and "answer" fields

Dataset link: [kotzeje/lamini_docs.jsonl](https://huggingface.co/datasets/kotzeje/lamini_docs.jsonl)

## Project Structure

```
Finetune_LLM/
│
├── finetune1.ipynb          # Main notebook with fine-tuning pipeline
├── README.md                 # This file
├── .gitignore               # Git ignore file
└── venv/                    # Virtual environment (not tracked in git)
```

## Key Components

### 1. Tokenization
- Text encoding and decoding
- Batch tokenization
- Padding and truncation strategies
- Left/right truncation options

### 2. Dataset Preparation
- Loading datasets from Hugging Face
- Formatting instruction datasets
- Creating prompt templates
- Dataset information display

### 3. Data Processing
- Converting datasets to Hugging Face Dataset format
- Applying tokenization functions
- Adding labels for training
- Train/test splitting

## Notebook Sections

The notebook is organized into the following sections:

1. **Import Required Libraries** - Import necessary packages
2. **Initialize Tokenizer** - Load the tokenizer model
3. **Tokenization Examples** - Demonstrate various tokenization techniques
4. **Prepare Instruction Dataset** - Load and format the dataset
5. **Tokenize Dataset** - Apply tokenization to the entire dataset
6. **Data Splitting** - Split into train/test sets

## Customization

### Change the Base Model
Modify the tokenizer initialization:
```python
tokenizer = AutoTokenizer.from_pretrained("your-model-name")
```

### Use a Different Dataset
Change the dataset path:
```python
dataset = load_dataset("your-dataset/path")
```

### Adjust Training Parameters
Modify the dataset split ratio:
```python
split_dataset = tokenized_dataset.train_test_split(test_size=0.1, shuffle=True, seed=123)
```

## Dependencies

Main dependencies:
- `transformers` - Hugging Face Transformers library
- `datasets` - Hugging Face Datasets library
- `pandas` - Data manipulation
- `torch` - PyTorch (required by transformers)
- `jupyter` - Jupyter Notebook interface

## Resources

- [Hugging Face Transformers Documentation](https://huggingface.co/docs/transformers)
- [Hugging Face Datasets Documentation](https://huggingface.co/docs/datasets)
- [Lamini Docs Dataset](https://huggingface.co/datasets/kotzeje/lamini_docs.jsonl)
- [Pythia Model](https://huggingface.co/EleutherAI/pythia-70m)

## License

This project is open source and available for educational purposes.

## Contributing

Contributions, issues, and feature requests are welcome!

## Acknowledgments

- Hugging Face for the excellent transformers and datasets libraries
- EleutherAI for the Pythia models
- Lamini for providing the instruction datasets


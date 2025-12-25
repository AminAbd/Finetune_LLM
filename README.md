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

## Understanding Labels in the Dataset

### What are Labels?

In this notebook, **labels are identical to input_ids**. This is standard for causal language model training.

### Example

**Original Data:**
- Question: "How are you?"
- Answer: "I'm fine, thanks."

**After formatting with prompt template:**
```
### Question:
How are you?

### Answer:
I'm fine, thanks.
```

**After tokenization:**
```python
# Question + Answer are concatenated and tokenized together
text = question + answer
input_ids = [4118, 19782, 27, 187, 2347, 476, 309, 7472, 253, 3045, ...]
#            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
#            Token IDs representing the entire sequence

# Labels are created as a copy of input_ids
labels = input_ids  # [4118, 19782, 27, 187, 2347, 476, 309, 7472, ...]
```

### How the Model Learns

The model learns to predict the next token in the sequence:
- At position 0: Given token `4118`, predict token `19782`
- At position 1: Given tokens `4118, 19782`, predict token `27`
- At position 2: Given tokens `4118, 19782, 27`, predict token `187`
- And so on...

This is an **autoregressive** approach where the model learns the entire question+answer sequence as one continuous text. During inference, you provide just the question, and the model generates the answer token by token.

**Note:** The current implementation includes question tokens in the training loss. For better instruction tuning, you could mask question tokens so the model only learns from answer tokens, but this notebook uses the simpler approach of learning the entire sequence.

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

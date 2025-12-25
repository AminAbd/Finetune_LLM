# LLM Fine-tuning Repository

This repository contains two Jupyter notebooks for working with Large Language Models: one for data preparation and tokenization, and another for fine-tuning models using Parameter-Efficient Fine-Tuning (PEFT) with LoRA.

## Notebooks

### 1. `tokenization_data_prep.ipynb`
**Tokenization and Data Preparation for LLM Fine-tuning**

This notebook demonstrates how to prepare and tokenize text data for LLM fine-tuning:
- Tokenization basics (encoding, decoding, padding, truncation)
- Loading datasets from Hugging Face Hub
- Formatting instruction datasets with prompt templates
- Tokenizing datasets for model training
- Splitting data into train/test sets

**Dataset:** Uses the Lamini Docs dataset (1,400 question-answer pairs) from Hugging Face: `kotzeje/lamini_docs.jsonl`

### 2. `lora_finetuning.ipynb`
**LoRA Fine-tuning for Text Classification**

This notebook demonstrates fine-tuning a DistilBERT model for text classification using PEFT/LoRA:
- Loading and preparing classification datasets (IMDB sentiment analysis)
- Setting up PEFT/LoRA configuration
- Fine-tuning with Hugging Face Trainer
- Saving and loading trained models
- Making predictions with the fine-tuned model

**Dataset:** Uses IMDB truncated dataset from Hugging Face: `shawhin/imdb-truncated`  
**Model:** `distilbert-base-uncased` fine-tuned for binary sentiment classification (Positive/Negative)

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

2. **Open and run the notebooks**
   - `tokenization_data_prep.ipynb` - For data preparation workflows
   - `lora_finetuning.ipynb` - For fine-tuning classification models

## Understanding Labels in tokenization_data_prep.ipynb

### What are Labels?

In the tokenization notebook, **labels are identical to input_ids**. This is standard for causal language model training.

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
input_ids = [4118, 19782, 27, 187, 2347, 476, 309, 7472, ...]

# Labels are created as a copy of input_ids
labels = input_ids  # [4118, 19782, 27, 187, 2347, ...]
```

### How the Model Learns

The model learns to predict the next token in the sequence using an autoregressive approach. During inference, you provide just the question, and the model generates the answer token by token.

**Note:** The current implementation includes question tokens in the training loss. For better instruction tuning, you could mask question tokens so the model only learns from answer tokens, but this notebook uses the simpler approach of learning the entire sequence.

## Dependencies

- `transformers` - Hugging Face Transformers
- `datasets` - Hugging Face Datasets
- `pandas` - Data manipulation
- `torch` - PyTorch
- `peft` - Parameter-Efficient Fine-Tuning
- `evaluate` - Model evaluation metrics
- `accelerate` - Training acceleration
- `jupyter` - Jupyter Notebook

See `requirements.txt` for full list with versions.

## Resources

- [Hugging Face Transformers Documentation](https://huggingface.co/docs/transformers)
- [Hugging Face Datasets Documentation](https://huggingface.co/docs/datasets)
- [PEFT Documentation](https://huggingface.co/docs/peft)
- [LoRA Paper](https://arxiv.org/abs/2106.09685)

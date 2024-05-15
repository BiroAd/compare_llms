# Examine modern architecture of LLMs

This repo hosts my homework project for the course [Project laboratoy](https://portal.vik.bme.hu/kepzes/targyak/VITMAL01/) at Budapest University of Technology and Economics. The aim of the project is to examine modern llm architectures such as Mamba and RWKV and compare them to Transformer-based LLMs.

# Result

## Testing models

In this experiment, I explored various Mamba, RWKV, and Transformer architectures with parameter counts ranging from 120 million to 3 billion. Each model was tasked with answering questions like "Who is Albert Einstein?". Differences in model answers can come not only from varying parameter numbers, but also from the amount of training data (tokens) a model was trained on. Here are my key observation about the models:

#### Mamba
Smaller models (130M) initially generated poor responses, behaved like a parrot but improved with few-shot prompting. Larger Mamba models (790M, 2.8B) performed exceptionally well.

#### RWKV
Smaller models (169M) showed some improvement with few-shot prompting, while larger models (3B) demonstrated strong content accuracy.

#### Transformer
Smaller models (124M) performed poorly, exhibiting parrot-like behavior, while larger models (2.7B) performed adequately, especially with zero-shot prompting.

## Pretrained model evaluation

Evaluation performance of the different models on the [SQuAD dataset](https://www.oxen.ai/ox/Mamba-Fine-Tune/file/main/squad_val_1k.jsonl). 

#### Mamba

| Model          | Zero-shot Prompting Accuracy | Token/s - Zero-shot | Three-shot Prompting Accuracy | Token/s - Three-shot |
|----------------|------------------------------|---------------------|-------------------------------|----------------------|
| Mamba 130M     | 1%                           | 2409                | 2%                           | 2531                 |
| Mamba 790M     | 9%                            | 1023                   | 24%                           | 761                  |
| Mamba 2.8B     | 19%                            | 242                   | 33%                             | 202                    |

#### RWKV

| Model          | Zero-shot Prompting Accuracy | Token/s - Zero-shot | Three-shot Prompting Accuracy | Token/s - Three-shot |
|----------------|------------------------------|---------------------|-------------------------------|----------------------|
| RWKV 169M      | 0%                           | 1075                | 0%                            | 1293                 |
| RWKV 3B        | 7%                           | 301                 | 29%                           | 225                  |

#### Transformer

| Model          | Zero-shot Prompting Accuracy | Token/s - Zero-shot | Three-shot Prompting Accuracy | Token/s - Three-shot |
|----------------|------------------------------|---------------------|-------------------------------|----------------------|
| GPT2 124M      | 0%                           | 3300                | 3%                            | 2709                 |
| GPT-Neo 2.7B   | 11%                          | 170                 | 33%                            | 85

## Fine-tuned model evaluation

Evaluation performance of the fine-tuned models on the [SQuAD dataset](https://www.oxen.ai/ox/Mamba-Fine-Tune/file/main/squad_val_1k.jsonl). 


| Model          | Zero-shot Prompting Accuracy | Token/s - Zero-shot | Three-shot Prompting Accuracy | Token/s - Three-shot |
|----------------|------------------------------|---------------------|-------------------------------|----------------------|
| GPT2 124M      | 0%                           | 3300                | 3%                            | 2709                 |
| GPT-Neo 2.7B   | 11%                          | 170                 | 33%                            | 85

# Files

To run the Jupyter notebooks on Kaggle, you simply need to download the [SQuAD dataset](https://www.oxen.ai/ox/Mamba-Fine-Tune/file/main/squad_val_1k.jsonl) for evaluation. Then you should specify the data path for the 'path' variable.

- `testing_models.ipynb`: In this file, I ask simple questions to various architectures, and you can see the answers to these questions in this notebook.
- `evaluation-mamba.ipynb`
- `evaluation-rwkv.ipynb`
- `evaluation-transformer.ipynb`: In these files, I evaluate various models (Mamba, RWKV, and Transformer) on the SQuAD question answering benchmark dataset.
- `peft-gpt2.ipynb`
- `peft-mamba.ipynb`: In these files, I fine-tuned a GPT2 and a Mamba model on the SQuAD dataset's train split, and then evaluated the fine-tuned models on the evaluation dataset mentioned above.
# FlowerTune LLM on Medical Dataset

This directory conducts federated instruction tuning with a pretrained Bio-Medical-Llama-3-8B (https://huggingface.co/ContactDoctor/Bio-Medical-Llama-3-8B) model on a [Medical dataset](https://huggingface.co/datasets/medalpaca/medical_meadow_medical_flashcards).
We use [Flower Datasets](https://flower.dev/docs/datasets/) to download, partition and preprocess the dataset.
Flower's Simulation Engine is used to simulate the LLM fine-tuning process in federated way,
which allows users to perform the training on a single GPU.


## Methodology

This baseline performs federated LLM fine-tuning with [LoRA](https://arxiv.org/pdf/2106.09685) using the [🤗PEFT](https://huggingface.co/docs/peft/en/index) library.
The clients' models are aggregated with either FedAvg or FlexLoRA strategy. 

## Environments setup

Project dependencies are defined in `pyproject.toml`. Install them in an activated Python environment with:

```shell
pip install -e .
```

## Experimental setup

The dataset is divided into 20 partitions in an IID fashion, a partition is assigned to each ClientApp.
We randomly sample a fraction (0.1) of the total nodes to participate in each round, for a total of `10` rounds.
All settings are defined in `pyproject.toml`. To run experiments with flexlora, set `use_flexlora` to `1`.

## Evaluation Result


|          | careqa | medmcqa | medqa | pubmedqa | Average |
|:--------:|:------:|:-------:|:-----:|:--------:|:-------:|
|  FedAvg  | 55.36  |  60.93  | 65.82 |   70.4   |  63.12  |
| FlexLoRA | 54.31  |  59.29  | 59.23 |   70.2   |  60.75  |


## Model saving

The PEFT checkpoint can be found in: https://drive.google.com/file/d/1PNviSb5IAwcx-0ABdCgcrkcGJyxINOdf/view?usp=sharing



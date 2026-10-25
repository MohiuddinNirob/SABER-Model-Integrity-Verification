# SABER: Joint Structural and Behavioral Verification for Edge-Deployed Model Integrity

This anonymous repository contains the implementation, evaluation scripts,
configurations, and supporting materials for **SABER**, a model integrity
verification framework for edge-deployed machine learning models.

This repository is provided for anonymous peer review and reproducibility.

---

## Repository Structure

```text
SABER/
│
├── README.md
│
├── SABER/
│   ├── ResNet18_CIFAR10.py
│   ├── ResNet18_MNIST.py
│   ├── RNN_CIFAR10.py
│   ├── RNN_MNIST.py
│   ├── MobileViT_CIFAR10.py
│   ├── TinyBERT_SST2.py
│   ├── LSTM_ETH.py
│   └── DCGAN_CIFAR10.py
│
└── Baselines/
    ├── PublicCheck.py
    ├── MiSentry.py
    └── EdgeThemis.py
```

## SABER Implementations

The `SABER/` directory contains eight standalone implementations for the following model–dataset configurations:

| Model | Dataset |
|---|---|
| ResNet18 | CIFAR-10 |
| ResNet18 | MNIST |
| RNN | CIFAR-10 |
| RNN | MNIST |
| MobileViT | CIFAR-10 |
| TinyBERT | SST-2 |
| LSTM | ETH |
| DCGAN | CIFAR-10 |

Each file contains the code for its corresponding configuration.

## Baseline Implementations

The `Baselines/` directory contains three implementations:

- **PublicCheck**
- **MiSentry**
- **EdgeThemis**

Each baseline is provided as a common standalone implementation for its evaluated configurations.

## How to Run

All codes are designed to run directly in **Google Colab**.

1. Open [Google Colab](https://colab.research.google.com/).
2. Create a new notebook.
3. Open the desired source file from this repository.
4. Copy the entire code and paste it into a single Colab cell.
5. Run the cell.

Each implementation can be executed independently. Required dependencies and experimental setup operations are handled within the corresponding code.

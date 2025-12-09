# Project Repository - Security in Federated Learning
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e9/Logo_de_l%27Université_Jean_Monnet_Saint-Etienne.png/640px-Logo_de_l%27Université_Jean_Monnet_Saint-Etienne.png" alt="Université Jean Monnet" title="Université Jean Monnet">

Master 2 DSC 2025-2026 - Université Jean Monnet

**Author:** Mohamed MOUDJAHED
**Supervisor:** Pierre-Louis CAYREL

## Overview

Implementation of cryptographic security mechanisms for Federated Learning, combining Secure Aggregation and RSA signatures to protect model exchanges while maintaining performance.

## Key Features

### Security Mechanisms
- **RSA Digital Signatures (2048-bit):** Authenticate client model updates
- **Secure Aggregation:** Mask individual updates using Diffie-Hellman protocol
- **Privacy Preservation:** Server only sees aggregated results, never individual client data

### Model Inversion Attack Demo
Demonstrates vulnerability of unprotected models by reconstructing training images from weights.
- Attack MAE: 0.058 (highly successful reconstruction)
- Model confidence: 95.61%

## Implementation

### Dataset
MNIST handwritten digits (70,000 images)

### Architecture
CNN: Conv2D(32) → MaxPool → Conv2D(64) → MaxPool → Conv2D(128) → Flatten → Dropout(0.5) → Dense(128) → Dense(10)

### Results

| Approach | Accuracy | F1-Score |
|----------|----------|----------|
| Centralized (100% data) | 0.9916 | 0.9916 |
| Single client (5% data) | 0.9576 | 0.9577 |
| **FL + Security (20 clients)** | **0.9786** | **0.9786** |

## Files

- `_M2_DSC__Sécurité_dans_l_apprentissage_fédérée.pdf`: Complete report (French)
- `FL_secure_aggregation_completes.ipynb`: Secure FL implementation
- `model_inversion_attack_mnist_script.ipynb`: Attack demonstration

## How It Works

1. **Key Generation:** Each client generates RSA key pairs
2. **Local Training:** Clients train on local data independently
3. **Masking:** Updates masked using Diffie-Hellman shared secrets
4. **Signing:** RSA signatures ensure authenticity
5. **Verification:** Server validates signatures before aggregation
6. **Aggregation:** FedAvg with automatic mask cancellation

## Technical Stack

- Python 3.x
- TensorFlow/Keras
- NumPy
- Cryptography libraries (RSA, SHA-256, Diffie-Hellman)
- Jupyter Notebook

## Key Takeaways

- Federated Learning enables collaborative model training without data sharing
- Cryptographic protections prevent model inversion and ensure authenticity
- 20-client FL achieves 97.86% accuracy, comparable to centralized training
- Secure Aggregation prevents server from accessing individual client updates

## References

- Bonawitz et al. (2017): Practical Secure Aggregation
- McMahan et al. (2017): Communication-Efficient FL
- Diffie-Hellman (1976): Key Exchange Protocol
- RSA (1978): Digital Signatures
- NIST FIPS 180-4: SHA-256 Standard

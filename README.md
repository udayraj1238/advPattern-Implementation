# advPattern: A PyTorch Implementation

This repository contains my (Uday Raj's) from-scratch implementation of the research paper: **"advPattern: Physical-World Attacks on Deep Person Re-Identification"** (Wang et al.).

The objective of this project was to replicate the paper's core findings by building a complete pipeline in PyTorch. This pipeline generates adversarial patterns designed to fool a state-of-the-art person re-identification (Re-ID) model, simulating a physical-world attack.

---

##  Core Features Implemented

This project successfully implements the two primary attack modalities described in the paper:

* **1. Evading Attack ("Invisible Cloak"):** An untargeted attack that generates a pattern to make a person "invisible" to a Re-ID system. The goal is to ensure that images of the same person, when seen by different cameras, are no longer matched to each other.

* **2. Impersonation Attack ("Identity Theft"):** A more complex targeted attack. This generates a pattern that, when "worn" by an attacker, tricks the Re-ID model into identifying them as a *specific target person* in the database.

---

##  victim-model The "Victim": OSNet

To ensure a robust and realistic test, this implementation does not attack a generic classification model. Instead, it targets a specialized, state-of-the-art Re-ID model: **OSNet (Omni-Scale Network)**.

This model is loaded using the `torchreid` library and comes pre-trained on the Market-1501 dataset, making it a powerful and challenging "victim" to fool.

---

##  Environment Setup & Installation

Reproducing this project requires a specific environment. This was built and tested using `conda` on Windows 11 with an NVIDIA RTX GPU.

### 1. The Dataset (Market-1501)

This repository **does not** include the dataset due to its large size. You must download the **Market-1501 dataset** manually.

* Download from the official source (or a mirror).
* Unzip the `Market-1501-v15.09.15` folder and place it in the root of this project directory.

### 2. Conda Environment Setup

These are the exact steps to create a clean, reproducible environment:

```bash
# 1. Create a new conda environment with a stable Python version
conda create --name pytorch_env python=3.11 -y

# 2. Activate the new environment
conda activate pytorch_env

# 1. Install PyTorch with CUDA (e.g., 11.8)
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia -y

# 2. Install all other required dependencies.
# This list includes all packages needed by torchreid and our scripts.
pip install torchreid numpy six h5py Pillow scipy scikit-learn metric-learn cython tabulate tqdm opencv-python gdown PyYAML tensorboard yacs

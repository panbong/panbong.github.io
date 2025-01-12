---
layout: post
title: How to install PyTorch and CUDA toolkits on the Ubuntu 20.04
subtitle: Also see Ubuntu.
gh-repo: panbong/panbong.github.io
gh-badge: [star, fork, follow]
comments: true
categories: [ml_py]
tags: Machine Learning, PyTorch, CUDA, Ubuntu
---

### How to install and set up PyTorch

- Download and install the latest Anacond
- Install Jupyter Notebook

```
conda install -y jupyter
```

- Create an environment for PyTorch

```
conda create -n ml_py38 python=3.8
```

- Activate the created environment

```
conda activate ml_py38)
```

- Install nb_conda

```
conda install nb_conda
```

- Install PyTorch, TorchVision, and cuda-toolkit


```
conda install pytorch torchvision cudatoolkit=11.2 -c pytorch
```

- Issue the following command

```
conda env update --file tools.yml
```

- Create a kernel for the environment

```
python -m ipykernel install --user --name ml_py38 --display-name "python 3.8 (pytorch)"
```

- Execute Jupyter Notebook

```
jupyter notebook
```

### Versions of the installed packages

- Conda 4,10.1
- Python 3.8.8
- CUDA 11.2
- Torch 1.81

### Useful commands

- If you want to see the versions of the installed packages (conda list)
- If you update the installed packages (conda update --all)
- If you upgrade Spyder (conda upgrade spyder)

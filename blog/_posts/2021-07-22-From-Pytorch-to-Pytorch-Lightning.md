---
layout: post
title: From Pytorch to Pytorch-Lightning
subtitle: Also see Pytorch
gh-repo: panbong/panbong.github.io
gh-badge: [star, fork, follow]
comments: true
categories: [ml_py]
tags: Machine Learning, Pytorch, Pytorch-Lightning, Ubuntu
---

## Pytorch-Lightning

### Lightning makes coding complex networks simple.

- PyTorch Lightning is a lightweight PyTorch wrapper for high-performance AI research.
- Spend more time on research, less on engineering. It is fully flexible to fit any use case and built on pure PyTorch so there is no need to learn a new language. A quick refactor will enable the following:

   - Running your code on any hardware
   - Logging
   - Performance & bottleneck profiler
   - Metrics
   - Model checkpointing
   - Visualization
   - 16-bit precision
   - Early stopping
   - Run distributed training

### Seamlessly train hundreds of models in the cloud from your laptop with Grid.

- Use Grid to seamlessly orchestrate training in the cloud and manage artifacts like checkpoints and logs - all from your laptop without changing a line of code.


### To install Pytorch-lightning

- Go to your virtual environment
- Execute a following cli command (don't use `pip2` or `pip3`)

```
pip install pytorch-lightning
```

- Insert `import pytorch-lightning as pl` in your python code


### To see tensorboard

- Execute a following cli command (don't put any space before and after =)

```
tensorboard --logdir=./runs
```

- Then execute your web browser and enter an url of `http://localhost:6006` (the default port # is 6006)

### An example of Pytorch-lightning code

```
import torch
from torch import nn
from torch.nn import functional as F
from torch.utils.data import DataLoader
from torch.utils.data import random_split
from torchvision.datasets import MNIST
from torchvision import transforms
import pytorch_lightning as pl

class LitAutoEncoder(pl.LightningModule):
	def __init__(self):
		super().__init__()
		self.encoder = nn.Sequential(
      nn.Linear(28 * 28, 64),
      nn.ReLU(),
      nn.Linear(64, 3))
		self.decoder = nn.Sequential(
      nn.Linear(3, 64),
      nn.ReLU(),
      nn.Linear(64, 28 * 28))

	def forward(self, x):
		embedding = self.encoder(x)
		return embedding

	def configure_optimizers(self):
		optimizer = torch.optim.Adam(self.parameters(), lr=1e-3)
		return optimizer

	def training_step(self, train_batch, batch_idx):
		x, y = train_batch
		x = x.view(x.size(0), -1)
		z = self.encoder(x)    
		x_hat = self.decoder(z)
		loss = F.mse_loss(x_hat, x)
		self.log('train_loss', loss)
		return loss

	def validation_step(self, val_batch, batch_idx):
		x, y = val_batch
		x = x.view(x.size(0), -1)
		z = self.encoder(x)
		x_hat = self.decoder(z)
		loss = F.mse_loss(x_hat, x)
		self.log('val_loss', loss)

# data
dataset = MNIST('', train=True, download=True, transform=transforms.ToTensor())
mnist_train, mnist_val = random_split(dataset, [55000, 5000])

train_loader = DataLoader(mnist_train, batch_size=32)
val_loader = DataLoader(mnist_val, batch_size=32)

# model
model = LitAutoEncoder()

# training
trainer = pl.Trainer(gpus=4, num_nodes=8, precision=16, limit_train_batches=0.5)
trainer.fit(model, train_loader, val_loader)
```    


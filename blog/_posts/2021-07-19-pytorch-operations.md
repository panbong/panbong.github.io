---
layout: post
title: Useful operators used in Pytorch
subtitle: Also see the Pytorch documentation
gh-repo: panbong/panbong.github.io
gh-badge: [star, fork, follow]
tags: [Pytorch, operators]
categories: [ml_py]
comments: true
---

### Useful operations you must know to begin Pytorch

#### Initialize tensors with known values
a is an integer tensor created in the CPU memory.<br/>
b is a float tensor created in the CPU memory.<br/>
c is a float tensor created in the GPU memory.<br/>
d is a float tensor created in the GPU memory which also stores its gradient.

    tensor([[1, 2, 3],
            [4, 5, 6]])
    tensor([[1., 2., 3.],
            [4., 5., 6.]])
    tensor([[1., 2., 3.],
            [4., 5., 6.]], device='cuda:0')
    tensor([[1., 2., 3.],
            [4., 5., 6.]], device='cuda:0', requires_grad=True)


#### Another initializers
xe is an uninitialized tensor.<br/>
xz is a zero tensor.<br/>
xr initializersis a random tensor.<br/>
xi is an identity tensor.

    tensor([0.0760, 0.6932, 0.8134])
    tensor([[1., 0., 0.],
            [0., 1., 0.],
            [0., 0., 1.]])


#### Initialize a tensor with a series of numbers from start to end inclusive by step

    tensor([0, 1, 2, 3, 4])


#### Initialize a tensor with a series of numbers from start to end with steps

xl = torch.linspace(start = 0, end = 5, steps = 10)
print(xl)

##### To generate Gausiian random numbers
torch.randn(1,5)

    tensor([[-0.7091, -0.8326, -0.0262, -0.7367, -0.4155]])


#### To generate random numbers of uniform distribution
torch.rand(5)

    tensor([[0.0805, 0.2932, 0.4297, 0.5209, 0.3425]])


#### To create a diagonal matrix

    tensor([[1, 0, 0],
            [0, 2, 0],
            [0, 0, 3]])


#### Conversion between a tensor and a numpy array

#### Elementwise multiplication and division

#### Elementwise exponentiation

#### Matrix multiplication

#### Batch matrix multiplication

#### Matrix exponentiation

#### Transpose

#### Permute

#### Concatenation

    torch.Size([4, 5])
    torch.Size([2, 10])


#### Unsqeeze and sqeeze

    tensor([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
    tensor([[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]])
    tensor([[[0],
             [1],
             [2],
             [3],
             [4],
             [5],
             [6],
             [7],
             [8],
             [9]]])
    tensor([[[[0],
              [1],
              [2],
              [3],
              [4],
              [5],
              [6],
              [7],
              [8],
              [9]]]])
    tensor([[[[[0],
               [1],
               [2],
               [3],
               [4],
               [5],
               [6],
               [7],
               [8],
               [9]]]]])


#### Type conversion

#### Indexing

#### Statistical functions

#### Logic

#### Miscellaneous

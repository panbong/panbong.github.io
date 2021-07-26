---
layout: post
title: Useful operators you must know to begin Pytorch
subtitle: Also see PyTorch documentation.
gh-repo: panbong/panbong.github.io
gh-badge: [star, fork, follow]
comments: true
categories: [ml_py]
tags: Machine Learning, PyTorch, Operators, Ubuntu
---

### Useful operations you must know to begin PyTorch


```python
import torch
import numpy as np
import os 
import ipyparams
```


    <IPython.core.display.Javascript object>


#### Initialize tensors with known values
a is an integer tensor created in the CPU memory.<br/>
b is a float tensor created in the CPU memory.<br/>
c is a float tensor created in the GPU memory.<br/>
d is a float tensor created in the GPU memory which also stores its gradient.


```python
a = torch.tensor([[1,2,3],[4,5,6]])
print(a)
b = torch.tensor([[1,2,3],[4,5,6]], dtype = torch.float32)
print(b)
c = torch.tensor([[1,2,3],[4,5,6]], dtype = torch.float32, device = 'cuda')
print(c)
d = torch.tensor([[1,2,3],[4,5,6]], dtype = torch.float32, device = 'cuda', requires_grad = True)
print(d)
```

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


```python
xe = torch.empty(size = (3,3))
xz = torch.zeros((3,3))
xr = torch.rand(3) # size = (1,3)
print(xr)
xi = torch.eye(3)
print(xi)
```

    tensor([0.1361, 0.1786, 0.3227])
    tensor([[1., 0., 0.],
            [0., 1., 0.],
            [0., 0., 1.]])


#### Initialize a tensor with a series of numbers from start to end inclusive by step


```python
xa = torch.arange(start = 0, end = 5, step = 1)
print(xa)
```

    tensor([0, 1, 2, 3, 4])


#### Initialize a tensor with a series of numbers from start to end with steps

xl = torch.linspace(start = 0, end = 5, steps = 10)
print(xl)

##### To generate Gausiian random numbers
torch.randn(1,5)


```python
xn = torch.empty(size = (1,5)).normal_(mean = 0, std = 1)
print(xn)
```

    tensor([[ 1.0059, -0.2311,  0.8946,  0.7181,  0.0745]])


#### To generate random numbers of uniform distribution
torch.rand(5)


```python
xu = torch.empty(1,5).uniform_(0,1)
print(xu)
```

    tensor([[0.9168, 0.1489, 0.6728, 0.6304, 0.3752]])


#### To create a diagonal matrix


```python
xd = torch.diag(torch.tensor([1,2,3])) # error: torch.diag([1,2,3])
print(xd)
```

    tensor([[1, 0, 0],
            [0, 2, 0],
            [0, 0, 3]])


#### Conversion between a tensor and a numpy array


```python
np_array = np.zeros((5,5))
tensor = torch.from_numpy(np_array)
np_array_back = tensor.numpy()
```

#### Elementwise multiplication and division


```python
e1 = torch.rand(3, 2)
e2 = torch.rand(3, 2)
e3 = e1 * e2    # e3 = torch.dot(e1, e2)
e4 = e1 / e2    # e4 = torch.true_divide(e1, e2)
e5 = torch.true_divide(e1, e2)
```

#### Elementwise exponentiation


```python
x = torch.rand(3,3)
z = x**2   # z = x.pow(2)
```

#### Matrix multiplication


```python
x1 = torch.rand(2,5)
x2 = torch.rand(5,3)
x3 = torch.mm(x1, x2) # x3 = x1.mm(x2)
```

#### Batch matrix multiplication


```python
batch = 32
n = 10
m = 20
p = 30
t1 = torch.rand(batch, n, m)
t2 = torch.rand(batch, m, p)
t3 = torch.bmm(t1, t2)        # batch x n x p
```

#### Matrix exponentiation


```python
me = torch.rand(5, 5)
me1 = torch.matrix_power(me, 3) # me1 = me.matrix_power(3)
```

#### Transpose


```python
x = torch.arange(9)
x_3x3 =x.view(3,3) # Reshaping a tensor which is applied for a contiguous memory
y = x_3x3.t() # This is not a contiguous memory
y1 = y.contiguous().view(9) # or use y1 = y.reshape(3,3),
                            # which can be applied for a non-contigous memory
```

#### Permute


```python
x = torch.rand(10, 3, 5) # size 10x3x5
y = x.permute(0, 2, 1)   # size 10x5x3
```

#### Concatenation


```python
x1 = torch.rand(2,5)
x2 = torch.rand(2,5)
x3 = torch.cat((x1, x2)) # default: concatenation in the o-th dimension
print(x3.size())
x4 = torch.cat((x1, x2), dim = 1)
print(x4.size())
```

    torch.Size([4, 5])
    torch.Size([2, 10])


#### Unsqeeze and sqeeze


```python
x = torch.arange(10)                          # 10
print(x)
x.unsqueeze_(-2)   # or torch.unsqueeze(x, 0) # 1x10
print(x)
x.unsqueeze_(-1)   # or torch.unsqueeze(x, 0) # 1x10x1
print(x)
x.unsqueeze_(0)   # or torch.unsqueeze(x, 0)  # 1x1x10x1
print(x)
x.unsqueeze_(1)   # or torch.unsqueeze(x, 1)  # 1x1x1x10x1
print(x)
```

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


```python
x = torch.tensor([[1,2,3], [-4,5,6], [7,8,9]])
xb = x.bool()        # boolean
xby = x.byte()       # uint8
xs = x.short()       # int16
xi = x.int()         # int32
xl = x.long()        # int64
xh = x.half()        # float16
xf = x.float()       # float32
xd = x.double()      # float64
```

#### Indexing


```python
x = torch.arange(10)       # x = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
y = x[(x < 2) & (x > 0)]   # y = [1]
z = x[3:6]                 # z = [3, 4, 5]
```

#### Statistical functions


```python
x1 = torch.tensor([[1,2,3], [-4,5,6], [7,8,9]])
xa = torch.abs(x1)
sum_x1 = torch.sum(x1, dim = 0)  # vertical sum
mean_x1 = torch.mean(x1.float(), dim = 0)
values, indices = torch.max(x1, dim = 0)
values, indices = torch.min(x1, dim = 0)
z1 = torch.argmax(x1, dim = 0)
z2 = torch.argmin(x1, dim = 0)
sorted_x1, indices = torch.sort(x1, dim = 0, descending = False) # sorting in the ascending
                                                                 # order
```

#### Logic


```python
x = torch.tensor([[1, 0, 2, 1], [1, 1, 1, 1]])
y = torch.tensor([[1, 1, 2, 2], [1, 1, 1, 1]])
a1 = x.any()         # Is there any non-zero element?
a2 = x.all()         # Are all elements non-zero?
a3 = torch.eq(x, y)  # elementwise comparison
```

#### Miscellaneous


```python
x = torch.arange(10)
r = x.remainder(2)           # modulus 2
e = x.numel()                # number of elements
n = x.ndimension()           # dimension
u = torch.unique(x)          # eliminates non-consecutive duplicate values
"""
w = []
for xe in x:
   if xe > 5:
      w.append(xe)
   else:
      w.append(xe*2)
"""
w = torch.where(x > 5, x, x*2) # [0, 2, 4, 6, 8, 10, 6, 7, 8, 9] 
```


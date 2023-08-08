# some basic concepts
 
**Pytorch**
- a python based scientific computing package
- a replacement for Numpy to utilise the power of GPUs
- https://pytorch.org/
 
**Tensors**
- tensors are the main type of object which Pytorch is built on
- can be any dimension, ranging from 0D to 3D and above: 0D is a scalar, 1D is a vector, 2D is a matrix 
- can perform many built in operations: summing all of the entries

**GPUs**
- used to accelerate the training process
- good at parallel computation
- ⚠ to utilise GPUs in code, tensors and model must be moved to the GPU

**Autograd**
- 参考BP中对edges (functions), nodes (values of variables)的计算

# Tutorial

import the package
```python
import torch 
import numpy as np
```

## tensor

construct a tensor
```python
# create a random 3-by-4 tensor
x = torch.rand(3,4)
print(x)

# create a tensor directly from a list object
x = torch.rand(3,4)
print(x)
print(x.shape)
```

get the size
```python
# both would come out with the same ouput
print(x.size())
print(x.shape)
```

perform arithematic to the tensors
```python
x = torch.rand(3,4)
y = torch.rand(3,4)
print(x+y)
print(torch.add(x, y))

# or store it in an empty tensor
result = torch.empty(3,4)
torch.add(x, y, out=result)
print(result)
```

access the data type
```python
x = torch.ones(5)
print(x)
print(x.dtype)

# the same with numpy
y = x.numpy()
print(y)
print(y.dtype)
```

convert between numpy array and tensor
```python
x = np.ones(3)
y = torch.from_numpy(x)
print(x)
print(y)

# ⚠ the returned ndarray and tensor share the same underlying storage
# how changing the np array has changed the Torch Tensor automatically
np.add(x, 1, out=x)
print(x)
print(y)

# to avoid using the same underlying sturcture, use .copy() to only copy the values
x = np.ones(3)
y = torch.from_numpy(x.copy())
np.add(x, 1, out=x)
print(x)
print(y)
```

## GPU and tensors
check whether a GPU is available
```python
# common command
device = 'cuda:0' if torch.cuda.is_available() else 'cpu'
```

transfer the tensor onto the GPU 

⚠ again, to utilise GPUs in code, tensors and model must be moved to the GPU
```python
y = torch.ones(3,4, device=device)  # directly create a tensor on GPU
x = torch.rand(3,4).to(device)      # or just use .to(device) 
z = x+y
print(z)
print(z.device)   # see what the device of an object is, by accessing its device attribute
```

## Autograd
to use autograd manually, we need to set the trquires_grad to True when we create it
```python
# ⚠ The input flag defaults to False if not given.
x = torch.randn(2, 2)
print(x.requires_grad)  # default to False

x.requires_grad_(True)   # change the flag to True
print(x.requires_grad)
```

```python
# left node
x = torch.ones(2, 2, requires_grad=True) 
print(x)
```

create a variable, recording what operation or function is used 

in the computational graph, the function is correspond to the edge, and y is the next node
```python
# second node
y = x + 2
print(y)
```

we can see which tunction has created the tensor
```python
print(y.grad_fn)  # <AddBackward0 object at 0x0000021A4FB96D90>
print(x.grad_fn)  # None, becuase this vareiable is manully created
```

see other operation
```python
# third node and root node
z = y * y * 2
out = z.mean()

print(z)
print(out)
```

## Backprop
we want to calculate the gradient of vector x when we call backwards
```python
x = torch.ones(4, 1, requires_grad=True)

# compute some intermediate functions 
y = x + 2
z = y * y * 3
out= z.mean()

print("1: ", x)
print("2: ", y)
print("3: ", y.grad_fn)
print("4: ", z)
print("5: ", out)
```

then we call .backward()
```python
out.backward()
```

print the gradient of out is w.r.t. each element of x
```python
print(x.grad)
```

➡ we have got a vector containing 4 entries. (the following explain why 4.5)

Let’s call the ``out`` *Tensor* “ $o$ ”.

We have that $o = \frac{1}{4}\sum_i z_i$ ,
$z_i = 3(x_i+2)^2$ and $z_i\bigr\rvert_{x_i=1} = 27$ (这里的27似乎不太重要）.

Therefore,
$\frac{\partial o}{\partial x_i} = \frac{3}{2}(x_i+2)$, hence
$\frac{\partial o}{\partial x_i}\bigr\rvert_{x_i=1} = \frac{9}{2} = 4.5$.

In the above function every entry of $x$ has the same function applied 
hence every entry in the gradient vector is the same (4.5), 
this will not always be the case. 

➡ Mathematically, we use Computation Graph and Jacobian Matrix
![1686039463206](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/3fb3ecb1-d2e3-4a5c-861e-7dc727897563)

![1686039032365](https://github.com/ChaosuiPeng/Kaggle_Note/assets/39878006/0d9c5abc-144a-4b09-b818-acb88f7eb449)

➡ about Jacobian Matrix

if you have a vector valued function $\vec{y}=f(\vec{x})$ ,
then the gradient of $\vec{y}$ with respect to $\vec{x}$
is a Jacobian matrix:

$$
\begin{align}J=\left(\begin{array}{ccc}
   \frac{\partial y_{1}}{\partial x_{1}} & \cdots & \frac{\partial y_{1}}{\partial x_{n}}\\
   \vdots & \ddots & \vdots\\
   \frac{\partial y_{m}}{\partial x_{1}} & \cdots & \frac{\partial y_{m}}{\partial x_{n}}
   \end{array}\right)\end{align}
$$

Generally speaking, ``torch.autograd`` is an engine for computing
vector-Jacobian product. That is, given any vector 

$$
v=\left(\begin{array}{cccc} v_{1} & v_{2} & \cdots & v_{m}\end{array}\right)^{T} 
$$

compute the product $v^{T}\cdot J$. If $v$ happens to be
the gradient of a scalar function $l=g\left(\vec{y}\right)$ ,
that is,

$$
v=\left(\begin{array}{ccc}\frac{\partial l}{\partial y_{1}} & \cdots & \frac{\partial l}{\partial y_{m}}\end{array}\right)^{T}
$$

then by the chain rule, the vector-Jacobian product would be the
gradient of $l$ with respect to $\vec{x}$ :

$$
\begin{align}J^{T}\cdot v=\left(\begin{array}{ccc}
   \frac{\partial y_{1}}{\partial x_{1}} & \cdots & \frac{\partial y_{m}}{\partial x_{1}}\\
   \vdots & \ddots & \vdots\\
   \frac{\partial y_{1}}{\partial x_{n}} & \cdots & \frac{\partial y_{m}}{\partial x_{n}}
   \end{array}\right)\left(\begin{array}{c}
   \frac{\partial l}{\partial y_{1}}\\
   \vdots\\
   \frac{\partial l}{\partial y_{m}}
   \end{array}\right)=\left(\begin{array}{c}
   \frac{\partial l}{\partial x_{1}}\\
   \vdots\\
   \frac{\partial l}{\partial x_{n}}
   \end{array}\right)\end{align}
$$

(Note that $v^{T}\cdot J$ gives a row vector which can be
treated as a column vector by taking the transpose i.e. $J^{T}\cdot v$.)

This characteristic of vector-Jacobian product makes it very
convenient to feed external gradients into a model that has
non-scalar output. 
In the case above, we consider a classic vector function where the function is displayed as a column vector. 
This method can still be applied to matrices, however the matrix must be converted into a vector 
(by concatenating the matrix's columns on top of eachother). 
The final gradient can then be rearranged into a matrix using the opposite of this proccess. 
You may want to try applying autograd to the function above only with a matrix input.

## Example: how to define a model in Pytorch

### let's create some synthetic data
We choose a vector of some points for our feature `x` and create our labels (targets) using the following model $y=a + b \cdot x + \epsilon\cdot  \mathcal{N}$, where `a`, `b` and $\epsilon$ are some constants and $\mathcal{N}$ is noise following a standard normal distribution (mean=0, variance=1).

Let's consider `a=1`, `b=2` and $\epsilon=0.1$
```python
import numpy as np
import torch

np.random.seed(42)
x = np.random.rand(100, 1) # Create an array of the given shape (100, 1) and populate it with
                           # random samples from a uniform distribution
                           # over ``[0, 1)``.
y = 1 + 2 * x + 0.1 * np.random.randn(100, 1)  # Return a sample (or samples) from the "standard normal" distribution.
```

we shuffle the indices so we don't get any biases within the data
```python
indx = np.arange(100)  # indices for all data points in x
print("Before shuffle: \n", indx)

np.random.shuffle(indx)
print("After shuffle: \n", indx)
```

split the data into training and validation
```python
# split the indices into two sets
train_indx = indx[:80]  # first 80% for training
val_indx = indx[80:]    # remaining 20% for validation

# use the indices to get our data 
x_train, y_train = x[train_indx], y[train_indx]
x_val, y_val = x[val_indx], y[val_indx]
```

transfer numpy's ndarray into roch tensors, make sure they are floating points
```python
x_train_tensor = torch.from_numpy(x_train).float()
y_train_tensor = torch.from_numpy(y_train).float()

x_val_tensor = torch.from_numpy(x_val).float()
y_val_tensor = torch.from_numpy(y_val).float()
```

visualize them using matplotlib
```python
import matplotlib.pyplot as plt
fig, axs = plt.subplots(nrows = 1, ncols = 2)
axs[0].scatter(x_train, y_train)  # plot the training dataset
axs[1].scatter(x_val, y_val)      # plot the validation dataset
```

### build our simple linear regression modle
a model can be constructed in Pytorch using the `torch.nn` class. 

To explicitly define the model, we need to implement (at least) the following methods:

- `__init__(self)`, which defines the components that make up the model. Here, you are not limited to defining parameters and other models (or layers in neural networks) as our model's attributes (see more about this later). In the `__init__` method, we define two parameters, `a` and `b`, using the `Parameter()` class. By doing this, you can invoke the `parameters()` method of our model to retrieve an iterator over all model's parameters, that we can feed our optimiser. Moreover, we can get the current values for all parameters using the model's `state_dict()` method.
- `forward(self, x)`, which performs the actual computation, that is, it ouputs a prediction, given the input `x`. You need not call the `forward(x)` method, and should call the whole model itself to perform a forward pass and output predictions.

Now, define our first model manually (usually we would use tools to build model but here is for illustration)

```python
import torch.nn as nn

class FirstModel(nn.Module):

    def __init__(self):
        super().__init__()
        self.a = nn.Parameter(torch.randn(1).float())
        self.b = nn.Parameter(torch.randn(1).float())
        
    def forward(self, x):
        return self.a + self.b * x
```

we use stochastic gradient descent, i.e., the `SGD` method from `torch.optim` package, which takes two arguments: the iterator over the model's parameters (`model.parameters()`) and the learning rate `lr`.

```python
import torch.optim as optim
torch.manual_seed(42)

device = 'cuda:0' if torch.cuda.is_available() else 'cpu'
print(f"The device used is: {device}\n") # f-string

# Now we can create a model
model = FirstModel().to(device)

# we can get the current values for all parameters using the model's `state_dict()` method.
print("Parameters before training: \n", model.state_dict())
```

```python
# set learning rate
lr = 1e-1

# set number of epoches, i.e., number of times we iterate through the training set
# in this case, it's SGD, so one sample for one round to the forward path, there're 100 training samples in total, so, 100 epoches.
epoches = 100

# We use mean square error (MSELoss)
loss_fn = nn.MSELoss(reduction='mean')

# We also use stochastic gradient descent (SGD) to update a and b
optimiser = optim.SGD(model.parameters(), lr=lr)

for epoch in range(epoches):
    model.train()             # set the model to training mode (the other mode is evaluate)
    optimiser.zero_grad()     # set all of the gradients to zero, and this is to avoid accumulating gradients
    y_pred = model(x_train_tensor.to(device))  # call the model (instance of the class), remember to move it to GPU
    loss = loss_fn(y_train_tensor.to(device), y_pred)  # calculate the loss function
    loss.backward()           # calculate gradients
    optimiser.step()          # updates model's params (weights at time T to weights at time T+1

print("Parameters after training: \n", model.state_dict())
```

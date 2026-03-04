![[Tensors]]

# Create our first tensor
- To create our first tensor, first load the PyTorch package.
```python
import torch
```
- Now lets create a tensor containing one single number.
```python
  torch.tensor(5)
```
- Now lets create a array ID tensor.
```python
torch.tensor([1, 2, 3, 4])
```
- We can check its shape , dimension and data type using this code, but first lets define a variable for this tensor.
```python
t = torch.tensor([1, 2, 3, 4])
t.shape, t.ndim, t,dtype
```
- We can also create a 2D tensor .
```python
torch.tensor([[1, 2, 3], [4, 5, 6]])
```
- We can also check max and min value in the tensor.
```python
t.max(), t.min()
```
# Define tensors with different data types.
- Lets create a tensor with float16 data type
```python
torch.tensor([0.9, 5.27, 4.5, 0.32, 2.1], dtype=torch.float16)
```

- Lets create a tensor with float32 data type.
```python
torch.tensor([1, 2, 3, 4], dtype=torch.int32)
```

- We can also use `.to` to define out data type for the tensor
```python
torch.tensor([1, 2, 3, 4]).to(dtype=torch.float64)
```

#  From numpy array to tensor
- We can convert a numpy array into tensor
```python
import numpy as np 
import torch

n = np.array([1, 2, 3, 4])
t = torch.tensor(n)

print(n, n.dtype, type(n)) # will print numpy array 
print(t, t.dtype, type(t)) # will print Pytorch tensor
```

#  Create tensor on dedicated CPU or GPU device
- We can decide our dedicated device(CPU or GPU)
>[!Important]
>For Mac system the dedicated GPU is `mps` and for nvidia GPU systems we use `cuda`

- Lets decide our device, check if if they are available or not
```python
import torch

device = torch.device("cpu")

if torch.cuda.is_vailable():
	print("CUDA GPU is available")
	device = torch.device("cuda")
elif torch.mps.is_available():
	print("MPS GPU is available")
	device = torch.device("mps")
else:
	print("Using default device which is CPU")

print(device)
```

###  Now lets create a tensor on dedicated device 
- We got our dedicated device which will be stored on `device` variable.
-  Now lets use this `device` variable and create a tensor on dedicated device(For me`cuda` works)
```python
t = torch.tensor([1, 2, 3, 4], device=device)
	print(t, "Tensor on device: ", t.device)
```
- To create a tensor on CPU and then copy it to the dedicated device we use `.to`
```python
t = torch.tensor([1, 2, 3, 4]) # default created by CPU
t = t.to(device=device)

print(t, "Tensor on device: ", t.device)
```
- We can also create a tensor with specific data type and dedicated device.
```python
t = torch.tensor([0.3, 2.4, 3.33, 5, 9.5]).to(dtype=torch.float32, device=device)
print(t)
```
> [!Note]
>  - We can also do mathematical operation on tensor.
>  - To work and understand tensors more refer to the dedicated documentation: [Tensor Doc link](https://docs.pytorch.org/docs/stable/tensors.html)




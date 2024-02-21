## Tensor Data Type
```python
a = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])

b = torch.Tensor(a)   # float, Alias for FloatTensor

c = torch.LongTensor(a)  # long int

d = torch.tensor(a)  # int

e = torch.tensor(a, dtype=torch.float)  # float32

f = torch.Tensor(2, 3) # zero tensor with float
```


# New Axis
> [!code]
> Add a new axis at the specified dimension.
```python
b.shape # (2,2,3)

b[np.newaxis].shape # (1,2,2,3)

b[:,np.newaxis].shape # (2,1,2,3)

b[:,:,np.newaxis].shape # (2,2,1,3)

b[:,:,:,np.newaxis].shape # (2,2,3,1)
```


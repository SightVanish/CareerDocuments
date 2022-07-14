# Pytorch

Here is some tips for pytorch1.x.

#### tensor

```python
>>> import torch
>>> torch.tensor([1]).dtype
torch.int64
>>> torch.tensor([1], dtype=torch.float32).dtype
torch.float32
>>> torch.tensor([1.]).dtype
torch.float32
>>> torch.Tensor([1]).dtype
torch.float32
>>> torch.tensor([True]).dtype
torch.bool
>>> torch.Tensor([True]).dtype
torch.float32
>>> exit()
```

note: torch.tensor will auto guess the type; torch.Tensor is same with dtype=float32

```python
x = torch.tensor([1])
# convert a scale in tensor to int
x = x.item() # x = (int)1
```

sort tensor and reverse sort

```python
# sort
x = torch.tensor([2,1,3])
sorted_x, sort_index = x.sort(dim=0, descending=True)
# sort_index is actually the result of x.argsort(dim=0)

# reverse sort
original_x = sorted_x.gather(dim=0, index=sort_index.argsort(dim=0))
```

you can also use `.index_select()`

```python
# the following part is a special case
data = [
    torch.Tensor([[11,12],[13,14],[15,16],[17,18]]),
    torch.Tensor([[19,20],[21,22],[23,24]]),
    torch.Tensor([[1,2],[3,4],[5,6],[7,8],[9,10]])
]
# get the length
seq_len = torch.tensor([s.size(0) for s in data], dtype=torch.int)
# sort based on the lenght
seq_len, sorting_index = seq_len.sort(0, descending=True)
data.sort(key=lambda x: len(x), reverse=True)
data = torch.cat(data)

# data is then padded
output = torch.Tensor([
    [[1,2],[3,4],[5,6],[7,8],[9,10]],
    [[11,12],[13,14],[15,16],[17,18],[0,0]],
    [[19,20],[21,22],[23,24],[0,0],[0,0]]
])
# reverse sorting, with padding
unsorted_data = output.index_select(0, sorting_index.argsort(0))
```


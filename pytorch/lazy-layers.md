In Pytorch, you can define a layer with only the desired output size without specifying the input size. Later, we the layer if first called, Pytorch would check the input size from the input tensor and creates the required parameters. This is kinda of lazy definition of a layer. It is very helpful when we're not sure about the input size but know the output size. All the layerer that support **lazy** definitions are prefixed with `Lazy` such as `LazyLinear` and `LazyConv2d`.

```python
x = torch.randn(1, 20)
layer = nn.LazyLinear(1)
layer(x) #=> tensor([[-1.3754]], grad_fn=<AddmmBackward0>)
```

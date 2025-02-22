## [ 返回参数类型不一致 ]torch.linalg.cholesky_ex

### [torch.linalg.cholesky_ex](https://pytorch.org/docs/stable/generated/torch.linalg.cholesky_ex.html)

```python
torch.linalg.cholesky_ex(input, *, upper=False, check_errors=False, out=None)
```

### [paddle.linalg.cholesky](https://www.paddlepaddle.org.cn/documentation/docs/zh/develop/api/paddle/linalg/cholesky_cn.html)

```python
paddle.linalg.cholesky(x, upper=False, name=None)
```

两者功能一致但返回参数类型不同，具体如下：

### 参数映射

| PyTorch      | PaddlePaddle | 备注                                                                                                                                                 |
| ------------ | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| input        | x            | 表示输入参数为多维 Tensor，它的维度应该为 [*, M, N]，其中*为零或更大的批次尺寸，并且最里面的两个维度上的矩阵都应为对称的正定矩阵，仅参数名不一致。 |
| upper        | upper        | 表示是否返回上三角矩阵或下三角矩阵。                                                                                                                 |
| check_errors | -            | 是否检查错误，Paddle 无此参数，一般对网络训练结果影响不大，可直接删除。                                                                                                                      |
| out          | -            | 表示输出的 Tensor ，Paddle 无此参数，需要转写。                                                                                                      |
| 返回值       | 返回值       | Pytorch 返回两个 out 与 info，Paddle 仅返回一个 Tensor：out，需转写。                                                                                |

### 转写示例

#### 返回值

```python
# PyTorch 写法
torch.linalg.cholesky_ex(x, upper=False)

# Paddle 写法
(paddle.linalg.cholesky(x, upper=False), paddle.zeros(x.shape[:-2], dtype='int32'))
```

#### out: 输出的 Tensor

```python
# PyTorch 写法
torch.linalg.cholesky_ex(x, upper=False, out=output)


# Paddle 写法
out1 = paddle.linalg.cholesky(x, upper=False)
out2 = paddle.zeros(x.shape[:-2], dtype='int32')
paddle.assign(out1, output=output[0]), paddle.assign(out2, output=output[1])
```

# 赫斯特指数:计算，价值和更多

> 原文：<https://blog.quantinsti.com/hurst-exponent/>

由[维布·辛格](https://www.linkedin.com/in/vibhu-singh-1b76b6105/)、[瓦伦·迪瓦卡尔](https://www.linkedin.com/in/varun-divakar-b862a667/)和阿希什·加尔格

在这篇博客中，我们将讨论时间序列分析中的一个重要概念:赫斯特指数。我们将借助一个例子来学习如何计算它。

首先让我们了解一下什么是赫斯特指数。

* * *

## 赫斯特指数定义

赫斯特指数被用来衡量时间序列的长期记忆。它与自相关有关(你可以阅读更多关于[自相关和](/autocorrelation-autocovariance/)自相关的内容。)以及它们随着值对之间的滞后增加而减小的速率。

* * *

## 赫斯特值

****赫斯特值大于 0.5****

如果赫斯特值大于 0.5，那么它将表明一个持续的时间序列(大致相当于一个趋势市场)。

**赫斯特值小于 0.5**

如果赫斯特值小于 0.5，那么它可以被认为是一个反持续时间序列(大致翻译为横向市场)。

****赫斯特值为 0.5****

如果赫斯特值是 0.5，那么它将表明一个[随机游走](/random-walk/)或一个不可能根据过去数据预测未来的市场。

* * *

## 如何计算赫斯特指数

为了计算指数，我们需要将数据分成不同的块。例如，如果您有过去 8 天的 BTC/美元的返回数据，那么您将它分成两半，如下所示。

以下 8 个观察值的示例仅用于说明目的 <sup>1</sup> :

| **数据** | **组块 1** |
| Zero point zero four |
| Zero point zero two |
| Zero point zero five |
| Zero point zero eight |
| Zero point zero two |
| -0.17 |
| Zero point zero five |
| Zero |

<sup>1</sup> 在实际应用中，子序列的长度通常要长得多，并且会影响 R/S 统计的均值和标准差。

**然后，我们将数据分成如下 3 个不同的缝隙:**

1.  第 1 部分-8 个观察值中的一个
2.  第 2 部分——两大块，每块 4 个观察值
3.  第 3 部分-四大块，每块两个观察值

| **数据** | **组块 1** |
| Zero point zero four |
| Zero point zero two |
| Zero point zero five |
| Zero point zero eight |
| Zero point zero two |
| -0.17 |
| Zero point zero five |
| Zero |

| **数据** | **组块 2** | **组块 3** |
| Zero point zero four | Zero point zero two |
| Zero point zero two | -0.17 |
| Zero point zero five | Zero point zero five |
| Zero point zero eight | Zero |

| **数据** | **组块 4** | **组块 5** | **组块 6** | **组块 7** |
| Zero point zero four | Zero point zero five | Zero point zero two | Zero point zero five |
| Zero point zero two | Zero point zero eight | -0.17 | Zero |

将数据划分为区块后，我们对每个区块执行以下计算:

### 第一步

首先，我们用 n 次观察来计算数据块的平均值，

```py
M = (1/n) [ h(1)+h(2)+...+h(n) ]
```

| **数据** | **组块 1** |
| Zero point zero four |
| Zero point zero two |
| Zero point zero five |
| Zero point zero eight |
| Zero point zero two |
| -0.17 |
| Zero point zero five |
| Zero |

| **数据** | **组块 2** | **组块 3** |
| Zero point zero four | Zero point zero two |
| Zero point zero two | -0.17 |
| Zero point zero five | Zero point zero five |
| Zero point zero eight | Zero |

| **数据** | **组块 4** | **组块 5** | **组块 6** | **组块 7** |
| Zero point zero four | Zero point zero five | Zero point zero two | Zero point zero five |
| Zero point zero two | Zero point zero eight | -0.17 | Zero |

### 第二步

然后我们计算 n 次观察的标准偏差

```py
s(n) = STD( h(1)+h(2)+...+h(n))
```

| **表示** | Zero point zero one one |
| **标准** | Zero point zero seven two |

| **表示** |  0.048 | -0.025 |
| **标准** | Zero point zero two two | Zero point zero nine nine |

| **表示** | Zero point zero three | Zero point zero six five | -0.075 | Zero point zero two five |
| **标准** | 0.0141 | Zero point zero two one | Zero point one three four | Zero point zero three five |

### 第三步

然后我们通过从观察值中减去平均值来创建一个以平均值为中心的序列，

```py
x(1) = h(1) - M x(2) = h(2) - M ... x(n) = h(n) - M
```

| **以平均值为中心的序列的累积和** | Zero point zero two nine |
| Zero point zero three eight |
| Zero point zero seven six |
| Zero point one four five |
| Zero point one five four |
| -0.028 |
| Zero point zero one one |
| Zero |

| **以平均值为中心的序列的累积和** | -0.008 | Zero point zero four five |
| -0.035 | -0.100 |
| -0.033 | -0.025 |
| Zero | Zero |

| **以平均值为中心的序列的累积和** | Zero point zero one | -0.015 | Zero point zero nine five | Zero point zero two five |
| Zero | Zero | Zero | Zero |

### 第四步

然后，我们通过对以平均值为中心的值求和来计算累积偏差，

```py
Y(1) = x(1) Y(2) = x(1) + x(2) ... Y(n) = x(1) + x(2) + ...+ x(n)
```

| **均值中心数列(h(n)-M)** | Zero point zero two nine |
| **标准** | Zero point zero zero nine |

| **均值中心数列(h(n)-M)** | -0.008 | Zero point zero four five |
| **标准** | -0.028 | -0.145 |

| **均值中心数列(h(n)-M)** | Zero point zero one | -0.015 | Zero point zero nine five | Zero point zero two five |
| **标准** | -0.010 | Zero point zero one five | -0.095 | -0.025 |

### 第五步

接下来，我们计算范围(R)，即累积偏差的最大值和最小值之间的差值:

| **范围** | Zero point one eight two |

| **范围** | Zero point zero three five | Zero point one four five |

| **范围** | Zero point zero one | Zero point zero one five | Zero point zero nine five | Zero point zero two five |

### 第六步

最后，我们计算范围 R 与标准偏差 s 的比率。这也称为**重新调整的范围**。

| **范围** | Zero point one eight two |
| **R/S(范围/标准)** | Two point five two eight |
| **平均 R/S** | Two point five two eight |

| **范围** | Zero point zero three five | Zero point one four five |
| **R/S(范围/标准)** | One point six one seven | One point four six seven |
| **平均 R/S** | One point five four two |   |

| **范围** | Zero point zero one | Zero point zero one five | Zero point zero nine five | Zero point zero two five |
| **R/S(范围/标准)** | Zero point seven zero seven | Zero point seven zero seven | Zero point seven zero seven | Zero point seven zero seven |
| **平均 R/S** | Zero point seven zero seven |   |   |   |

### 第七步

一旦我们有了所有块的重新标度范围，我们就计算每个分区的平均值，并记下它以及该分区的每个块中的样本数，如图所示。

![Hurst Exponent 10](img/2e34c5367bad691d02ccdbd19a2fcde9.png)

| **范围** | Zero point one eight two |
| **R/S(范围/标准)** | Two point five two eight |
| **平均 R/S** | Two point five two eight |

| **范围** | Zero point zero three five | Zero point one four five |
| **R/S(范围/标准)** | One point six one seven | One point four six seven |
| **平均 R/S** | One point five four two |   |

| **范围** | Zero point zero one | Zero point zero one five | Zero point zero nine five | Zero point zero two five |
| **R/S(范围/标准)** | Zero point seven zero seven | Zero point seven zero seven | Zero point seven zero seven | Zero point seven zero seven |
| **平均 R/S** | Zero point seven zero seven |   |   |   |

### 第八步

接下来，我们计算每个区域的大小和每个区域的重新调整范围的对数值。

| **总结** |
| **尺寸** | **R/S** | **日志大小** | **R/S 日志** |
| eight | Two point five two eight | Two point zero seven nine | Zero point nine two seven |
| four | One point five four two | One point three eight six | Zero point four three three |
| Two | Zero point seven zero seven | Zero point six nine three | -0.347 |

* * *

## 结果

赫斯特指数“H”只不过是每个区间的对数(R/S)与每个区间的对数(大小)的曲线斜率。

这里 log(R/S)是因变量或 y 变量，log(size)是自变量或 x 变量:

| **赫斯特指数** | **0.918** |

* * *

## 结论

这个赫斯特指数值表明我们的数据是持久的，但我们必须记住，我们的数据集太小，无法得出这样的结论。

例如，如果你想用 python 中的‘hurst’库计算 Hurst 指数，它要求你至少给出 100 个数据点。

我们希望你已经从这篇博客中学会了如何计算赫斯特指数。在我们关于加密货币的[高级课程中，我们展示了赫斯特指数和另一个技术指标如何产生优化的交易信号。](https://quantra.quantinsti.com/course/crypto-trading-strategies-advanced)

* * *

<small>*免责声明:股票市场的所有投资和交易都涉及风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。*T3】</small>
# RNN、LSTM 和 GRU 进行交易

> 原文：<https://blog.quantinsti.com/rnn-lstm-gru-trading/>

由 [Umesh Palai](https://my.linkedin.com/in/umesh-palai-56042818)

在我之前的[文章](/deep-learning-artificial-neural-network-tensorflow-python)中，我们已经开发了一个简单的人工神经网络，并预测了股票价格。但是，在本文中，我们将利用 RNN(递归神经网络)、LSTM(短期记忆网络)&、GRU(门控递归单元网络)的力量来预测股票价格。

我们将使用 python 中的 TensorFlow 1.12 来编码这个策略。您可以从我的 [GitHub 账户中访问所有 python 代码和数据集。](https://github.com/umeshpalai)

如果你还没有浏览过我之前的文章，我建议你在开始这个项目之前浏览一下。

如果你是机器学习和神经网络的新手，我会推荐你先去了解一下[机器学习](/machine-learning-basics)、深度学习、[人工神经网络](/working-neural-networks-stock-price-prediction)、RNN(递归神经网络)、LSTM(短时记忆网络)& GRU(门控递归单元网络)等的一些基本知识。

[![Machine Learning in Trading](img/4bd0a863b70ada6b41c3b47e3dc176af.png)](https://quantra.quantinsti.com/machine-learning-for-trading-ebook)

<u>**涵盖主题:**</u>

*   [编码策略](#Coding-the-Strategy)
*   [导入数据集](#Importing-the-dataset)
*   [缩放数据](#Scaling-data)
*   [分割数据集并构建 X & Y](#Splitting-the-dataset-and-Building)
*   [建立模型](#Building-the-Model)
*   [参数，占位符&变量](#Parameters-Placeholders)
*   [设计网络架构](#Designing-the-network-architecture)
*   [成本函数](#Cost-function)
*   [优化器](#Optimizer)
*   [拟合神经网络模型&预测](#Fitting-the-neural-network-model)
*   [LSTM](#LSTM)
*   [带窥视孔的 LSTM](#LSTM-with-peephole)
*   [GRU](#GRU)

* * *

## **编码策略**

我们将从导入所有库开始。请注意，如果下面的库还没有安装，您需要在导入之前首先在 anaconda 提示符下安装，否则您的 python 将抛出一个错误消息

![](img/766fab4eaf1b2a465460ed97fd7afb9f.png)

我假设你知道我们在这里使用的所有上述 [python 库](/python-trading-library)。

* * *

## **导入数据集**

在该模型中，我们将使用 1996 年 1 月 1 日至 2018 年 9 月 30 日期间在 NSE 上交易的“RELIANCE”股票的每日 OHLC 数据。

我们导入数据集。名为“RELIANCE”的 CSV 文件。“NS.csv”保存在您计算机的个人驱动器中。这是使用 **pandas** 库完成的，数据存储在名为 dataset 的数据帧中。

然后，我们使用 **dropna()** 函数删除数据集中缺失的值。我们仅从该数据集中选择 [OHLC](/tick-tick-ohlc-data-pandas-tutorial) 数据，该数据集中还包含日期、调整后收盘和成交量数据。

![Importing Dataset](img/1459b87c4a19439e25f1bbc3c9863c2d.png)

* * *

## **缩放数据**

在分割数据集之前，我们必须标准化数据集。此过程会使所有输入要素的平均值等于零，并将它们的方差转换为 1。这确保了在训练模型时不会因为所有输入要素的不同比例而产生偏差。

如果不这样做，[神经网络](https://quantra.quantinsti.com/course/neural-networks-deep-learning-trading-ernest-chan)可能会混淆，并给予那些平均值比其他特征高的特征更高的权重。此外，网络神经元(如 tanh 或 sigmoid)的最常见激活函数分别定义在[-1，1]或[0，1]区间上。

如今，**校正线性单位** (ReLU)激活是常用的激活，其在可能激活值的轴上是无界的。但是，我们将调整投入和目标。

我们将使用 sklearn 的 **MinMaxScaler** 进行缩放。

![Scaling data](img/86b6c82ed3cf63ee3fa8b5e97c3da669.png)

* * *

## **拆分数据集并构建 X & Y**

接下来，我们将整个数据集分为训练数据、有效数据和测试数据。然后我们可以建立 X & Y，所以我们会得到 x_train，y_train，x_valid，y_valid，x_test & y_test。这是至关重要的一部分。

请记住**我们不是像之前的项目**那样简单地对数据集进行切片。这里我们给定序列长度为 20。

![Splitting the dataset](img/89afbb5b1a2636e7ebab5ee09a7e926b.png)

我们的总数据集是 5640。所以前 19 个数据点是 x_train。接下来的 4497 个数据点是 y_train，其中最后 19 个数据点是 x_valid。接下来的 562 个数据点是 y_valid，其中最后 19 个数据点是 x_test。

最后，下一个和最后一个 562 个数据点是 y_test。我试着画这个只是为了让你明白。

![Data points](img/941749bfd8e0849ba0a45456e768f2ad.png)

* * *

## **建立模型**

我们将建立四个不同的模型——基本 RNN 单元、基本 LSTM 单元、带窥视孔连接的 LSTM 单元和 GRU 单元。请记住，您一次只能运行一个模型。我把所有东西都放进一个编码里。

每当运行一个模型时，确保将另一个模型作为注释，否则结果将是错误的，python 可能会抛出错误。

* * *

## **参数，占位符&变量**

我们将首先确定用于构建任何模型的参数、占位符和变量。[人工神经网络](https://quantra.quantinsti.com/course/neural-networks-deep-learning-trading-ernest-chan)从占位符开始。

为了适合我们的模型，我们需要两个占位符:X 包含网络的输入(T = t 时股票(OHLC)的特征), Y 包含网络的输出(T+1 时股票的价格)。

占位符的形状对应于 None，n_inputs，其中[None]表示输入是二维矩阵，输出是一维向量。

理解神经网络需要哪些输入和输出维度以正确设计它是至关重要的。我们将可变批量大小定义为 50，它控制每个训练批次的观察次数。

当 epoch 达到 100 时，我们停止训练网络，因为我们已经在参数中将 epoch 指定为 100。

![Parameters Placeholders Variables](img/eed07c691d60067161e9718fd3dd3521.png)

* * *

## **设计网络架构**

在我们继续之前，我们必须为任何模型编写运行下一批的函数。然后，我们将分别为每个模型编写层。

![Designing the network architecture](img/415d56f844d1af8a539d341a487ca66c.png)

请记住，无论何时运行一个特定的模型，您都需要将其他模型作为注释。在这里，我们只运行 RNN 基础，所以我把所有其他的作为一个注释。你可以运行一个又一个模型。

![RNN basic](img/b79a074cbb0eb13c34cf7db3e433d6bb.png)

* * *

## **成本函数**

我们使用成本函数来优化模型。成本函数用于生成网络预测和实际观察到的训练目标之间的偏差度量。

对于回归问题，常用的是**均方误差(MSE)** 函数。MSE 计算预测值和目标值之间的均方差。

![Cost function](img/797e8008bd4dfdeccac274605405853b.png)

* * *

## **优化器**

优化器负责必要的计算，这些计算用于在训练期间适应网络的权重和偏差变量。这些计算调用梯度的计算，该梯度指示在训练期间权重和偏差必须改变的方向，以便最小化网络的成本函数。

开发稳定和快速的优化器是神经网络和深度学习研究的一个主要领域。

![Optimizer](img/72430b9d8c092010888dc58c2c74b919.png)

在这个模型中，我们使用 **Adam** (自适应矩估计)优化器，它是随机梯度下降的扩展，是深度学习开发中的默认优化器之一。

* * *

## **拟合神经网络模型&预测**

现在，我们需要使我们创建的模型适合我们的训练数据集。在定义了网络的占位符、变量、初始化器、成本函数和优化器之后，需要训练模型。通常，这是通过小批量训练来完成的。

在小批量训练期间，从训练数据中抽取 n = batch_size 的随机数据样本，并输入到网络中。训练数据集被分成 n / batch_size 个批次，这些批次被顺序输入到网络中。此时，占位符 X 和 Y 开始发挥作用。它们存储输入和目标数据，并将它们作为输入和目标呈现给网络。

X 的一个采样数据批次流经网络，直到它到达输出层。在那里， [TensorFlow](/install-tensorflow-gpu) 将模型的预测与当前批次中实际观察到的目标 Y 进行比较。

之后，TensorFlow 执行优化步骤并更新网络参数，对应于所选的学习方案。更新重量和偏差后，对下一批进行采样，重复该过程。该过程继续进行，直到所有批次都被呈现给网络。

所有批次的一次完整扫描称为一个时期。一旦达到最大次数或者用户定义的另一个停止标准适用，网络的训练就停止。

当 epoch 达到 100 时，我们停止训练网络，因为我们已经在参数中将 epoch 指定为 100。

![Fitting the neural network model & prediction](img/0879c2a1fe7aa0920a182d951f0431fa.png)

现在我们已经预测了股票价格，并保存为 y_test_pred。我们可以将这些预测的股价与我们的目标股价进行比较，也就是 y_test。

为了检查输出的数量，我运行了下面的代码及其 562，它与 y_test 数据相匹配。

![Y_test code](img/a806febb6aeab0e8a682f318e3e1f152.png)

![y_test output](img/44fde3754d3ccf1536fbdaac16dc0e6c.png)

让我们比较一下我们的目标和预测。我将目标(y_test)和预测(y_test_pred)收盘价放在一个名为“comp”的数据框架中。

现在我把两个价格放在一个图中，让我们看看它看起来怎么样。

![Plotting the graph](img/aac45fee1f7ee70d2ab0a438973f83c8.png)

![Plotting output](img/689b6132f9ecd1b263d3724d831d13c8.png)

现在我们可以看到，结果还不错。预测值与目标值完全相同，并与我们预期的方向一致。你可以检查这两者之间的差异，并以各种方式比较结果&在建立交易策略之前优化模型。

* * *

## **LSTM**

现在我们可以运行基本的 LSTM 模型，看看结果。

![LSTM](img/c6c6d9833558c238a543a571b08cac41.png)

![LSTM output](img/cdc12d2f656010428c3b40f32b45cfa8.png)

* * *

## **带窥视孔的 LSTM**

让我们运行 LSTM 与窥视孔连接模型，看看结果。

![LSTM peephole](img/08e0aa3b9fed4c96526b8e667b9a419c.png)

![peephole output](img/3011eeeb27446bacfb3ed52b38651622.png)

* * *

## **GRU**

让我们运行 GRU 模型，看看结果。

![GRU](img/6174540bec9f710e8dab5c65e195a354.png)

![GRU output](img/edeca567e300af56053bffde820e1d29.png)

你可以用各种方式检查和比较结果&在建立交易策略之前优化模型。

* * *

## **结论**

这个项目的目标是让你了解如何建立一个不同的神经网络模型，像 RNN，LSTM 和 GRU 在 python 张量流和预测股票价格。

你可以通过各种方式优化这个模型，建立自己的交易策略，考虑**命中率**、**下降**等因素，获得良好的策略回报。另一个重要因素是，我们在这个模型中使用了每日价格，所以数据点实际上很少，只有 5，640 个数据点。

我的建议是，在建立人工神经网络或任何其他最有效的深度学习模型时，使用超过 100，000 个数据点(使用分钟或分笔成交点数据)来训练模型。

现在你可以利用机器的能力和智能来建立自己的交易策略。

*<small>免责声明:本文提供的所有数据和信息仅供参考。QuantInsti 对本文中任何信息的准确性、完整性、现时性、适用性或有效性不做任何陈述，也不对这些信息中的任何错误、遗漏或延迟或因其显示或使用而导致的任何损失、伤害或损害负责。所有信息均按原样提供。</small>*

* * *

**zip 存档中的文件列表:**

1.  深度学习 GRU LSTM RNN
2.  信赖。纳秒
# 使用蓝移可视化编程的机器学习策略

> 原文：<https://blog.quantinsti.com/machine-learning-strategy-using-blueshift-visual-programming/>

作者[高拉夫·辛格](https://www.linkedin.com/in/singh-gamer-gaurav/)

算法交易是关于你如何研究，回溯测试，分析，然后实时交易你的策略。Blueshift 是一个平台，在这里你可以**构建、分析**和**交易**你的系统投资策略。在 Blueshift 上，你可以根据历史数据**回溯测试**你的策略。在令人满意的回溯测试结果之后，你可以**通过连接你的经纪人和 Blueshift 进行纸上交易或现场交易**。Blueshift 的伟大之处在于它是一个免费使用的**平台！**

你可以在 Blueshift 上看到完整的机器学习策略会是什么样子。只需点击下面的按钮！一个新的窗口将会打开，带有在这篇博客中讨论的预先构建的策略。

<button onclick="createStrategy('blog_ml_strategy', 'blog_ml_strategy', 'visual_code', undefined, undefined)" style="background-color: #92c94a;
    padding: 12px 20px;
    border-radius: 5px;
    color: #fff;">在 Blueshift 上查看策略！</button>

在本文中，您将学习构建一个机器学习策略。你可以很容易地使用 Blueshift 的酷新添加的可视化编程接口来制定这个策略。这个策略将在不写一行计算机代码的情况下建立。此外，在您的系统中不需要特殊的软件安装。一切都将在[蓝移平台](https://blueshift.quantinsti.com/)上完成！

本文涵盖:

*   [什么是 Blueshift 的可视化编程？](#what-is-blueshift-s-visual-programming)
*   [blue shift 可视化编程中的机器学习管道](#machine-learning-pipeline-in-blueshift-s-visual-programming)
*   [构建机器学习策略](#building-a-machine-learning-strategy)
*   [回溯测试和实时交易策略](#backtesting-and-live-trading-the-strategy)
*   [战略的未来改进](#future-enhancements-to-the-strategy)

## Blueshift 的可视化编程是什么？

有很多人有丰富的交易经验，但他们不擅长计算机编程。这大大增加了参与算法交易的门槛。Blueshift 最近增加了一个名为**可视化编程**的功能。这个特性使你能够在没有任何编码知识的情况下创建策略**。没错，您只需通过**拖放**策略构建模块就可以创建策略！**

你可以在 Blueshift 的可视化编程上查看 7 集 youtube 系列。本系列解释了用户界面和平台的不同特性。它还构造了一个简单的交叉策略。

## Blueshift 可视化编程中的机器学习管道

可视化编程不仅仅是一个简单易用的界面来定义一套简单的交易规则。可视化编程是一种几乎**完整的编程语言**，能够处理任何逻辑。

这意味着你也可以**建立复杂的策略**，比如机器学习模型。你可以使用 Blueshift 来回溯测试或实时交易机器学习策略，就像你可以回溯测试一个简单的交叉策略一样容易。如果不熟悉机器学习，可以在 Quantra 上做免费课程[交易用机器学习入门](https://quantra.quantinsti.com/course/introduction-to-machine-learning-for-trading)！

在易于使用的界面下，是一个智能软件引擎，它验证可视块并将其转换为 python 代码。Blueshift 可视化编程中的**机器学习流水线**遵循 [sklearn 流水线流程](https://scikit-learn.org/stable/modules/generated/sklearn.pipeline.Pipeline.html)。

![Machine Learning Pipeline](img/8154d1d027efb2dc10eeffd612f97505.png)

如果您不熟悉管道术语，也不用担心！流水线只是一组应用于数据集的**转换器和估计器**。换句话说，应用一系列数学运算来适当地转换数据。然后，估计器基本上试图在数据中找到模式。这种模式发现也被称为“**模型拟合**”。衡量模型与新数据“吻合”程度的标准被称为“**得分**”。“分数”让我们了解模型预测任何未知数据的准确性。

机器学习流水线中的最后一个估计器只需要实现“fit”函数，就可以得到结果。分数调用估计量的基本“分数”函数。

下图给出了如何构建和使用机器学习模型的想法，以及相关的 Blueshift 可视化编程块。该模型通过添加特征、目标和估计器来建立。理想情况下，**特征**之间应该是不相关的，并且具有弱预测性。**目标**是数据集，该数据集是或者应该是机器学习输出。

基于手头的问题陈述选择**估计器**。例如，如果最终输出是预测价格，则使用回归估计量。但是，如果最终输出是一个分类(维持多头头寸或不维持头寸)，则使用分类器估计器。

**注**:目标可以是回归(不需要级别)也可以是分类(需要级别)。

![Machine Learning Model Flow](img/50ffbe7143ac0ec9f7d473d1df3426d1.png)

然后使用“估计”模块对模型**进行编译和拟合。然后使用“预测”模块**计算模型**预测。最后，使用“评分”模块**对未知数据的模型进行**评分。**

## 构建机器学习策略

在本文中，您将学习如何使用[随机森林分类](/random-forest-algorithm-in-python/)估计器**构建一个** **只长机器学习模型**。这意味着，该策略将只采取多头头寸，底层机器学习估计器是**随机森林分类器**。

您可以从这里建立的策略(回溯测试从 2015 年 1 月开始到 2020 年 11 月)中预期的关键[回溯测试](/backtesting/)结果如下:

| **公制** | **值** |
| 年度回报 | 10.98% |
| 累积回报 | 83.58% |
| 年度波动性 | 9.96% |
| 夏普比率 | One point zero nine |
| 最大水位下降 | -10.60% |

****注意**** :每次运行模型时，回溯测试的结果都会略有不同。这种差异是由于模型用来拟合数据的随机森林算法中固有的随机性。

现在，让我们使用 Blueshift 的可视化编程来创建这个策略。如果不熟悉用户界面，可以参考[界面概述](https://www.youtube.com/watch?v=0dvKxuWcGMY&list=PLD7IrLyN7uvKttgKqWOMBvRikEk3xezoU&index=2&t=50)视频。



[https://www.youtube.com/embed/0dvKxuWcGMY?start=50&feature=oembed](https://www.youtube.com/embed/0dvKxuWcGMY?start=50&feature=oembed)



该策略是通过以下步骤构建的:

### 策略设置

初始策略块如下所示:

![Initial Strategy Block](img/60be1da5c39e0bda90235424052381c2.png)

确保选择数据集为 **NYSE-DAILY** ，因为您将根据 NYSE 每日数据设计策略。当你在做多头策略时，将**多头选项设置为“真”**。要了解每个参数的更多信息，可以参考[策略设置和交易宇宙](https://www.youtube.com/watch?v=vu6HBVJbt6w&list=PLD7IrLyN7uvKttgKqWOMBvRikEk3xezoU&index=3)视频。



[https://www.youtube.com/embed/vu6HBVJbt6w?feature=oembed](https://www.youtube.com/embed/vu6HBVJbt6w?feature=oembed)



### 定义宇宙

将“设置范围”和“选择资产”块连接到“定义范围”步骤。对于这个样本策略，您可以选择这些股票:AMZN，AAPL，WMT，MU，BAC，KO，BA，AXP。

![Define the Universe](img/58a353df854c3bb3a5bbfd07a6c4f9bc.png)

### 定义 Alpha(机器学习模型)

你策略的 alpha 将是机器学习模型的预测输出。所以你需要将**机器学习模型定义为你的策略 alpha** 。为了刷新你对阿尔法和变量的记忆，你可以参考[变量和阿尔法函数](https://www.youtube.com/watch?v=1maN14wxVnQ&list=PLD7IrLyN7uvKttgKqWOMBvRikEk3xezoU&index=4)视频。



[https://www.youtube.com/embed/1maN14wxVnQ?feature=oembed](https://www.youtube.com/embed/1maN14wxVnQ?feature=oembed)



使用左侧机器学习菜单中的“使用模型”创建模型。可以将模型命名为“model_1”。

![Creating the Model](img/aa148ac1cc1bbf9ca53cc0f334b87d0a.png)

将“model_1”块连接到“定义 alpha”步骤。

![Connect the Model to the Define Alpha](img/ccb88a816c471688da8d5fdd731f8bc3.png)

要定义模型，您需要指定这三件事:

1.  特征
2.  目标
3.  估计量

### 特征

Blueshift 可视化编程中可用的功能如下:

1.  **技术**:交叉、MFI、RSI、斐波那契等等
2.  **统计**:峰度、var、均值、中值等
3.  **价格行为特征**:多空、吞没、跳空/下跌等

您可以使用这些功能的任意组合来分析性能。向模型添加特征非常容易。只需将相关模块连接到“添加功能”并点击选择功能。

![Add Features Menu](img/40827174e43b522a89eaa49d7b4fdd50.png)

菜单显示哪些功能可用，哪些功能当前已被选中。

通过加载本节末尾的 ****预构建策略，可以看到本示例策略中使用的特性。****

![Defining Features in the Model](img/6b6f6ad4cb48d4b39ffe23d7e0783347.png)

### 目标

目标将价格回报性能(基于收盘价)自动映射到估计器目标(分类或回归输出)。定义目标所需的输入有:

1.  **编码的级数**:在样本分类策略中，可以“保持多头”也可以“不保持仓位”。因此，编码级别将是二。如果估计量属于回归类型，那么级数将为零。
2.  **回望期**:收益计算的回望期。
3.  **衡量回报表现的方法**:在计算回报时使用百分比变化或差异。对于示例策略，选择“pct_change”选项。

![Defining Targets in the Model](img/0c0dc6e5ffed182bf5a7d16e875bde27.png)

### 估计量

除了预处理和特征选择，还可以使用 Blueshift 可视化编程中的机器学习管道进行降维。最后，添加一个估计器来获得模型输出。

可用选项包括:

1.  **特征选择**:选择 k 个最佳特征
2.  **降维** :
    a) PCA
    b)线性核 PCA
    c) rbf 核 PCA
3.  **估计器**和**滚动估计窗口** :
    a)分类:Logit、岭、随机森林、xgboost 等
    b)回归:OLS、拉索、岭、随机森林等

对于你的策略，选择 **PCA 降维到 25 个分量**。选择**分类估计器**块，估计器为“ **rf** ”(随机森林)，滚动估计窗口为**500 个周期**(日频率数据约为 2 年)。

![Defining Estimators in the Model](img/a17dbd573828d04890ebcf1f5c2c3dfa.png)

### 定义交易规则和交易时间表

你现在要定义交易规则并安排你的策略。如果不熟悉交易规则块，可以参考[交易规则和动作](https://www.youtube.com/watch?v=EJAh435hdoc&list=PLD7IrLyN7uvKttgKqWOMBvRikEk3xezoU&index=5)和[调度和下单参数](https://www.youtube.com/watch?v=djheRnTCu4U&list=PLD7IrLyN7uvKttgKqWOMBvRikEk3xezoU&index=6)教程视频。



[https://www.youtube.com/embed/djheRnTCu4U?feature=oembed](https://www.youtube.com/embed/djheRnTCu4U?feature=oembed)



样本策略在每月的第一天交易，在市场关闭前 2.5 小时。

相应地添加调度块。

![Add the Schedule Block](img/f089dfbe5cfd615ab26b5e1ff0ab52c0.png)

然后，您需要编译并拟合模型，然后才能使用其预测。您通过使用“估计”块来编译和拟合模型。

![Adding the Model](img/9f6f18f16a707d75c54473bcf3a55411.png)

现在你已经准备好利用这个模型了。但是，你想一直使用模型吗？

不要！当模型精度比随机预测差时，您不希望使用该模型。所以您添加了一个逻辑“如果条件”，它声明只有当模型得分优于 0.5 (50%平均准确度)时，我们才会使用该模型。

![Scoring the Model](img/bc487a07e7a8c6903f20f41de7b1d2ff.png)

“score”块调用估算器的基础 sklearn 得分函数**。由于您使用的是随机森林分类器，它会根据给定的测试数据和标签([来源](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html))为您提供**平均准确度**。**

现在，您将使用“predict”块来了解模型是将其预测为 0 类(不维持仓位)还是 1 类(维持多头仓位)。

![Predict Model Block](img/e9ef163b6ee7447e969666cdff044af0.png)

您可以为分类输出 1 制作一个**长条目。分类输出 0** 的**长退出。你已经在[交易规则和行动](https://www.youtube.com/watch?v=EJAh435hdoc&list=PLD7IrLyN7uvKttgKqWOMBvRikEk3xezoU&index=5)视频中学到了这些。**



[https://www.youtube.com/embed/EJAh435hdoc?feature=oembed](https://www.youtube.com/embed/EJAh435hdoc?feature=oembed)



![Adding the Trade Actions](img/841ffd71ca0f8cccb405cf067f5c3e07.png)

订单类型以“**目标**类型方法设置为 **0.1** 的“**组合分数**”。这意味着你将持有这些资产的头寸，从而将 10%的可用投资组合财富分配给多头头寸。同样，如果分类输出为 0，你退出多头。

您的策略现已完成！你可以点击这个按钮来启动蓝移可视化编程，这个策略是预先建立的！

<button onclick="createStrategy('blog_ml_strategy', 'blog_ml_strategy', 'visual_code', undefined, undefined)" style="background-color: #92c94a;
    padding: 12px 20px;
    border-radius: 5px;
    color: #fff;">启动蓝移上的预建策略</button>

您也可以通过点击屏幕右下方的“查看代码”按钮来查看自动生成的代码。

![Viewing the Code of the Visual Programming](img/7f99f4802ca7ea867b70917618105815.png)

可以在新的弹出窗口中看到生成的代码。可视化编程接口的所有模块都被转换成 python 代码，然后由 Blueshift 平台运行。

![Automatically Generated Code](img/19cdb4d5be68ffd4f8729e91912c21e3.png)

## 回溯测试和实时交易策略

您可以通过点击“新回测”按钮获得机器学习策略的详细回测。选择数据集为 **NYSE-DAILY** ，对 2015 年 1 月至 2020 年 11 月的策略进行回溯测试。

关键绩效指标如下:

![Strategy Performance](img/10123bfde94b27aa306ad625d7dacdbc.png)

有趣的是，由于新冠肺炎疫情，基准回报率在 2020 年初大幅下降。但是，在 2020 年的前几个月，投资组合回报显著优于基准。

总的来说，当基准回报率突然下降时，这种策略避免了大规模提款。在近 5 年的时间里，夏普比率达到 1.09 也被认为是好的。

在满意的回测结果后，你就可以进行纸上交易，然后对你的模型进行现场交易！只需点击“上线”按钮。

按照屏幕上的步骤实时交易您的策略！可以参考[回测和现场交易](https://www.youtube.com/watch?v=UrzDnv3w3qg&list=PLD7IrLyN7uvKttgKqWOMBvRikEk3xezoU&index=7)视频，详细看每个步骤。



[https://www.youtube.com/embed/UrzDnv3w3qg?feature=oembed](https://www.youtube.com/embed/UrzDnv3w3qg?feature=oembed)



一旦您连接了您的经纪人并添加了策略设置，该策略就被设置为在实时价格日期进行交易。您可以在实时交易概览中分析交易日志、策略指标和控制台输出。

![Live Trading Overview](img/c7451538307f1de26250adeb83bd937a.png)

## 该战略的未来改进

你在这里学到的策略实现了一个基于几个特征的随机森林分类器。您可以尝试不同的输入特性组合，看看是否能提高性能。如前所述，可以从易于使用的图形界面中选择功能。您只需将相关模块连接到“添加功能”并从菜单中选择。

您还可以**更改策略超参数**，如回顾窗口和估计器数量。在你的交易领域中，机器学习模型对不同的资产会有不同的表现。你可以改变可交易的资产并分析其表现。

您可以添加复杂的**风险管理交易规则**以及不同的止损和止盈标准。随意调整这个策略来满足你的需求！

如果你需要回忆如何使用界面或任何模块，你可以参考[可视化编程教程系列](https://www.youtube.com/watch?v=Dj_RUh1WHFg&list=PLD7IrLyN7uvKttgKqWOMBvRikEk3xezoU&index=1)。



[https://www.youtube.com/embed/videoseries?list=PLD7IrLyN7uvKttgKqWOMBvRikEk3xezoU](https://www.youtube.com/embed/videoseries?list=PLD7IrLyN7uvKttgKqWOMBvRikEk3xezoU)



* * *

**[<input name="Visit Blueshift" type="button" value="Visit Blueshift" style="
  background-color: #92c94a;
  padding: 12px 20px;
  border-radius: 5px;
  color: #fff;
  font-size: 18px;
">](https://blueshift.quantinsti.com/)T4】**

* * *

如果您需要任何帮助或支持，请通过 [Quantra 社区论坛](https://quantra.quantinsti.com/community)联系我们，或者通过 blueshift-support@quantinsti.com[给我们写信](mailto:blueshift-support@quantinsti.com)。

*<small>免责声明:股票市场的所有投资和交易都涉及风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。</small>T3】*
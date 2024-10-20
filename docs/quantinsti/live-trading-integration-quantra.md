# Quantra 上的实时交易集成

> 原文：<https://blog.quantinsti.com/live-trading-integration-quantra/>

由[维布·辛格](https://www.linkedin.com/in/vibhu-singh-1b76b6105/)

你想要一个可以学习、回溯测试、优化和交易市场策略的地方吗？

这样的地方难道不是交易爱好者的天堂吗？

Quantra 试图做到这一点。在 Quantra，你可以学习不同的交易策略，从[动量](https://quantra.quantinsti.com/course/momentum-trading-strategies)到均值回归，日间交易策略，甚至机器学习策略。

您还可以分析和优化策略的性能，一旦您对性能感到满意，通过一键式集成功能，您可以将您的策略投入使用。

在这篇博客中，您将学习基于机器学习创建一个简单的交易策略，通过 Quantra 平台在实时市场中一键实施相同的策略，并分析策略性能。

本文涵盖以下主题:

*   [什么是机器学习？](#what-is-machine-learning)
*   [构建简单的机器学习策略](#build-a-simple-machine-learning-strategy)
*   [通过 Quantra 在 Blueshift 上进行实时交易](#live-trade-on-blueshift-through-quantra)
*   [分析战略的绩效](#analyse-the-performance-of-the-strategy)

* * *

## 什么是机器学习？

[机器学习](/machine-learning-basics/)是[人工智能](/artificial-intelligence-machine-learning-trading/)的子集，它为机器提供了基于经验、观察和模式自主学习的能力，而无需显式编程。我们输入一个数据集，机器通过它学习并建立一个模型来进行预测和决策。

我们来了解一下如何在交易中使用机器学习。

假设你有一个[机器学习算法](/top-10-machine-learning-algorithms-beginners/)拥有所有的智能。该算法可以像线性回归、支持向量分类器一样简单，也可以像[深度神经网络](https://quantra.quantinsti.com/course/neural-networks-deep-learning-trading-ernest-chan)一样先进。

你需要决定的下一件事是你想从机器学习算法中得到什么。机器学习算法在交易中的典型结果是找到进入和退出头寸的点。

简单来说，什么时候买入或卖出，什么时候退出开仓。另一个结果是买卖的股票数量或买卖的价格。

你已经定义了你的机器学习算法，也定义了结果。但是这个算法是如何实现这个结果的呢？

这需要数据，或者用更复杂的语言来说，你可以说它是一个特征，它将帮助 ML 算法预测结果。

这是任何机器学习算法中最重要也是最耗时的部分之一。特征的一些例子是历史价格，如 OHLC 数据、[蜡烛图](/candlestick-patterns-meaning/)、交易时间、[技术指标](/tag/technical-indicators/)或基本面数据，如市盈率。

总而言之，你将特征或数据传递给机器学习算法，它将预测你定义的结果。

![Machine Learning Flow Diagram](img/5f4d8d0f648595098bab40dd52bc0238.png)

让我们用这个概念来构建一个机器学习交易策略，来预测标准普尔 500 第二天的走势。

* * *

## 构建简单的机器学习策略

### 导入库和包

设计和创建 ML 策略的第一步是导入您需要使用的库和包。一些常用的库是:

*   [熊猫](/python-pandas-tutorial/)和 [Numpy](/python-numpy-tutorial-installation-arrays-random-sampling/) 进行数据读取和操作。
*   Matplotlib 是另一个流行的用于绘图的 Python 库。
*   Sklearn 是 Python 编程语言最流行的机器学习库之一。

如果您不知道将在策略创建过程中使用的库，也可以根据需要导入这些库，而不是一次导入。
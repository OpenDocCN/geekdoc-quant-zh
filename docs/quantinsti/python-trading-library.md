# 用于算法交易的流行 Python 库

> 原文：<https://blog.quantinsti.com/python-trading-library/>

由[沙古塔塔西尔达](https://www.linkedin.com/in/shaguftatahsildar/)&T2】阿波瓦辛格

通过这篇关于“Python 库和平台”的文章，我们将涵盖最流行和最广泛使用的 Python 交易平台和用于量化交易的 Python 交易库。

我们之前也报道过最流行的量化交易回测平台，你可以在这里查看。

Python 是一种免费的开源和跨平台的语言，它有一个丰富的库，可以用于几乎所有可以想象的任务，还有一个专门的研究环境。 [Python](https://quantra.quantinsti.com/course/python-for-trading) 是中低交易频率(即持续时间不少于几秒钟的交易)自动交易的绝佳选择。它有多个 APIs 库，可以链接起来优化它，并允许多种交易想法的更大探索性发展。比如我们可以通过 [Python 股票 API](/historical-market-data-python-api/) 获取历史行情数据。

我们整理了一份由专家撰写的关于 Python 交易的最受欢迎的[博客列表。](/python-trading-top-blogs/)

在这篇博客中，除了流行的 [Python 交易平台](/python-trading-library/#PTP)，我们还将关注流行的 Python 交易库的各种功能，如:

*   [技术分析](#python-trading-library-for-technical-analysis)
*   [数据操作](#python-trading-libraries-for-data-manipulations)
*   [标绘结构](#python-trading-library-for-plotting-structures)
*   [机器学习](#python-trading-libraries-for-machine-learning)
*   [回溯测试](#python-trading-libraries-for-backtesting)
*   [数据收集](#python-trading-libraries-for-data-collection)

![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")

## 用于技术分析的 Python 交易库

### ****TA-Lib**T3】**

[TA-Lib](/install-ta-lib-python/) 或技术分析库是一个开源库，广泛用于使用 RSI(相对强弱指数)、布林线、MACD 等技术指标对金融数据进行技术分析。它不仅适用于 Python，还适用于其他编程语言，如 C/C++、Java、Perl 等。下面是 TA-Lib 中可用的一些函数:BBANDS -用于布林线，AROONOSC -用于 Aroon 振荡器，MACD -用于移动平均线收敛/发散，RSI -用于相对强弱指标。在此阅读更多此类功能[。](https://www.ta-lib.org/function.html)

![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")

## 用于数据操作的 Python 交易库

### ****NumPy**T3】**

NumPy 或数字 Python，提供了大型多维数组和矩阵的强大实现。该库由用于复杂数组处理和这些数组的高级计算的函数组成。这个库的一些数学函数包括三角函数(sin，cos，tan，弧度)，双曲函数(sinh，cosh，tanh)，对数函数(log，logaddexp，log10，log2)等。

### ****熊猫****

Pandas 是一个巨大的 Python 库，用于数据分析和操作，也用于处理数字表或数据框和时间序列，因此，大量用于使用 Python 的算法交易。熊猫可以用于各种功能，包括进口。csv 文件、串行执行算术运算、布尔索引、收集关于数据帧的信息等。

### ****SciPy****

[SciPy](https://www.scipy.org/) ，顾名思义，是一个用于科学计算的开源 Python 库。它与 NumPy 一起用于执行复杂的功能，如数值积分、优化、图像处理等。这是 SciPy 的几个模块，用于执行上述功能:scipy.integrate(用于数值积分)、scipy.signal(用于信号处理)、scipy.fftpack(用于快速傅立叶变换)等。

![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")

## 用于绘制结构的 Python 交易库

### ****【matplot lib】****

这是一个 Python 库，用于绘制 2D 结构，如图形、图表、直方图、散点图等。与用于计算的其他库一起，有必要使用 [matplotlib](/python-matplotlib-tutorial/) 使用图表和图形以图形格式表示数据。matplotlib 的一些功能包括散点图、饼图、堆积图、颜色条等。

![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")

## 用于机器学习的 Python 交易库

### ****Scikit-learn****

它是一个基于 SciPy 库构建的机器学习库，由各种算法组成，包括分类、聚类和回归，可以与其他 Python 库(如 NumPy 和 SciPy)一起用于科学和数值计算。它的一些类和函数是 sklearn.cluster、sklearn.datasets、sklearn.ensemble、sklearn.mixture 等。你可以在这里阅读更多关于图书馆及其功能的信息。

### ****张量流****

[TensorFlow](https://www.tensorflow.org/) 是一个开源软件库，用于高性能数值计算和机器学习应用，如[神经网络](https://quantra.quantinsti.com/course/neural-networks-deep-learning-trading-ernest-chan)。它允许跨各种平台(如 CPU、GPU、TPU 等)轻松部署计算。由于其灵活的架构。点击了解如何安装 TensorFlow GPU [。](/install-tensorflow-gpu/)

### ****Keras****

[Keras](https://keras.io/) 是深度学习库，用于开发神经网络和其他深度学习模型。它可以建立在 TensorFlow、Microsoft Cognitive Toolkit 或 Theano 之上，并专注于模块化和可扩展。它由用于构建神经网络的元素组成，如层、目标、优化器等。在 Python 和 R 上安装 Keras 在这里演示[。该库可用于利用人工神经网络](/installing-keras-python-r/)预测[股票价格的交易中。](/artificial-neural-network-python-using-keras-predicting-stock-price-movement/)

![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")

## 用于回溯测试的 Python 交易库

### ****PyAlgoTrade**T3】**

一个事件驱动的库，专注于回溯测试，支持纸上交易和现场交易。PyAlgoTrade 允许你用历史数据评估你的交易想法，看看它的表现如何。支持[事件驱动的](https://quantra.quantinsti.com/course/event-driven-trading-strategies)回溯测试，访问来自雅虎财经、谷歌财经、NinjaTrader CSVs 的数据以及 CSV 中任何类型的时间序列数据。文档很好，支持 TA-Lib 集成(技术分析库)。它在速度和灵活性方面胜过其他库，然而，最大的缺点是它不支持 Pandas-object 和 Pandas 模块。

### ****滑索****

这是一个事件驱动的系统，支持回溯测试和实时交易。Zipline 有很好的文档记录，有一个很棒的社区，支持交互式经纪人和熊猫集成。然而，与在已编译的应用程序中具有回溯测试功能的商业平台相比，Zipline 速度较慢，并且对于多种产品的交易来说不太方便。

### ****Pybacktest****

Python/pandas 中的矢量化回溯测试框架，旨在使您的回溯测试变得紧凑、简单和快速。它允许用户使用 pandas 的全部功能来指定交易策略，同时隐藏所有交易、股票、业绩统计的手动计算并创建可视化。产生的策略代码在研究和生产环境中都是可用的。目前，只支持单一安全性回溯测试，多重安全性测试可以通过运行单一 sec 回溯测试，然后结合股权来实现。它正在进一步发展，以包括多资产回溯测试能力。

![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")

## 用于数据收集的 Python 交易库

### ****超级金融****

这是一个矢量化系统。一个用于实时金融数据收集、分析和[回溯测试交易策略](https://quantra.quantinsti.com/course/backtesting-trading-strategies)的 python 项目。支持从 Yahoo Finance、Google Finance、HBade 和 Excel 访问数据。

### ****【TWP(用 Python 交易)****

TradingWithPython 或 TWP 库也是一个矢量化系统。它是用于量化交易的函数和类的集合。它包括从雅虎财经、CBOE 和互动经纪人等来源获取数据的工具，以及经常使用的 P&L 基准函数。然而，这个库的文档和课程要花费 395 美元。

### ****使用 Python 在互动券商上交易****

[Interactive Brokers](https://www.interactivebrokers.com/en/home.php) 是一个电子经纪人，它使用包括 Python 在内的各种编程语言提供了一个连接实时市场的交易平台。它为各种电子交易产品提供了全球 100 多个市场目的地，包括股票、期权、期货、外汇、债券、差价合约和基金。IB 不仅有非常有竞争力的佣金和利润率，而且有一个非常简单和用户友好的界面。这里我们将讨论如何使用 Python 连接到 IB。

有几个有趣的 Python 库可以用来连接使用 IB 的实时市场，你需要首先拥有一个 IB 帐户，才能利用这些库进行真实货币交易。

**这是一个易于使用且灵活的 python 库，可用于与交互式经纪人进行交易。它是一个围绕 IB 的 API 的包装器，提供了一个非常简单易用的解决方案，同时隐藏了 IB 的复杂性。为了学习使用 IBridgePy 库，你可以看看这个 T2 的 youtube 视频或者这个 T4 的神奇博客**

### ******IBPy******

**IBPy 是另一个 python 库，可用于使用交互式代理进行交易。关于安装和使用 IBPy 的细节可以在这里找到[。](/ibpy-tutorial-implement-python-interactive-brokers-api/)如上所述，每个库都有自己的优势和劣势。根据策略的要求，您可以在权衡利弊后选择最合适的库。到目前为止，我们已经看了不同的库，现在我们来看 Python 交易平台。**

**![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")**

## **开源 Python 交易平台**

**Python 交易平台提供多种功能，如开发策略代码、[回溯测试](/backtesting/)和提供[市场数据](https://quantra.quantinsti.com/course/getting-market-data)，这就是为什么这些 [Python 交易](https://quantra.quantinsti.com/course/python-trading-basic)平台被量化和算法交易员广泛使用。下面列出了几个流行的免费 python 交易平台，Python 爱好者可以用来进行算法交易。**

### ******蓝移******

**Blueshift 是一个免费的综合性交易和策略开发平台，也支持回溯测试。它有助于人们更专注于策略开发而不是编码，并提供集成的高质量分钟级数据。其基于云的回溯测试引擎使人们能够在 Python 编程环境中开发、测试和分析交易策略。您可以从[这里](https://blueshift.quantinsti.com/)开始使用该平台开发战略。**

****Quantiacs 是一个免费的开源 Python 交易平台，可以用来开发和回测使用 Quantiacs 工具箱的交易想法。Quantiacs 为 49 只期货和标准普尔 500 指数股票提供长达 25 年的免费和干净的金融市场数据。你可以想开发多少策略就开发多少策略，盈利策略可以在 Quantiacs 算法交易竞赛中提交。在 Quantiacs，你可以拥有自己交易想法的知识产权。Quantiacs 投资每场比赛的 3 个最佳策略，如果你的交易策略被选中投资，你将获得一半的绩效费。****

****这些是一些最常用的 Python 库和交易平台。你可以在这里了解一些流行的 Python ide[。但是仍然有很多东西需要探索，包括更多的库和平台，其中大部分你可以通过这门关于量化策略的课程来学习，这门课程不仅包括用于交易的](https://www.dunebook.com/best-python-ide-windows-mac/)[Python](/python-trading/)的基础知识，还包括各种策略，并解释了如何用 Python 实现它们。****

****观看关于“Python 中的自动化交易”的[网络研讨会](/automated-trading-with-python-webinar/)，了解如何用 Python 创建和执行量化策略。****

****您也可以查看这个[教程，使用 IBPy 在 Interactive Brokers API](/ibpy-tutorial-implement-python-interactive-brokers-api/) 中实现 Python。在 IB TWS 上为 quants 和 Python 编码者自动交易。****

******更新******

******我们注意到一些用户在从雅虎和谷歌金融平台下载市场数据时面临挑战。如果您正在寻找市场数据的替代来源，您可以使用 [Quandl](https://www.quandl.com/) 来获得相同的数据。******

******免责声明:本文提供的所有数据和信息仅供参考。QuantInsti 对本文中任何信息的准确性、完整性、现时性、适用性或有效性不做任何陈述，也不对这些信息中的任何错误、遗漏或延迟或因其显示或使用而导致的任何损失、伤害或损害承担任何责任。所有信息均按原样提供。******

******推荐阅读******

****[Python 交易入门](/getting-started-python-trading)****

****[在 Python 中处理错误和异常](/dealing-python-error-exceptions)****

****[Python 异常:在 Python 中引发和捕获异常](/python-exception)****

****[时间序列分析:Python 简介](/time-series-analysis-introduction-python)****

****[使用 Python 对股票数据的基本操作](/basic-operations-stock-data-using-python)****
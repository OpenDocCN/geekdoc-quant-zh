# 机器学习在外汇市场中的应用——工作模型

> 原文：<https://blog.quantinsti.com/machine-learning-application-forex-markets-working-models/>

### 由[米林德·帕拉德卡](https://www.linkedin.com/in/milind-paradkar-b37292107/)

在上一篇文章中，我们简要介绍了机器学习(ML)的概念。在这篇文章中，我们将解释更多的 ML 术语，然后使用 r 中的 SVM 算法为一个[外汇策略](https://blog.quantinsti.com/fx-market-pairs-trading-strategy/)制定规则

利用[机器学习进行交易](https://quantra.quantinsti.com/course/introduction-to-machine-learning-for-trading)，我们从历史数据(股价/外汇数据)入手，加入指标，用 R/Python/Java 建立模型。然后，我们选择正确的机器学习算法来进行预测。
T3[T5](https://quantra.quantinsti.com/machine-learning-for-trading-ebook)

在了解如何在外汇市场使用机器学习之前，我们先来看一些与 ML 相关的术语。

**机器学习算法—**有许多 ML 算法([算法列表](https://en.wikipedia.org/wiki/List_of_machine_learning_concepts))被设计用于学习和预测数据。ML 算法既可以用来预测类别(解决分类问题)，也可以用来预测方向和大小([机器学习回归](https://quantra.quantinsti.com/course/trading-with-machine-learning-regression)问题)。

示例:

*   根据公司过去的季度业绩，预测 3 个月后股票的价格。
*   预测美联储是否会提高基准利率。

**指标/特征—**指标可以包括技术指标(均线、波段、MACD 等。)，基本面指标，或者/和宏观经济指标。

示例 1 -相对强弱指标(14)，价格-均线(50)和 CCI(30)。我们可以使用这三个指标，来建立我们的模型，然后使用适当的 ML 算法来预测未来值。

示例 2 -相对强弱指数(14)，相对强弱指数(5)，相对强弱指数(10)，价格-SMA(50)，价格-SMA(10)，CCI(30)，CCI(15)，CCI(5)

在本例中，我们选择了 8 个指标。其中一些指标可能与我们的模型无关。为了选择正确的指标子集，我们利用特征选择技术。

**特征选择–**这是选择相关特征子集用于模型的过程。特征选择技术分为三大类:过滤方法、基于包装的方法和嵌入方法。为了选择正确的子集，我们基本上在某种组合中使用 ML 算法。所选择的特征在机器学习中被称为预测器。

![Feature Selection](img/cfec7aa4c657f198af674ae1978d50f7.png)

**[支持向量机](https://blog.quantinsti.com/support-vector-machines-introduction/)(SVM)–**SVM 是一种著名的监督机器学习算法，用于解决分类和回归问题。

一个 [SVM 算法](https://quantra.quantinsti.com/course/trading-machine-learning-classification-svm)作用于给定的标记数据点，并通过边界或超平面将它们分开。SVM 试图最大化分离超平面周围的余量。支持向量是最接近决策面的数据点。

![Support vectors](img/b35ef68eb8948d103475f12c8ed83438.png)

**在 R 中使用 SVM 的[外汇策略的框架规则](https://quantra.quantinsti.com/course/Value-Strategy-Forex)-**鉴于我们对特征和 SVM 的理解，让我们从 R 中的代码开始。我们选择了 1 小时时间框架可追溯到 2010 年的欧元/美元货币对。这里使用的指示器是 [MACD (12，26，9)](http://forextraininggroup.com/trading-macd-simple-effective-strategies-explained/) 和[抛物线 SAR](https://blog.quantinsti.com/parabolic-sar/) ，默认设置为(0.02，0.2)。

首先，我们在 R 中加载必要的库，然后读取 EUR/USD 数据。然后，我们使用“TTR”包中提供的各自的函数来计算 MACD 和抛物线 SAR。为了计算趋势，我们从每个数据点的 SAR 值中减去收盘欧元/美元价格。我们滞后指标值，以避免前瞻偏差。我们还根据价格变化创建了一个 Up/down 类。

![Frame rules](img/f855e386a60958fdc70fc632175baef4.png)

此后，我们将指标和类合并到一个数据框架中，称为模型数据。然后将模型数据分为训练数据和测试数据。

![Merging the indicators amd creating training](img/cffce3cd5df636908be48760b1843875.png)

然后，我们使用“e1071”软件包中的 SVM 函数来训练数据。我们使用预测函数进行预测，并绘制模式。我们在这里获得了 53%的准确率。

![Use SVM to find pattern](img/ac6706396482b2f591a90d4e71388306.png)

从图中我们可以看到两个不同的区域，上方较大的红色区域是算法进行短期预测的地方，下方较小的蓝色区域是算法进行长期预测的地方。

![SVM Predictions](img/182d3c4f4ea4bfdcafd0ef13e9b7045f.png)

SAR 指标落后于价格，因为趋势随着时间的推移而延伸。当价格上涨时，SAR 低于价格，当价格下跌时，SAR 高于价格。当价格趋势反转并突破它的上方或下方时，SAR 停止并反转。我们对价格和 SAR 的交叉感兴趣，因此在代码中将趋势度量作为价格和 SAR 之间的差异。类似地，我们使用 MACD 直方图值，这是 MACD 线和信号线值之间的差异。

看着这个图，我们设计了两个规则，并在测试数据上测试它们。短线法则=(价格-SAR)>-0.0025 &(价格-SAR)< 0.0100 & MACD >-0.0010 & MACD< 0.0010 Long rule = (Price–SAR) >-0.0150 &(价格-SAR)< -0.0050 & MACD >-0.0005

![Define rules for trades](img/5d37083b307df9e1eb515fae54ee01de.png)

我们的短线交易准确率为 54%,长线交易准确率为 50%。SVM 算法在这里似乎做得很好。我们在这一点上停下来，在我们下一篇关于机器学习的文章中，我们将看到像上面设计的框架规则如何被编码和回溯测试，以检查交易策略的可行性。

### **下一步**

QuantInsti 开展的算法交易(EPAT)课程中的高管课程涵盖了机器学习。要了解更多关于 EPAT 的信息，请查看 [EPAT 课程页面](https://www.quantinsti.com/epat)或随时联系我们在[contact@quantinsti.com](mailto:contact@quantinsti.com)的团队，咨询关于 EPAT 的问题。

在本系列的下一篇文章中，我们将更进一步，演示如何回测我们的发现。因此，请坐下来享受'[机器学习及其在外汇市场的应用](https://blog.quantinsti.com/machine-learning-application-forex-markets-part-2/ "Permalink to Machine Learning and Its Application in Forex Markets – Part 2 [WORKING MODEL]")的第二部分。

*免责声明:股票市场的所有投资和交易都涉及风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。T3】*

### **可下载内容**
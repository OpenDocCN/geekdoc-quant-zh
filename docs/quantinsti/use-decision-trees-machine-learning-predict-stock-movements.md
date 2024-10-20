# 在机器学习中使用决策树来预测股票走势

> 原文：<https://blog.quantinsti.com/use-decision-trees-machine-learning-predict-stock-movements/>

由[苏珊·拉特纳帕尔基](https://twitter.com/ssushh_79?lang=en) & [米林德·帕拉德卡](https://in.linkedin.com/in/milind-paradkar-b37292107)

用于交易的机器学习是今天的新流行语，一些科技公司正在用它做一些不可思议的事情。今天，我们将向您展示如何借助“决策树”来预测股票走势(上涨或下跌)，决策树是最常用的 ML 算法之一。

[![Machine Learning in Trading](img/4bd0a863b70ada6b41c3b47e3dc176af.png)](https://quantra.quantinsti.com/machine-learning-for-trading-ebook)T8】

机器学习中的决策树用于建立[分类](https://quantra.quantinsti.com/course/trading-machine-learning-classification-svm)和[回归](https://quantra.quantinsti.com/course/trading-with-machine-learning-regression)模型，用于数据挖掘和交易。决策树算法在到达最终结果之前执行一组递归操作，当您在屏幕上绘制这些操作时，视觉效果看起来像一棵大树，因此得名“决策树”。

这里有一个机器学习中简单决策树的例子。 [![Use Decision Trees In Machine Learning To Predict Stock Movement_1](img/184cfae7599d238a2e79606907d5753d.png)](https://d1rwhvwstyk9gu.cloudfront.net/2017/10/Use-Decision-Trees-In-Machine-Learning-To-Predict-Stock-Movement_1.jpg)

基本上，[决策树](https://quantra.quantinsti.com/course/decision-trees-analysis-trading-ernest-chan)是帮助你做决定的流程图。机器学习使用相同的技术来做出更好的决策，让我们来看看如何实现。

### **可视化样本数据集和决策树结构**

现在让我们进入正题，我们想使用机器学习中的决策树来预测你的股票将走向何方。为此我们需要股票过去的数据。考虑一个样本股票数据集，如下表所示。数据集包括开盘价、盘高、盘低、收盘价和成交量指标(OHLCV)。你可以使用雅虎财经或谷歌财经下载任何股票的历史数据。

我们将用 R 编程语言做这个练习，你必须在你的 mac/pc 上安装支持软件。这里有一个 [链接](http://www.dummies.com/programming/r/how-to-install-r/) 帮你搞定。下面是将这些数据导入到的代码(包含代码的数据文件将在博客的结尾提供)- ![code to import data](img/038513d49ba9c2a2f1f90ddb369fd776.png)

这是数据的可视化表示。

![visual representation of the data.](img/b721e9d9959bd35c4620167506412a8d.png)

让我们给这个数据集添加一些技术指标(RSI，SMA，LMA，ADX)。在我们的例子中，技术指标是使用基本股票价值(OHLC)计算的，它们帮助我们预测股票走势。我们的机器学习算法将利用技术指标的值来做出更准确的[股价预测](https://blog.quantinsti.com/machine-learning-trading-predict-stock-prices-regression/)。我们滞后于技术指标值，以避免前瞻偏差。

我们还添加了“Class”列，它表示基于股票收盘价的每日收益。在“类别”栏中，“向上”表示正回报，而“向下”表示负回报。这是相同的代码

![code to add Class column](img/db637cb0e258e086963ec8283711b059.png)

![code to add Class column](img/ad7df83f8145e82da826595b007f0f47.png)

现在有趣的部分来了，我们想用这些技术指标来预测每日的变化(涨/跌)。我们将通过在这个数据集上应用机器学习决策树算法来做到这一点。首先，我们必须将数据集分成两部分；训练数据集和测试数据集。该算法使用训练数据来了解股票的走势，并做出某些假设，这也称为“信息增益”。训练完成后，我们将其应用于测试数据集，以进行[股票价格预测](https://blog.quantinsti.com/machine-learning-trading-predict-stock-prices-regression/)。这种类型的机器学习被称为监督学习。下面是应用这些步骤的代码

![supervised learning](img/f45c570f25985c3b853de5b4b314c456.png)

训练数据集的结果输出可以以树形结构的形式查看，如下所示。

![output from the training dataset ](img/ec3b84917d1c336cac62b83e917a0f1d.png)

**决策树示例图**

在了解机器学习的决策树算法是如何工作的之前，我们先来了解一下树的结构。

### **决策树的组成部分**

决策树结构由根节点、测试节点和决策节点(叶子)组成。根节点是决策树中的主节点。在上面的决策树中，我们从 RSI>50 开始，因此 RSI 指标被用作根节点。你可能会问为什么 RSI 指标的值在 50，为什么不说 34？这就是训练发挥作用的地方，机器学习决策树算法能够理解 50 的 RSI 比任何其他值都有助于做出更准确的决策。

在根节点之后，每个测试节点根据一些设定的标准将数据分割成更多的部分。在上面的决策树中，我们有 SMA> 80，LMA>55，ADX>25(这些值也是训练的结果)。基于这些充当测试节点的指示器，数据被进一步分割。

最后一个节点是叶节点。在决策树图中，包含 Up/Down 类以及指示目标属性概率的概率值的节点是叶节点。任何节点的左侧都被认为是“是”，意味着在该节点询问的问题(例如 RSI >50，如果回答是，则算法导航到树的左侧，如果不是，则导航到右侧)

因此，根据设定的标准，通过从决策树的根节点向下导航到叶子，整个数据集得到分类。

![Components of a Decision Tree](img/90bcb27d453f90c5db74e5f14b23d8ee.png)

**决策树的组成部分**

例如，这支股票在某一天的 RSI 为 39，所以到树的右边检查 SMA 是否大于 80，如果是，那么到叶子上，它说，“这只股票有 0.52 的下跌概率”。

### 决策树算法是如何工作的？

现在我们已经理解了决策树的结构，让我们来理解决策树是如何构造的。

##### **决策树诱导器**

决策树由决策树诱导器(也称为分类器)构成。有各种决策树诱导器，如 ID3、C4.5、CART、CHAID、QUEST、CRUISE 等。等等。(你可以找到关于这些诱导器的更多信息[这里](https://www.quora.com/What-are-the-differences-between-ID3-C4-5-and-CART)和[这里](http://saiconference.com/Downloads/SpecialIssueNo10/Paper_3-A_comparative_study_of_decision_tree_ID3_and_C4.5.pdf))决策树诱导器基本上是一种算法，它从给定的(训练)数据集自动构建决策树。典型地，决策树诱导器的目标是基于指定的目标函数构建最优决策树。目标函数的一个例子可以是最小化决策树的节点数量，以便降低复杂性。另一个例子可以是最小化泛化误差(或者获得更精确的结果)。

虽然我们说了诱导器自动构造决策树，但实际上决策树诱导器遵循一定的方法。决策树归纳器通常使用两种流行的方法。其中包括广泛使用的自顶向下方法和不太流行的自底向上方法。

##### **自上而下方法解释**

在自顶向下的方法中，诱导器以自顶向下、递归的方式创建决策树。让我们使用之前创建的技术指标来理解这种自上而下的递归方法。

我们创建的技术指标是 RSI、SMA、LMA 和 ADX 指标。我们的决策树算法将这些指标视为属性。

从这些指标(属性)中，诱导者会使用哪个指标(属性)作为根节点开始？剩下的属性将如何拆分？

所有这些都由使用离散分裂函数的诱导器决定。离散分裂函数使用某些标准(例如，信息增益、基尼指数)来确定开始时的最佳属性，并分裂训练数据集。这里有一些链接可以了解更多关于[信息增益](http://www.saedsayad.com/decision_tree.htm)、[基尼指数](http://dni-institute.in/blogs/cart-decision-tree-gini-index-explained/)的信息。

在每次迭代中，诱导算法使用输入属性的离散函数的结果来划分训练数据集。在选择了适当的分裂之后，每个节点进一步将训练集细分成更小的子集，直到不可能进一步分裂或者当满足停止标准时。在完成树的创建之后，使用特定的修剪规则对其进行修剪，以减少分类错误。

这就是决策树是如何构建的，它可以用于在机器学习中进行[股票价格预测](https://blog.quantinsti.com/machine-learning-trading-predict-stock-prices-regression/)。在我们未来的帖子中，我们将演示如何用 python 构建决策树，还将探索一些基于决策树的机器学习模型。

### **下一步**

报名参加我们在 Quantra 上的最新课程“交易中的决策树”。本课程由 Ernest P. Chan 博士撰写，揭示了分类树中的黑盒，帮助您创建交易策略，并教会您理解模型的局限性。本课程由 7 个部分组成，从基础到高级。

阅读我们的下一篇文章“Python 中的机器学习分类策略”，这是一个使用支持向量分类器(SVC)在 S & P 500 上逐步实现机器学习分类算法的指南。分类算法基于训练数据建立模型，然后将测试数据分类到其中一个类别中。

**更新**

我们注意到一些用户在从雅虎和谷歌金融平台下载市场数据时面临挑战。如果你正在寻找市场数据的替代来源，你可以使用 [Quandl](https://www.quandl.com/) 来获得同样的信息。

### **下载数据文件**

*   决策树 R 代码第一部分。稀有
*   决策树 R 代码第二部分。稀有
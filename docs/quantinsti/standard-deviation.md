# 标准差及其在交易中的应用

> 原文：<https://blog.quantinsti.com/standard-deviation/>

由阿苏托什·戴夫和[乌迪莎·阿洛克](https://www.linkedin.com/in/udisha-alok/)

测量金融数据集中的离差是量化金融中最重要的任务之一。无论是交易策略中的信号生成还是风险管理，标准差都是金融市场中最常用的波动性度量。在这篇博客中，我们揭示了这一指标，并讨论了它在 Python 中处理真实金融数据的各种用例。

我们将讨论以下内容:

*   [标准差的定义](#definition-of-standard-deviation)
*   [什么是标准差？](#what-is-standard-deviation)
*   [标准差公式](#standard-deviation-formula)
*   [现实生活中标准偏差的例子](#examples-of-standard-deviation-from-real-life)
*   [为什么要用标准差？](#why-use-standard-deviation)
    *   [标准差单位](#unit-of-standard-deviation)
    *   [标准差与方差](#standard-deviation-vs-variance)
    *   [样本数据的标准偏差](#standard-deviation-for-sample-data)
    *   [样本数据的标准偏差-贝塞尔校正](#standard-deviation-for-sample-data-bessels-correction)
*   [金融和交易中的标准差](#standard-deviation-in-finance-and-trading)
    *   [作为波动性衡量标准的标准差](#standard-deviation-as-a-measure-of-volatility)
    *   [用 Python 计算股票的年波动率](#computing-annualized-volatility-of-stocks-using-python)
        *   [z 值](#the-z-score)
        *   [风险价值](#value-at-risk-var)
        *   [置信区间](#confidence-intervals)

* * *

## 标准差的定义

在统计学中，

> ****【σ】****标准差是用于量化数据相对于其均值的变化量或离差的度量。

换句话说，标准差给了我们关于数据平均值的平均偏差大小的信息。因此，如果数据集中的值靠得很近，标准偏差就会很小。

另一方面，如果数值分散，标准偏差会更大。

* * *

## 什么是标准差？

让我们回到最基本的问题。
*偏离均值是什么意思？*

Simply put, the deviation is the distance of a data point from the mean. Consider a random variable X which consists of n different observations \(x_1, x_2, ..., x_n\) Below, we show the deviations of two observations \(x_1\) and \(x_2\) from the mean of X.

![deviations](img/b011438ad426968eebe7d367f246cbc2.png)

Deviations of two observations



这里的偏差告诉我们一个观察值离平均值有多远。它可以是正的，也可以是负的，取决于观察值是大于还是小于平均值。

What if we measure the total deviation by summing all such values i.e., \(x_{1}-\overline{x}, x_{2}-\overline{x}, ..., x_{n}-\overline{x}?\)

我们最终会得到零，因为正值和负值会相互抵消！如果我们取绝对值并求和呢？我们可以。或者我们可以求差的平方，然后把它们加起来。后者是优选的，因为它具有吸引人的数学特性。

所以，重复一遍，我们对差值求平方，去掉正负符号，然后计算它们的平均值。这个结果量被称为**方差**，它捕获了数据中的离差。

标准差是方差的标准化版本，通过取方差的正平方根获得，因此得名**标准差**。在下一节中，我们将讨论计算标准差的公式。

* * *

## 标准差公式

计算标准偏差(用 **σ** 表示)的公式如下:

\(\西格玛= \sqrt\frac{{\sum_{i=1}^{n}(x_{i}-\mu)^2}}{n}\)

在哪里，

\(x_i\) = value of the \(i^{th}\) point in the data set
\(\mu\) = mean of the data points, calculated as \(\frac{1}{N}\sum_{i=1}^{N}x_i\)
N = total number of data points

* * *

## 现实生活中标准偏差的例子

标准差这个术语听起来像是你在统计学课上听到的，但是不要把它当成一个过于专业的术语。它可以用在我们生活的不同方面。

教师可以使用考试中学生分数的标准差作为衡量标准来评估学生对该科目的整体理解水平。如果平均值和标准差都很高，则表明平均而言，学生对主题有很好的理解。

然而，会有许多学生的分数远高于平均分数，也远低于平均分数。如果平均值较高而标准差较低，则表明平均分数与前一种情况相似。

低标准差告诉她，大多数学生的分数接近(即略高于和略低于)平均值。在天气预报中，它可以用来比较两个或更多地区的天气模式。

如果我们比较杰萨尔默(极端天气)和孟买(温和天气)的温度标准偏差，我们会发现前者在平均温度附近有更多的可变性。

* * *

## 为什么要用标准差？

### 标准偏差单位

标准差的单位将与我们数据的单位相同。与方差相比，这更容易解释。在下一节中，我们将对这两种离差度量进行详细比较。

### 标准差与方差

The variance \((σ^2)\) of a random variable X is given by the formula below:

\(方差= \frac{\sum_{i=1}^{n}(x_i-\mu)^2}{n}\)

正如我们所看到的，根据它的结构，方差是原始单位的平方。这意味着，如果我们用公里来表示距离，那么方差的单位就是平方公里。

Now, square kilometres may be easy to visualize as a unit, but what about \(year^2\) or \(IQ^2\), if we are working with ages or IQs of a group? They are harder to interpret.

因此，使用可以与相同规模/单位的数据进行比较的测量是有意义的，例如标准差。

标准差计算为方差的平方根。它与我们的数据具有相同的单位，这使得它易于使用和解释。

例如，考虑这样一个场景，我们正在查看一个街区居民的身高数据集。假设身高呈正态分布，平均值为 165 厘米，标准偏差为 5 厘米。

我们知道对于正态分布，

*   68%的数据点落在一个标准偏差内，
*   两个标准偏差内的 95%,以及
*   99.7%落在平均值的三个标准偏差内。

![Standard Normal Distribution](img/fb52170942db15401b1a5f84dc036b26.png)

Standard Normal Distribution (Image Source: [Standard Normal Distribution](https://quantra.quantinsti.com/glossary/Standard-Normal-Distribution#!))



因此，我们可以得出结论，几乎 68%的居民的身高将位于平均值的一个标准偏差之间，即在 160 cm(平均值-标准差)和 170 cm(平均值+标准差)之间。你可以在这里阅读更多关于正态分布[。](https://quantra.quantinsti.com/glossary/Standard-Normal-Distribution)

### 样本数据的标准偏差-贝塞尔校正

当计算总体的标准差时，我们使用上面讨论的公式。然而，我们在处理样本时会稍微修改一下。

这是因为与总体相比，样本要小得多。为了说明随机选择的样本和整个总体中的差异，我们通过在等式 1 的分母中使用“ **( *n-1* )** ”而不是“ ***n*** ”来“无偏”计算。这被称为贝塞尔校正。

因此，我们使用下面的公式来计算样本的**标准差**。

\(s = \sqrt\frac{{\sum_{i=1}^{n}(x_{i}-\overline{x})^2}}{n-1}\)

在哪里，

\(x_i\) = value of the \(i^{th}\) point in the sample
\(\overline{x}\) = sample mean
n = total number of data points in the sample

请注意，随着样本量 ***n*** 变大，除以“ **( *n-1* )** ”或“ ***n*** ”的影响会变小。

* * *

## 金融和交易中的标准差

### 标准差作为波动性的度量

在交易和金融中，量化资产的波动性很重要。与收益或价格不同，资产的波动性是一个不可观察的变量。

标准差在风险管理和绩效分析中具有特殊的意义，因为它通常被用作证券波动性的代表。例如，与小盘股相比，成熟的蓝筹股证券的回报率标准差较低。

另一方面，像[加密货币](https://quantra.quantinsti.com/course/crypto-trading-strategies-intermediate)这样的资产具有更高的标准差，因为它们的回报与其均值相差很大。

在下一节中，我们将学习用 Python 计算股票的年波动率。

### 使用 Python 计算股票的年波动率

现在让我们计算并比较两只印度股票的年波动率，即 ITC 和 Reliance。我们首先使用 **yfinance 库**获取最近 5 年的收盘价格数据:
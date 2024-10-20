# 中心极限定理介绍:例子，计算，Python 中的统计

> 原文：<https://blog.quantinsti.com/central-limit-theorem/>

由阿舒托什·戴夫

中心极限定理(CLT)经常被认为是最重要的定理之一，不仅在统计学中，而且在整个科学中。在这篇博客中，我们将尝试通过 Python 中的模拟来理解中心极限定理的本质。

**内容**

*   [样本和采样分布](#samples-and-the-sampling-distribution)
*   [什么是中心极限定理？](#what-is-the-central-limit-theorem)
*   [中心极限定理-陈述&假设](#central-limit-theorem-statement-assumptions)
*   [使用 Python 模拟演示 CLT 的实际操作，并举例说明](#demonstration-of-clt-in-action-using-simulations-in-python-with-examples)
*   [例 1 -指数分布人口](#example-1-exponentially-distributed-population)
*   [示例 2 -二项分布人口](#example-2-binomially-distributed-population)
*   [CLT 在投资/交易中的应用](#an-application-of-clt-in-investing-trading)
*   [投资者面临的挑战](#the-challenge-for-investors)
*   [金融正态性的伟大假设](#the-great-assumption-of-normality-in-finance)
*   [夏皮罗-维尔克测试](#the-shapiro-wilk-test)
*   [中心极限定理的作用](#the-role-of-central-limit-theorem)
*   [检验周收益和月收益的正态性](#testing-normality-of-weekly-and-monthly-returns)
*   [置信区间](#confidence-intervals)

* * *

## 样本和样本分布

在我们讨论定理本身之前，首先必须理解构建模块和上下文。推断统计学的主要目标是对给定的总体进行推断，仅使用其子集，称为样本。

We do so because generally, the parameters which define the distribution of the population, such as the population mean \(\mu\) and the population variance \(\sigma^{2}\), are not known.

在这种情况下，样本通常是以随机方式收集的，从样本中收集的信息随后被用于推导出整个总体的估计值。

对于进行分析的组织/公司/研究人员来说，上述方法既省时又省钱。为了以任何有意义的方式将从样本得出的推论推广到总体，样本很好地代表总体是很重要的。

挑战在于，作为一个子集，样本估计只是估计，因此容易出错！也就是说，它们可能没有准确反映人口。

For example, if we are trying to estimate the population mean \((\mu)\) using a sample mean \((\bar x)\), then depending on which observations land in the sample, we might get different estimates of the population with varying levels of errors.

* * *

## 什么是中心极限定理？

这里的核心点是样本均值本身是一个随机变量，依赖于样本观测值。

Like any other random variable in statistics, the sample mean \((\bar x)\) also has a probability distribution, which shows the probability densities for different values of the sample mean.

这种分布通常被称为“抽样分布”。下图直观地总结了这一点:

![sampling distribution](img/82370a731763cc8b714491fe5b97b613.png)

中心极限定理本质上是关于在某些特定条件下样本均值的抽样分布性质的陈述，我们将在下一节讨论这一点。

* * *

## 中心极限定理-陈述和假设

Suppose \(X\) is a random variable(not necessarily normal) representing the population data. And, the distribution of \(X\), has a mean of \(\mu\) and standard deviation \(\sigma\). Suppose we are taking repeated samples of size 'n' from the above population.

然后，中心极限定理指出，给定足够高的样本量，以下性质成立:

*   抽样分布的均值=总体均值\((\mu)\)，以及
*   抽样分布的标准偏差(标准误差)= \(\sigma/√n\)，因此
*   对于 n ≥ 30，在实际应用中，抽样分布趋于正态分布。

换句话说，对于大 N，$ $ \ bar { x } \ long right arrow \ mathbb { N } \ left(\ mu，\ frac { \ sigma } { \ sqrt { N } } \ right)$ $

在下一节中，我们将借助 Python 中的模拟来尝试理解 CLT 的工作原理。

* * *

## 使用 Python 中的模拟和示例演示 CLT 的实际应用

本节要论证的要点是，对于服从任何分布的总体，对于足够大的样本量，抽样分布(样本均值分布)将趋于正态分布。

我们将考虑两个例子，并检验 CLT 是否成立。

*   示例 1 -指数分布的人口
*   示例 2 -二项式分布的人口

* * *

## 示例 1 -指数分布的人口

假设我们正在处理一个呈指数分布的人口。指数分布是一种连续分布，通常用于模拟事件发生前需要等待的预期时间。

The main parameter of exponential distribution is the 'rate' parameter \(\lambda\), such that both the mean and the standard deviation of the distribution are given by \((1/\lambda)\).

以下代表我们指数分布的人口:

![exponentially distributed population](img/a4beeb7b35b42b30b282fe2c0d8c4492.png)

f(x)= \(\ cases { \λe^{-\lambda x } & if x > 0 \ cr0 & \ text { otherwise } } \)

e(x)= \(1/\λ\)= \(\ mu \)v(x)= \(1/\lambda^2\)= \(\sigma^2\)，意思是 SD(x)= \(1/\λ\)= \(\ sigma \)

我们可以看到我们人口的分布远非正常！在下面的代码中，假设\(\lambda\)=0.25，我们计算总体的平均值和标准差:
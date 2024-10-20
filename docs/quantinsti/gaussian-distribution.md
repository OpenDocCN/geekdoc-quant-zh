# 高斯分布:它是什么，如何计算，等等

> 原文：<https://blog.quantinsti.com/gaussian-distribution/>

马里奥·比萨

在这个博客中，我们了解了高斯分布的一切。我们将揭示数据集中最常见的分布之一的一些细节，深入研究计算高斯分布的公式，将其与正态分布进行比较，等等。

我们将涵盖:

*   [什么是高斯分布？](#what-is-gaussian-distribution)
*   [为什么叫高斯分布？](#why-is-it-called-a-gaussian-distribution)
*   [高斯分布和正态分布的差异](#difference-between-gaussian-distribution-and-normal-distribution)
*   [高斯分布是如何计算的？](#how-is-gaussian-distribution-calculated)
*   [使用 Python 计算高斯分布](#calculating-gaussian-distribution-using-python)
*   [金融中的高斯分布](#gaussian-distribution-in-finance)
*   [现代经济学和高斯分布](#modern-economics-and-gaussian-distribution)
    *   [什么是有效市场假说？](#what-is-the-efficient-market-hypothesis)
    *   [什么是布莱克-斯科尔斯-默顿模型？](#what-is-the-black-scholes-merton-model)
    *   什么是有效前沿投资组合理论？
*   [高斯分布的例子](#example-of-gaussian-distribution)

* * *

## 什么是高斯分布？

当我们在统计学中处理数据时，最基本的分析之一是检查数据分布。

根据数据的性质，我们可以找到不同的分布。例如二项式分布、泊松分布、柯西-洛伦兹分布等。

高斯分布被广泛用于描述价格行为，在本文中，我们将试图更好地理解这种分布及其对金融界和风险控制的影响。

* * *

## 为什么叫高斯分布？

*高斯分布*这个名字来源于数学家卡尔·弗里德里希·高斯(Carl Friedrich Gauss)在研究误差的随机性时认识到了曲线的形状。

或者为了纪念它的发现者，有时它被命名为拉普拉斯-高斯分布，因为高斯的研究是以拉普拉斯的研究为基础的。

* * *

## **高斯分布和正态分布的差异**

高斯分布如此普遍，以至于经常被称为正态分布。

在高斯分布中，大多数数据都集中在具有一定离差或方差的测量值周围。具体来说，高斯分布是对称的，并且具有恒定的均值和方差。

因此，当我们已经有一组服从高斯分布的已知值时，这允许我们对未知值进行预测。如果均值为零，方差为一，我们称之为**标准正态分布**。

高斯分布，正态分布，钟形曲线，高斯钟形...所有这些术语指的是同一个东西。正态或高斯分布在自然界中被反复发现，如人/动物的身高或体重、赛跑速度、智商等。

高斯分布是自然界中最常见的数据分布之一，因此，它被称为正态或标准分布。或者因为图形的形状，它也经常被称为高斯钟。

* * *

## 高斯分布是如何计算的？

高斯函数数学形式如下:

\(\ operator name { f }(x)= a* \ exp(-\ frac {(x-b)^{2}} {2c^{2}})\)

对于任意实常数\(a\)，\(b\)和*非零* \(c\)。

高斯函数在统计学中被广泛用于描述正态分布，因此经常被用来表示具有期望值和方差\(\sigma^2 = c^2\).的正态分布随机变量的概率密度函数

在这种情况下，高斯函数的形式为:

\(\ operator name { g }(x)= \ frac { 1 } { \ sigma \ sqrt { 2 \ pi } } \ exp(-\ frac { 1 } { 2 } \ frac {(x-\mu)^{2}} {\sigma^{2}})\)

* * *

## 使用 Python 计算高斯分布

让我们看看如何用 Python 计算高斯分布:
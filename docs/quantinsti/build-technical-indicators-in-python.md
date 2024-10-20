# 用 Python 构建技术指标

> 原文：<https://blog.quantinsti.com/build-technical-indicators-in-python/>

通过[chaineka Thakar](https://www.linkedin.com/in/chainika-bahl-thakar-b32971155/)和[丹麦 Khajuria](mailto:danish.k@quantinsti.com)

技术指标本质上是基于数据集的数学表示，如价格(高、低、开、闭等)。)或证券交易量来预测价格趋势。

有几种技术指标可以用来分析和检测价格的运动方向。比如[动量交易](https://quantra.quantinsti.com/course/momentum-trading-strategies)、[均值回复策略](https://quantra.quantinsti.com/course/python-mean-reversion-strategies-ernest-chan)等。交易者在交易时通常使用指标来预测未来的价格水平。

让我们通过这篇博客了解如何使用 Python 构建技术指标，这篇博客涵盖了:

*   [什么是技术指标？](#what-are-technical-indicators)
*   [为什么要用 Python 技术指标？](#why-use-python-technical-indicators)
*   [交易技术指标](#technical-indicators-for-trading)
    *   [移动平均线](#moving-average)
        *   [移动平均线的 Python 代码](#python-code-for-moving-average)
    *   [布林线](#bollinger-bands)
        *   [布林线的计算](#calculation-for-bollinger-bands)
        *   [布林线的 Python 代码](#python-code-for-bollinger-bands)
    *   [相对强度指数](#relative-strength-index)
        *   [RSI 的计算](#calculation-for-rsi)
        *   [用于 RSI 的 Python 代码](#python-code-for-rsi)
    *   [资金流动指数](#money-flow-index)
        *   [用于 MFI 的 Python 代码](#python-code-for-mfi)
    *   [平均真实范围](#average-true-range)
        *   [用于 ATR 的 Python 代码](#python-code-for-atr)
    *   [力指数](#force-index)
        *   [力指数的计算](#calculation-for-force-index)
        *   [力指数的 Python 代码](#python-code-for-force-index)
    *   [移动方便](#ease-of-movement)
        *   [EVM 的计算](#calculation-for-evm)
        *   [EVM 的 Python 代码](#python-code-for-evm)

* * *

### 什么是技术指标？

技术指标并不遵循一个通用的模式，也就是说，它们在每一种证券上都有不同的表现。对某一种证券来说可能是个好指标的东西，对另一种证券来说可能就不一定了。因此，使用一个[技术指标](/technical-indicators-trading/#:~:text=Step%202%20%2D%20Calculate%20technical%20indicators)需要法学和良好的经验。

因为这些分析可以在 [Python](/python-trading/) 中完成，所以还插入了一段代码以及指示器的描述。为清晰起见，还附上了示例图表。我们之前也报道过最受欢迎的交易博客，你可以看看[Python 上最受欢迎的交易博客](/python-trading-top-blogs/)。

* * *

### 为什么要用 Python 技术指标？

技术指标是一套应用于交易图表的工具，帮助交易者更清楚地进行市场分析。

例如，技术指标确认市场是否在跟随趋势，或者市场是否处于区间波动状态。

此外，指标可以提供具体的市场信息，如资产在一个范围内何时超买或超卖，以及何时反转。

我们将使用 python 对这些技术指标进行编码。Python 用于计算技术指标，是因为其简单的语法和易用性使其极具吸引力。

Python 也有许多现成的数据操作库，如 [Pandas](/python-pandas-tutorial/) 和 [Numpy](/python-numpy-tutorial-installation-arrays-random-sampling/) 以及数据可视化库，如 [Matplotlib](/python-matplotlib-tutorial/) 和 [Plotly](/plotly-python/) 。

* * *

### 交易的技术指标

现在，让我们看看用于交易的 Python 技术指标。有很多指标可以使用，但我们列出了交易领域最常用的指标。此外，用 Python 显示了指示器的用法，以方便用户。

下面是 Python 技术指标的列表，如下所示:

*   [移动平均线](#moving-average)
*   [布林线](#bollinger-bands)
*   [相对强度指数](#relative-strength-index)
*   [资金流动指数](#money-flow-index)
*   [平均真实范围](#average-true-range)
*   [力指数](#force-index)
*   [移动方便](#ease-of-movement)

### 移动平均数

移动平均，也称为滚动平均，是指定数据字段在给定的一组连续周期内的平均值。当有新数据可用时，通过删除最早的值并添加最新的值来计算数据的平均值。

因此，本质上，平均值是随着数据滚动的，因此被称为“移动平均线”。

此外，移动平均线是一个技术指标，通常与时间序列数据一起使用，以平滑短期波动并减少数据的临时变化。

有三种流行的移动平均线可以用来分析市场数据:

*   [简单移动平均线](https://quantra.quantinsti.com/glossary/Simple-Moving-Average)，
*   [指数移动平均线](https://quantra.quantinsti.com/glossary/Exponential-Moving-Average)，以及
*   [加权移动平均](https://quantra.quantinsti.com/glossary/Weighted-Moving-Average)。

**移动平均线的 Python 代码**

让我们用 Python 代码来看看移动平均线指标的工作原理:
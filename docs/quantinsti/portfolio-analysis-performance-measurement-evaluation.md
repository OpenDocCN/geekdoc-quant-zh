# 投资组合分析——绩效测量和评估

> 原文：<https://blog.quantinsti.com/portfolio-analysis-performance-measurement-evaluation/>

由[维布·辛格](https://www.linkedin.com/in/vibhu-singh-1b76b6105/)和[曼迪普·考尔](https://www.linkedin.com/in/mandeep-kaur-6b5313104/)

在这个博客中，我们将讨论投资组合评估和投资组合度量的各个方面。我们将开始讨论为什么评估和测量是必要的，然后将继续讨论如何计算和分析特定时间段后投资组合产生的回报。

在[前一篇博客](/portfolio-optimization-maximum-return-risk-ratio-python/)和这篇博客中投资组合回报的计算的一个关键区别是，在这里，我们将看到如何计算产生后的回报。在前一个案例中，我们是根据成份股的预期收益来计算投资组合的预期收益的。

本文涵盖:

*   [为什么需要绩效测量和评估？](#why-performance-measurement-and-evaluation-is-required)
*   [投资组合收益的计算](#calculation-of-portfolio-returns)
*   [时间加权收益率(TWRR)](#time-weighted-rate-of-return-twrr)
*   [货币加权收益率(MWRR)](#money-weighted-rate-of-return-mwrr)
*   [在 Python 中计算 TWRR](#computing-twrr-in-python)
*   [用 Python 计算 MWRR](#computing-mwrr-in-python)
*   [投资组合回报构成](#portfolio-return-components)
*   [业绩归因](#performance-attribution)
*   [总结](#summary)

* * *

## 为什么需要绩效测量和评估？

对于投资者和投资组合经理来说，绩效评估都是必要的。然而，对于这两组人来说，评估的需要可能是不同的。

绩效评估还显示了投资计划的有效性和改进方面。

评估投资组合表现的一些**好处**包括

1.  投资在一段时间内的回报表现(表现衡量)
2.  如何获得观察到的绩效(绩效归因)
3.  如果绩效是由于投资决策(绩效评估)

* * *

## 投资组合回报的计算

我们假设:
评估的时间段是 t，
时间段开始时的市值是 MV <sub>0</sub> ，这个时间段结束时的
是 MV <sub>t</sub> 。

此外，在时间段 t 的开始和结束时的现金流入是 CF <sub>0</sub> 和 CF <sub>t</sub> 。

该期间投资组合的回报可计算如下:

![Calculation of portfolio returns](img/2b2b16996222f40330e7b5ce1e8350fe.png)

考虑下面的例子。

2017 年 1 月 1 日，投资组合的价值为 100，000 美元，另有 50，000 美元被纳入投资组合。没有中间现金流，2017 年 12 月 31 日，又引入了 25，000 美元。

截至 2017 年 12 月 31 日营业结束时，投资组合价值为 200，000 美元。这里的时间周期是 1 年。

投资组合的回报可以用 python 计算，如图所示。
# 去趋势价格振荡器（DPO）[图表学校]

### 目录

+   [去趋势价格振荡器（DPO）](#detrended_price_oscillator_dpo)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [位移移动平均线](#displaced_moving_average)

    +   [DPO衡量什么？](#what_does_dpo_measure)

    +   [使用DPO](#using_dpo)

    +   [位移还是不位移](#to_shift_or_not_to_shift)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [建议的扫描](#suggested_scans)

    +   [进一步研究](#further_study)

## 介绍

去趋势价格振荡器（DPO）是一种设计用于去除价格趋势并更容易识别周期的指标。DPO不延伸到最后一个日期，因为它是基于一个位移的移动平均线。然而，与最近的对齐并不是问题，因为DPO不是动量振荡器。相反，DPO用于识别周期的高点/低点并估计周期长度。

## 计算

```py
Price {X/2 + 1} periods ago less the X-period simple moving average.

X refers to the number of periods used to calculate the Detrended Price 
Oscillator. A 20-day DPO would use a 20-day SMA that is displaced by 11 
periods {20/2 + 1 = 11}. This displacement shifts the 20-day SMA 11 days to the left, which actually puts it in the middle of the look-back 
period. The value of the 20-day SMA is then subtracted from the price
in the middle of this look-back period. In short, DPO(20) equals price
11 days ago less the 20-day SMA.  

```

## 位移移动平均线

移动平均线的位移实际上使移动平均线居中。考虑一个20日简单[移动平均线](/school/doku.php?id=chart_school:technical_indicators:moving_averages "chart_school:technical_indicators:moving_averages")向左偏移11天。在移动平均线前面有10天，在移动平均线上有1天，在移动平均线后面有9天。实际上，这个移动平均线处于其回顾期的中间。计算中使用的价格大约一半在右侧，一半在左侧。图表 1显示了标普500 ETF（SPY）的20日SMA（绿色虚线）和向左偏移11天的20日SMA（粉色线）。结束值相同（106.84），但粉色移动平均线结束于10月27日，绿色移动平均线结束于11月11日，这是图表上的最后日期。另外，请注意“居中”的移动平均线（粉色线）更接近实际价格走势。

![图表 1](../Images/8419e6c154fd8618f4c8a5b69608bd6f.jpg "图表 1")

## DPO衡量什么？

去趋势价格振荡器（DPO）衡量过去价格和移动平均线之间的差异。请记住，DPO本身是向左位移的。随着价格在移动平均线上下移动，指标在零线上下振荡。图表 2显示了标普500 ETF（SPY），其中包含一个向左位移 -11 天的20日移动平均线。指标窗口中显示了20日DPO。请注意，当价格高于移动平均线时，DPO为正，当价格低于移动平均线时，DPO为负。

![图表 2](../Images/ddda0101523677d0228d0be781a5ac45.jpg "图表 2")

## 使用DPO

尽管这个指标看起来像是一个经典的振荡器，但它并不是为动量信号而设计的。位移移动平均线设置在过去，这就是为什么 DPO 显示在过去的原因。即使有了这种位移，DPO 的峰值和谷值也可以用来估计周期长度。DPO 滤除了较长的趋势，专注于较短的周期。图 3 显示了纳斯达克 100 ETF（QQQQ）的 DPO（20）在指标窗口中。通过观察峰值和谷值，我们可以看到一个 20 天的周期，低点分别在九月初、十月初、十一月初和十二月初。这些低点之间大约相隔 20 天。一月初的周期被错过了。

![图表 3](../Images/92fec60995e6bccf644e015e6c93204b.jpg "图表 3")

## 是否位移

可以将去趋势价格振荡器（DPO）向右水平位移。如果 DPO 设置为 20，则需要 11 个周期的位移才能使其与最近的价格对齐。这个位移数字来自顶部的公式（20/2 + 1）= 11。虽然位移可能看起来是个好主意，但实际上它确实违背了这个指标的目的，即识别周期。

![图表 4](../Images/5f769e9237eac25d48823cf47a1a7141.jpg "图表 4")

即使有正位移，DPO 波动也与价格不太匹配。在下面的示例中，DPO（20,11）的最后一个值仍然基于 11 天前的收盘价和移动平均值。请注意，当价格在 11 天前移动到中心移动平均线以下时（橙色框），DPO 变为负值。DPO 简单地不能匹配当前的价格走势。与 DPO 不同，价格在过去 12 天一直低于 20 天 EMA。百分比价格振荡器（PPO）更适合识别超买和超卖水平。PPO(1,20,1)显示了当前价格与正常的 20 天指数移动平均线之间的百分比差异。当价格相对远离它们的 20 天 EMA 时，就会出现超买/超卖情况。

![图表 5](../Images/e8e908501dd600de3df7a9b5d6726160.jpg "图表 5")

## 结论

去趋势价格振荡器显示了过去价格与简单移动平均线之间的差异。与其他价格振荡器相比，DPO 不是一个动量指标。相反，它只是设计用来通过其峰值和谷值识别周期。可以通过计算峰值或谷值之间的周期数来估计周期。用户可以尝试不同的较短和较长的 DPO 设置来找到最合适的。

## 使用 SharpCharts

去趋势价格振荡器（DPO）可以在SharpCharts的指标列表中找到。默认参数为20个周期，但可以根据需要进行调整以找到周期。用户还可以添加另一个逗号分隔的参数。逗号加上一个正数会将指标向右移动。 DPO可以放置在价格图表的上方、下方或后面。[点击这里](http://stockcharts.com/h-sc/ui?s=SPY&p=D&b=5&g=0&id=p14005429311&listNum=30&a=191188211 "http://stockcharts.com/h-sc/ui?s=SPY&p=D&b=5&g=0&id=p14005429311&listNum=30&a=191188211") 查看去趋势价格振荡器的实时示例。

![图表 6](../Images/9edbeafb366991f09334999d5d3c547c.jpg "图表 6")

## 建议扫描

去趋势价格振荡器不适合用于扫描，因为该指标基于偏移移动平均线。20天的DPO对应于11天前的价格，这对于扫描来说并不实用。DPO还基于绝对水平，这使得它难以进行比较。一支股价为100美元的股票的DPO范围将比一支股价为20美元的股票宽得多。谷歌在一月初的股价约为590美元，DPO约为21。英特尔在一月初的股价约为20.5美元，DPO约为0.20，这要低得多。DPO较低是因为英特尔的股价远低于谷歌。

## 进一步研究

| **技术分析** 查尔斯·柯克帕特里克 & 朱莉·R·达尔奎斯特 |
| --- |
| [![](../Images/a24d1a5e5526382bfdec0424da3adce6.jpg)](http://store.stockcharts.com/products/technical-analysis-the-complete-resource-for-financial-market-technicians-2nd-edition "http://store.stockcharts.com/products/technical-analysis-the-complete-resource-for-financial-market-technicians-2nd-edition") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/technical-analysis-the-complete-resource-for-financial-market-technicians-2nd-edition "http://store.stockcharts.com/products/technical-analysis-the-complete-resource-for-financial-market-technicians-2nd-edition") |

# 知识确定事物（KST）[ChartSchool]

### 目录

+   [知识确定事物（KST）](#know_sure_thing_kst)

    +   [SharpCharts计算](#sharpcharts_calculation)

    +   [解释](#interpretation)

    +   [背离](#divergences)

    +   [强势趋势](#strong_trends)

    +   [时间框架](#timeframes)

    +   [进一步调整](#further_tweaks)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [建议扫描](#suggested_scans)

        +   [看涨KST信号线交叉](#bullish_kst_signal_line_cross)

        +   [看跌KST信号线交叉](#bearish_kst_signal_line_cross)

    +   [进一步研究](#further_study)

由Martin Pring开发，知识确定事物（KST）是基于四个不同时间框架的平滑变化率的动量振荡器。Pring在1992年的一篇文章中将这个指标称为“总变化率（KST）”*Stocks & Commodities*杂志。简而言之，KST衡量了四个不同价格周期的价格动量。它可以像任何动量振荡器一样使用。图表分析师可以寻找背离、超买/超卖读数、信号线交叉和中线交叉。Pring经常在KST上应用趋势线。尽管趋势线信号并不经常发生，但Pring指出这种突破会加强信号线交叉。

## SharpCharts计算

即使KST的公式看起来很复杂，但它实际上是一个相当直观的指标。它只是四个不同变化率的加权平均值，经过平滑处理。例如，计算10周期的变化率，然后用10周期的简单[移动平均](/school/doku.php?id=chart_school:technical_indicators:moving_averages "chart_school:technical_indicators:moving_averages")进行平滑处理。下图显示了四个不同的变化率指标及其适当的移动平均线进行平滑处理。

![图表1](../Images/a4dbc72c6b453c582aa2cb189599285f.jpg "图表1")

下方的公式框显示了四种不同组合及其默认设置。这些组合然后被加权和求和。最短的时间框架承载最小的权重（1），而最长的时间框架承载最大的权重（4）。添加了一个9周期的简单移动平均线作为信号线。

```py
RCMA1 = 10-Period SMA of 10-Period Rate-of-Change 
RCMA2 = 10-Period SMA of 15-Period Rate-of-Change 
RCMA3 = 10-Period SMA of 20-Period Rate-of-Change 
RCMA4 = 15-Period SMA of 30-Period Rate-of-Change 

KST = (RCMA1 x 1) + (RCMA2 x 2) + (RCMA3 x 3) + (RCMA4 x 4)  

Signal Line = 9-period SMA of KST

```

默认参数如下：KST(10,15,20,30,10,10,10,15,9)。前四个数字代表变化率设置，后四个代表这些变化率指标的移动平均线，最后一个数字是信号线移动平均线。

![电子表格](../Images/e63854c97e7839a6671159ee47b66a4e.jpg "电子表格")

[点击这里下载此电子表格示例](/school/lib/exe/fetch.php?media=chart_school:technical_indicators_and_overlays:know_sure_thing_kst:cs-kst.xls "chart_school:technical_indicators_and_overlays:know_sure_thing_kst:cs-kst.xls (45.5 KB)") 并在家里尝试。

## 解释

KST在零线上下波动。在最基本的情况下，当KST为正时，动量偏向多头，当KST为负时，动量偏向空头。正值意味着加权平滑的[变化率](/school/doku.php?id=chart_school:technical_indicators:rate_of_change_roc_and_momentum "chart_school:technical_indicators:rate_of_change_roc_and_momentum")值大多为正，并且价格上涨。负值表示价格下跌。

![图表 2](../Images/30578c37539f6cb30d853fc273e79471.jpg "图表 2")

在基本中线交叉之后，图表分析师可以寻找信号线交叉并判断总体方向。当KST在其信号线之上时，通常是上升的，当在其信号线之下时，通常是下降的。上升且为负的KST线表明下行动量正在减弱。相反，下降且为正的KST线表明上行动量正在减弱。

尽管KST可能有许多不同的信号，但基本的中线和信号线交叉通常是最可靠的。与RSI和随机振荡器不同，KST没有上限或下限。这使得它相对不适合超买和超卖信号。

## 背离

多头和[空头背离](/school/doku.php?id=chart_school:glossary_b#bearish_divergence "chart_school:glossary_b")也可能出现信号，但图表分析师在使用这些信号时需要谨慎。基本变化率指标中的大多数背离并不会导致价格逆转。同样，MACD和RSI中的背离也容易失败。最好在存在明显且明显的背离时使用背离。下面的示例显示了BroadCom (BRCM)存在明显的多头背离和空头背离。这些背离最终会随后的信号线交叉（红色和绿色箭头）而完成。

![图表 3](../Images/4569f826c64ea4a8f64dc83b4017a8b7.jpg "图表 3")

## 强势趋势

图表分析师在强劲上升趋势中应谨慎处理空头信号线交叉和在强劲下降趋势中的多头信号线交叉。在强劲上升趋势中，KST可能进入正区间并在较长时间内保持在正区间。指标将达到相对较高水平，然后转向下降，但永远不会进入负区间。这只是表明上行动量正在减缓。上行动量仍然强于下行动量，但上行动量不如之前的时期强劲。下面的示例显示了Sherwin Williams (SHW)从2011年11月到2012年8月的强劲上升趋势。尽管KST波动上下，但它从未跌破零线，并且在整个时间内保持在正区间。空头信号线交叉只是表明上行动量减缓，而不是趋势改变。

![图表 4](../Images/2a2131c4f73144515731b38473df9fd6.jpg "图表 4")

## 时间框架

+   短期日线 = KST(10,15,20,30,10,10,10,15,9)

+   中期周线 = KST(10,13,15,20,10,13,15,20,9)

+   长期月线 = KST(9,12,18,24,6,6,6,9,9)

正如Pring的文章中所指出的，KST可以用于短期、中期或长期时间框架。Pring建议不仅仅在日线、周线和月线图表之间切换，而是建议根据每个时间框架调整设置。使用周线和月线设置时，KST甚至更加平滑。这意味着图表分析师应该使用信号线交叉来检测价格的方向变化。中线交叉的滞后通常太大。下表显示了短期、中期和长期研究的变化率设置和移动平均设置。

![图表 5](../Images/ffce4972218595e8006e54413f427915.jpg "图表 5")

![图表 6](../Images/4c61b9b9b285d421836e97c95be174fc.jpg "图表 6")

![图表 7](../Images/cd1b8d2de245dec9c6e9d00f838c3d29.jpg "图表 7")

## 进一步调整

Pring承认KST不是一个完美的指标。这种东西是不存在的。然而，KST确实有其用途，Pring鼓励图表分析师尝试不同的设置，因为一刀切并不适用于所有情况。公用事业和消费品股票波动性较小，可能需要更敏感的设置。科技股更具波动性，可能需要更不敏感的设置。

图表分析师还可以混合和匹配变化率设置和移动平均设置。下图显示了第一个指标窗口中的默认KST和第二个窗口中偏向短期变化率的KST。第二个窗口显示的不是KST(10,15,20,30,10,10,10,15,9)，而是KST(30,20,15,10,10,10,10,10,9)。第一个变化率设置权重最小，第四个权重最大。请注意，前四个数字代表变化率设置。接下来的四个数字代表平滑这四个变化率指标的移动平均。最后一个数字是信号线。

![图表 8](../Images/260de45633af4ade9a5e6fb8539f3fea.jpg "图表 8")

## 结论

确信指标（KST）是基于四个不同时间周期的平滑变化率的动量振荡器。在这方面，它旨在捕捉四个不同的价格周期。KST可以像其他无约束的动量振荡器一样使用，例如MACD、百分比价格振荡器和TRIX。事实上，KST与[TRIX](/school/doku.php?id=chart_school:technical_indicators:trix "chart_school:technical_indicators:trix")非常相似。由于它是无约束的，KST不适合识别超买和超卖条件。创造者Martin Pring更倾向于信号线交叉和趋势线突破来发出信号。与所有指标一样，KST应与其他分析技术结合使用。

## 使用 SharpCharts

KST可作为SharpCharts的指标。一旦选择，用户可以将指标放置在基础价格图的上方、下方或后方。将KST直接放在价格图的后面，突出了相对于基础证券价格走势的波动。用户可以应用“高级选项”来添加水平线。调整参数框中的数字将更改设置。

![图表 9](../Images/704b7a2d1667b1b7175417693311f40a.jpg "Chart 9")

![图表 10](../Images/2de9da5e750477532e424d062e8fce22.jpg "Chart 10")

## 建议的扫描

### 看涨KST信号线穿越

此扫描显示了KST处于正区域的股票。当KST穿过其信号线时，将触发一个看涨信号。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [KST > 0]
AND [KST x KST Signal]

```

### 看跌KST信号线穿越

此扫描显示了KST处于负区域的股票。当KST穿过其信号线时，将触发一个看跌信号。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [KST < 0]
AND [KST Signal x KST]
```

有关用于KST扫描的语法详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#pring_s_know_sure_thing "http://stockcharts.com/docs/doku.php?id=scans:indicators#pring_s_know_sure_thing")在支持中心。

## 进一步研究

《金融市场技术分析》一书专门讨论了动量振荡器及其各种用途。墨菲涵盖了变动率的利弊以及一些特定于变动率的示例。普林的书通过涵盖背离、交叉和其他信号来展示动量指标的基础知识。还有两章涵盖了具体的动量指标，并提供了大量示例。

| **《金融市场技术分析》约翰·J·墨菲** | **《技术分析解析》马丁·普林** |
| --- | --- |
| [![](../Images/d9fb5f53997f0c87918070e360d1437d.jpg)](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | [![](../Images/907bb9e1dca336b6bedb79166d8efb0e.jpg)](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "Buy Now")](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "Buy Now")](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |

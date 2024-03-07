# 查金资金流量 [图表学校]

### 目录

+   [查金资金流量](#chaikin_money_flow)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [解释](#interpretation)

    +   [买入/卖出压力](#buying_selling_pressure)

    +   [计算特点](#calculation_quirk)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [建议的扫描](#suggested_scans)

        +   [查金资金流量转为正值且RSI移动超过50](#chaikin_money_flow_turns_positive_and_rsi_moves_above_50)

        +   [查金资金流量转为负值且RSI移动低于45](#chaikin_money_flow_turns_negative_and_rsi_moves_below_45)

    +   [进一步研究](#further_study)

    +   [其他资源](#additional_resources)

        +   [股票与商品杂志文章](#stocks_commodities_magazine_articles)

## 介绍

由马克·查金（Marc Chaikin）开发，查金资金流量（Chaikin Money Flow）衡量了特定时期内的资金流量量。资金流量量构成了积累分布线的基础。查金资金流量不是资金流量量的累积总和，而是简单地对特定回顾期内的资金流量量进行求和，通常为20或21天。所得指标像振荡器一样在零线上下波动。图表分析师根据查金资金流量的绝对水平权衡买入或卖出压力的平衡。图表分析师还可以寻找在零线上方或下方的交叉点，以识别资金流动的变化。

## 计算

计算查金资金流量（CMF）有四个步骤。下面的示例基于20个时期。首先，计算每个时期的资金流量乘数。其次，将此值乘以该时期的交易量，以找到资金流量量。第三，对20个时期的资金流量量进行求和，并除以20个时期的交易量总和。

```py

  1\. Money Flow Multiplier = [(Close  -  Low) - (High - Close)] /(High - Low) 

  2\. Money Flow Volume = Money Flow Multiplier x Volume for the Period

  3\. 20-period CMF = 20-period Sum of Money Flow Volume / 20 period Sum of Volume 

```

每个时期的资金流量量取决于资金流量乘数。当收盘价位于该时期最高-最低范围的上半部时，该乘数为正；当收盘价位于下半部时，该乘数为负。当收盘价等于最高价时，乘数为1；当收盘价等于最低价时，乘数为-1。通过这种方式，乘数调整了最终进入资金流量量的量。除非资金流量乘数处于极端值（+1或-1），否则实际上会减少交易量。

![图表1 - 查金资金流量](../Images/4f96a964b17239a0eb9ab8287749a875.jpg "图表1 - 查金资金流量")

上表显示了使用 Research in Motion（RIMM）的每日数据的一些示例。请注意，当股票在 1 月 5 日收盘时，乘数接近 +1。当股票在 1 月 18 日收盘时，乘数下降到 -0.97。当股票在 12 月 29 日收盘时，乘数接近零（-0.07），股票收于其高低范围的中点附近。[点击这里](/school/lib/exe/fetch.php?media=chart_school:technical_indicators_and_overlays:chaikin_money_flow_cmf:cs-cmf.xls "chart_school:technical_indicators_and_overlays:chaikin_money_flow_cmf:cs-cmf.xls (33 KB)") 查看 Excel 电子表格中 Chaikin Money Flow 的计算示例。

## 解释

Chaikin Money Flow（CMF）是在 -1 和 +1 之间波动的振荡器。极少情况下，指标会达到这些极端值。要使 20 天 Chaikin Money Flow 达到 +1（-1），需要连续 20 次收盘在高位（低位）。通常，这个振荡器在 -0.50 和 +0.50 之间波动，以零为中心线。

![图表 2  -  Chaikin Money Flow](../Images/84cabf5a30f42df1866f979d62d26555.jpg "图表 2  -  Chaikin Money Flow")

Chaikin Money Flow 衡量了一段时间内的买卖压力。进入正区域表示买盘压力，而进入负区域表示卖盘压力。图表分析师可以使用 Chaikin Money Flow 的绝对值来确认或质疑基础资产的价格走势。正 CMF 将确认上升趋势，但负 CMF 将质疑上升趋势背后的力量。对于下降趋势，情况相反。

## 买入/卖出压力

Chaikin Money Flow 可以用正值或负值简单地定义一般的买入或卖出偏见。该指标在零线上方/下方振荡。一般来说，当指标为正时，买盘压力更强，当指标为负时，卖盘压力更强。

虽然这个零线交叉看起来很简单，但实际情况要复杂得多。 Chaikin Money Flow 有时只是短暂地穿过零线，指标的变化几乎没有积极或消极的后续。没有跟进，这个零线交叉最终变成了一个鞭炮（错误信号）。图表分析师可以通过设置牛市阈值略高于零（+0.05）和熊市阈值略低于零（-0.05）来使用缓冲区来过滤这些信号。这些阈值不会完全消除错误信号，但可以帮助减少鞭炮并过滤掉较弱的信号。

![图表 2  -  Chaikin Money Flow](../Images/05718bc39a9021d21080dd33a7760b4e.jpg "图表 2  -  Chaikin Money Flow")

上面的图表显示了 Freeport McMoran (FCX) 的 20 天 Chaikin Money Flow 在指标窗口中。在 2010 年 2 月至 12 月之间至少有 10 次零线交叉。增加一个小缓冲区大大减少了多头和空头信号的数量。移动超过 +0.05 被视为多头，而移动低于 -0.05 被视为空头。只有三个信号。虽然这些信号会稍晚一些出现，但减少误导可能是值得的。

![图表 3  -  Chaikin Money Flow](../Images/13932b381e4912f0a447d9c75e3e8d9b.jpg "图表 3  -  Chaikin Money Flow")

Harley Davidson (HOG) 的图表显示了一些良好的信号和五月反弹的误导。CMF 在几天内上升到 +0.05 以上，但这个动作未能持续，指标在六月初再次跌破 -0.05。误导将会发生，特别是在波动期间或趋势变平时。CMF 在七月转为多头，并在今年的其余时间保持多头。请注意，HOG 形成了一个下降楔形，在八月回撤了超过 62%，而此时 CMF 仍处于多头模式。这次回撤提供了第二次参与 CMF 信号的机会。

![图表 4  -  Chaikin Money Flow](../Images/7621610bd32ba1b0a59609743acfa831.jpg "图表 4  -  Chaikin Money Flow")

Chaikin Money Flow 并不适用于所有证券。上面的图表显示了 P.F. Chang (PFCB) 的一些 18 次在 +0.05 或 -0.05 以上的交叉。基于这些交叉来制定 CMF 信号导致了一次又一次的误导。分析基本价格趋势和特定证券的指标特征是很重要的。PFCB 表现出一些趋势，但在这个趋势内的价格波动很大，资金流动无法保持正面或负面偏向。最好为这些股票找到不同的指标。

## 计算怪癖

Chaikin Money Flow 中的资金流乘数关注收盘价相对于给定期间（日、周、月）的高低范围的水平。根据这个公式，一支证券可能会跳空下跌并收盘明显较低，但如果收盘价高于高低范围的中点，资金流乘数将上升。下面的图表显示了 Clorox (CLX) 的大幅跳空下跌，收盘价接近当天的高低范围顶部。尽管股价在高交易量下急剧下跌，但由于资金流乘数为正且交易量远高于平均水平，Chaikin Money Flow 上升。忽略从收盘到收盘的变化意味着 Chaikin Money Flow 有时会与价格脱节。

![图表 5  -  Chaikin Money Flow](../Images/f8c8017066653f851b4cb536e3f37936.jpg "图表 5  -  Chaikin Money Flow")

当一只证券跳空上涨并且收盘接近当天的低点时，相反的情况可能发生。下图显示了Travelers（TRV）在当天跳空上涨并收盘超过1%。尽管有这一跳升，但收盘接近当天的低点，这导致了一个接近-1的资金流乘数。因此，几乎所有的交易量都被计为负资金流，Chaikin Money Flow 下降了。

![Chart 6  -  Chaikin Money Flow](../Images/fe882824fad9da1afa3ad218abd98050.jpg "Chart 6  -  Chaikin Money Flow")

## 结论

Chaikin Money Flow 是一种振荡器，用于衡量一段时间内的买入和卖出压力。在最基本的情况下，当CMF为正时，资金流向看涨，当为负时看跌。寻找更快资金流向变化的图表分析师可以寻找看涨和看跌的背离。不过要小心。即使存在看涨背离，卖出压力仍然占优势。这种看涨背离只是显示了较少的卖出压力。要指示实际的买入压力，需要进入正区域。作为资金流振荡器，CMF可以与纯价格振荡器一起使用，例如MACD或[RSI](/school/doku.php?id=chart_school:technical_indicators:relative_strength_index_rsi "chart_school:technical_indicators:relative_strength_index_rsi")。与所有指标一样，Chaikin Money Flow 不应作为独立指标使用。马克·查金还开发了[积聚分配线](/school/doku.php?id=chart_school:technical_indicators:accumulation_distribution_line "chart_school:technical_indicators:accumulation_distribution_line")和[查金振荡器](/school/doku.php?id=chart_school:technical_indicators:chaikin_oscillator "chart_school:technical_indicators:chaikin_oscillator")。

## 使用 SharpCharts

Chaikin Money Flow 可以设置为主窗口上方或下方的指标。由于它以区域格式显示，因此不适合放置在证券价格图后面。一旦从下拉列表中选择指标，就会出现默认参数（20）。这些参数可以调整以增加或减少灵敏度。用户可以点击“高级选项”添加水平线、移动平均线或其他叠加。图表分析师甚至可以在其他指标上方绘制第二个更长的Chaikin Money Flow指标。重叠期显示了两个不同期间的资金流强劲。[点击这里查看实时示例](http://stockcharts.com/h-sc/ui?s=AAPL&p=D&yr=0&mn=8&dy=0&id=p77394964602&listNum=30&a=223019825 "http://stockcharts.com/h-sc/ui?s=AAPL&p=D&yr=0&mn=8&dy=0&id=p77394964602&listNum=30&a=223019825")。

![Chart 7  -  Chaikin Money Flow](../Images/b48cb1392a499fc33cf3ba27363f8ed6.jpg "Chart 7  -  Chaikin Money Flow")

![SharpCharts  -  Chaikin Money Flow](../Images/7f77bf110b389674d4ec4987eca8780e.jpg "SharpCharts  -  Chaikin Money Flow")

## 建议的扫描

### Chaikin Money Flow 转为正值，RSI 上升至 50 以上

这个扫描从股价至少为$10且过去60天日均交易量为100,000的股票开始。当查金货币流指标进入正区时，会识别出积累和买入压力。当相对强弱指标（RSI）上穿50，即其中线时，价格动量得到确认。这个扫描旨在作为进一步分析和尽职调查的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily CMF(20) crosses 0] 
AND [Daily RSI(14,Daily Close) crosses 50]
```

### 查金货币流指标转为负值，RSI下穿45

这个扫描从股价至少为$10且过去60天日均交易量为100,000的股票开始。当查金货币流指标进入负区时，会识别出分销和卖出压力。当相对强弱指标（RSI）下穿50，即其中线时，价格动量得到确认。这个扫描旨在作为进一步分析和尽职调查的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [0 crosses Daily CMF(20)] 
AND [50 crosses Daily RSI(14,Daily Close)]
```

有关查金货币流扫描的语法详细信息，请参阅我们支持中心的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#chaikin_money_flow_cmf "http://stockcharts.com/docs/doku.php?id=scans:indicators#chaikin_money_flow_cmf")。

**注意**：出于扫描目的，交易日内的日交易量数据是不完整的。在运行基于交易量的指标（如CMF）的扫描时，请确保基于“上次市场收盘价”。其他基于交易量的指标的示例包括积累/分布指标、成交量平衡指标和PVO。

## 进一步研究

这本书通过简单清晰的解释涵盖了所有内容。墨菲涵盖了大部分主要的图表模式和指标。有一个完整的章节专门讨论了理解成交量和未平仓合约。

| **金融市场技术分析** 约翰·J·墨菲 |
| --- |
| [![](../Images/e00f9b0f57a7325646647a118f3ebe9e.jpg)](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |

* * *

## 其他资源

### 股票与商品杂志文章

**[查金货币流指标（作者：克里斯托弗·纳尔库齐）](http://stockcharts.com/h-mem/tascredirect.html?artid=\V18\C08\072CHA.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V18\C08\072CHA.pdf")**

2000年7月 - 股票与商品

**[比较七种货币流指标（作者：马科斯·卡特萨诺斯）](http://stockcharts.com/h-mem/tascredirect.html?artid=\V29\C07\110KATS.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V29\C07\110KATS.pdf")**

2011年6月 - 股票与商品

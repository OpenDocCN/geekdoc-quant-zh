# MACD（移动平均线收敛/发散振荡器）[图表学校]

### 目录

+   [MACD（移动平均线收敛/发散振荡器）](#macd_moving_average_convergence_divergence_oscillator)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [解释](#interpretation)

    +   [信号线交叉](#signal_line_crossovers)

    +   [中线交叉](#centerline_crossovers)

    +   [背离](#divergences)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [建议的扫描](#suggested_scans)

        +   [MACD看涨信号线交叉](#macd_bullish_signal_line_cross)

        +   [MACD看跌信号线交叉](#macd_bearish_signal_line_cross)

    +   [进一步研究：](#further_study)

    +   [额外资源](#additional_resources)

        +   [股票与商品杂志文章](#stocks_commodities_magazine_articles)

## 介绍

由杰拉尔德·阿普尔在七十年代末开发的移动平均线收敛/发散振荡器（MACD）是目前最简单和最有效的动量指标之一。MACD通过从较长的移动平均线中减去较短的移动平均线，将两个趋势跟踪指标[移动平均线](/school/doku.php?id=chart_school:technical_indicators:moving_averages "chart_school:technical_indicators:moving_averages")转化为动量振荡器。因此，MACD提供了趋势跟踪和动量的最佳结合。MACD在零线上下波动，因为移动平均线收敛、交叉和发散。交易者可以寻找信号线交叉、中线交叉和背离来生成信号。由于MACD没有上下限，因此不太适用于识别超买和超卖水平。

注意：MACD可以发音为“Mac-Dee”或“M-A-C-D”。

这里是一个示例图表，其中MACD指标显示在下方面板中：

[![](../Images/9cb2dc1a0d02d7e81394358199a42018.jpg)](http://stockcharts.com/h-sc/ui?s=QQQ&p=D&st=2009-01-01&en=2009-04-03&id=p70644026533&a=206516339 "http://stockcharts.com/h-sc/ui?s=QQQ&p=D&st=2009-01-01&en=2009-04-03&id=p70644026533&a=206516339")

点击图表查看实时示例。

## 计算

```py
MACD Line: (12-day EMA - 26-day EMA)

Signal Line: 9-day EMA of MACD Line

MACD Histogram: MACD Line - Signal Line

```

MACD线是12天的[指数移动平均线](/school/doku.php?id=chart_school:technical_indicators:moving_averages "chart_school:technical_indicators:moving_averages")（EMA）减去26天的EMA。这些移动平均线使用收盘价。MACD线的9天EMA与指标一起绘制，作为信号线并识别转折点。MACD柱状图表示MACD与其9天EMA（信号线）之间的差异。当MACD线高于其信号线时，柱状图为正，当MACD线低于其信号线时，柱状图为负。

**12、26和9**这些数值是MACD中典型的设置，然而根据您的交易风格和目标，可以替换其他数值。

## 解释

正如其名称所示，MACD 主要关注两个移动平均线的收敛和分歧。当移动平均线彼此靠近时，就会出现收敛。当移动平均线彼此远离时，就会出现分歧。较短的移动平均线（12天）更快，负责大部分 MACD 运动。较长的移动平均线（26天）更慢，对基础证券价格变化反应较弱。

MACD 线在零线上下振荡，也被称为中心线。这些交叉信号表明12天 EMA 已经穿过了26天 EMA。当然，方向取决于移动平均线的方向。正 MACD 表示12天 EMA 高于26天 EMA。随着较短 EMA 进一步偏离较长 EMA，正值增加。**这意味着上涨动能正在增加。** 负 MACD 值表示12天 EMA 低于26天 EMA。随着较短 EMA 进一步偏离较长 EMA，负值增加。**这意味着下行[动能](/school/doku.php?id=chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators#leading_indicators "chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators")正在增加。**

![](../Images/6470e8080db2c48f6cc0fffa1b79d642.jpg)

在上面的示例中，黄色区域显示了 MACD 线在负值区域，因为12天 EMA 低于26天 EMA。最初的交叉发生在九月底（黑色箭头），随着12天 EMA 进一步偏离26天 EMA，MACD 进一步进入负值区域。橙色区域突出显示了一段正 MACD 值的时期，即12天 EMA 高于26天 EMA。请注意，在此期间 MACD 线保持在1以下（红色虚线）。这意味着12天 EMA 和26天 EMA 之间的距离小于1点，这并不是一个很大的差异。

## 信号线交叉

信号线交叉是最常见的 MACD 信号。信号线是 MACD 线的9天 EMA。作为指标的移动平均线，它追踪 MACD 并更容易发现 MACD 转折点。当 MACD 向上转折并穿过信号线时，就会出现看涨交叉。当 MACD 向下转折并穿过信号线时，就会出现看跌交叉。交叉可能持续几天或几周，这完全取决于行情的强度。

在依赖这些常见信号之前需要进行尽职调查。在正负极端处的信号线交叉应该谨慎对待。尽管MACD没有上限和下限，但图表分析师可以通过简单的视觉评估来估计历史极端值。基础证券的强劲波动会增加交叉的数量。

下面的图表显示了IBM及其12日EMA（绿色）、26日EMA（红色）和指标窗口中的12,26,9 MACD。在六个月内有八次信号线交叉：四次上穿和四次下穿。有一些好的信号和一些坏的信号。黄色区域突出显示了MACD线在2以上激增达到正极端的时期。四月和五月出现了两次看跌的信号线交叉，但IBM继续上涨。尽管在激增后上涨动能减缓，但四月至五月的上涨动能仍然强于下行动能。五月的第三次看跌信号线交叉产生了一个良好的信号。

![](../Images/260b097fff49af332eaa75a0d4888e42.jpg)

## 中轴线交叉

中轴线交叉是MACD信号中次常见的信号。当MACD线上穿零线变为正数时，就会出现看涨的中轴线交叉。这发生在基础证券的12日EMA上穿26日EMA时。当MACD下穿零线变为负数时，就会出现看跌的中轴线交叉。这发生在12日EMA下穿26日EMA时。

中轴线交叉可能持续几天或几个月。这完全取决于趋势的强度。只要有持续的上升趋势，MACD就会保持正数。只要有持续的下降趋势，MACD就会保持负数。下一个图表显示了普尔特房屋（PHM）在九个月内至少有四次中轴线交叉。由于这些中轴线交叉出现时出现了强劲的趋势，所以产生的信号效果很好。

![](../Images/ef9768c2efe25ccc7f8d90fa8266cb74.jpg)

下面是康明斯公司（CMI）的图表，显示了五个月内七次中轴线交叉。与普尔特房屋不同，这些信号会导致许多震荡，因为在交叉后没有出现强劲的趋势。

![](../Images/bb6bd2ca07b145df99225c34a8a666fa.jpg)

下一个图表显示了3M（MMM）在2009年3月底出现了一个看涨的中轴线交叉，而在2010年2月初出现了一个看跌的中轴线交叉。这个信号持续了10个月。换句话说，12日EMA在10个月内一直高于26日EMA。这是一个强劲的趋势。

![](../Images/7d8ae0da668d16533117ffb7520a2bb6.jpg)

## 分歧

[分歧](/school/doku.php?id=chart_school:glossary_d#divergence "chart_school:glossary_d")是指MACD与基础证券的价格走势出现分歧。当一项证券记录了更低的低点，而MACD形成了更高的低点时，就形成了看涨的分歧。证券的更低低点确认了当前的下跌趋势，但MACD的更高低点显示出更少的下跌动量。尽管下跌动量较小，但只要MACD保持在负值区域，下跌动量仍然超过上涨动量。减缓的下跌动量有时可能预示着趋势反转或大幅上涨。

下图显示了2008年10月至11月间谷歌（GOOG）的看涨分歧。首先，请注意我们使用收盘价来识别分歧。MACD的移动平均线是基于收盘价的，我们也应该考虑证券的收盘价。其次，请注意在10月和11月底，谷歌和其MACD线都反弹时，都有明显的反应低点（低谷）。第三，请注意在11月份，随着谷歌形成更低的低点，MACD形成了更高的低点。MACD在12月初形成了一个看涨分歧，并通过信号线交叉确认了一次反转。谷歌通过突破阻力线确认了一次反转。

![](../Images/6c395a340095fde1f1d9309082940cfb.jpg)

当一项证券记录了更高的高点，而MACD线形成了更低的高点时，就形成了看跌的分歧。证券的更高高点对于上涨趋势是正常的，但MACD的更低高点显示出更少的上涨动量。尽管上涨动量可能较小，但只要MACD是正的，上涨动量仍然超过下跌动量。逐渐减弱的上涨动量有时可能预示着趋势反转或大幅下跌。

在下图中，我们看到Gamestop（GME）从8月至10月出现了一个大的看跌分歧。股票在28以上形成了更高的高点，但MACD线未达到先前的高点，并形成了更低的高点。随后的信号线交叉和MACD的支撑线突破是看跌的。在价格图表上，请注意在11月的回调反弹中，破裂的支撑线变成了阻力（红色虚线）。这次回调提供了第二次卖出或卖空的机会。

![](../Images/bfc211a32cb951ad168c3f5874da1976.jpg)

分歧应该谨慎对待。在强劲的上涨趋势中，看跌的分歧很常见，而在强劲的下跌趋势中，看涨的分歧经常发生。是的，你没看错。上涨趋势通常以强劲的上涨开始，产生了上涨动量（MACD）的激增。尽管上涨趋势持续，但它的速度变慢，导致MACD从高点下降。上涨动量可能不那么强劲，但只要MACD线在零线以上，上涨动量仍然超过下跌动量。相反，在强劲下跌趋势开始时会发生相反的情况。

下图显示了标普 500 ETF（SPY）从 2009 年 8 月至 11 月出现的四次看跌背离。尽管上涨动量较小，但由于上涨趋势强劲，ETF 仍然继续上涨。请注意 SPY 如何继续保持较高高点和较低低点的系列。请记住，只要 MACD 为正值，上涨动量就比下跌动量强。随着上涨的延伸，其 MACD（动量）可能不那么积极（强劲），但仍然主要为正值。

![](../Images/83e5b1f65e9c877cd1a3c88b597eb9a8.jpg)

## 结论

MACD 指标很特殊，因为它将动量和趋势结合在一个指标中。这种趋势和动量的独特融合可以应用于日线、周线或月线图表。MACD 的标准设置是 12 和 26 期 EMA 之间的差值。寻找更敏感性的图表分析师可以尝试更短的短期移动平均线和更长的长期移动平均线。MACD(5,35,5) 比 MACD(12,26,9) 更敏感，可能更适合周线图表。寻找更少敏感性的图表分析师可以考虑延长移动平均线。较不敏感的 MACD 仍会在零线上下波动，但中线交叉和信号线交叉会更少。

MACD 不是特别适用于识别超买和超卖水平。尽管可能识别出历史上超买或超卖的水平，但 MACD 没有任何上限或下限来限制其运动。在剧烈波动期间，MACD 可能会继续超出其历史极限。

最后，请记住，MACD 线是使用两个移动平均线的实际差值计算的。这意味着 MACD 值取决于基础证券的价格。一只 $20 的股票的 MACD 值可能在 -1.5 到 1.5 之间波动，而一只 $100 的股票的 MACD 值可能在 -10 到 +10 之间波动。不可能比较具有不同价格的一组证券的 MACD 值。如果要比较动量读数，应该使用[百分比价格振荡器（PPO）](/school/doku.php?id=chart_school:technical_indicators:price_oscillators_ppo "chart_school:technical_indicators:price_oscillators_ppo")而不是 MACD。

## 使用 SharpCharts

MACD 可以设置为在证券价格图上方、下方或后方的指标。将 MACD 放在价格图的“后方”可以方便地比较动量运动和价格运动。一旦从下拉菜单中选择指标，就会出现默认参数设置：(12,26,9)。这些参数可以调整以增加或减少灵敏度。MACD 柱状图会随指标一起显示，或者可以作为单独的指标添加。将信号线设置为 1 或留空，即 (12,26,1) 或 (12,26)，将删除 MACD 柱状图和信号线。可以通过从高级选项叠加菜单中选择“Exp. Moving Avg”来添加单独的信号线，而不带柱状图。

[点击这里](http://stockcharts.com/h-sc/ui?s=$INDU&p=D&b=5&g=0&id=p18754900449&listNum=30&a=199515976 "http://stockcharts.com/h-sc/ui?s=$INDU&p=D&b=5&g=0&id=p18754900449&listNum=30&a=199515976") 查看 MACD 指标的实时图表。

![](../Images/1494f28ca800b8667187ec60de2c6f29.jpg)

![](../Images/71629e069342fd509cdea8278bfff443.jpg)

## 建议的扫描

这里有一些股票图表会员可以用来扫描各种 MACD 信号的示例扫描：

### MACD 多头信号线交叉

这个扫描显示出那些交易高于它们的200日移动平均线并且在MACD中有一个多头信号线交叉的股票。还要注意，MACD必须为负以确保这种上升发生在回调之后。这个扫描只是作为进一步细化的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close > Daily SMA(200,Daily Close)] 
AND [Yesterday's Daily MACD Line(12,26,9,Daily Close) < Daily MACD Signal(12,26,9,Daily Close)] 
AND [Daily MACD Line(12,26,9,Daily Close) > Daily MACD Signal(12,26,9,Daily Close)] 
AND [Daily MACD Line(12,26,9,Daily Close) < 0]
```

### MACD 空头信号线交叉

这个扫描显示出那些交易低于它们的200日移动平均线并且在MACD中有一个空头信号线交叉的股票。还要注意，MACD必须为正以确保这种下降发生在反弹之后。这个扫描只是作为进一步细化的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close < Daily SMA(200,Daily Close)] 
AND [Yesterday's Daily MACD Line(12,26,9,Daily Close) > Daily MACD Signal(12,26,9,Daily Close)] 
AND [Daily MACD Line(12,26,9,Daily Close) < Daily MACD Signal(12,26,9,Daily Close)] 
AND [Daily MACD Line(12,26,9,Daily Close) > 0]
```

有关用于 MACD 扫描的语法的更多详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#moving_average_convergence-divergence_macd "http://stockcharts.com/docs/doku.php?id=scans:indicators#moving_average_convergence-divergence_macd")在支持中心。

## 进一步研究：

从创作者那里，这本书提供了一个全面的研究，用于使用和解释MACD。

| **技术分析 - 积极投资者的强大工具** 杰拉德·阿普尔 |
| --- |
| [![](../Images/a2673256615cb182a677e60a34c2b755.jpg)](http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors "http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors") |
| [![buynowbuttone.jpg](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "buynowbuttone.jpg")](http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors "http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors") |

* * *

## 其他资源

### 股票与商品杂志文章

**[移动平均线收敛/发散（MACD）by 汤姆·哈特尔](http://stockcharts.com/h-mem/tascredirect.html?artid=\V09\C03\MACD.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V09\C03\MACD.pdf")**

1991年2月 - 股票与商品 V. 9:3 (104-104)

**[马克·瓦库尔的移动平均线收敛/发散](http://stockcharts.com/h-mem/tascredirect.html?artid=\V15\C04\THEMOVI.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V15\C04\THEMOVI.pdf")**

1997年3月 - 股票与商品

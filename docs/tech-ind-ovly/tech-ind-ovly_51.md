# TRIX [ChartSchool]

### 目录

+   [TRIX](#trix)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [解释](#interpretation)

    +   [信号线交叉](#signal_line_crossovers)

    +   [中线交叉](#centerline_crossovers)

    +   [背离](#divergences)

    +   [结论](#conclusions)

    +   [使用SharpCharts](#using_with_sharpcharts)

    +   [建议扫描](#suggested_scans)

        +   [TRIX 阳市信号线交叉](#trix_bullish_signal_line_cross)

        +   [TRIX 熊市信号线交叉](#trix_bearish_signal_line_cross)

    +   [进一步研究](#further_study)

## 介绍

TRIX是一个动量振荡器，显示了三重指数平滑移动平均值的百分比[变化率](/school/doku.php?id=chart_school:technical_indicators:rate_of_change_roc_and_momentum "chart_school:technical_indicators:rate_of_change_roc_and_momentum")。它是由杰克·哈特森（Jack Hutson）在20世纪80年代初开发的，他是《股票与大宗商品技术分析》杂志的编辑。通过三重平滑，TRIX旨在过滤不重要的价格波动。图表分析师可以使用TRIX生成类似于MACD的信号。可以应用信号线来寻找信号线交叉。可以通过绝对水平确定方向性偏差。可以利用牛市和熊市的背离来预测反转。

## 计算

TRIX是三重平滑指数[移动平均线](/school/doku.php?id=chart_school:technical_indicators:moving_averages "chart_school:technical_indicators:moving_averages")（EMA）的1期百分比变化率，这是一个EMA的EMA的EMA。以下是15期TRIX所涉及的步骤的详细说明。

+   1\. 单一平滑的EMA = 收盘价的15日EMA

+   2\. 双重平滑的EMA = 单一平滑的EMA的15日EMA

+   3\. 三重平滑的EMA = 双重平滑的EMA的15日EMA

+   4\. TRIX = 三重平滑的EMA的1期百分比变化

下表和图提供了15日EMA、双重平滑的EMA和三重平滑的EMA的示例。请注意每个EMA都会滞后价格一段时间。尽管指数移动平均值更加重视最近的数据，但它们仍包含产生滞后的过去数据。这种滞后随着平滑次数的增加而增加。

![TRIX  -  表1](../Images/05ee67d08a8d798e1eba1ee33c927d0b.jpg "TRIX  -  表1")

![TRIX - 图表1](../Images/87ff30cd9841aaea46905e4876e4b919.jpg "TRIX - 图表1")

蓝线是SPY的价格走势图。它显然是四条线中最不平滑（波动最大）的。红线是15日EMA，它最接近价格走势。绿线是双重平滑的EMA，紫线是三重平滑的EMA。请注意随着滞后的增加，这两条线变得更加平坦。

只要三重平滑的15日EMA向下移动，TRIX就是负的。当三重平滑的15日EMA向上转变时，TRIX变为正。额外的平滑确保上涨和下跌被最小化。换句话说，需要超过一天的上涨才能扭转下降趋势。

![TRIX - 图表 2](../Images/15a026511c999fc032c9af5332bfb739.jpg "TRIX - 图表 2")

## 解释

TRIX（15,9）与[MACD（12,26,9）](/school/doku.php?id=chart_school:technical_indicators:moving_average_convergence_divergence_macd "chart_school:technical_indicators:moving_average_convergence_divergence_macd")非常相似。两者都是上下波动在零线上下的动量振荡器。两者都有基于9日EMA的信号线。最值得注意的是，两条线具有相似的形状、信号线交叉和中线交叉。TRIX和MACD之间最大的区别在于TRIX比MACD更平滑。TRIX线条不那么锯齿状，而且转折稍晚一些。

![TRIX - 图表 3](../Images/9de115e687509eddb31acc457494987f.jpg "TRIX - 图表 3")

鉴于相似性超过差异性，适用于MACD的信号也适用于TRIX。有三个主要信号需要关注。首先，信号线交叉是最常见的信号。这些表明TRIX和价格动量的方向变化。信号线上方交叉是第一个多头迹象，而下方交叉是第一个负面暗示。其次，中线交叉为图表分析师提供了一般的动量偏向。当TRIX为正时，三次平滑移动平均线上升，当为负时下降。同样，当TRIX为正时，动量有利于多头，当为负时有利于空头。第三，多头和空头背离可以提醒图表分析师可能的趋势反转。

## 信号线交叉

信号线交叉是最常见的TRIX信号。信号线是TRIX的9日EMA。作为指标的移动平均线，它追踪TRIX并更容易发现转折点。当TRIX向上转折并上穿信号线时出现多头交叉。当TRIX向下转折并下穿信号线时出现空头交叉。交叉可能持续几天或几周，这完全取决于行情的强度。在依赖这些频繁信号之前需要进行尽职调查。基础证券的波动性也可能增加交叉的数量。

![TRIX - 图表 4](../Images/357a48170163889d4a235ab720299530.jpg "TRIX - 图表 4")

上图显示了英特尔（INTC）和TRIX在七个月内出现了六次信号线交叉。几乎每个月都有一次。有三个好的信号和三个坏的信号导致了折返（黄色区域）。6月的多头交叉发生在顶部附近，6月底的空头交叉发生在低点附近，7月的多头交叉发生在顶部附近。在没有强劲行情的情况下，三次平滑的EMA滞后导致产生亏损的信号。8月的空头信号线交叉预示了急剧下跌，9月中旬的多头信号线交叉预示了强劲上涨。

## 中线交叉

[中心线交叉](/school/doku.php?id=chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators#centerline_crossovers "chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators")表示杯子是半满（多头）还是半空（空头）。将中心线视为橄榄球比赛中的50码线。进攻方在越过50码线（中点）后占据优势，而只要球仍然在50码线之外，防守方就占据优势。与信号线交叉一样，这些中心线交叉既产生好信号也产生坏信号。关键在于，始终是尽量减少坏信号的损失，最大化好信号的收益。

![TRIX - 图表 5](../Images/e0b6d47d6bb925c02619d2fd9e91cd34.jpg "TRIX - 图表 5")

上图显示了雷神（RTN）在16个月内出现的五个信号。前三个信号不好，因为股票很快在信号后改变了方向。换句话说，趋势未能确立。第四个信号（2009年11月）与阻力突破同时发生，并预示着20%的上涨。很好的信号！这也是将指标信号与图表信号结合起来加强的经典例子。价格图表上的阻力突破和TRIX的中心线交叉相互加强。TRIX在2010年5月产生了一个不错的空头信号，随后RTN下跌了约20%。

## 背离

当证券和指标不相互确认时，就会形成多头背离和空头背离。当证券形成较低的低点，但指标形成较高的低点时，就形成了多头背离。这种较高的低点显示出较少的下行动量，可能预示着一个多头反转。当证券形成较高的低点，但指标形成较低的高点时，就形成了空头背离。这种较低的高点显示出逐渐减弱的上行动量，有时可能预示着一个空头反转。在看一个成功的背离之前，请注意BHP比利顿（BHP）图表上的几个不成功的背离。

![TRIX - 图表 6](../Images/fd19580734c611a9a656a328d0f867ed.jpg "TRIX - 图表 6")

空头背离在强劲的上涨趋势中效果不佳。即使动量似乎在减弱，因为指标产生了较低的高点，只要指标在中心线上方，动量仍然具有多头偏向。上行动量可能不那么积极，但只要杯子还是半满的，它仍然是积极的。上涨只是不像以前那样快。而对于多头背离则相反。在强劲的下跌趋势中，多头背离效果不佳。即使指标显示出较高的低点，下行动量仍然比上行动量强，只要指标保持在中心线以下。

当多头和空头背离起作用时，它们确实效果很好。关键是区分坏信号和好信号。下图显示了 eBay（EBAY）成功的多头背离。股票在七月初创下更低的低点，但 TRIX 保持在其先前低点之上，并形成了多头背离。第一个潜在的确认是当 TRIX 移动到其信号线之上时。然而，当时图表上没有确认。这些稍后才出现。绿色箭头显示 EBAY 打破图表阻力，并伴有良好的成交量，TRIX 进入正区。即使确认发生在低点之外，仍有足够的强势迹象来验证突破。

![TRIX - 图表 7](../Images/8e451fee6d5a1d1646e5cfc4cce0e111.jpg "TRIX - 图表 7")

## 结论

TRIX 是一种将趋势与动量结合的指标。三重平滑移动平均线涵盖了趋势，而 1 期百分比变化测量了动量。在这方面，TRIX 类似于 MACD 和 PPO。TRIX 的标准设置为三重平滑 EMA 的 15 和信号线的 9。寻求更多灵敏度的图表分析师应该尝试更短的时间框架（5 对比 15）。这将使指标更加波动，并更适合中线交叉。寻求更少灵敏度的图表分析师应该尝试更长的时间框架（45 对比 15）。这将平滑指标，并使其更适合信号线交叉。与所有指标一样，TRIX 应与技术分析的其他方面结合使用，例如[图表模式](/school/doku.php?id=chart_school:chart_analysis:chart_patterns "chart_school:chart_analysis:chart_patterns")。

![TRIX - 图表 8](../Images/4bcf07a0c3254616188386f09c3fb2a5.jpg "TRIX - 图表 8")

## 使用 SharpCharts

TRIX 可以设置为一个指标，位于证券价格图表的上方、下方或后方。当指标放置在价格图表后面时，可以轻松比较指标/价格的变动。一旦从下拉列表中选择指标，将显示默认参数设置（15,9）。这些参数可以调整以增加或减少灵敏度。信号线默认为 9，也可以进行调整。[点击这里查看 TRIX 的实时示例](http://stockcharts.com/h-sc/ui?s=SPY&p=D&yr=0&mn=6&dy=0&id=p97840257416&listNum=30&a=218370394 "http://stockcharts.com/h-sc/ui?s=SPY&p=D&yr=0&mn=6&dy=0&id=p97840257416&listNum=30&a=218370394")。

![TRIX - 图表 7](../Images/8e451fee6d5a1d1646e5cfc4cce0e111.jpg "TRIX - 图表 7")

## 建议的扫描

### TRIX 多头信号线交叉

这种扫描揭示了符合四个标准的股票。首先，它们必须高于它们的 200 天移动平均线，以处于总体上升趋势中。其次，TRIX 必须为负以发出回调信号。第三，TRIX 穿过其信号线并向上转向。第四，成交量超过 250 天平均值，显示买盘压力增加。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close > Daily SMA(200,Daily Close)] 
AND [Yesterday's Daily TRIX(15,9,Daily Close) crosses Daily TRIX Signal(15,9,Daily Close)] 
AND [Daily Volume > Daily SMA(250,Daily Volume)] 
AND [Daily TRIX(15,9,Daily Close) < 0]
```

### TRIX 空头信号线交叉

这个扫描揭示了符合四个标准的股票。首先，它们必须低于它们的200日移动平均线，以处于总体下降趋势中。其次，TRIX必须为正以发出反弹信号。第三，TRIX穿过其信号线并转向下。第四，成交量超过250日均线，显示卖压增加。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close < Daily SMA(200,Daily Close)] 
AND [Yesterday's Daily TRIX Signal(15,9,Daily Close) crosses Daily TRIX(15,9,Daily Close)] 
AND [Daily Volume > Daily SMA(250,Daily Volume)] 
AND [Daily TRIX(15,9,Daily Close) > 0]
```

有关使用TRIX扫描的语法的更多详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#trix "http://stockcharts.com/docs/doku.php?id=scans:indicators#trix")在支持中心。

## 进一步研究

| **技术分析-活跃投资者的强大工具** 杰拉尔德·阿普尔 |
| --- |
| [![](../Images/a2673256615cb182a677e60a34c2b755.jpg)](http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors "http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "Buy Now")](http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors "http://store.stockcharts.com/products/technical-analysis-power-tools-for-active-investors") |

# 终极振荡器 [ChartSchool]

### 目录

+   [终极振荡器](#ultimate_oscillator)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [解释](#interpretation)

    +   [买入信号](#buy_signal)

    +   [卖出信号](#sell_signal)

    +   [时间框架](#timeframes)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [建议扫描](#suggested_scans)

        +   [看涨长期交叉](#bullish_long-term_cross)

        +   [看跌长期交叉](#bearish_long-term_cross)

    +   [进一步研究](#further_study)

    +   [额外资源](#additional_resources)

        +   [股票与商品杂志文章](#stocks_commodities_magazine_articles)

## 介绍

由Larry Williams于1976年开发，并于1985年在《股票与商品杂志》上推出的终极振荡器是一种动量振荡器，旨在捕捉三个不同时间框架的动量。多时间框架目标旨在避免其他振荡器的缺陷。许多[动量振荡器](/school/doku.php?id=chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators#momentum_oscillators "chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators")在强劲上涨开始时激增，然后随着上涨的持续形成熊市背离。这是因为它们被困在一个时间框架中。终极振荡器试图通过将较长的时间框架纳入基本公式来纠正这个缺陷。威廉姆斯根据看涨背离确定了买入信号，根据看跌背离确定了卖出信号。

## 计算

终极振荡器（UO）计算涉及许多步骤。此示例基于默认设置（7,14,28）。首先，计算买入压力（BP）以确定价格走势的总体方向。其次，测量买入压力相对于真实波幅（TR）。这告诉我们收益或损失的真实幅度。第三，基于涉及的三个时间框架（7,14,28）创建平均值。第四，创建三个平均值的加权平均值。

```py
BP = Close - Minimum(Low or Prior Close).

TR = Maximum(High or Prior Close)  -  Minimum(Low or Prior Close)

Average7 = (7-period BP Sum) / (7-period TR Sum)
Average14 = (14-period BP Sum) / (14-period TR Sum)
Average28 = (28-period BP Sum) / (28-period TR Sum)

UO = 100 x [(4 x Average7)+(2 x Average14)+Average28]/(4+2+1)

```

买入压力（BP）衡量当前收盘价相对于当前最低价或先前收盘价（以较低者为准）的水平。真实波幅（TR）衡量从当前最高价或先前收盘价（以较高者为准）到当前最低价或先前收盘价（以较低者为准）的价格范围。买入压力和真实波幅都包含先前收盘价，以考虑可能从一个周期到下一个周期的间隙。然后通过将BP的X周期总和除以TR的X周期总和来相对于真实波幅显示买入压力。为7、14和28个周期创建平均值。这些数字对应默认参数。然后通过将最短平均值乘以4、中间平均值乘以2和最长平均值乘以1来创建加权平均值。然后将这些加权金额相加，并除以权重之和（4+2+1）。

![终极振荡器- 电子表格](../Images/75cf3e5084a7859344fad15eba1c06e5.jpg "终极振荡器- 电子表格")

点击[这里](/school/lib/exe/fetch.php?media=chart_school:technical_indicators_and_overlays:ultimate_oscillator:cs-ultosc.xls "chart_school:technical_indicators_and_overlays:ultimate_oscillator:cs-ultosc.xls (41.5 KB)")查看Excel电子表格中的终极振荡器计算。

![终极振荡器  -  图表 1](../Images/881d6f7c3ce0a9992468abe01fe3f911.jpg "终极振荡器  -  图表 1")

## 解释

购买压力及其与真实波幅的关系构成了终极振荡器的基础。威廉姆斯认为，衡量购买压力的最佳方法就是简单地将收盘价减去最低价或前一收盘价中较低的那个。这将反映出真正的上涨幅度，因此也反映了购买压力。当购买压力强劲时，终极振荡器上升，而当购买压力较弱时则下降。

终极振荡器测量三个不同时间段的动量。请注意，第二个时间段是第一个时间段的两倍，第三个时间段是第二个时间段的两倍。尽管最短的时间段权重最大，但最长的时间段也不会被忽视，这应该会减少错误分歧的数量。这很重要，因为基本的买入信号是基于看涨分歧，而基本的卖出信号是基于看跌分歧。

## 买入信号

买入信号有三个步骤。首先，指标与证券价格之间形成了一个[看涨分歧](/school/doku.php?id=chart_school:glossary_b#bullish_divergence "chart_school:glossary_b")。这意味着终极振荡器形成了一个较高的低点，而价格则形成了一个较低的低点。振荡器中的较高低点显示出较小的下行动量。其次，看涨分歧的低点应低于30。这是为了确保价格有些超卖或处于相对极端状态。第三，振荡器上升至看涨分歧的高点之上。

最佳购买（BBY）显示终极振荡器（7,14,28）在六月底超卖，并在八月底形成与之形成大的看涨分歧，直到九月中旬技术上指标才确认了分歧。然而，技术分析需要一些灵活性。图表分析师可以使用超过50的移动作为终极振荡器的触发器。这个中心线充当指标的牛熊阈值。当在上方时，杯子是半满的（看涨偏向），当在下方时，杯子是半空的（看跌偏向）。还要注意，该股票突破了六月的趋势线，并在九月初突破了短期阻力以进一步确认。

![终极振荡器  -  图表 2](../Images/3e23e5fe6d76f8ecb02d1f8c4efcea1e.jpg "终极振荡器  -  图表 2")

下图显示了美国鹰（AEO）的一个较小的看涨背离信号。随着股票在6月初下跌，终极振荡器跌至超卖水平（<30）。虽然股票在6月底创下新低，但指标仍高于先前的低点和30以上。随后突破间歇高点确认了看涨背离信号。还要注意，AEO在四天内突破了阻力。即使错过了突破的人也有第二次机会，因为股票在8月回落后再次突破了阻力。

![终极振荡器 - 图表 3](../Images/21b96bc25a8916323240d34134fc4377.jpg "终极振荡器 - 图表 3")

## 卖出信号

卖出信号有三个步骤。首先，在指标和证券价格之间形成了一个[看跌背离](/school/doku.php?id=chart_school:glossary_b#bearish_divergence "chart_school:glossary_b")。这意味着终极振荡器形成了一个较低的高点，而价格则形成了一个较高的高点。振荡器中的较低高点显示出较少的上涨动能。其次，看跌背离的高点应该在70以上。这是为了确保价格有些超买或处于相对极端状态。第三，振荡器跌破看跌背离的低点以确认逆转。

![终极振荡器 - 图表 4](../Images/4d9b956466467d4315ee93da89324529.jpg "终极振荡器 - 图表 4")

卡特彼勒在4月下旬大幅上涨，但终极振荡器未能确认这一高点，并形成了一个较低的高点。此外，请注意指标在4月中旬变得超买。随后在4月下旬突破背离低点确认了看跌信号。CAT两天后突破了趋势线支撑，并在6月初急剧下跌。

![终极振荡器 - 图表 5](../Images/02c99b2c56267273954ba3ce6f8630e2.jpg "终极振荡器 - 图表 5")

上图显示了星巴克的一个未经证实的看跌信号，然后是一个经证实的信号。终极振荡器在4月下旬变得超买。随着股票创下新高，指标在5月中旬和6月底再次形成较低高点。一个看跌背离在5月中旬起作用，但指标从未突破其背离低点以确认。在形成更大的背离后，指标在6月底突破了其背离低点，预示了一次相当急剧的下跌。

## 时间框架

终极振荡器可用于日内、日线、周线或月线图表。有时需要调整参数以生成超买或超卖读数，这些是买入和卖出信号的一部分。相对温和的股票或证券可能不会使用默认参数（7,14,28）生成超买或超卖读数。图表分析师需要通过缩短时间框架来增加灵敏度。波音（BA）的图表显示终极振荡器（7,14,28）在六个月内在30和70之间交易。没有超买或超卖读数。将时间框架缩短至（4,8,16）可以增加灵敏度，并生成至少六个超买或超卖读数。对于波动性较高的证券，有时需要延长时间框架以减少灵敏度和信号数量。

![终极振荡器 - 图表 6](../Images/d4b7712722fc5e1f7f14a40cd8f4f3fd.jpg "终极振荡器 - 图表 6")

## 结论

终极振荡器是一个结合了三个不同时间框架的动量振荡器。传统信号来自看涨和看跌的背离，但图表分析师也可以查看实际水平以获取交易偏好。这通常在较长参数和较长趋势下效果更好。例如，当终极振荡器（20,40,80）和价格趋势在50以上时，偏向多头，而在50以下时偏向空头。与所有指标一样，终极振荡器不应单独使用。应该使用辅助指标、[图表模式](/school/doku.php?id=chart_school:chart_analysis:chart_patterns "chart_school:chart_analysis:chart_patterns")和其他分析工具来确认信号。

## 与SharpCharts一起使用

终极振荡器可作为SharpCharts指标使用，可以放置在基础证券的价格图表的上方、下方或后方。将其直接放在价格图表的后面并使用鲜明的颜色使得比较指标运动与价格运动变得容易。用户可以点击“高级选项”旁边的绿色箭头添加水平线或[移动平均线](/school/doku.php?id=chart_school:technical_indicators:moving_averages "chart_school:technical_indicators:moving_averages")。

[![终极振荡器 - 图表 7](../Images/acf0c829ff080e42e2c09c63e63ca02c.jpg "终极振荡器 - 图表 7")](http://stockcharts.com/h-sc/ui?s=IWM&p=D&yr=0&mn=6&dy=0&id=p72157742291&listNum=30&a=223328852 "http://stockcharts.com/h-sc/ui?s=IWM&p=D&yr=0&mn=6&dy=0&id=p72157742291&listNum=30&a=223328852")

![终极振荡器 - SharpCharts](../Images/cc1659c27aae37050a1762de3dbd375c.jpg "终极振荡器 - SharpCharts")

## 建议扫描

### 看涨的长期交叉

此扫描显示终极振荡器上穿50的股票，这是一个看涨的信号。这个扫描只是一个起点。需要进一步的细化和分析。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Ultimate Osc(20,40,80) x 50]
```

### 看跌的长期交叉

这个扫描显示了终极振荡器下穿50的股票，这是一个看涨的信号。这个扫描只是一个起点。需要进一步的细化和分析。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [50 x Ultimate Osc(20,40,80)]
```

有关使用终极振荡器扫描的语法详细信息，请参阅我们[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#ultimate_oscillator_ultimate_osc "http://stockcharts.com/docs/doku.php?id=scans:indicators#ultimate_oscillator_ultimate_osc")中的支持中心。

## 进一步研究

墨菲的书有一个专门讨论动量振荡器及其各种用途的章节。墨菲涵盖了优缺点以及一些特定于商品通道指数的示例。

《技术分析解析》展示了动量指标的基础知识，涵盖了背离、交叉和其他信号。还有两个章节涵盖了具体的动量指标，并提供了大量示例。

| **金融市场技术分析** 约翰·J·墨菲 | **技术分析解析** 马丁·普林 |
| --- | --- |
| [![](../Images/d9fb5f53997f0c87918070e360d1437d.jpg)](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | [![](../Images/907bb9e1dca336b6bedb79166d8efb0e.jpg)](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |

* * *

## 其他资源

### 股票与商品杂志文章

**[拉里·威廉姆斯的终极振荡器](http://stockcharts.com/h-mem/tascredirect.html?artid=\V03\C04\ULTI.PDF "http://stockcharts.com/h-mem/tascredirect.html?artid=\V03\C04\ULTI.PDF")**

1985年7月 - 股票与商品 V. 3:4 (140-141)
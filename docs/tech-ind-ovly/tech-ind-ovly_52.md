# 真实强度指数（TSI）[图表学校]

### 目录

+   [真实强度指数（TSI）](#true_strength_index_tsi)

    +   [计算](#calculation)

    +   [解释](#interpretation)

    +   [中线交叉](#center_line_crossover)

    +   [趋势线](#trend_lines)

    +   [超买/超卖](#overbought_oversold)

    +   [信号线交叉](#signal_line_crossovers)

    +   [结论](#conclusions)

    +   [在SharpCharts中使用](#using_with_sharpcharts)

    +   [建议的扫描](#suggested_scans)

        +   [多头TSI信号线交叉](#bullish_tsi_signal_line_cross)

        +   [空头TSI信号线交叉](#bearish_tsi_signal_line_cross)

    +   [进一步研究](#further_study)

由威廉·布劳（William Blau）开发并在《股票与商品杂志》（Stocks & Commodities Magazine）中介绍的真实强度指数（TSI）是基于价格变化的双重平滑的动量振荡器。尽管需要进行几个步骤来计算，但该指标实际上非常直观。通过平滑价格变化，TSI捕捉价格行动的起伏，形成一条更稳定的线，过滤掉噪音。与大多数动量振荡器一样，技术分析师可以从超买/超卖读数、中线交叉、多头/空头背离和信号线交叉中得出信号。

## 计算

真实强度指数（TSI）可以分为三部分：双重平滑价格变化、双重平滑绝对价格变化和TSI公式。首先，计算一个周期到下一个周期的价格变化。其次，计算这种价格变化的25周期EMA。第三，计算这个25周期EMA的13周期EMA以创建双重平滑。绝对价格变化也使用相同的双重平滑技术。在这些初始计算之后，将双重平滑价格变化除以绝对双重平滑价格变化，并乘以100以将小数点移动两位。

![图表 1](../Images/af49ce62de72393fa4ac88806b1506e8.jpg "图表 1")

```py
Double Smoothed PC
------------------
PC = Current Price minus Prior Price
First Smoothing = 25-period EMA of PC
Second Smoothing = 13-period EMA of 25-period EMA of PC

Double Smoothed Absolute PC
---------------------------
Absolute Price Change |PC| = Absolute Value of Current Price minus Prior Price
First Smoothing = 25-period EMA of |PC|
Second Smoothing = 13-period EMA of 25-period EMA of |PC|

TSI = 100 x (Double Smoothed PC / Double Smoothed Absolute PC)

```

第一部分，即双重平滑价格变化，为TSI设定了正面或负面的基调。当双重平滑价格变化为负时，指标为负，当为正时，指标为正。双重平滑绝对价格变化对指标进行了标准化，并限制了随后振荡器的范围。换句话说，该指标衡量了双重平滑价格变化相对于双重平滑绝对价格变化的情况。一连串的大幅正价格变化导致相对较高的正读数，因为这表示强劲的上行动量。一连串的大幅负价格变化将TSI推入深度负值区域。

![电子表格](../Images/67ed19dfb3a7046f43b7006d84a5d63e.jpg "电子表格")

上表来自Excel电子表格。请注意，计算中使用了[指数移动平均线](/school/doku.php?id=chart_school:technical_indicators:moving_averages "chart_school:technical_indicators:moving_averages")。这些从简单移动平均线开始，然后使用乘数进行计算，这意味着需要额外的历史数据来达到真实值。[点击这里下载此电子表格示例](/school/lib/exe/fetch.php?media=chart_school:technical_indicators_and_overlays:true_strength_index:cs-tsi.xls "chart_school:technical_indicators_and_overlays:true_strength_index:cs-tsi.xls (213 KB)")，并在家里尝试。

## 解释

真实强度指数（TSI）是一个在正负区间波动的振荡器。与许多动量振荡器一样，中线定义了总体偏向。当TSI为正时，多头具有动量优势，当TSI为负时，空头具有优势。与MACD一样，可以应用信号线来识别上升和下降。然而，信号线的交叉频繁，需要进一步结合其他技术进行过滤。图表分析师还可以寻找牛市和熊市背离来预测趋势反转；但是，请记住，在强势趋势中，背离可能会误导。

TSI在某种程度上是独特的，因为它很好地跟踪了基础价格。换句话说，振荡器可以捕捉价格朝一个方向持续移动的情况。振荡器中的峰值和谷值通常与价格中的峰值和谷值相匹配。在这方面，图表分析师可以使用TSI绘制趋势线并标记支撑/阻力水平。然后可以利用线的突破来生成信号。

## 中线交叉

中线交叉是最纯粹的信号。当TSI高于零时，价格变化的双重平滑动量为正，当TSI低于零时为负。当TSI为正时，价格通常上涨，当TSI为负时，价格通常下跌。下面的例子显示了耐克（NKE）在2011年9月转为看涨，因为TSI进入了正区域（绿线）。随着上涨趋势延伸至2012年春季，股票保持看涨。当TSI转为负数并且股票跌破支撑时，耐克转为看跌。

![图表 2](../Images/a8a126b97a26c1b91ed2dc469e0931f2.jpg "图表 2")

## 趋势线

TSI经常产生支撑和阻力水平，图表分析师可以用来识别突破或跌破。下面的例子显示了花旗集团（C）的TSI在三月份建立了支撑位。该指标在四月初跌破支撑，这一跌破预示着五月份的显著下跌。TSI随后在六月反弹，并形成七月的平整整理。这种整理类似于下降旗形态，TSI在七月底突破了趋势线。这一突破预示着进一步的强势到八月份。

![图表 3](../Images/91bdaa57cb8ccc8058058acc22a97488.jpg "图表 3")

## 超买/超卖

对于真实强度指数的超买和超卖水平会根据证券的波动性和指标的周期设置而变化。对于波动性低的股票，如公用事业股，TSI 范围会较小。对于波动性高的股票，如生物技术股，TSI 范围会较大。使用较短的平滑时间段将导致范围更广、指标线更波动。较长的时间段将导致范围更小、线条更平滑。这是经典的技术分析权衡。图表分析师使用较短的周期可以获得更快的信号和更少的滞后，但这是以更多的虚假信号和震荡为代价。较长的周期减少了虚假信号，但这些信号伴随着更多的滞后和较差的风险收益比。

![图表 4](../Images/5225712091cb35513a8ec51340a0043b.jpg "图表 4")

上图显示了纳斯达克 100 ETF（QQQ）使用两个不同时间框架的 TSI。上部指标窗口显示了 TSI (40,20,7) 在 -20 和 +44 之间波动，20/-20 标记为超买/超卖。下部窗口显示了 TSI (13,7,7) 在 +78 和 -69 之间波动，50/-50 标记为超买/超卖。请注意下部窗口中的 TSI 比上部窗口中的 TSI 更波动。此外，请注意，更敏感的 TSI 产生了两次超卖读数和四次超买读数（蓝色箭头）。超买和超卖并不是即将发生逆转的信号。它们只是表明价格上涨或下跌过快。图表分析师必须等待确认信号以表明实际逆转。蓝色线标记了支撑和阻力，使用趋势线、峰值或谷底。一旦出现超买或超卖读数，图表分析师可以使用这些线条来定义价格逆转。这不会消除虚假信号，但会减少错误信号。

## 信号线交叉

TSI 设置中的最后一个参数是信号线，它只是 TSI 的指数移动平均值。信号线交叉是迄今为止最常见的信号。这意味着会有好的、坏的和丑陋的信号。为了减少信号和噪音，图表分析师应考虑增加 TSI 或价格图表设置的设置。下面的示例显示了使用周线图的 TSI(40,20,10)。这意味着信号线是 TSI 的 10 期 EMA。在这张图上，TSI 从 2007 年 4 月到 2012 年 7 月至少与信号线交叉了 12 次。

![图表 5](../Images/3426f468c310fc4ea7535754e4b96907.jpg "图表 5")

## 结论

真实强度指数（TSI）是一种基于双重平滑价格变化的独特指标。价格变化代表了动量的真实形式。通过两个指数移动平均线的双重平滑，降低了噪音，并产生了一个相当好地跟踪价格的振荡器。除了通常的振荡器信号外，图表分析师通常可以直接在TSI上绘制趋势线、支撑线和阻力线。然后可以利用这些线来生成基于突破和跌破的信号。与所有指标一样，TSI信号应该与其他指标和分析技术一起确认。

## 使用SharpCharts

真实强度指数（TSI）可作为SharpCharts的指标使用。一旦选择，用户可以将指标放置在基础价格图的上方、下方或后方。将TSI直接放在价格图后面，突出了相对于基础证券价格走势的波动。用户可以应用“高级选项”添加水平线以设置超买和超卖水平。调整参数框中的数字将更改设置。[点击这里](http://stockcharts.com/h-sc/ui?s=$COMPQ&p=D&yr=0&mn=6&dy=0&id=p28704616394&a=276577901 "http://stockcharts.com/h-sc/ui?s=$COMPQ&p=D&yr=0&mn=6&dy=0&id=p28704616394&a=276577901")查看TSI实际运行的实时示例。

![图表 6](../Images/6f820f9a1b626cab77c7810cb9ecbb19.jpg "图表 6")

![图表 7](../Images/02782217604d8aebb9dab43bcb46256d.jpg "图表 7")

## 建议扫描

### 多头TSI信号线穿越

这个扫描显示了TSI处于正值领域的股票。当TSI穿过其信号线时，将触发一个多头信号。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [TSI(40,20,10) > 0]
AND [TSI(40,20,10) x TSI Signal(40,20,10)]

```

### 空头TSI信号线穿越

这个扫描显示了TSI处于负值领域的股票。当TSI穿过其信号线时，将触发一个空头信号。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [TSI(40,20,10) < 0]
AND [TSI Signal(40,20,10) x TSI(40,20,10)]
```

欲了解有关TSI扫描的语法细节，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#true_strength_index "http://stockcharts.com/docs/doku.php?id=scans:indicators#true_strength_index")在支持中心。

## 进一步研究

《金融市场技术分析》一书专门讨论了动量振荡器及其各种用途。墨菲涵盖了涨跌率的利弊以及一些特定于变化率的示例。普林的书通过涵盖背离、交叉和其他信号来展示动量指标的基础知识。还有两章涵盖了具体的动量指标，并提供了大量示例。

| **金融市场技术分析** 约翰·J·墨菲 | **马丁·普林解读技术分析** 马丁·普林 |
| --- | --- |
| [![](../Images/d9fb5f53997f0c87918070e360d1437d.jpg)](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | [![](../Images/907bb9e1dca336b6bedb79166d8efb0e.jpg)](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |

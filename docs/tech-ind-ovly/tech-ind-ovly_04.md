# 一目均衡云 [图表学校]

### 目录

+   [一目均衡云](#ichimoku_clouds)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [分析云图](#analyzing_the_cloud)

    +   [趋势和信号](#trend_and_signals)

    +   [转换-基准线信号](#conversion-base_line_signals)

    +   [价格-基准线信号](#price-base_line_signals)

    +   [信号摘要](#signal_summary)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [建议扫描](#suggested_scans)

        +   [一目均衡云上涨趋势，收盘价高于基准线](#ichimoku_uptrend_with_close_above_base_line)

        +   [一目均衡云下跌趋势，收盘价低于基准线](#ichimoku_downtrend_with_close_below_base_line)

    +   [进一步研究](#further_study)

    +   [额外资源](#additional_resources)

        +   [股票与商品杂志文章](#stocks_commodities_magazine_articles)

## 介绍

一目均衡云，也被称为一目均衡表，是一种多功能指标，定义支撑和阻力，确定趋势方向，衡量动量并提供交易信号。一目均衡表翻译为“一目平衡图”。通过一目之览，图表分析师可以确定趋势并寻找该趋势内的潜在信号。该指标由记者星野豪一开发，并于1969年出版在他的著作中。尽管一目均衡云在价格图上看起来复杂，但实际上是一个非常易用的直观指标。毕竟，它是由一位记者而不是火箭科学家创造的！此外，概念易于理解，信号明确。

## 计算

一目均衡云中的五个图表中的四个是基于一定时间内的高低平均值。例如，第一个图表只是9天高点和9天低点的平均值。在计算机普及之前，计算这种高低平均值可能比计算9天[移动平均线](/school/doku.php?id=chart_school:technical_indicators:moving_averages "chart_school:technical_indicators:moving_averages")更容易。一目均衡云由五个图表组成：

```py
Tenkan-sen (Conversion Line): (9-period high + 9-period low)/2))

The default setting is 9 periods and can be adjusted. On a daily chart, this line is the midpoint of the 9-day high-low range, 
which is almost two weeks.  
```

```py
Kijun-sen (Base Line): (26-period high + 26-period low)/2))

The default setting is 26 periods and can be adjusted. On a daily chart, this line is the midpoint of the 26-day high-low range, which is almost one month).  
```

```py
Senkou Span A (Leading Span A): (Conversion Line + Base Line)/2))

This is the midpoint between the Conversion Line and the Base Line. The Leading Span A forms one of the two Cloud boundaries. It is referred to as "Leading" because it is plotted 26 periods in the future and forms the faster Cloud boundary. 
```

```py
Senkou Span B (Leading Span B): (52-period high + 52-period low)/2))

On the daily chart, this line is the midpoint of the 52-day high-low range, which is a little less than 3 months. The default calculation setting is 52 periods, but can be adjusted. This value is plotted 26 periods in the future and forms the slower Cloud boundary.
```

```py
Chikou Span (Lagging Span): Close plotted 26 days in the past

The default setting is 26 periods, but can be adjusted. 

```

本教程在解释各种图表时将使用英文等效词。下表显示了道琼斯工业指数与一目均衡云图的情况。转换线（蓝色）是最快、最敏感的线。请注意，它最接近价格走势。基准线（红色）落后于更快的转换线，但在很大程度上跟随价格走势。转换线和基准线之间的关系类似于9日移动平均线和26日移动平均线之间的关系。9日线更快，更紧密地跟随价格走势。26日线较慢，落后于9日线。顺便提一下，注意到9和26是用来计算[MACD](/school/doku.php?id=chart_school:technical_indicators:moving_average_convergence_divergence_macd "chart_school:technical_indicators:moving_average_convergence_divergence_macd")的相同周期。

![图表1 - 一目云图](../Images/bdd79746a4c3180489cb85237f053f56.jpg "图表1 - 一目云图")

## 分析云端

云端（云）是一目了然的一种特征，出现在一目云图中。主导跨度A（绿色）和主导跨度B（红色）形成云端。主导跨度A是转换线和基准线的平均值。由于转换线和基准线分别计算了9和26个周期，绿色云端边界比红色云端边界移动更快，后者是52天高点和52天低点的平均值。这与移动平均线的原理相同。较短的移动平均线比较长的移动平均线更敏感且更快。

有两种方法可以使用云端来识别整体趋势。**首先，当价格在云端之上时，趋势为上升，当价格在云端之下时，趋势为下降，当价格在云端内时，趋势为平稳。** 其次，当主导跨度A（绿色云线）上升并在主导跨度B（红色云线）之上时，上升趋势得到加强。这种情况产生了一个***绿色云端***。相反，当主导跨度A（绿色云线）下降并在主导跨度B（红色云线）之下时，下降趋势得到加强。这种情况产生了一个***红色云端***。由于云端向前偏移26天，它还提供了未来支撑或阻力的预览。

图表2显示了IBM关注上升趋势和云端。首先，请注意IBM从6月到1月处于上升趋势，因为它交易在云端之上。其次，请注意云端在7月、10月初和11月初提供支撑。第三，请注意云端如何提供未来[阻力](/school/doku.php?id=chart_school:chart_analysis:support_and_resistance "chart_school:chart_analysis:support_and_resistance")的预览。**记住，整个云端向前偏移26天。** 这意味着它比最后一个价格点提前26天绘制，以指示未来的支撑或阻力。

![图表2 - 一目云图](../Images/fac386b1c584418089980bfb7544819e.jpg "图表2 - 一目云图")

图表3显示了波音（BA）关注下降趋势和云端。当波音在6月突破云端支撑时，趋势发生了变化。当主导跨度A（绿色）在7月移动到主导跨度B（红色）之下时，云端从绿色变为红色。云端突破代表了第一个趋势变化信号，而颜色变化代表了第二个趋势变化信号。请注意云端随后如何在8月和1月充当阻力。

![图表3 - 一目云图](../Images/61304952cefc74e631c48cc9a11e20e6.jpg "图表3 - 一目云图")

## 趋势和信号

价格、转换线和基准线用于识别更快、更频繁的信号。重要的是要记住，当价格在云层上方且云层为绿色时，看涨信号得到加强。当价格在云层下方且云层为红色时，看跌信号得到加强。换句话说，当更大的趋势向上时（价格在绿色云层上方），更倾向于看涨信号，而当更大的趋势向下时（价格在红色云层下方），更倾向于看跌信号。这就是沿着更大趋势方向交易的本质。与现有趋势相反的信号被认为较弱。在长期下降趋势中的短期看涨信号和在长期上升趋势中的短期看跌信号较不稳健。

## 转换线-基准线信号

图表 4 显示金伯利-克拉克（KMB）在上升趋势中产生了两个看涨信号。首先，趋势向上，因为股票交易在云层上方，而云层是绿色的。转换线在6月底的几天内下跌到基准线以下，以启动设置。当转换线在7月份再次移回基准线上方时，触发了一个看涨交叉信号。第二个信号发生在股票朝着云层[支撑](/school/doku.php?id=chart_school:chart_analysis:support_and_resistance "chart_school:chart_analysis:support_and_resistance")移动时。转换线在9月份下移到基准线以下，以启动设置。当转换线在10月份再次移回基准线上方时，触发了另一个看涨交叉信号。有时很难在价格图表上确定确切的转换线和基准线水平。作为参考，这些数字显示在每个 Sharpchart 的左上角。截至1月8日收盘，转换线为62.62（蓝色），基准线为63.71（红色）。

![图表 6 - 一目云](../Images/75f23a7f8c1b45d9596fa3f4a320d207.jpg "图表 6 - 一目云")

图表 5 显示 AT&T（T）在下降趋势中产生了一个看跌信号。首先，趋势向下，因为股票交易在云层下方，而云层是红色的。在8月份的横盘之后，转换线移动到基准线上方以启动设置。这并没有持续很久，因为转换线在9月15日再次移回基准线以下，触发了一个看跌信号。

![图表 5 - 一目云](../Images/08e655546f0193f13ff133d21245f342.jpg "图表 5 - 一目云")

## 价格-基准线信号

图表 6 显示迪士尼在上升趋势中产生了两个看涨信号。随着股票交易在绿色云层上方，价格下跌到基准线（红色）以下以启动设置。这一举动代表了更大上升趋势中的短期超卖情况。当价格再次上涨到基准线以上时，结束了回调并触发了看涨信号。

![图表 6 - 一目云](../Images/52ddebaf763774112fe5e84ddb3c40a3.jpg "图表 6 - 一目云")

图表 7 显示了DR Horton（DHI）在下降趋势中产生了两个看跌信号。随着股价交易在红色云层以下，价格反弹至基准线（红色）以上以启动设置。这一举动在更大的下降趋势中创造了一个短期超买情况。当价格再次下跌至基准线以下时，反弹结束，触发了看跌信号。

![图表 7 - 一目云](../Images/51d20fcb698fb1c4bffd0f451487fcec.jpg "图表 7 - 一目云")

## 信号总结

本文介绍了从一目云图中得出的四个看涨信号和四个看跌信号。趋势跟踪信号关注云层，而动量信号关注转换线和基准线。一般来说，云层之上或之下的运动定义了整体趋势。在这个趋势中，随着趋势的起伏，云层的颜色也会发生变化。一旦趋势被确认，转换线和基准线的作用类似于MACD用于信号生成。最后，简单的价格运动在基准线之上或之下可以用于生成信号。

**看涨信号：**

+   价格上涨至云层以上（趋势）

+   云从红色变为绿色（趋势中的潮汐）

+   价格上涨至基准线以上（动量）

+   转换线上穿基准线（动量）

**看跌信号：**

+   价格下跌至云层以下（趋势）

+   云从绿色变为红色（趋势中的潮汐）

+   价格下跌至基准线以下（动量）

+   转换线下穿基准线（动量）

## 结论

一目云是一个设计用于产生清晰信号的综合指标。图表分析师可以首先通过使用云来确定趋势。一旦趋势确立，可以使用价格图、转换线和基准线确定适当的信号。经典信号是寻找转换线穿过基准线。虽然这个信号可能有效，但在强势趋势中可能很少见。通过寻找价格穿过基准线（甚至是转换线）可以找到更多信号。

在寻找信号时，重要的是要朝着更大趋势的方向寻找。在上升趋势中，云提供支撑，交易者在价格接近云层时应当警惕看涨信号，无论是在回调还是整理时。相反，在更大的下降趋势中，交易者应当在价格接近云层时警惕看跌信号，无论是在超卖反弹还是整理时。

一目云也可以与其他指标结合使用。交易者可以使用云来确定趋势，然后使用经典的动量振荡器来识别超买或超卖条件。[点击这里](http://stockcharts.com/h-sc/ui?s=IWM&p=D&yr=0&mn=6&dy=0&id=p03667051915&listNum=30&a=193876371 "http://stockcharts.com/h-sc/ui?s=IWM&p=D&yr=0&mn=6&dy=0&id=p03667051915&listNum=30&a=193876371") 查看使用一目云的实时示例。

## 使用SharpCharts

通过在“叠加”下拉框中选择它作为指标，SharpCharts 上提供了一种名为一目云的指标。默认设置为转换线为9，基准线为26，领先跨度 B 为52。领先跨度 A 基于转换线和基准线。基准线的数字（26）也用于将云向前移动（26 天）。这些数字可以根据个人的交易和投资风格进行调整。有时在增加基准线时需要向图表添加额外的条形，这也会增加云的前进运动。

![](../Images/9bd54a62eb5c151943fa68cc71c22b01.jpg)

[![图表 8 - 一目云](../Images/8ddae703d19f58f7adbd98a42e637b2e.jpg "图表 8 - 一目云")](http://stockcharts.com/h-sc/ui?s=IWM&p=D&yr=0&mn=6&dy=0&id=p03667051915&listNum=30&a=193876371 "http://stockcharts.com/h-sc/ui?s=IWM&p=D&yr=0&mn=6&dy=0&id=p03667051915&listNum=30&a=193876371")

## 建议的扫描

### 一目云上升趋势，收盘价高于基准线

此扫描从至少在过去60天内平均价格为$10且每日交易量为100,000的股票基础开始。只要 Span A 高于 Span B 且收盘价高于 Span B，股票就被归类为上升趋势。在此上升趋势中，当价格上涨到基准线以上时，就会出现突破。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily Close > Daily Ichimoku Span B(9,26,52)] 
AND [Daily Ichimoku Span A(9,26,52) > Daily Ichimoku Span B(9,26,52)] 
AND [Daily Close x Daily Ichimoku Base Line(9,26,52)]
```

### 一目云下降趋势，收盘价低于基准线

此扫描从至少在过去60天内平均价格为$10且每日交易量为100,000的股票基础开始。只要 Span A 低于 Span B 且收盘价低于 Span A，股票就被归类为下降趋势。当价格跌破基准线时，这种下降趋势可能开始延续。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily Close < Daily Ichimoku Span A(9,26,52)] 
AND [Daily Ichimoku Span A(9,26,52) < Daily Ichimoku Span B(9,26,52)] 
AND [Daily Ichimoku Base Line(9,26,52) x Daily Close]
```

有关用于一目云扫描的语法详细信息，请参阅我们支持中心的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#ichimoku_cloud "http://stockcharts.com/docs/doku.php?id=scans:indicators#ichimoku_cloud")。

## 进一步研究

| **一目图** 尼科尔·埃利奥特 |
| --- |
| [![](../Images/0f3b7b6868a2ab78a4d698e4336b0a65.jpg)](http://store.stockcharts.com/products/ichimoku-charts-an-introduction-to-ichimoku-kinko-clouds "http://store.stockcharts.com/products/ichimoku-charts-an-introduction-to-ichimoku-kinko-clouds") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/ichimoku-charts-an-introduction-to-ichimoku-kinko-clouds "http://store.stockcharts.com/products/ichimoku-charts-an-introduction-to-ichimoku-kinko-clouds") |

* * *

## 其他资源

### 股票与商品杂志文章

**[一目图 由村中健](http://stockcharts.com/h-mem/tascredirect.html?artid=\V18\C10\088ICH.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V18\C10\088ICH.pdf")**

2000年9月 - 股票与商品 V. 18:10 (22-30)

**[Nicole Elliott的一目均衡图表](http://stockcharts.com/h-mem/tascredirect.html?artid=\V25\C09\172ELLT.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V25\C09\172ELLT.pdf")**

2007年8月 - 《股票与商品》V. 25:9 (34-36)

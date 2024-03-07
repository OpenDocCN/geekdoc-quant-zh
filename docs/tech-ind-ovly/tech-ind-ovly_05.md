# 考夫曼自适应移动平均线（KAMA）[ChartSchool]

### 目录

+   [考夫曼自适应移动平均线（KAMA）](#kaufman_s_adaptive_moving_average_kama)

    +   [介绍](#introduction)

    +   [计算](#calculation)

        +   [效率比率（ER）](#efficiency_ratio_er)

        +   [平滑常数（SC）](#smoothing_constant_sc)

        +   [KAMA](#kama)

    +   [计算示例/图表](#calculation_example_chart)

    +   [用法和信号](#usage_and_signals)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [建议扫描](#suggested_scans)

        +   [价格上穿KAMA时的总体上升趋势](#overall_uptrend_with_price_crossing_above_kama)

        +   [价格下穿KAMA时的总体下降趋势](#overall_downtrend_with_price_crossing_below_kama)

    +   [进一步研究](#further_study)

    +   [额外资源](#additional_resources)

        +   [股票与商品杂志文章](#stocks_commodities_magazine_articles)

## 介绍

由佩里·考夫曼（Perry Kaufman）开发，考夫曼自适应移动平均线（KAMA）是一种移动平均线，旨在考虑市场噪音或波动性。当价格波动相对较小且噪音较低时，KAMA将紧密跟随价格。当价格波动加大并且距离价格较远时，KAMA将进行调整。这种趋势跟踪指标可用于识别总体趋势，时间转折点和过滤价格波动。

## 计算

计算考夫曼自适应移动平均线需要几个步骤。让我们首先从佩里·考夫曼推荐的设置开始：KAMA(10,2,30)。

+   10是效率比率（ER）的周期数。

+   2是最快EMA常数的周期数。

+   30是最慢EMA常数的周期数。

在计算KAMA之前，我们需要计算效率比率（ER）和平滑常数（SC）。将公式分解成易于理解的小块有助于理解指标背后的方法论。请注意，ABS代表绝对值。

### 效率比率（ER）

ER基本上是根据日常波动调整的价格变化。

```py
ER = Change/Volatility

Change = ABS(Close - Close (10 periods ago))

Volatility = Sum10(ABS(Close - Prior Close))

Volatility is the sum of the absolute value of the last ten price changes (Close - Prior Close). 

```

从统计学角度来看，效率比率告诉我们价格变化的分形效率。ER在1和0之间波动，但这些极端情况是例外，而不是规范。如果价格连续上涨10个周期或下跌10个周期，ER将为1。如果价格在10个周期内保持不变，ER将为零。

### 平滑常数（SC）

平滑常数使用ER和基于指数移动平均的两个平滑常数。

```py
SC = [ER x (fastest SC - slowest SC) + slowest SC]2

SC = [ER x (2/(2+1) - 2/(30+1)) + 2/(30+1)]2

```

正如您可能已经注意到的，平滑常数在其公式中使用了指数移动平均的平滑常数。（2/30+1）是30周期EMA的平滑常数。最快的SC是较短EMA（2周期）的平滑常数。最慢的SC是最慢EMA（30周期）的平滑常数。请注意，结尾处的“2”是为了平方该方程。

### KAMA

有了效率比率（ER）和平滑常数（SC），我们现在可以计算考夫曼自适应移动平均线（KAMA）。由于我们需要一个初始值来开始计算，第一个KAMA只是一个简单移动平均线。以下计算基于以下公式。

```py
Current KAMA = Prior KAMA + SC x (Price - Prior KAMA)

```

## 计算示例/图表

下面的图片显示了用于计算KAMA和相应QQQ图表的Excel电子表格的截图。

![KAMA Excel](../Images/441992ab2bda308626f77c5870c65118.jpg "KAMA Excel")

![KAMA 图表](../Images/7a8955b0c604f97aa6390ce96636ba62.jpg "KAMA Chart")

[点击这里下载](/school/lib/exe/fetch.php?media=chart_school:technical_indicators_and_overlays:kaufman_s_adaptive_moving_average:cs-kama.xls "chart_school:technical_indicators_and_overlays:kaufman_s_adaptive_moving_average:cs-kama.xls (32 KB)") 这个电子表格示例。

## 使用和信号

图表分析师可以像使用其他趋势跟踪指标（如移动平均线）一样使用KAMA。图表分析师可以寻找价格交叉、方向变化和滤波信号。

首先，KAMA上下交叉表示价格方向变化。与任何移动平均线一样，简单的交叉系统会产生大量信号和大量虚假信号。图表分析师可以通过将价格或时间过滤器应用于交叉来减少虚假信号。可以要求价格保持交叉一定数量的天数，或要求交叉超过KAMA一定百分比。

![KAMA 图表](../Images/27b5366a3fad49ee504fbbf5d0103a8d.jpg "KAMA Chart")

其次，图表分析师可以利用KAMA的方向来定义证券的整体趋势。这可能需要调整参数以进一步平滑指标。图表分析师可以更改中间参数，即最快的EMA常数，以平滑KAMA并寻找方向变化。只要KAMA下降并形成较低低点，趋势就是向下的。只要KAMA上升并形成较高高点，趋势就是向上的。下面的Kroger示例显示了KAMA（10,5,30）从12月到3月的陡峭上升趋势，以及从5月到8月的较缓上升趋势。

![KAMA 图表](../Images/49e20a05745a02e78b0122448294c476.jpg "KAMA Chart")

最后，图表分析师可以结合信号和技术。图表分析师可以使用长期KAMA来定义更大的趋势，使用短期KAMA进行交易信号。例如，KAMA（10,5,30）可以用作趋势过滤器，在上升时被视为看涨。一旦看涨，图表分析师可以寻找价格上穿KAMA（10,2,30）时的看涨交叉。下面的示例显示了MMM在长期KAMA上升并在12月、1月和2月出现看涨交叉。长期KAMA在4月转为下跌，并在5月、6月和7月出现看跌交叉。

![KAMA 图表](../Images/96012cd0fb5c720af03617b85b9dd1a5.jpg "KAMA Chart")

## 使用SharpCharts

KAMA可以作为SharpCharts工作台中的指标叠加显示。一旦选择了默认设置，参数框将自动显示在图表中，图表分析师可以根据自己的分析需求更改这些参数。第一个参数是效率比率，图表分析师应该避免增加这个数字。相反，图表分析师可以减少它以增加灵敏度。希望平滑KAMA以进行长期趋势分析的图表分析师可以逐步增加中间参数。即使差异只有3，KAMA(10,5,30)比KAMA(10,2,30)平滑得多。

[![KAMA图表](../Images/859f469ec594ba39c2a6f640efe2fe84.jpg "KAMA图表")](http://stockcharts.com/h-sc/ui?s=SPY&p=D&yr=0&mn=6&dy=0&id=p71426978293 "http://stockcharts.com/h-sc/ui?s=SPY&p=D&yr=0&mn=6&dy=0&id=p71426978293")

## 建议扫描

### 价格上涨趋势，价格上穿KAMA

这个扫描从平均每日交易100,000股并且平均收盘价高于10的股票开始。当交易在长期KAMA(10,5,30)上方时存在上升趋势。当价格移动到短期KAMA(10,2,30)上方时，买入信号出现。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [KAMA(10,5,30) >  Daily SMA(50,KAMA(10,5,30))]
AND [Daily Close crosses KAMA(10,2,30)] 
```

### 价格跌破KAMA，整体下降趋势

这个扫描从平均每日交易100,000股并且平均收盘价高于10的股票开始。当交易在长期KAMA(10,5,30)下方时存在下降趋势。当价格移动到短期KAMA(10,2,30)下方时，卖出信号出现。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [KAMA(10,5,30) <  Daily SMA(50,KAMA(10,5,30))]
AND [KAMA(10,2,30) crosses Daily Close] 
```

有关KAMA扫描的语法详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#kaufman_s_adaptive_moving_average_kama "http://stockcharts.com/docs/doku.php?id=scans:indicators#kaufman_s_adaptive_moving_average_kama")在支持中心。

## 进一步研究

从作者那里，下面的书提供了关于指标、程序、算法和系统的详细信息，包括有关KAMA和其他移动平均系统的详细信息。

| **交易系统和方法** Perry Kaufman |
| --- |
| [![](../Images/b7ad49e1f866a868a5497661e81092f0.jpg)](https://store.stockcharts.com/products/new-trading-systems-and-methods-5th-edition "https://store.stockcharts.com/products/new-trading-systems-and-methods-5th-edition") |
| [![buynowbuttone.jpg](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "buynowbuttone.jpg")](https://store.stockcharts.com/products/new-trading-systems-and-methods-5th-edition "https://store.stockcharts.com/products/new-trading-systems-and-methods-5th-edition") |

## 其他资源

### 股票与商品杂志文章

**[Perry Kaufman与Thom Hartle的访谈](https://technical.traders.com/archive/articlefinal.asp?file=\V13\C06\SIDEADA.pdf "https://technical.traders.com/archive/articlefinal.asp?file=\V13\C06\SIDEADA.pdf")**

1995年5月 - 股票与商品

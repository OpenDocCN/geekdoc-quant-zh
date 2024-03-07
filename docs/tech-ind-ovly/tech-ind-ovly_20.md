# 布林带宽度 [ChartSchool]

### 目录

+   [布林带宽度](#bollinger_bandwidth)

    +   [介绍](#introduction)

    +   [SharpCharts 计算](#sharpcharts_calculation)

    +   [定义窄度](#defining_narrowness)

    +   [信号：挤压](#signalthe_squeeze)

    +   [摘要](#summary)

    +   [与 SharpCharts 一起使用](#using_with_sharpcharts)

    +   [与 MarketCarpets 一起使用](#using_with_marketcarpets)

    +   [建议的扫描](#suggested_scans)

        +   [布林带突破](#bollinger_band_breakout)

## 介绍

布林带宽度是从[布林带](/school/doku.php?id=chart_school:technical_indicators:bollinger_bands "chart_school:technical_indicators:bollinger_bands")衍生出的指标。在他的书《布林带上的布林格》中，约翰·布林格将布林带宽度称为可以从布林带中衍生出的两个指标之一。另一个指标是%B。

带宽度衡量上带和下带之间的百分比差异。随着布林带变窄，带宽度减小，随着布林带扩大，带宽度增加。由于布林带基于标准差，带宽度的下降反映了波动性的减少，而带宽度的上升反映了波动性的增加。

## SharpCharts 计算

```py
( (Upper Band - Lower Band) / Middle Band) * 100

```

布林带由一个中间带和两个外部带组成。中间带通常设置为20个周期的[简单移动平均](/school/doku.php?id=chart_school:technical_indicators:moving_averages "chart_school:technical_indicators:moving_averages")。外部带通常设置为中间带上下2个标准差。设置可以根据特定证券或交易风格的特征进行调整。

在计算带宽时，第一步是从上带的值中减去下带的值。这显示了绝对差异。然后将此差异除以中间带，这将使值标准化。然后可以在不同时间段内或与其他证券的带宽值进行比较。

![图表 1](img/8bd0aeb209a3a38dfff98b8965105e8a.jpg "图表 1")

上图显示了纳斯达克100 ETF（QQQ）的布林带、带宽度和标准差。请注意带宽度如何跟踪标准差（波动性）。两者一起上升和下降。下图显示了一个带有计算示例的电子表格。

![电子表格 1](img/419fa826e8678c1f564a5b12dcf646f4.jpg "电子表格 1")

## 定义窄度

窄带宽是相对的。带宽值应该相对于一段时间内先前的带宽值进行评估。重要的是要获得一个良好的回顾期，以定义特定ETF、指数或股票的带宽范围。例如，八到十二个月的图表将显示一段重要时间内的带宽高点和低点。当带宽接近此范围的低点时被认为是窄的，当接近高点时被认为是宽的。

![图表 2](img/101cfde779c6dc426a5112525e9d7919.jpg "图表 2")

![图表 3](img/c2ea79b827cdab1e1534f6b739ab70f8.jpg "图表 3")

低波动性证券的BandWidth值将低于高波动性证券。例如，Utilities SPDR（XLU）代表公用事业股票，其波动性相对较低。Technology SPDR（XLK）代表科技股票，其波动性相对较高。由于低波动性，XLU的BandWidth值将始终低于XLK。XLU的BandWidth 200日移动平均值低于5，而XLK的BandWidth 200日移动平均值高于7。

## 信号：挤压

Bollinger BandWidth最为人所知的是用于识别“挤压”现象。当波动性降至非常低的水平时，就会出现狭窄的带状。上下带基于标准偏差，这是波动性的一种度量。当价格趋于平稳或在相对狭窄的范围内波动时，带状变窄。理论认为，低波动性期后将会出现高波动性期。相对较窄的BandWidth（也称为挤压）可能预示着重大上涨或下跌。挤压后，价格激增并随后带状突破信号标志着新趋势的开始。新的上涨始于挤压和随后突破上带。新的下跌始于挤压和随后突破下带。

图表2显示了阿拉斯加航空（ALK）在6月中旬出现的挤压现象。在4月至5月下跌后，ALK在6月初稳定下来，因为Bollinger带变窄。BandWidth下降到10以下，使6月中旬的挤压现象出现。请记住，10指的是10%。换句话说，带的宽度等于中间带的10%。尽管这个水平看起来很高，但对于ALK来说实际上相当低。股价在15-16左右时，BandWidth低于10%，是一年多来的最低水平。随着股价突破上带，股票开始大幅上涨。

![图表 4](img/6c133691e15036f8ec526db70662778d.jpg "图表 4")

图表3显示了Aeropostale（ARO）出现了几次挤压现象。在指标窗口中添加了一条水平线。这条线标记为8，根据历史范围被认为相对较低。BandWidth指标提醒交易者准备在8月中旬进行交易。股票随后突破上带并在整个9月持续上涨。上涨在9月底停滞，BandWidth再次收窄在10月。请注意，BandWidth下降到低于8月份设定的低点，然后趋于平稳。随后在10月底突破下轨的信号触发了一个熊市信号。

![图表 5](img/3a533d1f5b5762881484c97d9a00b5dd.jpg "图表 5")

挤压也可以应用于周线图或更长的时间框架。周线时间框架上的波动性和带宽通常比日线时间框架上更高。这是因为在更长的时间框架上可以预期更大的价格波动。图4显示了 Barrick Gold (ABX) 在2006年和2007年持续整理。随着整理变窄并形成三角形，布林带收缩，带宽在2007年1月下降到10以下。请注意，随着整理的延伸，带宽保持在低水平。在2007年7月突破时触发了一个看涨信号。随着价格朝一个方向急剧变动，布林带也扩大，带宽也上升。

![图表 6](img/012e4c92bffebf8d406af9e3d3a12955.jpg "图表 6")

图5显示了 Honeywell (HON) 在50-55区域的扩展交易范围。5月份价格上涨到上轨，但没有突破信号。相反，HON 明显跌破下轨，于2007年6月触发了一个看跌信号。

![图表 7](img/729369505c25ce3c7aa56f3ed9264230.jpg "图表 7")

## 总结

带宽指标可用于识别布林带挤压。这警示图表分析师准备行动，但方向取决于随后的带突破。挤压后上轨突破是看涨的，而下轨突破是看跌的。但要小心虚假突破。有时第一次突破未能保持，价格会反转。强劲的突破保持并且很少回头。上涨突破后立即回调应作为警告。

## 使用 SharpCharts

带宽指标可以在 SharpCharts 的指标列表中找到。默认参数（20,2）基于布林带的默认参数。这些可以相应地更改。20代表简单移动平均。2代表上下轨的标准差数。带宽可以放置在价格图的上方、下方或后面。[点击这里](http://stockcharts.com/h-sc/ui?s=SPY&p=D&yr=0&mn=6&dy=0&id=p38029592805&listNum=30&a=195096097 "http://stockcharts.com/h-sc/ui?s=SPY&p=D&yr=0&mn=6&dy=0&id=p38029592805&listNum=30&a=195096097") 查看带宽的实时示例。

![图表 8](img/224833de27c84ea95f9553b76b87112a.jpg "图表 8")

## 使用 MarketCarpets

标准化的布林带宽显示在市场地毯中，这使用户可以比较多个证券的带宽。以[S&P行业市场地毯](http://stockcharts.com/freecharts/carpet.html "http://stockcharts.com/freecharts/carpet.html")为例，选择布林带宽，然后点击三角形的Δ图标查看绝对水平。有阴影的Δ图标显示百分比变化。白色的Δ图标显示绝对水平。绿色框显示带宽相对较宽的股票。浅色框显示带宽相对较窄的股票。在市场地毯右下方显示带宽最窄的股票列表（底部5）。点击名称可查看上方的小图表。用户可以通过点击行业标题（例如技术）来深入了解各个行业。有九个行业和每个行业列出的底部5个股票，用户可以快速查看相对带宽较窄的45只股票。

![图表 9](img/355729f80d9c152bfee8122a2d3e8982.jpg "图表 9")

## 建议的扫描

### 布林带突破

此扫描显示了布林带在收缩5天或更长时间后迅速扩张的股票。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily BB Width(20,2) > Yesterday's max(5, BB Width(20,2)) * 2]
```

有关用于带宽扫描的语法的更多详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#bollinger_band_width_bb_width "http://stockcharts.com/docs/doku.php?id=scans:indicators#bollinger_band_width_bb_width")在支持中心。

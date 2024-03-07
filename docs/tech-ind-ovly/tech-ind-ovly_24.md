# 查德趋势仪表盘（CTM）[ChartSchool]

### 目录

+   [查德趋势仪表盘（CTM）](#chande_trend_meter_ctm)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [解释](#interpretation)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [建议的扫描](#suggested_scans)

        +   [CTM在大量交易量下突破60](#ctm_crosses_above_60_on_heavy_volume)

        +   [持续高CTM的股票](#stocks_with_consistently_high_ctm)

## 介绍

查德趋势仪表盘（CTM），由图沙尔·查德（Tushar Chande）开发，根据涵盖六个不同时间框架的几种不同技术指标为股票或其他证券分配一个数值分数。将所有这些技术信息压缩成一个数字，提供了一种简单的方法来识别给定证券的趋势强度。

## 计算

查德趋势仪表盘的计算基于以下技术指标：

+   高、低和收盘价相对于四个不同时间框架（20天、50天、75天和100天）的[布林带](/school/doku.php?id=chart_school:technical_indicators:bollinger_bands "chart_school:technical_indicators:bollinger_bands")的位置

+   过去100天相对于[标准偏差](/school/doku.php?id=chart_school:technical_indicators:standard_deviation_volatility "chart_school:technical_indicators:standard_deviation_volatility")的价格变化

+   14天的[RSI值](/school/doku.php?id=chart_school:technical_indicators:relative_strength_index_rsi "chart_school:technical_indicators:relative_strength_index_rsi")

+   任何短期（2天）[价格通道突破](/school/doku.php?id=chart_school:technical_indicators:price_channels "chart_school:technical_indicators:price_channels")的存在

最终得分转换为0-100的尺度以便比较。

## 解释

在0到100的查德趋势仪表盘尺度上，分数为100的股票处于非常强劲的上升趋势中。相反，分数为0的股票处于非常强劲的下跌趋势中。

这个尺度可以分为5个不同的级别：

+   分数为90-100的股票处于非常强劲的上升趋势中

+   分数为80-90的股票处于强劲上升趋势中

+   分数为60-80的股票处于弱势上升趋势中

+   分数为20-60的股票要么是平稳的，要么是弱势下跌趋势中

+   分数为0-20的股票处于非常强劲的下跌趋势中

动量交易者应寻找查德趋势仪表盘分数为80或更高的股票。这表示强劲的上升趋势。趋势越强劲，延续该趋势的可能性就越大。

查德趋势仪表盘也可以与指数和交易所交易基金（ETF）一起使用，以了解特定行业和行业甚至整个市场的相对趋势。

查德趋势仪表盘的一个优点是其数值是在绝对尺度上设置的，而不是相对于同一组股票。因此，当您比较几种不同类型证券的CTM分数时，您正在跨所有证券进行苹果对苹果的比较。

## 结论

Chande趋势仪提供了一种简单的方法来确定股票是处于上升趋势还是下降趋势，并且便于评估该趋势的强度。通过将几种不同的经过验证的技术趋势指标结合在一起，并将它们简化为一个数字，CTM使图表分析师能够在快速浏览时获得丰富的趋势信息。

## 使用SharpCharts

Chande趋势仪可以在图表下方的指标部分找到。CTM指标可以放置在主价格图的上方、下方或后面。

当放置在主价格图之上或之下时，背景颜色编码以指示不同的趋势强度水平：

+   **深绿色**: 90-100（非常强劲上升趋势）

+   **中绿色**: 80-90（强劲上升趋势）

+   **浅绿色**: 60-80（弱上升趋势）

+   **黄色**: 20-60（平稳或弱下跌趋势）

+   **粉色**: 0-20（强劲下跌趋势）

![](img/6c5b52684e5b20214e5ea35d2ff227cb.jpg)

## 建议扫描

### CTM在大量交易量下突破60

此扫描显示了Chande趋势仪已经在较重的交易量下突破60的股票。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Chande Trend Meter x 60.0]
AND [volume > SMA(50,volume) * 1.5]
```

### 持续高CTM的股票

此扫描显示了美国股票的Chande趋势仪持续高，过去50个交易日平均为80或更高。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [SMA(50,Chande Trend Meter) > 80.0]
```

有关Chande趋势仪扫描的语法详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#chande_trend_meter "http://stockcharts.com/docs/doku.php?id=scans:indicators#chande_trend_meter")在支持中心中。

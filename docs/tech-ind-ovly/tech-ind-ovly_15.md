# 积累分布线 [ChartSchool]

### 目录

+   [积累分布线](#accumulation_distribution_line)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [解释](#interpretation)

    +   [ADL与OBV](#adl_versus_obv)

    +   [趋势确认](#trend_confirmation)

    +   [背离](#divergences)

    +   [与价格脱节](#disconnect_with_prices)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [建议扫描](#suggested_scans)

        +   [OBV和ADL中的看涨背离](#bullish_divergence_in_obv_and_adl)

        +   [OBV和ADL中的熊市背离](#bearish_divergence_in_obv_and_adl)

    +   [进一步研究](#further_study)

## 介绍

由马克·查金（Marc Chaikin）开发的积累分布线是一种基于成交量的指标，旨在衡量资金流入和流出证券的累积流动。查金最初将该指标称为累积资金流线。与累积指标一样，积累分布线是每个周期资金流量的累积总和。首先，根据收盘价与高低范围的关系计算乘数。其次，将资金流乘数乘以周期的成交量，得出资金流量。资金流量的累积总和形成积累分布线。图表分析师可以使用此指标来确认证券的基本趋势或在指标与证券价格出现背离时预测逆转。

## 计算

计算积累分布线（ADL）有三个步骤。首先，计算资金流乘数。其次，将此值乘以成交量以找到资金流量。第三，创建资金流量的累积总和以形成积累分布线（ADL）。

```py

  1\. Money Flow Multiplier = [(Close  -  Low) - (High - Close)] /(High - Low) 

  2\. Money Flow Volume = Money Flow Multiplier x Volume for the Period

  3\. ADL = Previous ADL + Current Period's Money Flow Volume

```

资金流乘数在+1和-1之间波动。因此，它是资金流量和积累分布线的关键。当收盘价位于高低范围的上半部时，乘数为正，当位于下半部时为负。这是完全合理的。当价格收于周期范围的上半部时，买盘压力大于卖盘压力（反之亦然）。当乘数为正时，积累分布线上升，当乘数为负时，积累分布线下降。

![图表 1  -  积累分布线](../Images/6059f42a4a2c03fb55b1c8e7ad292058.jpg "图表 1  -  积累分布线")

乘数调整了最终进入资金流量的量。除非资金流量乘数处于极端值（+1或-1），否则实际上会减少交易量。当收盘价处于高位时，乘数为+1，当收盘价处于低位时，乘数为-1。当乘数为+1时，所有交易量为正，当乘数为-1时，所有交易量为负。在0.50时，只有一半的交易量转化为该时期的资金流量。下表显示了Research-in-Motion（RIMM）的资金流量乘数、资金流量和累积分布线。请注意，当收盘价强劲时，乘数在0.50和1之间，当收盘价疲弱时，乘数在-0.50和-1之间。

![表格1 - 累积分布线](../Images/bbb5d28a22efb997ac60ab9cf943b0f3.jpg "表格1 - 累积分布线")

[点击这里](/school/lib/exe/fetch.php?media=chart_school:technical_indicators_and_overlays:accumulation_distribution_line:cs-accum.xls "chart_school:technical_indicators_and_overlays:accumulation_distribution_line:cs-accum.xls (33.5 KB)") 查看Excel电子表格中累积分布线的计算。

## 解释

累积分布线是每个时期交易量流或资金流的累积度量。高正乘数与高交易量结合显示出强劲的买盘压力，推动指标上涨。相反，低负数与高交易量结合反映出强劲的卖盘压力，推动指标下跌。资金流量累积形成一条线，该线要么确认基础价格趋势，要么对其可持续性表示怀疑。价格上涨趋势与累积分布线下降趋势相结合，表明基础卖盘压力（分布），可能预示价格图表上的熊市反转。价格下跌趋势与累积分布线上升趋势表明基础买盘压力（积累），可能预示价格的牛市反转。

## ADL与OBV

累积分布线和平衡成交量（OBV）是基于累积交易量的指标，有时会朝相反方向移动，因为它们的基本公式不同。乔·格兰维尔（Joe Granville）开发了[平衡成交量](/school/doku.php?id=chart_school:technical_indicators:on_balance_volume_obv "chart_school:technical_indicators:on_balance_volume_obv")（OBV）作为正负交易量流的累积度量。当收盘价上涨时，OBV会增加该时期的总交易量，当收盘价下跌时，OBV会减少该时期的总交易量。这些正负交易量流的累积总和形成OBV线。然后可以将该线与基础证券的价格图表进行比较，以寻找背离或确认。

![图表2 - 累积分布线](../Images/06f4000d84a40426a266d54b6920d1be.jpg "图表2 - 累积分布线")

如上述公式所示，Chaikin采取了一种不同的方法，完全忽略了从一个时期到下一个时期的变化。相反，积累分布线关注的是收盘价相对于给定时期（日、周、月）的高低范围的水平。根据这个公式，一个证券可能会跳空下跌并且收盘价明显较低，但如果收盘价高于高低范围的中点，积累分布线将上升。上图显示了Clorox（CLX）出现大幅跳空下跌，收盘价接近当天的高低范围顶部。OBV急剧下降，因为收盘价低于前一次收盘价。积累分布线上升，因为收盘价接近当天的高点。

## 趋势确认

趋势确认是一个相当直接的概念。在积累分布线上升趋势加强了价格图表上的上升趋势，反之亦然。下图显示了自由港麦克莫兰（FCX）和积累分布线在二月至三月上升，四月至六月下降，然后七月至一月上升。积累分布线确认了每一个价格趋势。

![图表 3  -  积累分布线](../Images/edf68ebcd21571cba81beb4bf3323d16.jpg "图表 3  -  积累分布线")

## 背离

看涨和看跌的背离是开始变得有趣的地方。当价格创新低时，但积累分布线不确认这些低点并上升时，形成了一个看涨的背离。上升的积累分布线显示了积累。将这视为基本上是潜在的买盘压力。根据成交量领先价格的理论，图表分析师应该警惕价格图表上的看涨反转。

上图显示了 Nordstrom（JWN）的积累分布线。注意当指标放置在价格图表“后面”时，比较价格走势是多么容易。指标（粉色）和价格趋势从二月到六月同步移动。随着指标在七月初触底并开始上升，积累的迹象出现。JWN在八月底创下新低。即使指标显示出买盘压力的迹象，等待价格图表上的看涨催化剂或确认是很重要的。这个催化剂是股票跳空上涨并伴随着大量交易。

![图表 4  -  积累分布线](../Images/ae7322d4649c689187bbb1517239ec7e.jpg "图表 4  -  积累分布线")

当价格创新高时，但积累分布线不确认并下降时，形成了一个看跌的背离。这显示了分销或潜在的卖压，可能预示价格图表上的看跌反转。

![图表 5  -  积累分布线](../Images/2008ad33442385f54eb2b1c881ca5052.jpg "图表 5  -  积累分布线")

上图显示了西南航空公司（LUV）的累积分布线在价格两个月前达到峰值。该指标不仅达到峰值，而且在三月和四月下降，反映了一些卖压。LUV在价格图表上确认了弱势，并且RSI随后在40以下移动。RSI通常在牛市区（40-80）和熊市区（20-60）交易。[RSI](/school/doku.php?id=chart_school:technical_indicators:relative_strength_index_rsi "chart_school:technical_indicators:relative_strength_index_rsi")一直保持在牛市区，直到五月初才进入熊市区。

## 与价格脱节

累积分布线是基于价格和成交量的衍生指标。这使得它至少比基础证券的实际价格远了两步。此外，资金流乘数不考虑期间内价格的变化。因此，不能期望它总是确认价格走势或成功预测出现背离的价格反转。有时价格和指标之间存在脱节。有时累积分布线简单地不起作用。这就是为什么在价格/趋势分析和/或其他指标方面，使用累积分布线以及所有指标至关重要。

![图表6  -  累积分布线](../Images/2125a7954b93a553f6da1308b98b7701.jpg "图表6  -  累积分布线")

## 结论

**累积分布线可用于衡量成交量的一般流向。**上升趋势表明买盘压力经常占优势，而下降趋势表明卖盘压力占优势。牛市和熊市背离可作为价格图表可能反转的警示。与所有指标一样，重要的是将累积分布线与技术分析的其他方面结合使用，如[动量振荡器](/school/doku.php?id=chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators#momentum_oscillators "chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators")和[图表形态](/school/doku.php?id=chart_school:chart_analysis:chart_patterns "chart_school:chart_analysis:chart_patterns")。它不是一个独立的指标。

## 使用SharpCharts

积聚分布线在SharpCharts中作为一个指标可用。选择后，指标可以放置在基础证券的价格上方、下方或后面。将其“放在价格后面”可以方便与基础证券进行比较。图表分析师还可以通过使用高级选项向指标添加移动平均线。**[点击这里](http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=8&dy=0&id=p93414126571&listNum=30&a=222506084 "http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=8&dy=0&id=p93414126571&listNum=30&a=222506084")** 查看带有积聚分布线的实时图表。

![图表 7  -  积聚分布线](../Images/f805062269290aa87897d6396eb1311b.jpg "图表 7  -  积聚分布线")

![SharpCharts  -  积聚分布线](../Images/370a6f19ba12a1fbd2a386d6dbbc86fe.jpg "SharpCharts  -  积聚分布线")

## 建议扫描

### OBV和ADL中的看涨背离

这个扫描从股票的基础开始，这些股票在过去60天的平均价格至少为$10，每日交易量为100,000。通过查找价格低于65日SMA和20日SMA的股票，但OBV和积聚分布线高于65日SMA和20日SMA，可以找到潜在的看涨背离。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily Close < Daily SMA(65,Daily Close)] 
AND [Daily AccDist > Daily AccDist Signal (65)] 
AND [Daily OBV > Daily OBV Signal(65)] 
AND [Daily Close < Daily SMA(20,Daily Close)] 
AND [Daily AccDist > Daily AccDist Signal (20)] 
AND [Daily OBV > Daily OBV Signal(20)]
```

### OBV和ADL中的看跌背离

这个扫描从股票的基础开始，这些股票在过去60天的平均价格至少为$10，每日交易量为100,000。通过查找价格高于65日SMA和20日SMA的股票，但OBV和积聚分布线低于65日SMA和20日SMA，可以找到潜在的看跌背离。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily Close > Daily SMA(65,Daily Close)] 
AND [Daily AccDist < Daily AccDist Signal (65)] 
AND [Daily OBV < Daily OBV Signal(65)] 
AND [Daily Close > Daily SMA(20,Daily Close)] 
AND [Daily AccDist < Daily AccDist Signal (20)] 
AND [Daily OBV < Daily OBV Signal(20)]
```

有关用于积聚分布线扫描的语法的更多详细信息，请参阅我们支持中心的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#accumulation_distribution "http://stockcharts.com/docs/doku.php?id=scans:indicators#accumulation_distribution")。

**注意**：出于扫描目的，交易日内的每日交易量数据是不完整的。在运行基于交易量的指标（如积聚/分布）的扫描时，请确保基于“最后市场收盘价”。其他基于交易量的指标的示例包括Chaikin Money Flow、On Balance Volume和PVO。

## 进一步学习

这本书涵盖了所有内容，并且解释简单清晰。墨菲涵盖了大部分主要的图表模式和指标。一个完整的章节专门讨论了理解成交量和未平仓合约。

| **《金融市场技术分析》** 约翰·J·墨菲 |
| --- |
| [![](../Images/e00f9b0f57a7325646647a118f3ebe9e.jpg)](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |

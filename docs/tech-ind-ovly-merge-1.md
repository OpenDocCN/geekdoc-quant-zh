# 技术指标和振荡器大全（二）



# 成交量加权平均价格（VWAP）

### 目录

+   成交量加权平均价格（VWAP）

    +   介绍

    +   Tick 与 Minute

    +   计算

    +   特点

    +   VWAP 的用途

    +   结论

    +   与 SharpCharts 一起使用

## 介绍

成交量加权平均价格（VWAP）就是字面意思：**按成交量加权的平均价格**。VWAP 等于所有交易周期的美元价值除以当天的总交易量。计算从交易开盘开始，到交易收盘结束。因为它仅适用于当天的交易，所以计算中使用了日内周期和数据。

## Tick 与 Minute

传统 VWAP 基于 tick 数据。可以想象，在一天的每一分钟内都会有许多 tick（交易）。在活跃时间段内活跃的证券每分钟可以有 20-30 个 tick。在典型股票交易日的 390 分钟内，许多股票每天的 tick 数量远远超过 5000。每天有超过 5000 只股票交易，这些 tick 开始呈指数增长。不用说，tick 数据非常耗费资源。

![VWAP - 图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/8d71258545bff6d5b4176905acff1c43.jpg "VWAP - 图表 1")

与基于 tick 数据的 VWAP 不同，StockCharts.com 提供基于日内周期（1、5、10、15、30 或 60 分钟）的日内 VWAP。请注意，由于计算的性质（见下文），VWAP 在日常、周常或月常周期中没有定义。

## 计算

VWAP 计算涉及五个步骤。首先，计算日内周期的典型价格。这是高、低和收盘价的平均值：{(H+L+C)/3)}。其次，将典型价格乘以周期的成交量。第三，创建这些值的累积总和。这也被称为累积总和。第四，创建成交量的累积总和（累积成交量）。第五，将价格-成交量的累积总和除以成交量的累积总和。

```py
Cumulative(Volume x Typical Price)/Cumulative(Volume)

```

![VWAP - 电子表格 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/b95b66afabcb769e415104b71652cec0.jpg "VWAP - 电子表格 1")

上面的示例显示了 IBM 交易的前 30 分钟的 1 分钟 VWAP。通过将累积价格-成交量除以累积成交量，产生一个根据成交量调整（加权）的价格水平。第一个 VWAP 值始终是典型价格，因为分子和分母中的成交量相等。它们在第一次计算中互相抵消。下图显示了 IBM 的 1 分钟 K 线图和 VWAP。在交易的前 30 分钟内，价格从最高的 127.36 到最低的 126.67。实际上，前 30 分钟非常波动。VWAP 的范围从 127.21 到 127.09，并且大部分时间处于这个范围的中间。

![VWAP - 图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/566c94be67f7a73087710b66c5aa0f68.jpg "VWAP - 图表 2")

## 特点

像移动平均一样，VWAP 滞后于价格，因为它是基于过去数据的平均值。数据越多，滞后越大。到下午 3:00，一只股票已经交易了约 331 分钟。作为一个累积“平均”，这个指标类似于一个 330 周期的移动平均。这是很多过去的数据。一天结束时的 1 分钟 VWAP 值通常与 390 分钟移动平均的结束值非常接近。这两个移动平均都是基于当天的 1 分钟柱状图。在收盘时，两者都是基于 390 分钟的数据（一整天）。然而，在白天无法将 390 分钟移动平均与 VWAP 进行比较。中午 12:00 的 390 分钟移动平均将包含前一天的数据。而 VWAP 不会。请记住，VWAP 的计算从开盘开始，到收盘结束。到中午 12:00 已经过去了 150 分钟的交易时间。因此，中午 12:00 的 VWAP 需要与 150 分钟移动平均进行比较。

![VWAP - 图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/69a39c486c78865e7695c942ad5b22de.jpg "VWAP - 图表 3")

尽管存在滞后，图表分析师可以将 VWAP 与当前价格进行比较，以确定日内价格的大致方向。它类似于移动平均。一般来说，当价格低于 VWAP 时，日内价格下跌，当价格高于 VWAP 时，日内价格上涨。当价格在一天内处于区间时，VWAP 将落在当天的高低范围之间。接下来的三个图表展示了 VWAP 上升、下降和持平的示例。

![VWAP - 图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/afaa7cbbbb3bea3913f335a1c9776f61.jpg "VWAP - 图表 4") ![VWAP - 图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/5897839258c78dd92ec788bfba18f522.jpg "VWAP - 图表 5") ![VWAP - 图表 6](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/64cc72c64fb470c1bc7144604770fded.jpg "VWAP - 图表 6")

## VWAP 的用途

VWAP 用于识别流动性点。作为一个以成交量加权的价格衡量标准，VWAP 反映了以成交量加权的价格水平。这可以帮助有大额订单的机构。其理念是在输入大额买入或卖出订单时不要扰乱市场。VWAP 帮助这些机构在非常短的时间内确定特定证券的流动和非流动价格点。

VWAP 也可以用于衡量交易效率。在买入或卖出证券后，机构或个人可以将其价格与 VWAP 值进行比较。在 VWAP 值以下执行的买入订单将被视为良好的成交，因为证券是以低于平均价格购买的。相反，在 VWAP 以上执行的卖出订单将被视为良好的成交，因为它是以高于平均价格出售的。

## 结论

VWAP 作为一天价格的参考点。因此，它最适合**盘中分析**。图表分析师可以将当前价格与 VWAP 值进行比较，以确定盘中趋势。VWAP 还可以用于确定相对价值。低于 VWAP 值的价格在当天或特定时间相对较低。高于 VWAP 值的价格在当天或特定时间相对较高。**请记住，VWAP 是一个累积指标，这意味着数据点数量在一天内逐渐增加。**在 1 分钟图表上，IBM 在上午 11:00 将有 90 个数据点（分钟），下午 1:00 将有 210 个数据点，收盘时将有 390 个数据点。随着一天的延长，数据点数量急剧增加。这就是为什么 VWAP 滞后于价格，而这种滞后随着一天的延长而增加。

## 使用 SharpCharts

成交量加权平均价格（VWAP）可以作为 Sharpcharts 上的“叠加”指标绘制。输入证券代码后，选择“盘中”时段和“范围”。这可以是 1 天或“填充图表”。寻找更多细节的图表分析师可以选择“填充图表”。寻找一般水平的图表分析师可以选择 1 天。VWAP 可以绘制超过一天，但随着新的计算周期开始，指标将从其先前的收盘价跳至下一个开盘价的典型价格。此外，请注意 VWAP 值有时可能会脱离价格图表。价格范围从 45.8 到 47 的图表上将显示 45.5 的 VWAP。图表分析师有时需要将范围扩展到整天才能在图表上看到 VWAP。VWAP 值始终显示在图表的左上角。点击下面的图表查看实时示例。

![VWAP - Chart 7](http://stockcharts.com/h-sc/ui?s=INTC&p=1&b=5&g=0&id=p44523558053&listNum=30&a=208264972 "http://stockcharts.com/h-sc/ui?s=INTC&p=1&b=5&g=0&id=p44523558053&listNum=30&a=208264972")

![VWAP - SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/670c45bf78990297dfb991e0f9d3e289.jpg "VWAP - SharpCharts")


# ZigZag 

### 目录

+   ZigZag

    +   简介

    +   计算

    +   艾略特波动计数

    +   回撤和投影

    +   结论

    +   与 SharpCharts 一起使用

    +   进一步研究

## 简介

SharpCharts 上的 ZigZag 功能本身不是指标，而是一种过滤较小价格波动的手段。设置为 10%的 ZigZag 将忽略所有小于 10%的价格波动。只有大于 10%的价格波动才会显示出来。过滤掉较小的波动使图表分析者能够看到整体情况而不仅仅是细节。重要的是要记住，ZigZag 功能没有预测能力，因为它是基于事后的绘制线条。任何预测能力都将来自应用程序，如艾略特波动、价格模式分析或指标。图表分析者还可以使用 ZigZag 与回撤功能来识别斐波那契回撤和投影。

## 计算

ZigZag 基于图表的“类型”。基于收盘价的线状和点状图表将显示基于收盘价的 ZigZag。高低收盘价柱状图（HLC）、开盘-最高-最低-收盘价柱状图（OHLC）和蜡烛图显示了周期的高低范围，将显示基于这一高低范围的 ZigZag。基于高低范围的 ZigZag 更有可能改变方向，因为高低范围会更大，产生更大的波动。

参数框允许图表分析者设置 ZigZag 功能的灵敏度。参数框中设置为 5 的 ZigZag 将过滤掉所有小于 5%的波动。设置为 10 的 ZigZag 将过滤掉小于 10%的波动。如果一支股票从 100 的反弹低点到 109 的高点（+9%），则不会有线条，因为波动小于 10%。如果股票从 100 的低点上涨到 110 的高点（+10%），则会有一条线从 100 到 110。如果股票继续上涨到 112，这条线将延伸到 112（从 100 到 112）。直到股票从高点下跌 10%或更多，ZigZag 才会反转。从 112 的高点开始，股票必须下跌 11.2 点（或至 100.8 的低点）才能再次出现线条。下面的图表显示了一个带有 7% ZigZag 的 QQQQ 线状图。6 月初的反弹被忽略，因为小于 7%（黑色箭头）。7 月的两次回调也被忽略，因为它们远低于 7%（红色箭头）。

![ZigZag - 图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/0a062c468971ec2a37068fd17aa8ce58.jpg "ZigZag - 图表 1")

注意最后一个 ZigZag 线。敏锐的图表分析师会注意到，尽管 QQQQ 仅上涨了 4.13%（43.36 至 45.15），但最后一个 ZigZag 线是向上的。这只是一个临时线，因为 QQQQ 尚未达到 7%的变化阈值。需要到 46.40 才能获得 7%的增长，然后才会有一个永久的 ZigZag 线。如果 QQQQ 在此反弹中未能达到 7%的阈值，然后下跌至 43 以下，这条临时线将消失，之前的 ZigZag 线将从 8 月初的高点继续。

![ZigZag - Chart 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/e3d7fefaf2cec25331994401bd084724.jpg "ZigZag - Chart 2")

## Elliott Wave Counts

ZigZag 功能可用于过滤小幅波动，并使 Elliott Wave 计数更加直观。下图显示了标普 500ETF 的 6% ZigZag，以过滤小于 6%的波动。经过一些试验，6%被认为是重要的阈值。大于 6%的上涨或下跌被认为足够重要，需要为 Elliott 计数做出波浪。请记住，这只是一个例子。阈值和波浪计数是主观的，取决于个人偏好。基于 6% ZigZag，从 2009 年 3 月到 2010 年 7 月识别出了一个完整的周期。一个完整的周期包括 8 个波动，5 个上涨和 3 个下跌。

![ZigZag - Chart 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/c7bc2129d97eae138657f14d227f97e9.jpg "ZigZag - Chart 4")

## Retracements and Projections

Sharpcharts 用户可以在正常的“ZigZag”和“ZigZag (Retrace.)”之间选择。如上面的示例所示，正常的 ZigZag 显示至少移动特定百分比的线条。ZigZag (Retrace.)连接反应高点和低点，并标记测量先前移动的标签。虚线上的数字反映了当前 Zigzag 线与之前的 ZigZag 线之间的差异。例如，下图显示了 Altera (ALTR)的 15% ZigZag (Retrace.)功能。已标记了三条 ZigZag 线（1、2 和 3）。连接线 1 的低点和线 2 的低点的虚线显示了一个框，其中包含 0.638。这意味着线 2 是线 1 的 0.638（63.8%）。小于 1 的数字表示该线比先前的线短。连接线 2 的高点和线 3 的高点的虚线显示了一个框，其中包含 1.646。这意味着线 3 是线 2 的 1.646（164.6%）。大于 1 的数字表示该线比先前的线长。

![ZigZag - Chart 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/a82588f71d48ba3b7a944f177603537b.jpg "ZigZag - Chart 3")

你可能已经猜到，将这些线看作前一线的百分比，可以评估斐波那契投影。8 月下跌（线 2）回撤了 6 月至 7 月上涨（线 1）的大约 61.8%。这是经典的斐波那契回撤。从 9 月初到 11 月初的上涨是 8 月下跌的 1.646 倍。在这种意义上，ZigZag（Retrace.）可以用来预测上涨的长度。再次，1.646 接近斐波那契 1.618，这是许多投影估计中使用的黄金比例。查看我们的 ChartSchool 文章，了解更多关于斐波那契回撤的信息。

## 结论

ZigZag 和 ZigZag（Retrace.）过滤价格走势，并没有任何预测能力。当价格移动一定百分比时，ZigZag 线会做出反应。图表分析师可以将各种技术分析工具应用于 ZigZag。通过比较反应高点和低点，图表分析师可以进行基本趋势分析。图表分析师还可以叠加 ZigZag 功能，以寻找在普通柱状图或折线图上可能不太明显的价格模式。ZigZag 有一种突出重要走势并忽略噪音的方式。使用 ZigZag 功能时，不要忘记测量最后一条线，以确定它是暂时的还是永久的。如果当前价格变动小于 ZigZag 参数，则最后一条 ZigZag 线是暂时的。当价格变动大于或等于 ZigZag 参数时，最后一条线是永久的。

## 使用 SharpCharts

ZigZag 和 ZigZag（Retrace.）可以在 SharpCharts 中作为图表属性部分的价格叠加或作为指标的附加项找到。在从下拉框中选择 Zigzag 功能后，参数窗口将为空白。默认参数为 5%，但这取决于证券的价格特征。一些证券在 5%时产生的 Zigzag 线太少，因此默认设置较低（例如 3.75%）。一些证券在 5%时产生太多的 Zigzag 线，因此默认设置较高（例如 6.25%）。Zigzag 参数可以在图表的左上角看到。应用 Zigzag 功能后，图表分析师可以调整参数以满足其图表需求。较低的数字会使功能更敏感，而较高的数字会使其不太敏感。[点击这里](http://stockcharts.com/h-sc/ui?s=$COMPQ&p=D&yr=0&mn=8&dy=0&id=p52942080253&listNum=30&a=213475204 "http://stockcharts.com/h-sc/ui?s=$COMPQ&p=D&yr=0&mn=8&dy=0&id=p52942080253&listNum=30&a=213475204")查看带有 Zigzag（Retrace.）功能的实时图表。

![ZigZag - SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/0647435763830c7f4686202a27f2e98b.jpg "ZigZag - SharpCharts")

![ZigZag - SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/a30c4b8e935ac023c8ac3870d0a2efc8.jpg "ZigZag - SharpCharts")

![ZigZag - SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/950acc8018316dd367477e78e1aa0913.jpg "ZigZag - SharpCharts")

## 进一步学习

| **艾略特波浪理论** 罗伯特·普雷克特 |
| --- |
| ![](http://store.stockcharts.com/products/elliott-wave-principle-key-to-market-behavior "http://store.stockcharts.com/products/elliott-wave-principle-key-to-market-behavior") |
| ![立即购买](http://store.stockcharts.com/products/elliott-wave-principle-key-to-market-behavior "http://store.stockcharts.com/products/elliott-wave-principle-key-to-market-behavior") |


# 积累分布线 

### 目录

+   积累分布线

    +   介绍

    +   计算

    +   解释

    +   ADL 与 OBV

    +   趋势确认

    +   背离

    +   与价格脱节

    +   结论

    +   与 SharpCharts 一起使用

    +   建议扫描

        +   OBV 和 ADL 中的看涨背离

        +   OBV 和 ADL 中的熊市背离

    +   进一步研究

## 介绍

由马克·查金（Marc Chaikin）开发的积累分布线是一种基于成交量的指标，旨在衡量资金流入和流出证券的累积流动。查金最初将该指标称为累积资金流线。与累积指标一样，积累分布线是每个周期资金流量的累积总和。首先，根据收盘价与高低范围的关系计算乘数。其次，将资金流乘数乘以周期的成交量，得出资金流量。资金流量的累积总和形成积累分布线。图表分析师可以使用此指标来确认证券的基本趋势或在指标与证券价格出现背离时预测逆转。

## 计算

计算积累分布线（ADL）有三个步骤。首先，计算资金流乘数。其次，将此值乘以成交量以找到资金流量。第三，创建资金流量的累积总和以形成积累分布线（ADL）。

```py

  1\. Money Flow Multiplier = [(Close  -  Low) - (High - Close)] /(High - Low) 

  2\. Money Flow Volume = Money Flow Multiplier x Volume for the Period

  3\. ADL = Previous ADL + Current Period's Money Flow Volume

```

资金流乘数在+1 和-1 之间波动。因此，它是资金流量和积累分布线的关键。当收盘价位于高低范围的上半部时，乘数为正，当位于下半部时为负。这是完全合理的。当价格收于周期范围的上半部时，买盘压力大于卖盘压力（反之亦然）。当乘数为正时，积累分布线上升，当乘数为负时，积累分布线下降。

![图表 1  -  积累分布线](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/6059f42a4a2c03fb55b1c8e7ad292058.jpg "图表 1  -  积累分布线")

乘数调整了最终进入资金流量的量。除非资金流量乘数处于极端值（+1 或-1），否则实际上会减少交易量。当收盘价处于高位时，乘数为+1，当收盘价处于低位时，乘数为-1。当乘数为+1 时，所有交易量为正，当乘数为-1 时，所有交易量为负。在 0.50 时，只有一半的交易量转化为该时期的资金流量。下表显示了 Research-in-Motion（RIMM）的资金流量乘数、资金流量和累积分布线。请注意，当收盘价强劲时，乘数在 0.50 和 1 之间，当收盘价疲弱时，乘数在-0.50 和-1 之间。

![表格 1 - 累积分布线](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/bbb5d28a22efb997ac60ab9cf943b0f3.jpg "表格 1 - 累积分布线")

点击这里") 查看 Excel 电子表格中累积分布线的计算。

## 解释

累积分布线是每个时期交易量流或资金流的累积度量。高正乘数与高交易量结合显示出强劲的买盘压力，推动指标上涨。相反，低负数与高交易量结合反映出强劲的卖盘压力，推动指标下跌。资金流量累积形成一条线，该线要么确认基础价格趋势，要么对其可持续性表示怀疑。价格上涨趋势与累积分布线下降趋势相结合，表明基础卖盘压力（分布），可能预示价格图表上的熊市反转。价格下跌趋势与累积分布线上升趋势表明基础买盘压力（积累），可能预示价格的牛市反转。

## ADL 与 OBV

累积分布线和平衡成交量（OBV）是基于累积交易量的指标，有时会朝相反方向移动，因为它们的基本公式不同。乔·格兰维尔（Joe Granville）开发了平衡成交量（OBV）作为正负交易量流的累积度量。当收盘价上涨时，OBV 会增加该时期的总交易量，当收盘价下跌时，OBV 会减少该时期的总交易量。这些正负交易量流的累积总和形成 OBV 线。然后可以将该线与基础证券的价格图表进行比较，以寻找背离或确认。

![图表 2 - 累积分布线](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/06f4000d84a40426a266d54b6920d1be.jpg "图表 2 - 累积分布线")

如上述公式所示，Chaikin 采取了一种不同的方法，完全忽略了从一个时期到下一个时期的变化。相反，积累分布线关注的是收盘价相对于给定时期（日、周、月）的高低范围的水平。根据这个公式，一个证券可能会跳空下跌并且收盘价明显较低，但如果收盘价高于高低范围的中点，积累分布线将上升。上图显示了 Clorox（CLX）出现大幅跳空下跌，收盘价接近当天的高低范围顶部。OBV 急剧下降，因为收盘价低于前一次收盘价。积累分布线上升，因为收盘价接近当天的高点。

## 趋势确认

趋势确认是一个相当直接的概念。在积累分布线上升趋势加强了价格图表上的上升趋势，反之亦然。下图显示了自由港麦克莫兰（FCX）和积累分布线在二月至三月上升，四月至六月下降，然后七月至一月上升。积累分布线确认了每一个价格趋势。

![图表 3  -  积累分布线](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/edf68ebcd21571cba81beb4bf3323d16.jpg "图表 3  -  积累分布线")

## 背离

看涨和看跌的背离是开始变得有趣的地方。当价格创新低时，但积累分布线不确认这些低点并上升时，形成了一个看涨的背离。上升的积累分布线显示了积累。将这视为基本上是潜在的买盘压力。根据成交量领先价格的理论，图表分析师应该警惕价格图表上的看涨反转。

上图显示了 Nordstrom（JWN）的积累分布线。注意当指标放置在价格图表“后面”时，比较价格走势是多么容易。指标（粉色）和价格趋势从二月到六月同步移动。随着指标在七月初触底并开始上升，积累的迹象出现。JWN 在八月底创下新低。即使指标显示出买盘压力的迹象，等待价格图表上的看涨催化剂或确认是很重要的。这个催化剂是股票跳空上涨并伴随着大量交易。

![图表 4  -  积累分布线](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/ae7322d4649c689187bbb1517239ec7e.jpg "图表 4  -  积累分布线")

当价格创新高时，但积累分布线不确认并下降时，形成了一个看跌的背离。这显示了分销或潜在的卖压，可能预示价格图表上的看跌反转。

![图表 5  -  积累分布线](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/2008ad33442385f54eb2b1c881ca5052.jpg "图表 5  -  积累分布线")

上图显示了西南航空公司（LUV）的累积分布线在价格两个月前达到峰值。该指标不仅达到峰值，而且在三月和四月下降，反映了一些卖压。LUV 在价格图表上确认了弱势，并且 RSI 随后在 40 以下移动。RSI 通常在牛市区（40-80）和熊市区（20-60）交易。RSI 一直保持在牛市区，直到五月初才进入熊市区。

## 与价格脱节

累积分布线是基于价格和成交量的衍生指标。这使得它至少比基础证券的实际价格远了两步。此外，资金流乘数不考虑期间内价格的变化。因此，不能期望它总是确认价格走势或成功预测出现背离的价格反转。有时价格和指标之间存在脱节。有时累积分布线简单地不起作用。这就是为什么在价格/趋势分析和/或其他指标方面，使用累积分布线以及所有指标至关重要。

![图表 6  -  累积分布线](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/2125a7954b93a553f6da1308b98b7701.jpg "图表 6  -  累积分布线")

## 结论

**累积分布线可用于衡量成交量的一般流向。**上升趋势表明买盘压力经常占优势，而下降趋势表明卖盘压力占优势。牛市和熊市背离可作为价格图表可能反转的警示。与所有指标一样，重要的是将累积分布线与技术分析的其他方面结合使用，如动量振荡器和图表形态。它不是一个独立的指标。

## 使用 SharpCharts

积聚分布线在 SharpCharts 中作为一个指标可用。选择后，指标可以放置在基础证券的价格上方、下方或后面。将其“放在价格后面”可以方便与基础证券进行比较。图表分析师还可以通过使用高级选项向指标添加移动平均线。**[点击这里](http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=8&dy=0&id=p93414126571&listNum=30&a=222506084 "http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=8&dy=0&id=p93414126571&listNum=30&a=222506084")** 查看带有积聚分布线的实时图表。

![图表 7  -  积聚分布线](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/f805062269290aa87897d6396eb1311b.jpg "图表 7  -  积聚分布线")

![SharpCharts  -  积聚分布线](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/370a6f19ba12a1fbd2a386d6dbbc86fe.jpg "SharpCharts  -  积聚分布线")

## 建议扫描

### OBV 和 ADL 中的看涨背离

这个扫描从股票的基础开始，这些股票在过去 60 天的平均价格至少为$10，每日交易量为 100,000。通过查找价格低于 65 日 SMA 和 20 日 SMA 的股票，但 OBV 和积聚分布线高于 65 日 SMA 和 20 日 SMA，可以找到潜在的看涨背离。

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

### OBV 和 ADL 中的看跌背离

这个扫描从股票的基础开始，这些股票在过去 60 天的平均价格至少为$10，每日交易量为 100,000。通过查找价格高于 65 日 SMA 和 20 日 SMA 的股票，但 OBV 和积聚分布线低于 65 日 SMA 和 20 日 SMA，可以找到潜在的看跌背离。

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

**注意**：出于扫描目的，交易日内的每日交易量数据是不完整的。在运行基于交易量的指标（如积聚/分布）的扫描时，请确保基于“最后市场收盘价”。其他基于交易量的指标的示例包括 Chaikin Money Flow、On Balance Volume 和 PVO。

## 进一步学习

这本书涵盖了所有内容，并且解释简单清晰。墨菲涵盖了大部分主要的图表模式和指标。一个完整的章节专门讨论了理解成交量和未平仓合约。

| **《金融市场技术分析》** 约翰·J·墨菲 |
| --- |
| ![](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |


# Aroon 

### 目录

+   Aroon

    +   介绍

    +   计算

    +   解释

    +   新趋势出现

    +   整理期

    +   结论

    +   使用 SharpCharts

    +   建议扫描

        +   Aroon-Up 和 Aroon-Down 低于 20

## 介绍

由 Tushar Chande 在 1995 年开发，Aroon 是一个指标系统，用于确定股票是否处于趋势状态以及趋势强度如何。“Aroon” 在梵文中意为“黎明的第一缕光”。Chande 选择这个名字是因为这些指标旨在揭示新趋势的开始。Aroon 指标衡量自价格记录 x 天高点或低点以来的周期数。有两个独立的指标：Aroon-Up 和 Aroon-Down。25 天 Aroon-Up 衡量自 25 天高点以来的天数。25 天 Aroon-Down 衡量自 25 天低点以来的天数。在这个意义上，Aroon 指标与典型的动量振荡器有很大不同，后者侧重于价格相对于时间。Aroon 是独特的，因为它侧重于时间相对于价格。图表分析师可以使用 Aroon 指标来发现新兴趋势，识别整理期，定义修正期，并预测逆转。

## 计算

Aroon 指标以百分比形式显示，并在 0 到 100 之间波动。Aroon-Up 基于价格高点，而 Aroon-Down 基于价格低点。这两个指标并排绘制，便于比较。SharpCharts 中的默认参数设置为 25，下面的示例基于 25 天。

```py
Aroon-Up = ((25 - Days Since 25-day High)/25) x 100
Aroon-Down = ((25 - Days Since 25-day Low)/25) x 100

```

![Aroon - 图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/3ab84ab991d5385d78051ec79cb27ba4.jpg "Aroon - 图表 1")

随着新高点或新低点之间经过的时间增加，Aroon 会下降。50 是分界点。因为 12.5 天标记着确切的中点，在日线图上不可能出现恰好为 50 的读数。在其他时间框架上是可能的。在日线图上，Aroon 要么低于 50（48），要么高于 50（52）。高于 50 的读数意味着在过去的 12 天或更短时间内记录了新高点或新低点。这是最近一半的回顾期。低于 50 的读数意味着在过去的 13 天或更长时间内记录了新高点或新低点（（25-13）/25 x 100 = 48）。这是回顾期的后一半。下表显示了 25 天 Aroon-Up 和 25 天 Aroon-Down 的数值范围。

![Aroon - 表格 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/8612b00403ab9e3c3934c406586ae5cb.jpg "Aroon - 表格 1")

## 解释

Aroon 指标在中心线（50）上下波动，并在 0 到 100 之间。这三个水平对于解释很重要。在最基本的情况下，当 Aroon-Up 在 50 以上，Aroon-Down 在 50 以下时，多头占优势。这表示新 x 天的高点比低点更多。对于下降趋势，情况相反。当 Aroon-Up 低于 50，Aroon-Down 高于 50 时，空头占优势。

Aroon 指标达到 100 表示可能出现新趋势。这可以通过另一个 Aroon 指标的下降来确认。例如，Aroon-Up 达到 100，同时 Aroon-Down 降至 30 以下，显示上涨力量。持续高读数意味着价格定期达到指定期间的新高或新低。当 Aroon-Up 在 70-100 范围内持续一段时间时，价格持续上涨。相反，持续低读数表明价格很少达到新高或新低。当 Aroon-Down 在 0-30 范围内持续一段时间时，价格不会下降。但这并不意味着价格在上涨。为此，我们需要检查 Aroon-Up。

## 新趋势的出现

新趋势信号有三个阶段。首先，Aroon 线会交叉。其次，Aroon 线会在 50 以上/以下交叉。第三，Aroon 线中的一条将达到 100。例如，上升趋势信号的第一阶段是当 Aroon-Up 移动到 Aroon-Down 之上。这显示新高比新低更近。请记住，Aroon 衡量的是经过的时间，而不是价格。第二阶段是当 Aroon-Up 移动到 50 以上，Aroon-Down 移动到 50 以下。第三阶段是当 Aroon-Up 达到 100，而 Aroon-Down 保持在相对较低水平。第一和第二阶段并不总是按照这个顺序发生。有时 Aroon-Up 会突破 50，然后突破 Aroon-Down。逆向工程上升趋势阶段将给出新兴下降趋势信号。Aroon-Down 突破 Aroon-Up，突破 50，并达到 100。

![Aroon - 图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/ea3beba1b1659579a7ce335a49d2db50.jpg "Aroon - 图表 2")

上图显示了 CSX Corp（CSX）的周线和 25 周 Aroon。首先，请注意，随着 Aroon-Down 在 2007 年底（最左侧）下降至 50 以下，下降趋势开始减弱。上升趋势的第一阶段是在 2008 年初 Aroon-Up 移动到 Aroon-Down 之上时发出的（第一个橙色圆圈）。Aroon-Up 继续保持在 50 以上，并在 Aroon-Down 保持在相对较低水平时达到 100。请注意，随着上涨的持续，Aroon-Up 保持接近 100。这种新兴上升趋势信号持续到 2008 年 9 月，当 Aroon-Down 突破 Aroon-Up，超过 50 并激增至 100 时（第二个橙色圆圈）。请注意，随着下降趋势的延伸，Aroon-Down 保持接近 100。这张图上的第三个趋势是在 2009 年 6 月 Aroon-Up 激增至 100 并连续一年以上保持在 50 以上时发出的信号（第三个橙色圆圈）。另外，请注意，Aroon-Down 保持在 50 以下一年以上。

## 巩固期

当两条线都低于 50 和/或平行下降时，Aroon 指标会发出巩固信号。一致低于 50 的读数表明平稳交易。对于 25 天 Aroon，低于 50 的读数意味着在 13 天或更长时间内没有记录到 25 天的高点或低点。当没有记录到新高点或新低点时，价格显然是平稳的。同样，当 Aroon-Up 和 Aroon-Down 齐头并进地平行下降，且两条线之间的距离非常小时，通常会形成巩固。这种狭窄的平行下降表明某种交易范围正在形成。第一个突破 50 并达到 100 的 Aroon 指标将触发下一个信号。

![Aroon - 图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/ab449227af3b97ad603c42c6cfb97a72.jpg "Aroon - 图表 3")

上图显示了 Omnicom (OMC) 的 Aroon 指标在平行下降中移动至 50 以下。通道的宽度可能较窄，但我们可以在价格图表上看到巩固形成的迹象。Aroon-Up 和 Aroon-Down 都在黄色区域低于 50。随后，Aroon-Up 突破并飙升至 100，这是在突破之前发生的。另一个 Aroon-Up 在突破点再次飙升，进一步确认了巩固结束和上涨开始的信号。

![Aroon - 图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/b3cf47fd93a5a65bcfa27032edb514f7.jpg "Aroon - 图表 4")

下图显示了 Lifepoint Hospitals (LPNT) 的 25 天 Aroon 指标。五月份，两条线同时下降，呈平行下降趋势。在整个下降过程中，两条线之间的距离大约为 25 点。六月份，Aroon-Up 和 Aroon-Down 趋于平缓，两者在三角形巩固期间都保持在 50 以下约两周时间。Aroon-Down（红色）首先突破 50，正好在价格图表上的三角形突破之前。随着价格突破三角形支撑位，Aroon-Down 达到 100，预示着继续下跌。

## 结论

**Aroon-Up 和 Aroon-Down 是互补指标，分别衡量新 x 天高点和低点之间经过的时间。** 它们一起显示，以便图表分析师可以轻松识别两者中更强的，并确定趋势偏好。 Aroon-Up 的激增伴随着 Aroon-Down 的下降，表明***上升趋势***的出现。相反，Aroon-Down 的激增伴随着 Aroon-Up 的下降，表明***下降趋势***的开始。当两者以平行方式下降或保持在低水平（低于 30）时，就会出现整理。图表分析师可以使用 Aroon 指标来确定某个证券是处于趋势还是横盘交易，然后使用其他指标生成适当的信号。例如，图表分析师可能使用动量振荡器来识别超卖水平，当 25 周 Aroon 表明长期趋势向上时。

## 使用 SharpCharts

Aroon 指标在 SharpCharts 上作为一个指标可用。简单地选择“Aroon”将显示 Aroon-Up 和 Aroon-Down。这些指标可以放置在基础证券的价格图之上、之下或之后。用户可以点击指标右侧的绿色箭头查看高级选项，并在 50 处添加水平线。用户甚至可以将另一个指标应用于 Aroon 指标。**[点击这里](http://stockcharts.com/h-sc/ui?s=DIA&p=D&yr=0&mn=8&dy=0&id=p93531652664&listNum=30&a=191771207 "http://stockcharts.com/h-sc/ui?s=DIA&p=D&yr=0&mn=8&dy=0&id=p93531652664&listNum=30&a=191771207")** 查看带有 Aroon 指标的实时图表。

![Aroon - 图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/5639c1604f4256b51c609e45acd66e8e.jpg "Aroon - 图表 5")

## 建议的扫描

### Aroon-Up 和 Aroon-Down 都低于 20

这个简单的扫描搜索股票，其中 Aroon-Up 和 Aroon-Down 都低于 20。当这两个指标都处于如此低的水平时，通常会出现整理。首先突破 50 的指标表明下一个方向线索。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Aroon Up(25) < 20] 
AND [Daily Aroon Down(25) < 20]
```

有关用于 Aroon 扫描的语法详细信息，请参阅我们支持中心的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#aroon_oscillator "http://stockcharts.com/docs/doku.php?id=scans:indicators#aroon_oscillator")。


# Aroon 振荡器

### 目录

+   Aroon 振荡器

    +   介绍

    +   计算

    +   解释

    +   总体趋势偏差

    +   强劲趋势偏差

    +   结论

    +   与 SharpCharts 一起使用

    +   建议扫描

        +   Aroon 振荡器上穿零线

        +   Aroon 振荡器下穿零线

## 介绍

Aroon 振荡器是 Aroon-Up 和 Aroon-Down 之间的差值。这两个指标通常一起绘制以便进行简单比较，但图表分析师也可以通过 Aroon 振荡器查看这两个指标之间的差异。该指标在-100 和+100 之间波动，以零为中线。当振荡器为正时存在上升趋势偏差，而当振荡器为负时存在下降趋势偏差。图表分析师还可以扩大牛熊阈值以识别更强的信号。查看我们的 ChartSchool 文章以获取有关 Aroon-Up 和 Aroon-Down 的更多详细信息。

## 计算

Aroon-Up 和 Aroon-Down 衡量价格记录 x 天高点或低点以来的周期数。Aroon Up 基于时间和价格高点。Aroon Down 基于时间和价格低点。例如，25 天 Aroon-Up 衡量自 25 天高点以来的天数，而 25 天 Aroon-Down 衡量自 25 天低点以来的天数。这些指标以百分比形式显示，并在 0 和 100 之间波动。Aroon 振荡器简单地是 Aroon-Up 减去 Aroon-Down。SharpCharts 中的默认参数为 25，下面的示例基于 25 天 Aroon 振荡器。

```py
Aroon Up = 100 x (25 - Days Since 25-day High)/25
Aroon Down = 100 x (25 - Days Since 25-day Low)/25
Aroon Oscillator = Aroon-Up  -  Aroon-Down

```

![Aroon Oscillator - Chart 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/d63579f789ea11724000b6f1a0d1f359.jpg "Aroon Oscillator - Chart 1")

简单地计算数字会揭示一些有趣的配对。要达到或超过某个阈值，需要 Aroon-Up 或 Aroon-Down 达到最低水平。例如，当 Aroon-Up 等于 100 且 Aroon-Down 等于 0 时，振荡器等于+100。类似地，当 Aroon-Up 为 0 且 Aroon-Down 为 100 时，Aroon 振荡器等于-100。要使振荡器达到+100，需要一些强劲的上涨价格运动。同样，要使振荡器达到-100，需要一些强劲的下跌价格运动。

等于+40 的 Aroon 振荡器要求 Aroon-Up 至少为 40，这意味着 Aroon-Down 将为 0。正 40 可能来自一系列 Aroon-Up 和 Aroon-Down 的组合（40-0, 44-4, 48-8, 60-20, 72-32, 80-40 或 100-40）。颠倒这些数字以查看可能产生负 40 的组合。

一般来说，相对较高的正数要求 Aroon-Up 相对较高，而相对较低的负数要求 Aroon-Down 相对较高。下表显示了一系列 Aroon-Up 和 Aroon-Down 配对以形成 Aroon 振荡器。

![Aroon 振荡器 - 表格 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/9ed3dd5936466984b501ca93825364d3.jpg "Aroon 振荡器 - 表格 1")

## 解释

读数高于零意味着 Aroon-Up 大于 Aroon-Down，这意味着价格最近的新高比新低更多。相反，低于零的读数表明 Aroon-Down 大于 Aroon-Up。这意味着价格最近的新低比新高更多。正如你所看到的，Aroon 振荡器大部分时间要么是正的，要么是负的。这使得解释变得直接。当指标为正时，时间和价格有利于上涨趋势，当指标为负时，时间和价格有利于下跌趋势。可以使用正负阈值来定义趋势的强度。例如，突破+50 将反映出强劲的上涨，而跌破-50 将表明强劲的下跌。

## 一般的趋势偏向

定义一般的趋势偏向是 Aroon 振荡器的最基本用途。该指标在强劲上升趋势中保持在正区间，在强劲下降趋势中保持在负区间。根据参数设置，短期趋势或波动交易可能会导致指标经常在零线上下移动。下图显示了迪士尼的两种不同 Aroon 振荡器设置：25 天和 75 天。25 天 Aroon 比 75 天 Aroon 更敏感。请注意，25 天 Aroon 在十八个月内超过八次穿越零线。75 天 Aroon 只穿越零线四次。图表分析师必须首先确定他们的时间框架，然后选择最能捕捉这个时间框架的设置。短期交易者显然会选择 25 天 Aroon 或更短的时间，而寻找 2-4 个月走势的持仓交易者会选择 75 天 Aroon。

![Aroon 振荡器 - 图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/f2d5ac47329234ee594c3bc1bbbf3536.jpg "Aroon 振荡器 - 图表 3")

图表还显示，Aroon 振荡器并不免疫滞后，因为振荡器在价格已经移动后才变为正或负。参数设置越长，滞后越多。不要期望通过正负交叉来捕捉底部或顶部。作为更多趋势跟踪指标，Aroon 振荡器识别可能足够强劲以信号开始持续趋势的走势。然而，并非所有趋势都会延伸。 

## 强劲的趋势偏向

图表分析师可以扩大多头和空头参数以进一步过滤信号。扩大参数将产生更多滞后和更长时间范围的信号。例如，多头阈值可以设置为+90，空头阈值为-90。+90 表示 Aroon-Up 在 90 到 100 之间，而 Aroon-Down 在 0 到 10 之间。对于低于-90 的读数，情况相反。这样的强劲读数发生在一个重大移动之后，可以预示着一个延续趋势的开始。超过+90 的移动被认为是多头的，直到通过低于-90 的移动来否定。这个水平足够深，可以吸收大部分上涨趋势中的回调。同样，低于-90 的移动被认为足够强大，可以信号延续性下降的开始。直到有一个高于+90 的移动，这个信号才会被扭转，这个水平足够高，可以吸收大部分超卖反弹。

![Aroon 振荡器 - 图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/c189e740a78b18f0373a7afe578a522f.jpg "Aroon 振荡器 - 图表 4")

谷歌（GOOG）图表显示了 Aroon 振荡器（25）的水平线在+90 和-90 处。该指标被添加了两次，并使用“高级选项”添加了水平线。在下面的 SharpCharts 部分显示了一个实时示例。尽管这些信号滞后，但它们比简单的零线交叉持续时间更长。显然，这些信号不会捕捉底部或顶部，因为它们发生在重大移动之后。此外，请注意在信号发出后，谷歌是如何反向移动的。在 2009 年 1 月的多头信号之后，出现了两次急剧的回调。在这些逆势移动之后，趋势继续朝着信号的方向发展。这些 90/90 信号可用于建立大趋势，然后沿着该趋势方向交易。例如，图表分析师可以在大趋势向上时（Aroon > +90）专注于多头信号。相反，当大趋势向下时（Aroon < -90），图表分析师可以专注于空头信号。图表分析师甚至可以微调多头和空头的阈值。但要小心不要过度拟合。

## 结论

Aroon Oscillator 将 Aroon-Up 和 Aroon-Down 指标合并为一个指标。这使得更容易识别两者中更强的那个。当 Aroon-Up 强于 Aroon-Down 时，振荡器为正，当 Aroon-Down 强于 Aroon-Up 时，振荡器为负。当振荡器为正时，存在一般的看涨偏向，当为负时存在看跌偏向。人们很容易寻找看涨和看跌的背离，但该指标并非为传统振荡器信号而设计。与所有技术指标一样，Aroon Oscillator 应与技术分析的其他方面一起使用，例如图表模式分析或动量指标。

## 使用 SharpCharts

Aroon Oscillator 在 SharpCharts 上作为一个指标可放置在基础证券的价格图表的上方、下方或后方。如上所述，用户可以添加两个具有相同参数的 Aroon Oscillators，然后单击绿色箭头以获取高级选项。然后可以添加水平线以设置看涨和看跌的阈值。这些阈值可能根据基础证券的特性而变化。单击下面的图像查看设置。SharpCharts 订阅者甚至可以通过单击图表右上角的“添加新”链接将此图表保存到其收藏列表中。**[点击这里](http://stockcharts.com/h-sc/ui?s=SPY&p=D&yr=1&mn=0&dy=0&id=p74556881166&a=214937192 "http://stockcharts.com/h-sc/ui?s=SPY&p=D&yr=1&mn=0&dy=0&id=p74556881166&a=214937192")** 查看带有 Aroon Oscillator 的实时图表。

![Aroon Oscillator - SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/842bef31f4ac71c23dffd3c795c1cb7f.jpg "Aroon Oscillator - SharpCharts")

![Aroon Oscillator - SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/d96e753d179ea6cd5d86472b6284d478.jpg "Aroon Oscillator - SharpCharts")

## 建议的扫描

### Aroon Oscillator 穿越零线

这个简单的扫描搜索股票，其中 Aroon Oscillator 从负区域穿越到正区域，而每日成交量高于成交量的 50 日移动平均线。换句话说，看涨交叉发生时成交量在扩大。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Aroon Osc(25) crosses 0] 
AND [Daily Volume > Daily SMA(50,Daily Volume)]
```

### Aroon Oscillator 穿越零线以下

这个简单的扫描搜索股票，其中 Aroon Oscillator 从正区域穿越到负区域，而每日成交量高于成交量的 50 日移动平均线。换句话说，看跌交叉发生时成交量在扩大。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [0 crosses Daily Aroon Osc(25)] 
AND [Daily Volume > Daily SMA(50,Daily Volume)]
```

欲了解更多有关 Aroon Oscillator 扫描语法的详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#aroon_oscillator "http://stockcharts.com/docs/doku.php?id=scans:indicators#aroon_oscillator")，位于支持中心。


# 平均趋向指数（ADX）

### 目录

+   平均趋向指数（ADX）

    +   介绍

    +   计算

        +   指标计算

        +   Wilder 的平滑技术

    +   解释

        +   趋势强度

    +   趋势方向和交叉点

    +   结论

    +   使用 SharpCharts

    +   建议扫描

        +   整体上涨，+DI 穿过-DI

        +   整体下跌，-DI 穿过+DI

    +   额外资源

        +   股票与商品杂志文章

## 介绍

平均趋向指数（ADX）、负向指标（-DI）和正向指标（+DI）代表了由 Welles Wilder 开发的一组方向运动指标，形成了一个交易系统。尽管 Wilder 设计他的方向运动系统时考虑了商品和每日价格，但这些指标也可以应用于股票。

正向和负向运动构成了方向运动系统的基础。Wilder 通过比较两个连续低点之间的差值与它们各自高点之间的差值来确定方向运动。

**正向指标（+DI）** 和 **负向指标（-DI）** 是由这些差值的平滑平均值导出的，它们测量了趋势随时间的***方向***。这两个指标通常被统称为方向运动指标（DMI）。

**平均趋向指数（ADX）** 反过来是由+DI 和-DI 之间的差值的平滑平均值导出的，它测量了趋势的***强度***（无论方向如何）随时间的变化。

使用这三个指标，图表分析师可以确定趋势的***方向***和***强度***。

Wilder 在他的 1978 年著作《技术交易系统中的新概念》中介绍了方向运动指标。这本书还包括了关于真实波幅（ATR）、抛物线 SAR 系统和 RSI 的详细信息。尽管是在计算机时代之前开发的，Wilder 的指标在计算上非常详细，并经受住了时间的考验。

## 计算

方向运动是通过比较两个连续低点之间的差异与它们各自高点之间的差异来计算的。

当前高点减去先前高点大于先前低点减去当前低点时，方向运动是**正数**（加号）。这种所谓的正向方向运动（+DM）等于当前高点减去先前高点，前提是它是正数。负值将简单地输入为零。

当前低点减去先前低点大于当前高点减去先前高点时，方向运动是**负数**（减号）。这种所谓的负向方向运动（-DM）等于先前低点减去当前低点，前提是它是正数。负值将简单地输入为零。

![图片](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/3339cb9422bd3e637443ef99c926525e.jpg)

上图显示了四个方向运动计算示例。第一对显示了强烈的正向方向运动（+DM）的高点之间的巨大正差异。第二对显示了一个外部日，负向方向运动（-DM）占优势。第三对显示了低点之间的巨大差异，形成强烈的负向方向运动（-DM）。最后一对显示了一个内部日，相当于没有方向运动（零）。正向方向运动（+DM）和负向方向运动（-DM）都是负数并恢复为零，因此它们互相抵消。所有内部日都将有零方向运动。

### 指标计算

平均定向指数（ADX）、正向指标（+DI）和负向指标（-DI）的计算步骤基于上面计算的正向方向运动（+DM）和负向方向运动（-DM）值，以及平均真实范围。+DM 和-DM 的平滑版本除以平均真实范围的平滑版本，以反映移动的真实幅度。

注意：未描述平均真实范围（ATR），因为整个 ChartSchool 文章都有关于这个。基本上，ATR 是 Wilder 对两周期交易范围的版本。

下面的计算示例基于一个 14 周期的指标设置，这是 Wilder 推荐的。

1.  为每个周期计算真实范围（TR）、正向方向运动（+DM）和负向方向运动（-DM）。

1.  使用 Wilder 的平滑技术平滑这些周期值。这些将在下一节详细解释。

1.  将 14 天平滑的正向方向运动（+DM）除以 14 天平滑的真实范围，以找到 14 天正向指标（+DI14）。乘以 100 将小数点移动两位。这个+DI14 是绿色的正向指标线（+DI），与 ADX 线一起绘制。

1.  将 14 天平滑的负向动向指标（-DM）除以 14 天平滑的真实范围，以找到 14 天的负向指标（-DI14）。乘以 100 将小数点移动两位。这个-DI14 是红色的负向指标线（-DI），与 ADX 线一起绘制。

1.  方向运动指数（DX）等于+DI14 减去-DI14 的绝对值除以+DI14 和-DI14 的总和。将结果乘以 100 将小数点移动两位。

1.  经过所有这些步骤，现在是计算平均趋向指数（ADX）线的时候了。第一个 ADX 值只是 DX 的 14 天平均值。随后的 ADX 值通过将前一个 14 天的 ADX 值乘以 13，加上最新的 DX 值，然后将总和除以 14 来平滑。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/0d0dabfcc23db99add7ffcf5182969bd.jpg)

上面是一个包含所有计算的电子表格示例。由于需要大约 150 个周期来吸收平滑技术，因此存在 119 天的计算间隙。ADX/DMI 爱好者可以点击此处下载")这个电子表格并查看详细信息。下面的图表显示了使用纳斯达克 100ETF（QQQQ）的 ADX 与+DI 和-DI 的示例。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/784b2ce5a39aaad9f2d73e3fca03b3aa.jpg)

### Wilder 的平滑技术

如 ADX、+DI 和-DI 的计算所示，涉及大量平滑处理，了解其影响很重要。由于 Wilder 的平滑技术，需要大约 150 个数据周期才能获得真实的 ADX 值。Wilder 在 RSI 和真实波幅计算中使用类似的平滑技术。仅使用 30 个历史数据周期的 ADX 值将无法匹配使用 150 个历史数据周期的 ADX 值。具有 150 天或更多数据的 ADX 值将保持一致。

第一种技术用于平滑每个周期的+DM1、-DM1 和 TR1 值，持续 14 个周期。与指数移动平均一样，计算必须从某个地方开始，因此第一个值只是前 14 个周期的总和。如下所示，平滑从第二个 14 周期计算开始，并持续进行。

```py
First TR14 = Sum of first 14 periods of TR1 
Second TR14 = First TR14 - (First TR14/14) + Current TR1 
Subsequent Values = Prior TR14 - (Prior TR14/14) + Current TR1
```

第二种技术用于平滑每个周期的 DX 值，以得到平均趋向指数（ADX）。首先，计算前 14 天的平均值作为起点。第二次和随后的计算使用以下平滑技术：

```py
First ADX14 = 14 period Average of DX 
Second ADX14 = ((First ADX14 x 13) + Current DX Value)/14 
Subsequent ADX14 = ((Prior ADX14 x 13) + Current DX Value)/14
```

## 解释

平均趋向指数（ADX）用于衡量趋势的强度或弱势，而不是实际方向。方向运动由+DI 和-DI 定义。一般来说，当+DI 大于-DI 时，多头占优势，而当-DI 大于+DI 时，空头占优势。这些方向指标的交叉可以与 ADX 结合使用，形成一个完整的交易系统。

在查看一些信号示例之前，请记住，Wilder 是一名商品和货币交易员。他书中的示例是基于这些工具，而不是股票。这并不意味着他的指标不能用于股票。一些股票具有类似商品的价格特征，往往更具有短期和强劲趋势的波动性。波动性较低的股票可能不会生成基于 Wilder 参数的信号。图表分析师可能需要根据证券的特性调整指标设置或信号参数。

### 趋势强度

在最基本的层面上，平均趋向指数（ADX）可用于确定证券是否处于趋势状态。这种判断有助于交易员选择趋势跟踪系统或非趋势跟踪系统。Wilder 建议当 ADX 高于 25 时存在强劲趋势，当低于 20 时不存在趋势。20 和 25 之间似乎存在一个灰色区域。如上所述，图表分析师可能需要调整设置以增加灵敏度和信号。由于所有平滑技术的影响，ADX 也存在相当大的滞后性。许多技术分析师使用 20 作为 ADX 的关键水平。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/eb5fabd1028aa4638404dbdfee96dad7.jpg)

上图显示了 Nordstrom（JWN）的 50 日简单移动平均线和 14 日平均趋向指数（ADX）。该股票在 4 月至 5 月间从强劲上升趋势转为强劲下降趋势，但 ADX 仍保持在 20 以上，因为强劲上升趋势迅速转变为强劲下降趋势。该股票在 2 月和 8 月形成底部时出现了两个非趋势期。在 8 月底部形成后，出现了强劲趋势，因为 ADX 上升到 20 以上并保持在 20 以上。

## 趋势方向和交叉

Wilder 提出了一个简单的交易系统，使用这些方向运动指标进行交易。第一个要求是 ADX 交易在 25 以上。这确保了价格正在趋势。然而，许多交易员使用 20 作为关键水平。当+DI 穿过-DI 时，会出现买入信号。Wilder 将初始止损设定为信号日的低点。只要这个低点保持，即使+DI 再次穿过-DI，信号仍然有效。在放弃信号之前，等待这个低点被突破。如果/当 ADX 转向上并且趋势加强时，这个多头信号会得到加强。一旦趋势发展并变得有利可图，交易员将不得不加入止损和移动止损，以防趋势持续。当-DI 穿过+DI 时，会触发卖出信号。卖出信号日的高点成为初始止损。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/cb3923d0ab1bf987c95e1c1af48e34c4.jpg)

上图显示了 Medco Health Solutions 的三个方向运动指标。请注意，使用 20 而不是 25 来确定 ADX 信号。较低的设置意味着更多可能的信号。绿色虚线表示买入信号，红色虚线表示卖出信号。为了专注于指标信号，Wilder 的初始止损未被纳入。正如图表清楚显示的那样，有大量的 +DI 和 -DI 交叉。一些发生在 ADX 大于 20 时以验证信号。其他发生在无效信号时。与大多数这类系统一样，会有虚假信号、好信号和坏信号。关键始终是要结合技术分析的其他方面。例如，2009 年 9 月的第一组虚假信号发生在一次整理期间。此外，这种整理看起来像一面旗帜，这是在上涨后形成的一种看涨整理。在形成看涨整理的情况下，忽略看跌信号是明智的。2010 年 6 月的买入信号发生在一个由破支撑和 50-62% 回撤区域标记的阻力区附近。在如此接近这一阻力区的情况下忽略买入信号是明智的。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/84c145349e142211e786c87d87b753f9.jpg)

上图显示了 AT&T（T）在 12 个月内出现的三个信号。这三个信号相当不错，前提是要获利并使用移动止损。Wilder 的拟合停损可以用来设置移动止损。请注意，在 3 月和 7 月买入信号之间没有卖出信号。这是因为当 -DI 在 4 月底超过 +DI 时，ADX 不到 20。

## 结论

Directional Movement System（方向运动系统）指标的计算复杂，解释简单，成功实施需要实践。 +DI 和 -DI 的交叉频繁发生，图表分析师需要用补充分析来过滤这些信号。设置 ADX 要求将减少信号，但这种超平滑的指标往往会过滤掉许多好信号和坏信号。换句话说，图表分析师可能考虑将 ADX 放在次要位置，专注于方向运动指标（+DI 和 -DI）来生成信号。这些交叉信号将类似于使用动量振荡器生成的信号。因此，图表分析师需要在其他地方寻找确认帮助。基于成交量的指标、基本趋势分析和图表模式可以帮助区分强势交叉信号和弱势交叉信号。例如，图表分析师可以在更大的趋势向上时专注于 +DI 买入信号，而在更大的趋势向下时专注于 -DI 卖出信号。

## 使用 SharpCharts

SharpCharts 用户可以通过从指标下拉列表中选择平均趋向指数（ADX）来绘制这三个方向运动指标。默认情况下，ADX 线为黑色，正向指标（+DI）为绿色，负向指标（-DI）为红色。这样可以轻松识别方向指标的交叉点。虽然 ADX 可以绘制在主价格图表的上方、下方或后面，但建议绘制在上方或下方，因为涉及到三条线。可以添加水平线来帮助识别 ADX 的变化。下面的图表示例还显示了 50 日简单移动平均线和抛物线 SAR 绘制在价格图表的后面。移动平均线用于过滤信号。只有在交易高于 50 日移动平均线时才使用买入信号。一旦启动，抛物线 SAR 可用于设置止损。[点击这里](http://stockcharts.com/h-sc/ui?s=AAPL&p=D&yr=0&mn=6&dy=0&id=p00212055984&listNum=30&a=224849203 "http://stockcharts.com/h-sc/ui?s=AAPL&p=D&yr=0&mn=6&dy=0&id=p00212055984&listNum=30&a=224849203") 查看 ADX 的实时示例。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/087aa74cee0a8201b012f0e546dff45e.jpg)

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/f07ddbee5e38107caeab5b3fe20a8593.jpg)

## 建议扫描

### 总体上升趋势，+DI 穿过-DI

这个扫描从平均每日成交量为 100,000 股且平均收盘价高于 10 美元的股票开始。当交易高于 50 日简单移动平均线时存在上升趋势。当 ADX 高于 20 时可能出现买入信号。当+DI 移动到-DI 上方时，这个信号会实现。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily ADX Line(14) > 20] 
AND [Daily Plus DI(14) crosses Daily Minus DI(14)] 
AND [Daily Close > Daily SMA(50,Daily Close)]
```

### 总体下降趋势，-DI 穿过+DI

这个扫描从平均每日成交量为 100,000 股且平均收盘价高于 10 美元的股票开始。当交易低于 50 日简单移动平均线时存在下降趋势。当 ADX 高于 20 时可能出现卖出信号。当-DI 移动到+DI 上方时，这个信号会实现。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily ADX Line(14) > 20] 
AND [Daily Minus DI(14) crosses Daily Plus DI(14)] 
AND [Daily Close < Daily SMA(50,Daily Close)]
```

欲了解如何使用平均趋向指数、正向 DI 和负向 DI 扫描的语法详情，请参阅我们支持中心的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#average_directional_indicator "http://stockcharts.com/docs/doku.php?id=scans:indicators#average_directional_indicator")。

* * *

## 其他资源

### 股票与商品杂志文章

**[平均趋向运动指数（ADX）作者：汤姆·哈特尔](http://stockcharts.com/h-mem/tascredirect.html?artid=\V09\C03\ADX.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V09\C03\ADX.pdf")**

1991 年 2 月 - 股票与商品 V. 9:3 (101-102)

**[专家如何使用平均趋向指数，作者：芭芭拉·斯塔尔，博士](http://stockcharts.com/h-mem/tascredirect.html?artid=\V17\C10\076HOW.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V17\C10\076HOW.pdf")**

1999 年 9 月 - 股票与商品

* * *


# 真实波动幅度（ATR）

### 目录

+   平均真实波动幅度（ATR）

    +   介绍

    +   真实波动幅度

    +   计算

    +   绝对 ATR

    +   结论

    +   与 SharpCharts 一起使用

    +   建议扫描

        +   排除高波动性

    +   额外资源

        +   股票与商品杂志文章

## 介绍

由 J.韦尔斯·怀尔德（J. Welles Wilder）开发，平均真实波动幅度（ATR）是一种衡量波动性的指标。与他的大多数指标一样，怀尔德设计 ATR 时考虑了商品和每日价格。商品通常比股票更具波动性。它们经常受到间隙和涨跌停限制的影响，当商品开盘时向上或向下移动到当日允许的最大幅度。基于高低范围的波动性公式无法捕捉间隙或涨跌停限制移动的波动性。怀尔德创建了平均真实波动幅度来捕捉这种“缺失”的波动性。重要的是要记住，ATR 并不提供价格方向的指示，只是波动性。

怀尔德在他的 1978 年著作《技术交易系统中的新概念》中介绍了 ATR。这本书还包括抛物线 SAR、RSI 和方向运动概念（ADX）。尽管是在计算机时代之前开发的，怀尔德的指标经受住了时间的考验，仍然非常受欢迎。

## 真实波动幅度

怀尔德最初提出了一个称为**真实波动幅度（TR）**的概念，它被定义为以下三者中的最大值：

+   方法 1：当前高价减去当前低价

+   方法 2：当前高价减去前一日收盘价（绝对值）

+   方法 3：当前低价减去前一日收盘价（绝对值）

使用绝对值确保为正数。毕竟，怀尔德感兴趣的是测量两点之间的距离，而不是方向。如果当前周期的高价高于前一周期的高价，且低价低于前一周期的低价，则当前周期的高低范围将被用作真实波动幅度。这是一个使用方法 1 计算 TR 的外部日。这非常直接了当。当存在间隙或内部日时，将使用方法 2 和 3。间隙发生在前一日收盘价高于当前高价（表示可能的向下间隙或涨跌停限制移动）或前一日收盘价低于当前低价（表示可能的向上间隙或涨跌停限制移动）时。下面的图像显示了何时适合使用方法 2 和 3 的示例。

![ATR - 真实波动幅度图像](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/6c7cbf77edbb814a44b1e0ddfd30df1e.jpg "ATR - 真实波动幅度图像")

示例 A：间隙上涨后形成的小高低范围。TR 等于当前高价与前一日收盘价之间的差的绝对值。

示例 B：在跳空下跌后形成了一个较小的高/低范围。TR 等于当前最低价和前一收盘价之间的差值的绝对值。

示例 C：尽管当前收盘价在前一高/低范围内，但当前高/低范围非常小。事实上，它比当前高价和前一收盘价之间的差值的绝对值还要小，而这个差值用于计算 TR。

## 计算

通常，平均真实范围（ATR）基于 14 个周期，并可以根据分钟、日、周或月的基础数据进行计算。在这个示例中，ATR 将基于日数据。因为必须有一个起点，第一个 TR 值简单地是最高价减去最低价，而前 14 天的 ATR 是过去 14 天的每日 TR 值的平均值。之后，Wilder 试图通过纳入前一期的 ATR 值来平滑数据。

```py

Current ATR = [(Prior ATR x 13) + Current TR] / 14

  - Multiply the previous 14-day ATR by 13.
  - Add the most recent day's TR value.
  - Divide the total by 14

```

![ATR - 电子表格](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/4e5fdcdb3297687e6a55a9ba1a1e3c3b.jpg "ATR - 电子表格")

点击这里查看一个 Excel 电子表格")，展示了 QQQ ATR 计算的开始。

在电子表格示例中，第一个真实范围值（.91）等于最高价减去最低价（黄色单元格）。第一个 14 天 ATR 值（.56）是通过计算前 14 个真实范围值的平均值（蓝色单元格）得出的。随后的 ATR 值使用上述公式进行平滑处理。电子表格中的数值对应下图中的黄色区域。请注意，随着 QQQ 在五月份暴跌并出现许多长蜡烛图，ATR 值激增。

![ATR - 图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/a7861e6f3a4e458eec5688b13a3cfccc.jpg "ATR - 图表 1")

对于那些在家尝试的人，有一些注意事项。首先，就像指数移动平均线（EMAs）一样，ATR 值取决于你从多远的历史数据开始计算。第一个真实范围值简单地是当前最高价减去当前最低价，而第一个 ATR 是前 14 个真实范围值的平均值。真正的 ATR 公式直到第 15 天才开始生效。即便如此，这两个计算的残留效应会略微影响随后的 ATR 值。对于一小部分数据的电子表格数值可能与价格图表上看到的不完全匹配。小数四舍五入也可能会略微影响 ATR 值。在我们的图表中，我们至少计算了 250 个周期（通常更多），以确保我们的 ATR 值更加准确。

## 绝对 ATR

ATR 基于真实范围，使用绝对价格变动。因此，ATR 反映波动性作为绝对水平。换句话说，ATR 不显示为当前收盘价的百分比。这意味着低价股的 ATR 值将低于高价股。例如，一只$20-30 的证券的 ATR 值将远低于一只$200-300 的证券。由于这个原因，ATR 值是不可比较的。即使对于单个证券的大幅价格波动，比如从 70 下跌到 20，也会使长期 ATR 比较变得不切实际。图表 4 显示了谷歌的两位数 ATR 值，图表 5 显示了微软的 ATR 值低于 1。尽管值不同，它们的 ATR 线形状相似。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/207f49e32b661497845df4fe774b04f7.jpg)

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/c5b5e44faaa25c8f45d7430fd33ea31f.jpg)

## 结论

ATR 不是一个方向性指标，如 MACD 或 RSI。相反，ATR 是一个反映移动的兴趣或不感兴趣程度的独特波动性指标。强劲的移动，无论是向任何方向，通常伴随着大范围或大真实范围。这在移动开始时尤其明显。乏味的移动可能伴随着相对较窄的范围。因此，ATR 可用于验证移动或突破背后的热情。具有 ATR 增加的牛市逆转将显示强劲的买盘压力并加强逆转。具有 ATR 增加的熊市支撑突破将显示强劲的卖盘压力并加强支撑突破。

## 使用 SharpCharts

在指标下拉菜单中列为“平均真实范围”，ATR。指标右侧的“参数”框包含用于平滑数据的周期数的默认值，14。要调整周期设置，请突出显示默认值并输入新设置。Wilder 经常使用 8 周期 ATR。SharpCharts 还允许用户将指标放置在价格图表的上方、下方或后面。可以添加移动平均线以识别 ATR 的上升或下降。单击“高级选项”以将移动平均线添加为指标叠加。[点击这里](http://stockcharts.com/h-sc/ui?s=$INDU&p=D&b=5&g=0&id=p51341747448&listNum=30&a=202613287 "http://stockcharts.com/h-sc/ui?s=$INDU&p=D&b=5&g=0&id=p51341747448&listNum=30&a=202613287")查看 ATR 的实时示例。

![ATR - SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/ee27c0be5574d4226be3c3b0d63cda12.jpg "ATR - SharpCharts")

## 建议的扫描

### 筛选出高波动性

平均真实范围指标可用于扫描以筛选出波动极高的证券。这个简单的扫描搜索处于上升趋势的 S&P 600 股票。最终的扫描条款排除了高波动性股票的结果。请注意，ATR 被转换为一种百分比，以便可以在相同的比例上比较不同股票的 ATR。

```py
[group is SP600]
AND [Daily EMA(50,close) > Daily EMA(200,close)]  

AND [ATR(250) / SMA(20,Close) * 100 < 4] 
```

欲了解有关 ATR 扫描使用的语法详情，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#average_true_range_atr "http://stockcharts.com/docs/doku.php?id=scans:indicators#average_true_range_atr")在支持中心。

## 其他资源

### 股票与商品杂志文章

**[工作资金：真实波幅 by Sharon Yamanaka](http://stockcharts.com/h-mem/tascredirect.html?artid=\V20\C03\054ATR.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V20\C03\054ATR.pdf")**

2002 年 2 月 - 股票与商品

**[哪种波动率度量方法？by Gordon Gustafson](http://stockcharts.com/h-mem/tascredirect.html?artid=\V19\C06\067VOL.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V19\C06\067VOL.pdf")**

2001 年 5 月 - 股票与商品 V. 19:6 (46-50)


# 布林带宽度 

### 目录

+   布林带宽度

    +   介绍

    +   SharpCharts 计算

    +   定义窄度

    +   信号：挤压

    +   摘要

    +   与 SharpCharts 一起使用

    +   与 MarketCarpets 一起使用

    +   建议的扫描

        +   布林带突破

## 介绍

布林带宽度是从布林带衍生出的指标。在他的书《布林带上的布林格》中，约翰·布林格将布林带宽度称为可以从布林带中衍生出的两个指标之一。另一个指标是%B。

带宽度衡量上带和下带之间的百分比差异。随着布林带变窄，带宽度减小，随着布林带扩大，带宽度增加。由于布林带基于标准差，带宽度的下降反映了波动性的减少，而带宽度的上升反映了波动性的增加。

## SharpCharts 计算

```py
( (Upper Band - Lower Band) / Middle Band) * 100

```

布林带由一个中间带和两个外部带组成。中间带通常设置为 20 个周期的简单移动平均。外部带通常设置为中间带上下 2 个标准差。设置可以根据特定证券或交易风格的特征进行调整。

在计算带宽时，第一步是从上带的值中减去下带的值。这显示了绝对差异。然后将此差异除以中间带，这将使值标准化。然后可以在不同时间段内或与其他证券的带宽值进行比较。

![图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/8bd0aeb209a3a38dfff98b8965105e8a.jpg "图表 1")

上图显示了纳斯达克 100 ETF（QQQ）的布林带、带宽度和标准差。请注意带宽度如何跟踪标准差（波动性）。两者一起上升和下降。下图显示了一个带有计算示例的电子表格。

![电子表格 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/419fa826e8678c1f564a5b12dcf646f4.jpg "电子表格 1")

## 定义窄度

窄带宽是相对的。带宽值应该相对于一段时间内先前的带宽值进行评估。重要的是要获得一个良好的回顾期，以定义特定 ETF、指数或股票的带宽范围。例如，八到十二个月的图表将显示一段重要时间内的带宽高点和低点。当带宽接近此范围的低点时被认为是窄的，当接近高点时被认为是宽的。

![图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/101cfde779c6dc426a5112525e9d7919.jpg "图表 2")

![图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/c2ea79b827cdab1e1534f6b739ab70f8.jpg "图表 3")

低波动性证券的 BandWidth 值将低于高波动性证券。例如，Utilities SPDR（XLU）代表公用事业股票，其波动性相对较低。Technology SPDR（XLK）代表科技股票，其波动性相对较高。由于低波动性，XLU 的 BandWidth 值将始终低于 XLK。XLU 的 BandWidth 200 日移动平均值低于 5，而 XLK 的 BandWidth 200 日移动平均值高于 7。

## 信号：挤压

Bollinger BandWidth 最为人所知的是用于识别“挤压”现象。当波动性降至非常低的水平时，就会出现狭窄的带状。上下带基于标准偏差，这是波动性的一种度量。当价格趋于平稳或在相对狭窄的范围内波动时，带状变窄。理论认为，低波动性期后将会出现高波动性期。相对较窄的 BandWidth（也称为挤压）可能预示着重大上涨或下跌。挤压后，价格激增并随后带状突破信号标志着新趋势的开始。新的上涨始于挤压和随后突破上带。新的下跌始于挤压和随后突破下带。

图表 2 显示了阿拉斯加航空（ALK）在 6 月中旬出现的挤压现象。在 4 月至 5 月下跌后，ALK 在 6 月初稳定下来，因为 Bollinger 带变窄。BandWidth 下降到 10 以下，使 6 月中旬的挤压现象出现。请记住，10 指的是 10%。换句话说，带的宽度等于中间带的 10%。尽管这个水平看起来很高，但对于 ALK 来说实际上相当低。股价在 15-16 左右时，BandWidth 低于 10%，是一年多来的最低水平。随着股价突破上带，股票开始大幅上涨。

![图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/6c133691e15036f8ec526db70662778d.jpg "图表 4")

图表 3 显示了 Aeropostale（ARO）出现了几次挤压现象。在指标窗口中添加了一条水平线。这条线标记为 8，根据历史范围被认为相对较低。BandWidth 指标提醒交易者准备在 8 月中旬进行交易。股票随后突破上带并在整个 9 月持续上涨。上涨在 9 月底停滞，BandWidth 再次收窄在 10 月。请注意，BandWidth 下降到低于 8 月份设定的低点，然后趋于平稳。随后在 10 月底突破下轨的信号触发了一个熊市信号。

![图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/3a533d1f5b5762881484c97d9a00b5dd.jpg "图表 5")

挤压也可以应用于周线图或更长的时间框架。周线时间框架上的波动性和带宽通常比日线时间框架上更高。这是因为在更长的时间框架上可以预期更大的价格波动。图 4 显示了 Barrick Gold (ABX) 在 2006 年和 2007 年持续整理。随着整理变窄并形成三角形，布林带收缩，带宽在 2007 年 1 月下降到 10 以下。请注意，随着整理的延伸，带宽保持在低水平。在 2007 年 7 月突破时触发了一个看涨信号。随着价格朝一个方向急剧变动，布林带也扩大，带宽也上升。

![图表 6](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/012e4c92bffebf8d406af9e3d3a12955.jpg "图表 6")

图 5 显示了 Honeywell (HON) 在 50-55 区域的扩展交易范围。5 月份价格上涨到上轨，但没有突破信号。相反，HON 明显跌破下轨，于 2007 年 6 月触发了一个看跌信号。

![图表 7](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/729369505c25ce3c7aa56f3ed9264230.jpg "图表 7")

## 总结

带宽指标可用于识别布林带挤压。这警示图表分析师准备行动，但方向取决于随后的带突破。挤压后上轨突破是看涨的，而下轨突破是看跌的。但要小心虚假突破。有时第一次突破未能保持，价格会反转。强劲的突破保持并且很少回头。上涨突破后立即回调应作为警告。

## 使用 SharpCharts

带宽指标可以在 SharpCharts 的指标列表中找到。默认参数（20,2）基于布林带的默认参数。这些可以相应地更改。20 代表简单移动平均。2 代表上下轨的标准差数。带宽可以放置在价格图的上方、下方或后面。[点击这里](http://stockcharts.com/h-sc/ui?s=SPY&p=D&yr=0&mn=6&dy=0&id=p38029592805&listNum=30&a=195096097 "http://stockcharts.com/h-sc/ui?s=SPY&p=D&yr=0&mn=6&dy=0&id=p38029592805&listNum=30&a=195096097") 查看带宽的实时示例。

![图表 8](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/224833de27c84ea95f9553b76b87112a.jpg "图表 8")

## 使用 MarketCarpets

标准化的布林带宽显示在市场地毯中，这使用户可以比较多个证券的带宽。以[S&P 行业市场地毯](http://stockcharts.com/freecharts/carpet.html "http://stockcharts.com/freecharts/carpet.html")为例，选择布林带宽，然后点击三角形的Δ图标查看绝对水平。有阴影的Δ图标显示百分比变化。白色的Δ图标显示绝对水平。绿色框显示带宽相对较宽的股票。浅色框显示带宽相对较窄的股票。在市场地毯右下方显示带宽最窄的股票列表（底部 5）。点击名称可查看上方的小图表。用户可以通过点击行业标题（例如技术）来深入了解各个行业。有九个行业和每个行业列出的底部 5 个股票，用户可以快速查看相对带宽较窄的 45 只股票。

![图表 9](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/355729f80d9c152bfee8122a2d3e8982.jpg "图表 9")

## 建议的扫描

### 布林带突破

此扫描显示了布林带在收缩 5 天或更长时间后迅速扩张的股票。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily BB Width(20,2) > Yesterday's max(5, BB Width(20,2)) * 2]
```

有关用于带宽扫描的语法的更多详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#bollinger_band_width_bb_width "http://stockcharts.com/docs/doku.php?id=scans:indicators#bollinger_band_width_bb_width")在支持中心。


# %B 指标 

### 目录

+   %B 指标](#b_indicator)

    +   简介

    +   计算方法

    +   信号：超买/超卖

    +   信号：趋势识别

    +   结论

    +   与 SharpCharts 一起使用

    +   建议扫描

        +   %B 上升趋势扫描

        +   %B 下降趋势扫描

## 简介

%B 量化了一个证券的价格相对于上下布林带的关系。有六个基本的关系水平：

+   当价格位于上轨时，%B 等于 1

+   当价格位于下轨时，%B 等于 0

+   当价格高于上轨时，%B 大于 1

+   当价格低于下轨时，%B 低于 0

+   当价格高于中轨（20 日简单移动平均线）时，%B 大于 0.50

+   当价格低于中轨（20 日简单移动平均线）时，%B 低于 0.50

## 计算

```py
%B = (Price - Lower Band)/(Upper Band - Lower Band)

```

%B 的默认设置基于布林带（20,2）的默认设置。这些带子设置在 20 日简单移动平均线的上下 2 个标准差处，这也是中轨。证券价格是收盘价或最后交易价。

## 信号：超买/超卖

%B 可用于识别超买和超卖情况。然而，重要的是要知道何时寻找超买读数和何时寻找超卖读数。与大多数动量振荡器一样，最好在中期趋势向上时寻找短期超卖情况，在中期趋势向下时寻找短期超买情况。换句话说，在寻找超买或超卖读数之前，要先定义更大的趋势。

图表 1 显示了苹果（AAPL）处于强劲上升趋势中。请注意，%B 多次上升到 1 以上，但甚至没有接近 0。即使%B 多次上升到 1 以上，这些“超买”读数也没有产生良好的卖出信号。随着苹果在下轨上方迅速反转并恢复其上升趋势，回调幅度较小。约翰·布林格在强劲趋势中提到“走在带子上”。在强劲上升趋势中，价格可以沿着上轨上涨，很少触及下轨。相反，在强劲下跌趋势中，价格可以沿着下轨下跌，很少触及上轨。

![图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/c4fa534a5d5084d8eec51018e540dc06.jpg "图表 1")

在确认了更大的上升趋势后，当%B 移动到零或以下时，可以认为%B 被超卖了。记住，当价格触及下轨时，%B 会移动到零，当价格低于下轨时，%B 会低于零。这代表了一个比 20 日移动平均线低 2 个标准差的移动。图表 2 显示了纳斯达克 100 ETF（QQQQ）在 2009 年 3 月开始的上升趋势中。在这一上升趋势中，%B 在零以下移动了三次。7 月初和 11 月初的超卖读数为参与更大上升趋势提供了良好的入场点（绿色箭头）。

![图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/52356e78881d017a2e0ca7130dd14ba3.jpg "图表 2")

## 信号：趋势识别

约翰·波林格描述了一个使用%B 和资金流指数（MFI）的趋势跟踪系统。当%B 高于 0.80 且 MFI(10)高于 80 时，开始了一段上升趋势。MFI 的取值范围在 0 到 100 之间。当 MFI(10)超过 80 时，处于其范围的上 20%，这是一个强劲的读数。当%B 低于 0.20 且 MFI(10)低于 20 时，可以识别出下降趋势。

图表 3 显示了联邦快递（FDX）的%B 和 MFI(10)。自 7 月底%B 高于 0.80 且 MFI 高于 80 时开始了一段上升趋势。这一上升趋势随后在 9 月初和 11 月中旬得到了另外两个信号的确认。虽然这些信号对于趋势识别是有益的，但交易者在经历如此大的波动后可能会遇到风险回报比的问题。要让%B 高于 0.80 且 MFI(10)高于 80 同时发生，需要有大幅价格上涨。交易者可以考虑使用这种方法来识别趋势，然后寻找适当的超买或超卖水平以获得更好的入场点。

![图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/399aab008a29a4f5157274f8fd11b0d7.jpg "图表 3")

## 结论

%B 量化了价格与波林格带之间的关系。高于 0.80 的读数表明价格接近上轨。低于 0.20 的读数表明价格接近下轨。朝向上轨的激增显示出力量，但有时可能被解释为超买。朝向下轨的暴跌显示出弱势，但有时可能被解释为超卖。很多情况取决于基础趋势和其他指标。虽然%B 本身可能具有一定价值，但最好与其他指标或价格分析一起使用。[点击这里](http://stockcharts.com/h-sc/ui?s=$SPX&p=D&yr=0&mn=6&dy=0&id=p62195116429&listNum=61&a=259167452 "http://stockcharts.com/h-sc/ui?s=$SPX&p=D&yr=0&mn=6&dy=0&id=p62195116429&listNum=61&a=259167452") 查看实时图表。

## 使用 SharpCharts

%B 可在 SharpCharts 的指标列表中找到。默认参数（20,2）基于布林带的默认参数。这些可以相应地进行更改。20 代表简单移动平均。2 代表上下轨的标准偏差数量。%B 可以位于价格图表的上方、下方或后方。[点击这里](http://stockcharts.com/h-sc/ui?s=$SPX&p=D&yr=0&mn=6&dy=0&id=p62195116429&listNum=61&a=259167452 "http://stockcharts.com/h-sc/ui?s=$SPX&p=D&yr=0&mn=6&dy=0&id=p62195116429&listNum=61&a=259167452") 查看 %B 的实时示例。

![图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/425ebea37a0c8a5ab7614f2e902ca3c7.jpg "图表 4")

## 建议的扫描

### %B 上升趋势扫描

此扫描筛选出 %B 大于 0.80 且 MFI 刚刚突破 80 的股票。根据布林格尔的说法，这些股票可能开始新的上涨。这个扫描只是一个起点。需要进一步的细化和分析。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 5] 

AND [Daily %B(20,2.0,Daily Close) > 0.8] 
AND [Daily MFI(14) > 80] 
AND [Yesterday's Daily MFI(14) < 80]
```

### %B 下降趋势扫描

此扫描筛选出 %B 低于 0.20 且 MFI 刚刚跌破 20 的股票。根据布林格尔的说法，这些股票可能开始新的下跌。这个扫描只是一个起点。需要进一步的细化和分析。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 5] 

AND [Daily %B(20,2.0,Daily Close) < 0.2] 
AND [Daily MFI(14) < 20] 
AND [Yesterday's Daily MFI(14) > 20]
```

有关用于 %B 扫描的语法详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#bollinger_s_b_indicator "http://stockcharts.com/docs/doku.php?id=scans:indicators#bollinger_s_b_indicator") 在支持中心。


# 查金资金流量 

### 目录

+   查金资金流量

    +   介绍

    +   计算

    +   解释

    +   买入/卖出压力

    +   计算特点

    +   结论

    +   与 SharpCharts 一起使用

    +   建议的扫描

        +   查金资金流量转为正值且 RSI 移动超过 50

        +   查金资金流量转为负值且 RSI 移动低于 45

    +   进一步研究

    +   其他资源

        +   股票与商品杂志文章

## 介绍

由马克·查金（Marc Chaikin）开发，查金资金流量（Chaikin Money Flow）衡量了特定时期内的资金流量量。资金流量量构成了积累分布线的基础。查金资金流量不是资金流量量的累积总和，而是简单地对特定回顾期内的资金流量量进行求和，通常为 20 或 21 天。所得指标像振荡器一样在零线上下波动。图表分析师根据查金资金流量的绝对水平权衡买入或卖出压力的平衡。图表分析师还可以寻找在零线上方或下方的交叉点，以识别资金流动的变化。

## 计算

计算查金资金流量（CMF）有四个步骤。下面的示例基于 20 个时期。首先，计算每个时期的资金流量乘数。其次，将此值乘以该时期的交易量，以找到资金流量量。第三，对 20 个时期的资金流量量进行求和，并除以 20 个时期的交易量总和。

```py

  1\. Money Flow Multiplier = [(Close  -  Low) - (High - Close)] /(High - Low) 

  2\. Money Flow Volume = Money Flow Multiplier x Volume for the Period

  3\. 20-period CMF = 20-period Sum of Money Flow Volume / 20 period Sum of Volume 

```

每个时期的资金流量量取决于资金流量乘数。当收盘价位于该时期最高-最低范围的上半部时，该乘数为正；当收盘价位于下半部时，该乘数为负。当收盘价等于最高价时，乘数为 1；当收盘价等于最低价时，乘数为-1。通过这种方式，乘数调整了最终进入资金流量量的量。除非资金流量乘数处于极端值（+1 或-1），否则实际上会减少交易量。

![图表 1 - 查金资金流量](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/4f96a964b17239a0eb9ab8287749a875.jpg "图表 1 - 查金资金流量")

上表显示了使用 Research in Motion（RIMM）的每日数据的一些示例。请注意，当股票在 1 月 5 日收盘时，乘数接近 +1。当股票在 1 月 18 日收盘时，乘数下降到 -0.97。当股票在 12 月 29 日收盘时，乘数接近零（-0.07），股票收于其高低范围的中点附近。点击这里") 查看 Excel 电子表格中 Chaikin Money Flow 的计算示例。

## 解释

Chaikin Money Flow（CMF）是在 -1 和 +1 之间波动的振荡器。极少情况下，指标会达到这些极端值。要使 20 天 Chaikin Money Flow 达到 +1（-1），需要连续 20 次收盘在高位（低位）。通常，这个振荡器在 -0.50 和 +0.50 之间波动，以零为中心线。

![图表 2  -  Chaikin Money Flow](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/84cabf5a30f42df1866f979d62d26555.jpg "图表 2  -  Chaikin Money Flow")

Chaikin Money Flow 衡量了一段时间内的买卖压力。进入正区域表示买盘压力，而进入负区域表示卖盘压力。图表分析师可以使用 Chaikin Money Flow 的绝对值来确认或质疑基础资产的价格走势。正 CMF 将确认上升趋势，但负 CMF 将质疑上升趋势背后的力量。对于下降趋势，情况相反。

## 买入/卖出压力

Chaikin Money Flow 可以用正值或负值简单地定义一般的买入或卖出偏见。该指标在零线上方/下方振荡。一般来说，当指标为正时，买盘压力更强，当指标为负时，卖盘压力更强。

虽然这个零线交叉看起来很简单，但实际情况要复杂得多。 Chaikin Money Flow 有时只是短暂地穿过零线，指标的变化几乎没有积极或消极的后续。没有跟进，这个零线交叉最终变成了一个鞭炮（错误信号）。图表分析师可以通过设置牛市阈值略高于零（+0.05）和熊市阈值略低于零（-0.05）来使用缓冲区来过滤这些信号。这些阈值不会完全消除错误信号，但可以帮助减少鞭炮并过滤掉较弱的信号。

![图表 2  -  Chaikin Money Flow](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/05718bc39a9021d21080dd33a7760b4e.jpg "图表 2  -  Chaikin Money Flow")

上面的图表显示了 Freeport McMoran (FCX) 的 20 天 Chaikin Money Flow 在指标窗口中。在 2010 年 2 月至 12 月之间至少有 10 次零线交叉。增加一个小缓冲区大大减少了多头和空头信号的数量。移动超过 +0.05 被视为多头，而移动低于 -0.05 被视为空头。只有三个信号。虽然这些信号会稍晚一些出现，但减少误导可能是值得的。

![图表 3  -  Chaikin Money Flow](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/13932b381e4912f0a447d9c75e3e8d9b.jpg "图表 3  -  Chaikin Money Flow")

Harley Davidson (HOG) 的图表显示了一些良好的信号和五月反弹的误导。CMF 在几天内上升到 +0.05 以上，但这个动作未能持续，指标在六月初再次跌破 -0.05。误导将会发生，特别是在波动期间或趋势变平时。CMF 在七月转为多头，并在今年的其余时间保持多头。请注意，HOG 形成了一个下降楔形，在八月回撤了超过 62%，而此时 CMF 仍处于多头模式。这次回撤提供了第二次参与 CMF 信号的机会。

![图表 4  -  Chaikin Money Flow](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/7621610bd32ba1b0a59609743acfa831.jpg "图表 4  -  Chaikin Money Flow")

Chaikin Money Flow 并不适用于所有证券。上面的图表显示了 P.F. Chang (PFCB) 的一些 18 次在 +0.05 或 -0.05 以上的交叉。基于这些交叉来制定 CMF 信号导致了一次又一次的误导。分析基本价格趋势和特定证券的指标特征是很重要的。PFCB 表现出一些趋势，但在这个趋势内的价格波动很大，资金流动无法保持正面或负面偏向。最好为这些股票找到不同的指标。

## 计算怪癖

Chaikin Money Flow 中的资金流乘数关注收盘价相对于给定期间（日、周、月）的高低范围的水平。根据这个公式，一支证券可能会跳空下跌并收盘明显较低，但如果收盘价高于高低范围的中点，资金流乘数将上升。下面的图表显示了 Clorox (CLX) 的大幅跳空下跌，收盘价接近当天的高低范围顶部。尽管股价在高交易量下急剧下跌，但由于资金流乘数为正且交易量远高于平均水平，Chaikin Money Flow 上升。忽略从收盘到收盘的变化意味着 Chaikin Money Flow 有时会与价格脱节。

![图表 5  -  Chaikin Money Flow](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/f8c8017066653f851b4cb536e3f37936.jpg "图表 5  -  Chaikin Money Flow")

当一只证券跳空上涨并且收盘接近当天的低点时，相反的情况可能发生。下图显示了 Travelers（TRV）在当天跳空上涨并收盘超过 1%。尽管有这一跳升，但收盘接近当天的低点，这导致了一个接近-1 的资金流乘数。因此，几乎所有的交易量都被计为负资金流，Chaikin Money Flow 下降了。

![Chart 6  -  Chaikin Money Flow](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/fe882824fad9da1afa3ad218abd98050.jpg "Chart 6  -  Chaikin Money Flow")

## 结论

Chaikin Money Flow 是一种振荡器，用于衡量一段时间内的买入和卖出压力。在最基本的情况下，当 CMF 为正时，资金流向看涨，当为负时看跌。寻找更快资金流向变化的图表分析师可以寻找看涨和看跌的背离。不过要小心。即使存在看涨背离，卖出压力仍然占优势。这种看涨背离只是显示了较少的卖出压力。要指示实际的买入压力，需要进入正区域。作为资金流振荡器，CMF 可以与纯价格振荡器一起使用，例如 MACD 或 RSI。与所有指标一样，Chaikin Money Flow 不应作为独立指标使用。马克·查金还开发了积聚分配线和查金振荡器。

## 使用 SharpCharts

Chaikin Money Flow 可以设置为主窗口上方或下方的指标。由于它以区域格式显示，因此不适合放置在证券价格图后面。一旦从下拉列表中选择指标，就会出现默认参数（20）。这些参数可以调整以增加或减少灵敏度。用户可以点击“高级选项”添加水平线、移动平均线或其他叠加。图表分析师甚至可以在其他指标上方绘制第二个更长的 Chaikin Money Flow 指标。重叠期显示了两个不同期间的资金流强劲。[点击这里查看实时示例](http://stockcharts.com/h-sc/ui?s=AAPL&p=D&yr=0&mn=8&dy=0&id=p77394964602&listNum=30&a=223019825 "http://stockcharts.com/h-sc/ui?s=AAPL&p=D&yr=0&mn=8&dy=0&id=p77394964602&listNum=30&a=223019825")。

![Chart 7  -  Chaikin Money Flow](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/b48cb1392a499fc33cf3ba27363f8ed6.jpg "Chart 7  -  Chaikin Money Flow")

![SharpCharts  -  Chaikin Money Flow](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/7f77bf110b389674d4ec4987eca8780e.jpg "SharpCharts  -  Chaikin Money Flow")

## 建议的扫描

### Chaikin Money Flow 转为正值，RSI 上升至 50 以上

这个扫描从股价至少为$10 且过去 60 天日均交易量为 100,000 的股票开始。当查金货币流指标进入正区时，会识别出积累和买入压力。当相对强弱指标（RSI）上穿 50，即其中线时，价格动量得到确认。这个扫描旨在作为进一步分析和尽职调查的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily CMF(20) crosses 0] 
AND [Daily RSI(14,Daily Close) crosses 50]
```

### 查金货币流指标转为负值，RSI 下穿 45

这个扫描从股价至少为$10 且过去 60 天日均交易量为 100,000 的股票开始。当查金货币流指标进入负区时，会识别出分销和卖出压力。当相对强弱指标（RSI）下穿 50，即其中线时，价格动量得到确认。这个扫描旨在作为进一步分析和尽职调查的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [0 crosses Daily CMF(20)] 
AND [50 crosses Daily RSI(14,Daily Close)]
```

有关查金货币流扫描的语法详细信息，请参阅我们支持中心的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#chaikin_money_flow_cmf "http://stockcharts.com/docs/doku.php?id=scans:indicators#chaikin_money_flow_cmf")。

**注意**：出于扫描目的，交易日内的日交易量数据是不完整的。在运行基于交易量的指标（如 CMF）的扫描时，请确保基于“上次市场收盘价”。其他基于交易量的指标的示例包括积累/分布指标、成交量平衡指标和 PVO。

## 进一步研究

这本书通过简单清晰的解释涵盖了所有内容。墨菲涵盖了大部分主要的图表模式和指标。有一个完整的章节专门讨论了理解成交量和未平仓合约。

| **金融市场技术分析** 约翰·J·墨菲 |
| --- |
| ![](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |

* * *

## 其他资源

### 股票与商品杂志文章

**[查金货币流指标（作者：克里斯托弗·纳尔库齐）](http://stockcharts.com/h-mem/tascredirect.html?artid=\V18\C08\072CHA.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V18\C08\072CHA.pdf")**

2000 年 7 月 - 股票与商品

**[比较七种货币流指标（作者：马科斯·卡特萨诺斯）](http://stockcharts.com/h-mem/tascredirect.html?artid=\V29\C07\110KATS.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V29\C07\110KATS.pdf")**

2011 年 6 月 - 股票与商品


# Chaikin Oscillator 

### 目录

+   Chaikin Oscillator

    +   介绍

    +   Calculation

    +   解释

    +   买入/卖出偏好

    +   分歧

    +   结论

    +   与 SharpCharts 一起使用

    +   建议扫描

        +   Chaikin Oscillator Turns Positive and RSI Moves Above 55

        +   Chaikin Oscillator Turns Negative and RSI Moves Below 45

    +   进一步研究

## 介绍

由 Marc Chaikin 开发，Chaikin Oscillator 使用 MACD 公式来衡量累积分布线的动量。这使其成为一个指标的指标。Chaikin Oscillator 是累积分布线的 3 日 EMA 与 10 日 EMA 之间的差异。与其他动量指标一样，该指标旨在通过测量背后的动量来预测累积分布线的方向变化。动量变化是趋势变化的第一步。预测累积分布线的趋势变化可以帮助图表分析师预测基础证券的趋势变化。Chaikin Oscillator 通过穿越零线或出现牛市/熊市分歧来生成信号。

## 计算

计算累积分布线（ADL）是计算 Chaikin Oscillator 的第一步。本文将介绍累积分布线的基本要素。查看我们的 ChartSchool 文章获取详细信息。计算累积分布线（ADL）有三个步骤。首先，计算资金流量乘数。其次，将此值乘以成交量以找到资金流量。第三，创建资金流量的累积总和以形成累积分布线（ADL）。第四，取两个移动平均线之间的差异来计算 Chaikin Oscillator。

```py

  1\. Money Flow Multiplier = [(Close  -  Low) - (High - Close)] /(High - Low) 

  2\. Money Flow Volume = Money Flow Multiplier x Volume for the Period

  3\. ADL = Previous ADL + Current Period's Money Flow Volume

  4\. Chaikin Oscillator = (3-day EMA of ADL)  -  (10-day EMA of ADL)		

```

当资金流量乘数为正时，累积分布线上升；当为负时下降。当收盘价位于周期高低范围的上半部时，该乘数为正；当收盘价位于下半部时，该乘数为负。作为 MACD 类型的振荡器，当较快的 3 日 EMA 移动超过较慢的 10 日 EMA 时，Chaikin Oscillator 变为正。相反，当 3 日 EMA 移动低于 10 日 EMA 时，指标变为负。

![图表 1 - 柴金波动指标](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/6a2b98d5e5015b9d3a012a1cc7d9a461.jpg "图表 1 - 柴金波动指标")

上图显示了积累分布线（灰色）与 3 日 EMA（蓝色）和 10 日 EMA（红色）。通用电气（GE）的价格不可见，因此我们可以专注于积累分布线和柴金波动指标之间的关系。请注意，当 3 日 EMA 低于 10 日 EMA 时，柴金波动指标进入负值区域。相反，当 3 日 EMA 穿过 10 日 EMA 时，振荡器变为正值。

## 解释

首先要记住，柴金波动指标是一个指标的指标。它衡量了积累分布线的动量。这使得它至少比基础证券的价格远了三步。首先，价格和成交量被重塑成积累分布线。其次，指数移动平均线被应用于积累分布线。第三，移动平均线之间的差异被用来形成柴金波动指标。作为第三阶导数，该指标更容易脱离基础证券的价格。

![图表 2 - 柴金波动指标](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/a63a87fab844269e40feaa0d3d1b1adb.jpg "图表 2 - 柴金波动指标")

在澄清了这一点之后，该指标旨在衡量买入和卖出压力（积累分布线）背后的动量。进入正值区域表示积累分布线上升，买入压力占优势。进入负值区域表示积累分布线下降，卖出压力占优势。图表分析师可以通过寻找看涨或看跌的背离来预期进入正值或负值区域的交叉点。

## 买入/卖出偏见

柴金波动指标可以用正值或负值简单地定义一般的买入或卖出偏见。该指标在零线上下振荡。一般来说，当指标为正时，买入压力更大，当指标为负时，卖出压力更大。

柴金波动指标的默认设置（3,10）经常产生经常穿过零线的线。图表分析师可以通过延长移动平均线来平滑指标。下面的示例显示了柴金波动指标（6,20）。两个移动平均线都加倍以保持比例并平滑指标。

![图表 3 - 柴金波动指标](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/74180cfba1db5969bef067c95411b0fb.jpg "图表 3 - 柴金波动指标")

美国钢铁 (X) 的柴金波动指标在 12 个月内穿越零线六次。有一些好的信号，比如四月的卖出信号和十月的买入信号。也有一些不好的信号或剧烈波动。关键是，与所有指标一样，要用技术分析的其他方面来确认波动指标的信号，比如纯价格动量指标或图案分析。

![图表 4  -  柴金波动指标](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/3ebf8f4c5d541d422ff23447f104aa1d.jpg "图表 4  -  柴金波动指标")

Alcoa (AA) 的图表显示了 2010 年六次零线穿越。前五次没有产生良好的信号，但第六次是一个好的信号。图表分析师应该尝试不同的设置，并考虑添加趋势线以增强他们的分析。趋势线的突破通常比零线穿越早。趋势线还捕捉了指标的方向。上升的柴金波动指标反映了买入压力的稳定增加。下降的柴金波动指标反映了卖出压力的稳定增加。

## 背离

看涨和看跌背离警示图表分析师买入或卖出压力的动量转变，可能预示价格图表上的趋势反转。当价格下跌到新低点时，而柴金波动指标形成较高低点时，就形成了一个看涨背离。这种较高低点显示了较少的卖出压力。等待某种确认非常重要，比如指标的上升或进入正值区的交叉。进入正值区显示了积累分布线上行动量的上升。

Fastenal (FAST) 图表显示了 2010 年柴金波动指标的五个背离。默认设置 (3,10) 产生了一个相当敏感的波动指标，会产生许多背离。关键是通过等待确认来区分强劲信号和虚假信号。即使有看涨背离，卖出压力仍然超过买入压力，直到出现零线上方的交叉。买入压力主导，直到出现进入负值区的交叉。

![图表 5  -  柴金波动指标](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/55b65063e330d5fbc4521ecc17d45669.jpg "图表 5  -  柴金波动指标")

绿色线显示了柴金波动指标形成较低低点，而股票形成较低低点以形成看涨背离。绿色虚线显示了指标进入正值区以确认信号。二月中旬、九月初和十一月末的信号非常好。六月中旬的买入信号会导致剧烈波动，而十月卖出信号后的看跌背离后并没有太多的弱势。

当价格上涨到新高点时，而柴金波动指标未能确认这一新高点时，就形成了一个看跌的背离。这种失败反映了较少的买入压力，有时可能预示价格图表上的看跌反转。确认发生在波动指标进入负值区时。

![图表 6  -  蔡金振荡器 ](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/e0b8124a4e255c522d8e7bf03fe13560.jpg "图表 6  -  蔡金振荡器 ")

Kohls（KSS）的图表显示了在 12 个月内三次看跌背离和两次看涨背离。当蔡金振荡器进入负值区域时，确认了看跌背离（红线），显示了积累分布线中实际的下行动量。请记住，当积累分布线的 3 日 EMA 移动低于 10 日 EMA 时，蔡金振荡器（3,10）会转为负值。

## 结论

蔡金振荡器是积累分布线的动量指标。基本上，蔡金振荡器通过测量动量来加速积累分布线。使用蔡金振荡器时，信号更频繁，通常更容易量化。作为资金流动振荡器，它可以与纯价格振荡器一起使用，例如 MACD 或 RSI。与所有指标一样，蔡金振荡器不应作为独立指标使用。

## 使用 SharpCharts

蔡金振荡器可以设置为在证券价格图表的上方、下方或后方的指标。当指标放置在价格图表后面时，可以轻松比较指标/价格的变化。一旦从下拉列表中选择了指标，就会出现默认参数设置（3,10）。这些参数可以调整以增加或减少灵敏度。用户可以点击“高级选项”添加水平线或移动平均线。[点击这里查看实时示例](http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=6&dy=0&id=p43640188268&listNum=30&a=222998125 "http://stockcharts.com/h-sc/ui?s=IBM&p=D&yr=0&mn=6&dy=0&id=p43640188268&listNum=30&a=222998125")。

![图表 7  -  蔡金振荡器](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/ed3d636fb37e4c53a273c41c623a11be.jpg "图表 7  -  蔡金振荡器")

![SharpCharts  -  蔡金振荡器](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/8e524e3dcf1dcccd23f1a194f975c3a9.jpg "SharpCharts  -  蔡金振荡器")

## 建议的扫描

### 蔡金振荡器转为正值，RSI 移动超过 55

这个扫描从至少在过去 60 天内平均价格为$10 且每日交易量为 100,000 的股票基础开始。当蔡金振荡器移动超过+1000 时，即略高于其中心线（0）时，可以识别出交易量较大的上涨。这一点通过价格动量得到确认，因为 RSI 需要移动超过 55，即略高于其中心线（50）。这个扫描旨在作为进一步分析和尽职调查的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [Daily Chaikin Osc(3,10) crosses 1000] 
AND [Daily RSI(14,Daily Close) crosses 55]
```

### 蔡金振荡器转为负值，RSI 移动低于 45

这个扫描从股票的基础开始，这些股票在过去 60 天的平均价格至少为$10，每日交易量至少为 100,000。当查金振荡器移动到-1000 以下时，即在其中心线（0）的稍下方时，就会识别出有良好交易量的下降趋势。这一点通过价格动量得到确认，因为需要 RSI 移动到 45 以下，即在其中心线（50）的稍下方。这个扫描旨在作为进一步分析和尽职调查的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [-1000 crosses Daily Chaikin Osc(3,10)] 
AND [45 crosses Daily RSI(14,Daily Close)]
```

欲了解如何使用查金振荡器扫描的语法详情，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#chaikin_oscillator_chaikin_osc "http://stockcharts.com/docs/doku.php?id=scans:indicators#chaikin_oscillator_chaikin_osc")在支持中心。

## 进一步研究

这本书涵盖了所有内容，并且解释简单清晰。墨菲涵盖了大部分主要的图表模式和指标。一个完整的章节专门讨论了理解成交量和未平仓合约。

| **金融市场技术分析** 约翰·J·墨菲 |
| --- |
| ![](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") |


# 查德趋势仪表盘（CTM）

### 目录

+   查德趋势仪表盘（CTM）

    +   介绍

    +   计算

    +   解释

    +   结论

    +   与 SharpCharts 一起使用

    +   建议的扫描

        +   CTM 在大量交易量下突破 60

        +   持续高 CTM 的股票

## 介绍

查德趋势仪表盘（CTM），由图沙尔·查德（Tushar Chande）开发，根据涵盖六个不同时间框架的几种不同技术指标为股票或其他证券分配一个数值分数。将所有这些技术信息压缩成一个数字，提供了一种简单的方法来识别给定证券的趋势强度。

## 计算

查德趋势仪表盘的计算基于以下技术指标：

+   高、低和收盘价相对于四个不同时间框架（20 天、50 天、75 天和 100 天）的布林带的位置

+   过去 100 天相对于标准偏差的价格变化

+   14 天的 RSI 值

+   任何短期（2 天）价格通道突破的存在

最终得分转换为 0-100 的尺度以便比较。

## 解释

在 0 到 100 的查德趋势仪表盘尺度上，分数为 100 的股票处于非常强劲的上升趋势中。相反，分数为 0 的股票处于非常强劲的下跌趋势中。

这个尺度可以分为 5 个不同的级别：

+   分数为 90-100 的股票处于非常强劲的上升趋势中

+   分数为 80-90 的股票处于强劲上升趋势中

+   分数为 60-80 的股票处于弱势上升趋势中

+   分数为 20-60 的股票要么是平稳的，要么是弱势下跌趋势中

+   分数为 0-20 的股票处于非常强劲的下跌趋势中

动量交易者应寻找查德趋势仪表盘分数为 80 或更高的股票。这表示强劲的上升趋势。趋势越强劲，延续该趋势的可能性就越大。

查德趋势仪表盘也可以与指数和交易所交易基金（ETF）一起使用，以了解特定行业和行业甚至整个市场的相对趋势。

查德趋势仪表盘的一个优点是其数值是在绝对尺度上设置的，而不是相对于同一组股票。因此，当您比较几种不同类型证券的 CTM 分数时，您正在跨所有证券进行苹果对苹果的比较。

## 结论

Chande 趋势仪提供了一种简单的方法来确定股票是处于上升趋势还是下降趋势，并且便于评估该趋势的强度。通过将几种不同的经过验证的技术趋势指标结合在一起，并将它们简化为一个数字，CTM 使图表分析师能够在快速浏览时获得丰富的趋势信息。

## 使用 SharpCharts

Chande 趋势仪可以在图表下方的指标部分找到。CTM 指标可以放置在主价格图的上方、下方或后面。

当放置在主价格图之上或之下时，背景颜色编码以指示不同的趋势强度水平：

+   **深绿色**: 90-100（非常强劲上升趋势）

+   **中绿色**: 80-90（强劲上升趋势）

+   **浅绿色**: 60-80（弱上升趋势）

+   **黄色**: 20-60（平稳或弱下跌趋势）

+   **粉色**: 0-20（强劲下跌趋势）

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/6c5b52684e5b20214e5ea35d2ff227cb.jpg)

## 建议扫描

### CTM 在大量交易量下突破 60

此扫描显示了 Chande 趋势仪已经在较重的交易量下突破 60 的股票。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Chande Trend Meter x 60.0]
AND [volume > SMA(50,volume) * 1.5]
```

### 持续高 CTM 的股票

此扫描显示了美国股票的 Chande 趋势仪持续高，过去 50 个交易日平均为 80 或更高。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [SMA(50,Chande Trend Meter) > 80.0]
```

有关 Chande 趋势仪扫描的语法详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#chande_trend_meter "http://stockcharts.com/docs/doku.php?id=scans:indicators#chande_trend_meter")在支持中心中。


# 商品通道指数（CCI）

### 目录

+   商品通道指数（CCI）

    +   介绍

    +   计算

    +   解释

    +   新趋势出现

    +   超买/超卖

    +   看涨/看跌背离

    +   结论

    +   与 SharpCharts 一起使用

    +   建议扫描

        +   CCI 在上升趋势中超卖

        +   CCI 在下降趋势中超买

    +   进一步研究

## 介绍

由唐纳德·兰伯特（Donald Lambert）开发，并于 1980 年在《商品》杂志上推出的商品通道指数（CCI）是一种多功能指标，可用于识别新趋势或警示极端条件。兰伯特最初开发 CCI 是为了识别商品的周期性转折，但该指标也可以成功应用于指数、ETF、股票和其他证券。总的来说，CCI 衡量当前价格水平相对于一定时期内的平均价格水平。当价格远高于其平均水平时，CCI 相对较高。当价格远低于其平均水平时，CCI 相对较低。通过这种方式，CCI 可用于识别超买和超卖水平。

## 计算

下面的示例基于 20 周期商品通道指数（CCI）的计算。CCI 周期数也用于简单移动平均和平均偏差的计算。

```py
CCI = (Typical Price  -  20-period SMA of TP) / (.015 x Mean Deviation)

Typical Price (TP) = (High + Low + Close)/3

Constant = .015

There are four steps to calculating the Mean Deviation: 
First, subtract the most recent 20-period average of the typical price from each period's typical price. 
Second, take the absolute values of these numbers. 
Third, sum the absolute values. 
Fourth, divide by the total number of periods (20). 

```

Lambert 将常数设定为 0.015，以确保大约 70%到 80%的 CCI 值落在-100 和+100 之间。这个百分比还取决于回顾期。较短的 CCI（10 个周期）将更加波动，在+100 和-100 之间的值的百分比较小。相反，较长的 CCI（40 个周期）将在+100 和-100 之间的值有更高的百分比。

![CCI- 电子表格](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/9c685e4d92befe735a206b838a47effd.jpg "CCI- 电子表格")

点击这里查看在 Excel 电子表格中计算 CCI 的链接")。

![CCI  -  图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/7d6f9ce0f86f76ed976a31f9483f9b7e.jpg "CCI  -  图表 1")

## 解释

CCI 衡量证券价格变动与其平均价格变动之间的差异。高正读数表明价格远高于其平均水平，这显示了强势。低负读数表明价格远低于其平均水平，这显示了弱势。

商品通道指数（CCI）可以用作同时发生或领先发生指标。作为同时发生指标，CCI 上涨到+100 以上反映出强劲的价格行动，可能预示着一段上升趋势的开始。下跌到-100 以下反映出弱劲的价格行动，可能预示着一段下降趋势的开始。

作为领先指标，图表分析师可以寻找可能预示均值回归的超买或超卖条件。同样，看涨和看跌的背离可以用来检测早期动量转变并预测趋势反转。

## 新趋势出现

如上所述，CCI 的大部分波动发生在-100 和+100 之间。超出这一范围的波动显示出异常的强度或弱势，可能预示着一个持续的波动。将这些水平视为看涨或看跌的过滤器。从技术上讲，CCI 在正数时偏向多头，在负数时偏向空头。然而，使用简单的零线交叉可能会导致许多虚假信号。尽管入场点会更滞后，需要 CCI 上升到+100 以上才能发出看涨信号，下降到-100 以下才能发出看跌信号可以减少虚假信号。

下图显示了卡特彼勒（CAT）的 20 日 CCI。在七个月的时间内出现了四个趋势信号。显然，20 日 CCI 不适合用于长期信号。图表分析师需要使用周线或月线图表来获取长期信号。股票在 1 月 11 日达到顶峰并开始下跌。CCI 在 1 月 22 日（8 天后）下跌到-100 以下，预示着一个持续波动的开始。同样，股票在 2 月 8 日触底，CCI 在 2 月 17 日（6 天后）上升到+100 以上，预示着一个持续上涨的开始。CCI 并不能准确捕捉到顶部或底部，但它可以帮助过滤掉不重要的波动，专注于更大的趋势。

![CCI  -  图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/1763c789e7f19c87c31ee52d48305605.jpg "CCI  -  图表 2")

当 CAT 在 6 月上涨到 60 以上时，CCI 触发了一个看涨信号。一些交易者可能认为股票已经超买，这些水平下的风险收益比不利。在看涨信号生效的情况下，重点将放在具有良好风险收益比的看涨设置上。请注意，股票在 6 月底回撤了先前涨幅的约 62%，并形成了一个下降旗形态。随后突破旗形趋势线提供了另一个 CCI 仍处于多头模式的看涨信号。

## 超买/超卖

识别商品通道指数（CCI）或任何其他动量振荡器的超买和超卖水平可能有些棘手。首先，CCI 是一个无限振荡器。从理论上讲，没有上限或下限。这使得超买或超卖的评估是主观的。其次，证券在指标超买后仍可继续上涨。同样，证券在指标超卖后仍可继续下跌。

对于商品通道指数（CCI），超买或超卖的定义有所不同。±100 可能适用于交易范围，但对于其他情况需要更极端的水平。±200 是一个更难达到的水平，更能代表真正的极端。超买/超卖水平的选择还取决于基础证券的波动性。例如，指数 ETF（如 SPY）的 CCI 范围通常比大多数股票（如谷歌）要小。

![CCI  -  图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/e13b282f8d5cca2aca7bcaf2cab818bf.jpg "CCI  -  图表 3")

上图显示了谷歌（GOOG）的 CCI（20）。使用高级指标选项添加了±200 的水平线。从 2010 年 2 月初到 10 月初，谷歌至少五次超过了±200。红色虚线显示了 CCI 回落至+200 以下的时刻，绿色虚线显示了 CCI 回升至-200 以上的时刻。重要的是要等待这些交叉点，以减少趋势延伸时的错误信号。然而，这样的系统并非绝对可靠。请注意，即使 CCI 在 9 月中旬超买并下跌至-200 以下后，谷歌仍在不断上涨。

## 牛市和熊市分歧

分歧信号可能标志着潜在的反转点，因为方向性动量不确认价格。当基础证券创下较低低点而 CCI 形成较高低点时，形成牛市分歧，显示出较少的下行动量。当证券记录较高高点而 CCI 形成较低高点时，形成熊市分歧，显示出较少的上行动量。在对分歧作为良好反转指标感到兴奋之前，请注意，在强劲趋势中，分歧可能具有误导性。强劲的上升趋势在顶部实际出现之前可能会显示出许多熊市分歧。相反，在持续的下跌趋势中经常出现牛市分歧。

确认是分歧的关键。虽然分歧反映了动量的变化，可以预示趋势反转，但图表分析师应为 CCI 或价格图表设定一个确认点。如果 CCI 或价格图表下破零点，可以确认熊市分歧；相反，如果 CCI 或价格图表上破零点，可以确认牛市分歧。

![CCI  -  图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/0d83531ea614e45e0ce7613239449687.jpg "CCI  -  图表 4")

上图显示了联合包裹服务（UPS）的 40 天 CCI。为了减少波动性，使用了较长的时间框架，40 天而不是 20 天。在七个月的时间内出现了三次相当大的背离，对于仅仅七个月来说实际上是相当多的。首先，UPS 在五月初飙升至新高，但 CCI 未能超过三月的高点，并形成了一个看跌的背离。价格图表上的支撑线突破和 CCI 转入负值领域几天后证实了这一背离。其次，七月初形成了一个看涨的背离，因为股票走低至一个更低的低点，但 CCI 形成了一个更高的低点。这一背离在 CCI 转入正值领域时得到了确认。还要注意，UPS 在七月初迅速填补了六月底的跳空缺口。第三，九月初形成了一个看跌的背离，当 CCI 跌入负值领域时得到了确认。尽管 CCI 确认了这一背离，但价格从未突破支撑线，背离并未导致趋势逆转。并非所有的背离都会产生良好的信号。

## 结论

CCI 是一种多功能的动量振荡器，可用于识别超买/超卖水平或趋势逆转。当指标达到相对极端时，它就会变得超买或超卣。这一极端取决于基础证券的特征和 CCI 的历史范围。波动性较大的证券可能需要比温和证券更大的极端。当 CCI 穿越零和 100 之间的特定阈值时，可以识别出趋势变化。无论如何使用 CCI，图表分析师都应该将 CCI 与其他指标或价格分析结合使用。另一个动量振荡器会显得多余，但累积/派发线（OBV）或累积/派发线可以为 CCI 信号增加价值。

## 使用 SharpCharts 时

CCI 可作为 SharpCharts 指标使用，可以放置在基础证券的价格图表的上方、下方或后方。将 CCI 直接放在价格后面可以方便地比较指标运动与价格运动。默认设置为 20 个周期，但可以根据分析需求进行调整。较短的时间框架使指标更为敏感。较长的时间框架使其不太敏感。会员可以点击“高级选项”旁边的绿色箭头，添加水平线以标记超买或超卖水平。可以通过用逗号分隔数字（200，-200）来添加两条线。[点击这里查看实时示例](http://stockcharts.com/h-sc/ui?s=SPY&p=D&yr=0&mn=8&dy=0&id=p10448180746&listNum=30&a=221403127 "http://stockcharts.com/h-sc/ui?s=SPY&p=D&yr=0&mn=8&dy=0&id=p10448180746&listNum=30&a=221403127")。

![CCI - 图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/62dd4b7f415aa13b5c20ab56a32d063e.jpg "CCI - 图表 5")

![CCI - SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/22f76e80de0846d80c931e6431e83a6a.jpg "CCI - SharpCharts")

## 建议的扫描

### CCI 超卖处于上升趋势

这个扫描显示了处于上升趋势的股票，CCI 处于超卖状态并开始上涨。首先，股票必须在它们的 200 日移动平均线之上，才能处于总体上升趋势。其次，CCI 必须上穿-200，以显示指标从超卖水平上升。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close > Daily SMA(200,Daily Close)] 
AND [Daily CCI(20) crosses -200]
```

### CCI 超买处于下降趋势

这个扫描显示了处于下降趋势的股票，CCI 处于超买状态并开始下降。首先，股票必须在它们的 200 日移动平均线之下，才能处于总体下降趋势。其次，CCI 必须下穿+200，以显示指标从超买水平下降。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 40000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Close < Daily SMA(200,Daily Close)] 
AND [200 crosses Daily CCI(20)]
```

有关用于 CCI 扫描的语法的更多详细信息，请参阅我们支持中心的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#commodity_channel_index_cci "http://stockcharts.com/docs/doku.php?id=scans:indicators#commodity_channel_index_cci")。

## 进一步研究

Murphy 有一个专门讨论动量振荡器及其各种用途的章节。Murphy 涵盖了优缺点以及一些特定于商品通道指数的示例。

Pring 通过涵盖背离、交叉和其他信号展示了动量指标的基础知识。还有两个章节涵盖了具体的动量指标，并提供了大量示例。

| **金融市场技术分析** 约翰·J·墨菲 | **马丁·普林格的技术分析解析** 马丁·普林格 |
| --- | --- |
| ![](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | ![](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | ![立即购买](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |


# 科波克曲线 

### 目录

+   科波克曲线

    +   介绍

    +   SharpCharts 计算

    +   信号

    +   灵活性

    +   结论

    +   与 SharpCharts 一起使用

    +   建议扫描

        +   科波克曲线上穿零线

        +   科波克曲线下穿零线

    +   进一步研究

## 介绍

科波克曲线是由埃德温“塞奇”科波克开发的动量指标，他是一位经济学家。科波克在 1965 年 10 月的《巴伦周刊》中介绍了这一指标。该指标的目标是识别标普 500 和道琼斯工业指数的长期买入机会。信号非常简单。科波克使用月度数据来识别当指标从负值区域移动到正值区域时的买入机会。尽管科波克没有将其用于卖出信号，但许多技术分析师认为从正值区域到负值区域的交叉是一个卖出信号。

## SharpCharts 计算

```py
Coppock Curve = 10-period WMA of 14-period RoC + 11-perod RoC

WMA = Weighted moving average
RoC = Rate-of-Change
```

变动率指标是一个动量振荡器，它在零线上下振荡。科波克使用了 11 和 14 个周期，因为据一个圣公会牧师说，这是悼念所爱之人丧失的平均哀悼期。科波克推测，股市损失的恢复期将类似于这个时间段。

![图表 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/090124138fd2094e161e31af676fa021.jpg "图表 1")

然后，变动率指标通过加权移动平均进行平滑处理。顾名思义，加权移动平均对最新数据赋予更高的权重，对较旧的数据赋予较低的权重。例如，3 期加权移动平均会将第一个数据点乘以 1，第二个数据点乘以 2，第三个数据点乘以 3。然后，这三个数字的总和除以 6，即权重之和（1 + 2 + 3），以创建加权平均值。下表显示了从 Excel 电子表格中的计算。

![电子表格 1](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/59dcbc5a0aa62857dbc89eebb338b93d.jpg "电子表格 1")

点击此处下载此电子表格示例。")

## 信号

使用月度数据，这个指标不会触发很多信号。买入信号在穿越进入正区域时触发，而卖出信号在穿越进入负区域时触发。毫不奇怪，自上世纪 80 年代末以来只有五次信号。下图显示了最近的四个信号。第一个信号在 1988 年触发，那是在 1987 年的崩盘之后。

![图表 2](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/4c5c5f83d2a5944c1e38afa4766befe4.jpg "图表 2")

遵循这两个卖出信号的技术分析师将避开最后两次熊市。2001 年 2 月的卖出信号将避开 2000 年至 2002 年的大部分熊市。2008 年 6 月的卖出信号将使投资者在 2008 年下半年市场暴跌之前退出。这些卖出信号可以简单用于退出股市并转入现金，从而降低市场风险和整体风险。

## 灵活性

如上所述，科波克曲线只是一个平滑的动量振荡器。变动率指标衡量动量，加权移动平均平滑数据。这意味着该指标可以用于任何时间框架。分钟图、日图和周图可以用于适应个人的交易/投资风格和时间跨度。下图显示了在道琼斯工业指数上使用周度数据的科波克曲线。如预期的那样，周图产生了比月度图更多的信号。

![图表 3](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/550f7b92341fb33be036374b88e3ba66.jpg "图表 3")

除了不同的时间框架，参数可以调整以使指标更快或更慢。较短的变动率设置将使科波克曲线更敏感和更快，而较长的设置将使其更不敏感和更慢。下图显示了纳斯达克 100 ETF（QQQ）和科波克曲线（20,10,10）的日线图。这种设置使科波克曲线稍微不那么敏感，可能更适合日线图。

![图表 4](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/44cc79ba8fb3a67960e8960cce634535.jpg "图表 4")

## 结论

科波克曲线只是一个平滑的动量振荡器。尽管最初设计用于月度图表和长期分析，但它可以用于分钟图、日图或周图，并且可以调整设置以适应个人的风格。主要信号是在零线上方和下方的交叉点生成的。更激进的技术分析师可以考虑寻找看涨和看跌的背离来预测这种交叉。但要小心。背离并不总是导致趋势反转，因为趋势可能只是减缓并继续朝着同一方向发展。

## 使用 SharpCharts

科波克曲线可以在图表下方的指标部分找到。用户可以通过更改参数框中的数字来调整设置。然后可以将指标定位在“价格后面”，“主窗口上方”或“主窗口下方”。在将其放在价格后面时更改颜色会有所帮助。图表分析师还可以使用“高级”选项添加移动平均线。这个移动平均线类似于信号线，类似于 MACD。

![图表 5](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/618f6c1cb1a174722cd65228be635034.jpg "图表 5") ![图表 6](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/4b1081f7c788fab96f42991e840e858c.jpg "图表 6")

## 建议的扫描

### 科波克曲线上穿零线

这个简单的扫描搜索股票，其中科波克曲线从负区域穿越到正区域，每日成交量高于成交量的 50 日移动平均线。换句话说，牛市交叉发生时成交量在扩大。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [Daily Coppock(20,10,10) crosses 0] 
AND [Daily Volume > Daily SMA(50,Daily Volume)]
```

### 科波克曲线下穿零线

这个简单的扫描搜索股票，其中科波克曲线从正区域穿越到负区域，每日成交量高于成交量的 50 日移动平均线。换句话说，熊市交叉发生时成交量在扩大。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(20,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 20] 

AND [0 crosses Daily Coppock(20,10,10)] 
AND [Daily Volume > Daily SMA(50,Daily Volume)]
```

有关科波克曲线扫描的语法详细信息，请参阅我们支持中心的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#coppock_curve_coppock "http://stockcharts.com/docs/doku.php?id=scans:indicators#coppock_curve_coppock")。

## 进一步研究

《金融市场技术分析》有一章专门讨论动量振荡器及其各种用途。墨菲涵盖了涨跌幅特定的优缺点以及一些例子。普林的书展示了通过涵盖背离、交叉和其他信号来介绍动量指标的基础知识。还有两章涵盖特定动量指标并提供大量示例。

| **金融市场技术分析** 约翰·J·墨菲 | **马丁·普林解释的技术分析** 马丁·普林 |
| --- | --- |
| ![](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | ![](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |
| ![立即购买](http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1 "http://store.stockcharts.com/products/technical-analysis-of-the-financial-markets-1") | ![立即购买](http://store.stockcharts.com/products/technical-analysis-explained-4th-edition "http://store.stockcharts.com/products/technical-analysis-explained-4th-edition") |


# 相关系数 

### 目录

+   相关系数

    +   介绍

    +   计算

    +   解释

    +   多样化

    +   结论

    +   与 SharpCharts 一起使用

## 介绍

相关系数是反映两个证券之间相关性的统计量。换句话说，这个统计量告诉我们一个证券与另一个证券之间的关系有多密切。当两个证券向同一方向移动时，相关系数为正，无论是上涨还是下跌。当两个证券朝相反方向移动时，相关系数为负。确定两个证券之间的关系对于分析市场间关系、部门/股票关系和部门/市场关系非常有用。这个指标还可以帮助投资者通过识别与股市相关性低或负相关的证券来实现多样化。

## 计算

相关系数的计算相当复杂，所以可以跳过这一部分。我们只会简单看一些基本内容，以了解其中的方法。这个指标正是经典统计学的核心。第一步是选择两个证券。在这个例子中，我们将使用英特尔（INTC）和纳斯达克 100ETF（QQQ）。换句话说，我们想要看到英特尔和 QQQ 之间的相关程度。下面的 Excel 表格展示了基础工作。

![相关系数 - Excel 示例](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/77af7d6083199f02f34a7774a33c9762.jpg "相关系数 - Excel 示例")

+   INTC 列显示了英特尔在 20 天内的价格，底部显示了平均值。

+   QQQ 列显示了 QQQ 的情况。

+   接下来的两列显示了每个期间的价格平方，底部显示了平均值。

+   最后几列显示了每个期间的 INTC 乘以 QQQ，底部显示了平均值。

利用底部行，我们现在可以计算方差、协方差和相关系数。Excel 公式显示在长公式旁边。结果显示，在 6 月 22 日至 7 月 20 日的 20 天期间，英特尔与纳斯达克 100ETF 表现出强烈的正相关性（+.95）。

![相关系数 - 英特尔](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/5d49358a0e02c4ac44fcaf0d4cdc14b8.jpg "相关系数 - 英特尔")

这里有一个展示相关系数的 Excel 电子表格")。由于四舍五入问题，一些数字可能略有不同。

## 解释

相关系数在-1 和+1 之间波动。尽管它不是动量振荡器，但它会从正相关的时期转向负相关的时期。+1 被认为是完美的正相关，这是罕见的。0 到+1 之间的任何值表示两个证券朝着相同的方向移动。正相关的程度随时间可能会有所变化。石油股票和石油大部分时间都呈正相关。下面的例子显示了能源 SPDR（XLE）与现货轻质原油（$WTIC）之间的关系。毫不奇怪，20 天的相关系数大部分时间保持正值，经常超过+0.75。这两个证券之间显然存在着积极的关系。一般来说，任何大于 0.50 的值都显示出强烈的正相关。

![相关系数 - 石油和石油股票](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/b689c4126d59a296b4105f90068e9f98.jpg "相关系数 - 石油和石油股票")

在另一端，-1 被认为是完美的负相关，这也是罕见的。0 到-1 之间的任何值表示两个证券朝着相反的方向移动。负相关的程度随时间可能会有所变化。黄金和美元是我想到的第一对负相关的证券。下面的图表显示了现货黄金（$GOLD）与美元指数（$USD）之间的关系。尽管相关系数在正值区域停留了一段时间，但大部分时间都是负值。一般来说，任何小于-0.50 的值都显示出强烈的负相关。

![相关系数 - 黄金和美元](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/30b24667d3b93e41ffc9e418660a064f.jpg "相关系数 - 黄金和美元")

## 多样化

相关系数可用于识别不相关的证券，这在构建多样化投资组合中非常重要。毫不奇怪，标普九大部门与标普 500 指数大多呈正相关。然而，有些部门的正相关性比其他部门更强。例如，在过去三年中，科技 ETF（XLK）和消费者自由支出 SPDR（XLY）与标普 500 指数有着强烈的正相关性。以下相关系数基于 50 天。消费者自由支出部门在过去三年中只有一次低于 0.50。科技部门从未低于 0.50，因为科技仍然与市场强相关。相比之下，消费品部门的相关系数在过去几次低于 0.50，而公用事业部门的相关系数甚至两次低于零。这一指标表明，消费品和公用事业部门与标普 500 指数的相关性低于消费者自由支出和科技部门。

![相关系数 - 部门](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/05549c34a02e0df590bd58513dfa665b.jpg "相关系数 - 部门")

为了真正实现股票的多样化，通常需要看向股票市场之外。下图显示了四个 ETF 与股票市场（SPY）有许多负相关期的情况。请注意相关系数多次低于零。在此示例中，我还使用了 50 天相关系数。20+年期债券 ETF（TLT）代表债券，大部分时间与股票呈负相关。黄金（红色）在正负相关期间变动。总体而言，过去三年来，它更多地呈正相关而不是负相关。日元信托（绿色）似乎在正负相关期间分别占据时间。令人惊讶的是，美元基金（UUP）显示出与股票市场负相关的倾向。

![相关系数 - 其他资产](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/6b1d5a2cfae43db56646757cf0a11988.jpg "相关系数 - 其他资产")

## 结论

相关系数告诉我们两个证券之间的关系。在给定的时间段内，当相关系数为正时，两个证券一起移动。相反，当相关系数为负时，两个证券移动方向相反。上面的示例显示了 20 天和 50 天的相关系数。长期投资者可能使用 150 甚至 250 天（一年）以获得反映长期关系的更平滑线条。

## 使用 SharpCharts

相关系数在 SharpCharts 中的“指标”下可见。首先，在图表顶部的符号框中输入基础证券创建图表（INTC）。其次，在下拉菜单中选择相关系数作为指标。第三，输入另一证券的符号和时间范围在参数框中（$SPX,20）。这两者用逗号分隔。下面的示例显示了英特尔在主窗口中，带有 10 天相关系数的指标窗口。这显示了英特尔与标普 500 的相关性。另外，请注意标普 500 价格图（红色虚线）放在英特尔价格图后面以进行比较。[点击这里](http://stockcharts.com/h-sc/ui?s=$SPX&p=D&yr=0&mn=6&dy=0&id=p61512839073&listNum=30&a=239762181 "http://stockcharts.com/h-sc/ui?s=$SPX&p=D&yr=0&mn=6&dy=0&id=p61512839073&listNum=30&a=239762181") 查看带有相关系数的实时图表。

![相关系数 - 英特尔 SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/51c5ab73134bcf509d6ee450828be753.jpg "相关系数 - 英特尔 SharpCharts")

![相关系数 - SharpCharts](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/77da97cb5e6fe5079347dda736b8f9e4.jpg "相关系数 - SharpCharts")


# DecisionPoint 价格动量振荡器（PMO）

### 目录

+   DecisionPoint 价格动量振荡器（PMO）

    +   介绍

    +   计算

    +   解释

    +   超买/超卖指标

    +   动量指标

    +   信号生成器

    +   PMO 配置

    +   结论

    +   与 SharpCharts 一起使用

    +   建议的扫描

        +   PMO 上涨但尚未跨越信号线

        +   PMO 下跌但尚未跌破信号线

## 介绍

DecisionPoint 价格动量振荡器（PMO）是基于变化率（ROC）计算的振荡器，该计算通过使用自定义平滑过程两次平滑指数移动平均线。由于 PMO 是标准化的，因此它也可以用作相对强度工具。因此，股票可以根据其 PMO 值排名，作为相对强度的表达。

## 计算

DecisionPoint 价格动量振荡器是通过采用一个周期变化率并使用两个自定义平滑函数对其进行平滑而导出的。这些自定义平滑函数与指数移动平均线非常相似，但是与真正的 EMA 不同，它们不是将时间周期设置加一来创建平滑乘数（如真正的 EMA 中那样），而是只使用周期本身。

```py
Smoothing Multiplier = (2 / Time period)

Custom Smoothing Function = {Close - Smoothing Function(previous day)} *
 Smoothing Multiplier + Smoothing Function(previous day) 

PMO Line = 20-period Custom Smoothing of
(10 * 35-period Custom Smoothing of
 ( ( (Today's Price/Yesterday's Price) * 100) - 100) )

PMO Signal Line = 10-period EMA of the PMO Line
```

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/fcf273d3319262ef16792bc1bc61ab3d.jpg)

下表显示了亚马逊的 PMO 计算：

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/848e8a353e052ece6f3bcd60d6a8d12d.jpg)

要下载包含这些计算的 Excel 电子表格，请点击这里")。

## 解释

PMO 在与零线相关的振荡。通常，PMO 方向指示强度是增加还是减少，趋势角度的陡峭程度显示了动力的强度。由于这是一个内部比率计算（与外部相比，如标准相对强度计算，它将一个价格除以另一个价格指数），它返回一个经过标准化的结果，并且可以与任何其他证券或指数的 PMO 结果进行比较。因此，图表分析师可以通过使用它们的 PMO 值简单地对证券或指数列表进行相对强度排序。列表不必是同质的 - PMO 可以用来对市场指数、股票和共同基金进行排名。

一个与 PMO 非常相似的指标是由杰拉尔德·阿普尔（Gerald Appel）发明的 MACD（移动平均线收敛-发散）指标。PMO 和 MACD 之间的主要区别是每个指标的绝对值。MACD 基于移动平均计算，一个 MACD 读数与另一个毫无关系；而正如上面所解释的，PMO 是一个内部比率。下面的图表显示了 PMO 和 MACD 在一起。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/457845a6ea2559fed652cafacd582514.jpg)

尽管在短期图表上，PMO 和 MACD 的形状相似，但是在长期图表上，PMO 的比率型计算的优势是显而易见的，因为 PMO 相对稳定，不像 MACD。请参见下面的周度和月度图表。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/a08bcced80290d35246987d59e81dc54.jpg)

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/20c4ca5aa0b58aeca3a430277fa2a5e4.jpg)

## 超买/超卖指标

如下所示，PMO 可以帮助确定价格指数是否超买或超卖。下面是标普 500 指数的五年图表，显示了各种极端市场条件。该指数的正常 PMO 范围约为+2.5（超买）至-2.5（超卖），当 PMO 接近或突破这些限制时，通常会发出价格反转的信号。当 PMO 在或超出其正常范围的极端位置改变方向时，这往往是价格方向发生中期变化的相当可靠的指示。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/b239a0f4276f4700c25ce232f3e93497.jpg)

虽然+2.5 至-2.5 是广泛股市指数的通常范围，但每个价格指数都将有其自己的“特征”范围。例如，下面的微软（MSFT）图表显示了+5.0 至-5.0 的范围。始终检查长期图表以验证您正在分析的指数的正常范围。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/5d9d22230c2bc2b87a50c7f89a529be1.jpg)

此外，请记住，技术指标是根据在所讨论的时间范围内的特定时间段计算的，因此月度 PMO 看起来完全不同于日常 PMO。请参见下面基于相同七年期间的月度图表，该图表与上面的日常 MSFT 图表相同。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/10dfebd3a39e9bfd5a8df9dd956a17e4.jpg)

## 动量指标

作为动量指标，PMO 表达价格运动的方向和速度。在这方面，它类似于其他动量指标。在下面的黄金 ETF（GLD）图表中，任一方向上最强烈的移动都以直线、陡峭、平滑的 PMO 运动为特征。更为停滞的趋势通常伴随着频繁的 PMO 方向变化。PMO 的底部和顶部表明价格动量已经转向，因此它们可以提供价格顶部和底部的早期信号。当 PMO 处于超买或超卖区域时，它们通常更可靠。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/1d6878b0e6c3cd294add5976d7cb3b69.jpg)

最后，与其他振荡器一样，PMO 通过形成与价格指数的背离来提示重要方向变化的迹象。下面突出显示了三个独立的背离。两个负面背离（红线）警告着重要的顶部，因为价格指数创造了一个更高的高点，而 PMO 创造了一个更低的高点。正面背离（绿线）信号着重要的底部，价格创造了一个更低的低点，而 PMO 创造了一个更高的低点。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/89a082a88c19e71ee85e527a1a1b4b27.jpg)

## 信号生成器

当 PMO 穿过其 10 周期 EMA 时，PMO 会产生交叉信号。这些信号往往持续时间较短，但可能持续几周。不要直接接受它们，因为它们可能会频繁震荡。它们应该用于提醒您可能的交易机会，而不是作为机械交易模型使用。始终检查图表以验证价格模式和 PMO 的配置。当价格看起来过度，接近支撑或阻力，并且 PMO 非常超买或超卖时，信号效果最佳。这些信号也可以与 DecisionPoint 趋势分析一起使用，使用 20/50/200-EMA 交叉确定长期、中期和短期的牛市或熊市偏好。

当 PMO 接近其正常范围的极端位置时，或者在一个强烈、清晰、直线的 PMO 移动之后发生方向变化和交叉时，最可靠的信号会被产生。在零线周围和 PMO 在相对平坦模式中移动时，会产生相当多的“噪音”。下图突出显示了交叉信号：

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/952d8b706d469bae41b4c1a63a297b3b.jpg)

## PMO 配置

**横向摆动**

以下图表展示了一个常见的 PMO 形态，强调了为什么所有 PMO 交叉信号不能被字面接受。红色圈出的区域是在价格稳步上涨趋势中典型的 PMO 运动。价格波动很小，所以 PMO 横向移动。PMO 保持在零线以上的事实证明了价格走势的强劲；然而，价格波动中的小波动导致 PMO 在其 10-EMA 上下震荡，产生许多无利润的交叉牛市信号。这张图还展示了横向摆动最终会结束以及如何提供微妙线索表明趋势即将结束。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/a267835c9e58dc8c96412576062c795f.jpg)

**熊市之吻**

“熊市之吻”是 PMO 经常显示的三个明显顶部动作中的最后一部分。当我们看到这种经典形态时，它提供了额外的保证，表明可交易的顶部已经形成。当 PMO 相对超买且价格指数经历了大幅上涨时，我们开始寻找这种形态。这种形态并不总是出现在顶部，但是当出现时，它有助于增强我们对信号可靠性的信心。

第一个动作是一个虚假的 PMO 顶部。主要顶部总是伴随着一个超买的 PMO 顶部，但并非所有 PMO 顶部都预示着主要价格顶部。虚假顶部提醒我们，价格顶部可能只有几周的时间。

接下来我们会看到一个略高的 PMO 顶部，随后是一个交叉卖出信号，当 PMO（蓝线）穿过其 10-EMA（绿线）向下交叉时生成。当这些信号发生在非常超买的水平时，它们可能暂时被视为准确，但是，当它们之前有非常强劲的价格行动时，价格可能再次创造新高，这会导致 PMO 再次开始上升。

最后，随着价格从最终顶部开始回落，PMO 再次上涨，这次仅在勉强“吻”到 10-EMA 的下侧后达到顶峰。有些人称之为“死亡之吻”，但这似乎有点夸张，因此熊市之吻似乎更合适。此外，在重要底部还有一个相反的形态，术语“公牛之吻”似乎比“生命之吻”更贴切。

请注意，这一分析的一个重要方面是，价格指数已经突破了一个上升趋势线，并伴随着熊市之吻。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/4a5c4d6de8e91a0cca696d0531374246.jpg)

**公牛之吻**

“公牛之吻”发生在 PMO 交叉买入信号之后不久，是在产生交叉信号后的初始向上推力后价格回撤的结果。虽然公牛之吻和熊市之吻本质上是相等但相反的形态，但两者之间的价格行为是不同的。通常情况下，熊市之吻是一个不确认信号，与一次上涨中的最终价格高点相一致；而公牛之吻通常与新一轮上涨中的更高价格低点相一致。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/f366d38c3af656f556528191e87cdcb8.jpg)

**清晰信号**

虽然公牛和熊市之吻形态相当常见，但也有可能出现非常清晰的 PMO 反转和交叉，而没有与爆发和重新测试相关的摆动，因为价格趋势的变化相对平稳。关键是，反转和交叉行为可以涵盖各种配置。对图表的研究将有助于更好地理解导致某种类型 PMO 行为的价格行为。PMO 行为还提供了关于可以预期的价格行为类型的线索。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/3b9d93e56c554d2b93239a87ad899bde.jpg)

## 结论

决策点价格动量振荡器（PMO）可用作相对强度、动量和超买/超卖条件的衡量标准。它还可以用于通过牛市和熊市交叉确定价格反转。

## 使用 SharpCharts

决策点 PMO 可作为 SharpCharts 的指标使用。默认设置使用 35 期和 20 期 EMA，带有 10 期 EMA 信号线，但用户可以选择更短的时间框架以产生更敏感的振荡器，或选择更长的时间框架以产生更不敏感的振荡器。一旦选择，指标可以放置在基础价格图表的上方、下方或后方。

![](https://gitcode.net/OpenDocCN/geekdoc-quant-zh/-/raw/master/docs/tech-ind-ovly/img/9fbde43fe23bd887d872262f67faf3c8.jpg)

## 建议的扫描

### PMO 上升但尚未穿越信号线

这个扫描从过去 60 天至少平均价格为$10 和每日交易量为 100,000 的股票基础开始。股票的 PMO 必须在过去三天内上升，但尚未穿过其信号线。此外，20 日 EMA 高于 50 日 EMA，50 日 EMA 高于 200 日 EMA，表明股票处于中期或长期牛市。这个扫描旨在作为进一步分析和尽职调查的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [today's PMO Line(35,20,10) > yesterday's PMO Line(35,20,10)]
AND [yesterday's PMO Line(35,20,10) > 2 days ago PMO Line(35,20,10)] 
AND [2 days ago PMO Line(35,20,10) > 3 days ago PMO Line(35,20,10)]
AND [today's PMO Line(35,20,10) < today's PMO Signal(35,20,10)]
AND [today's EMA(20,close) > today's EMA(50,close)]
AND [today's EMA(50,close) > today's EMA(200,close)]
```

### PMO 下降但尚未跌破信号线

这个扫描从过去 60 天至少平均价格为$10 和每日交易量为 100,000 的股票基础开始。股票的 PMO 必须在过去三天内下降，但尚未跌破其信号线。此外，20 日 EMA 低于 50 日 EMA，50 日 EMA 低于 200 日 EMA，表明股票处于中期或长期熊市。这个扫描旨在作为进一步分析和尽职调查的起点。

```py
[type = stock] AND [country = US] 
AND [Daily SMA(60,Daily Volume) > 100000] 
AND [Daily SMA(60,Daily Close) > 10] 

AND [today's PMO Line(35,20,10) < yesterday's PMO Line(35,20,10)]
AND [yesterday's PMO Line(35,20,10) < 2 days ago PMO Line(35,20,10)] 
AND [2 days ago PMO Line(35,20,10) < 3 days ago PMO Line(35,20,10)]
AND [today's PMO Line(35,20,10) > today's PMO Signal(35,20,10)]
AND [today's EMA(20,close) < today's EMA(50,close)]
AND [today's EMA(50,close) < today's EMA(200,close)]
```

有关 PMO 扫描的语法详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#decisionpoint_price_momentum_oscillator_pmo "http://stockcharts.com/docs/doku.php?id=scans:indicators#decisionpoint_price_momentum_oscillator_pmo")在支持中心。

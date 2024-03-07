# ZigZag [ChartSchool]

### 目录

+   [ZigZag](#zigzag)

    +   [简介](#introduction)

    +   [计算](#calculation)

    +   [艾略特波动计数](#elliott_wave_counts)

    +   [回撤和投影](#retracements_and_projections)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [进一步研究](#further_study)

## 简介

SharpCharts上的ZigZag功能本身不是指标，而是一种过滤较小价格波动的手段。设置为10%的ZigZag将忽略所有小于10%的价格波动。只有大于10%的价格波动才会显示出来。过滤掉较小的波动使图表分析者能够看到整体情况而不仅仅是细节。重要的是要记住，ZigZag功能没有预测能力，因为它是基于事后的绘制线条。任何预测能力都将来自应用程序，如艾略特波动、价格模式分析或指标。图表分析者还可以使用ZigZag与回撤功能来识别斐波那契回撤和投影。

## 计算

ZigZag基于图表的“类型”。基于收盘价的线状和点状图表将显示基于收盘价的ZigZag。高低收盘价柱状图（HLC）、开盘-最高-最低-收盘价柱状图（OHLC）和蜡烛图显示了周期的高低范围，将显示基于这一高低范围的ZigZag。基于高低范围的ZigZag更有可能改变方向，因为高低范围会更大，产生更大的波动。

参数框允许图表分析者设置ZigZag功能的灵敏度。参数框中设置为5的ZigZag将过滤掉所有小于5%的波动。设置为10的ZigZag将过滤掉小于10%的波动。如果一支股票从100的反弹低点到109的高点（+9%），则不会有线条，因为波动小于10%。如果股票从100的低点上涨到110的高点（+10%），则会有一条线从100到110。如果股票继续上涨到112，这条线将延伸到112（从100到112）。直到股票从高点下跌10%或更多，ZigZag才会反转。从112的高点开始，股票必须下跌11.2点（或至100.8的低点）才能再次出现线条。下面的图表显示了一个带有7% ZigZag的QQQQ线状图。6月初的反弹被忽略，因为小于7%（黑色箭头）。7月的两次回调也被忽略，因为它们远低于7%（红色箭头）。

![ZigZag - 图表1](../Images/0a062c468971ec2a37068fd17aa8ce58.jpg "ZigZag - 图表1")

注意最后一个ZigZag线。敏锐的图表分析师会注意到，尽管QQQQ仅上涨了4.13%（43.36至45.15），但最后一个ZigZag线是向上的。这只是一个临时线，因为QQQQ尚未达到7%的变化阈值。需要到46.40才能获得7%的增长，然后才会有一个永久的ZigZag线。如果QQQQ在此反弹中未能达到7%的阈值，然后下跌至43以下，这条临时线将消失，之前的ZigZag线将从8月初的高点继续。

![ZigZag - Chart 2](../Images/e3d7fefaf2cec25331994401bd084724.jpg "ZigZag - Chart 2")

## Elliott Wave Counts

ZigZag功能可用于过滤小幅波动，并使[Elliott Wave](/school/doku.php?id=chart_school:market_analysis:introduction_to_elliott_wave_theory "chart_school:market_analysis:introduction_to_elliott_wave_theory")计数更加直观。下图显示了标普500ETF的6% ZigZag，以过滤小于6%的波动。经过一些试验，6%被认为是重要的阈值。大于6%的上涨或下跌被认为足够重要，需要为Elliott计数做出波浪。请记住，这只是一个例子。阈值和波浪计数是主观的，取决于个人偏好。基于6% ZigZag，从2009年3月到2010年7月识别出了一个完整的周期。一个完整的周期包括8个波动，5个上涨和3个下跌。

![ZigZag - Chart 4](../Images/c7bc2129d97eae138657f14d227f97e9.jpg "ZigZag - Chart 4")

## Retracements and Projections

Sharpcharts用户可以在正常的“ZigZag”和“ZigZag (Retrace.)”之间选择。如上面的示例所示，正常的ZigZag显示至少移动特定百分比的线条。ZigZag (Retrace.)连接反应高点和低点，并标记测量先前移动的标签。虚线上的数字反映了当前Zigzag线与之前的ZigZag线之间的差异。例如，下图显示了Altera (ALTR)的15% ZigZag (Retrace.)功能。已标记了三条ZigZag线（1、2和3）。连接线1的低点和线2的低点的虚线显示了一个框，其中包含0.638。这意味着线2是线1的0.638（63.8%）。小于1的数字表示该线比先前的线短。连接线2的高点和线3的高点的虚线显示了一个框，其中包含1.646。这意味着线3是线2的1.646（164.6%）。大于1的数字表示该线比先前的线长。

![ZigZag - Chart 3](../Images/a82588f71d48ba3b7a944f177603537b.jpg "ZigZag - Chart 3")

你可能已经猜到，将这些线看作前一线的百分比，可以评估斐波那契投影。8月下跌（线2）回撤了6月至7月上涨（线1）的大约61.8%。这是经典的斐波那契回撤。从9月初到11月初的上涨是8月下跌的1.646倍。在这种意义上，ZigZag（Retrace.）可以用来预测上涨的长度。再次，1.646接近斐波那契1.618，这是许多投影估计中使用的黄金比例。查看我们的ChartSchool文章，了解更多关于[斐波那契回撤](/school/doku.php?id=chart_school:chart_analysis:fibonacci_retracemen "chart_school:chart_analysis:fibonacci_retracemen")的信息。

## 结论

ZigZag和ZigZag（Retrace.）过滤价格走势，并没有任何预测能力。当价格移动一定百分比时，ZigZag线会做出反应。图表分析师可以将各种[技术分析工具](/school/doku.php?id=chart_school:chart_analysis "chart_school:chart_analysis")应用于ZigZag。通过比较反应高点和低点，图表分析师可以进行基本趋势分析。图表分析师还可以叠加ZigZag功能，以寻找在普通柱状图或折线图上可能不太明显的价格模式。ZigZag有一种突出重要走势并忽略噪音的方式。使用ZigZag功能时，不要忘记测量最后一条线，以确定它是暂时的还是永久的。如果当前价格变动小于ZigZag参数，则最后一条ZigZag线是暂时的。当价格变动大于或等于ZigZag参数时，最后一条线是永久的。

## 使用SharpCharts

ZigZag和ZigZag（Retrace.）可以在SharpCharts中作为图表属性部分的价格叠加或作为指标的附加项找到。在从下拉框中选择Zigzag功能后，参数窗口将为空白。默认参数为5%，但这取决于证券的价格特征。一些证券在5%时产生的Zigzag线太少，因此默认设置较低（例如3.75%）。一些证券在5%时产生太多的Zigzag线，因此默认设置较高（例如6.25%）。Zigzag参数可以在图表的左上角看到。应用Zigzag功能后，图表分析师可以调整参数以满足其图表需求。较低的数字会使功能更敏感，而较高的数字会使其不太敏感。[点击这里](http://stockcharts.com/h-sc/ui?s=$COMPQ&p=D&yr=0&mn=8&dy=0&id=p52942080253&listNum=30&a=213475204 "http://stockcharts.com/h-sc/ui?s=$COMPQ&p=D&yr=0&mn=8&dy=0&id=p52942080253&listNum=30&a=213475204")查看带有Zigzag（Retrace.）功能的实时图表。

![ZigZag - SharpCharts](../Images/0647435763830c7f4686202a27f2e98b.jpg "ZigZag - SharpCharts")

![ZigZag - SharpCharts](../Images/a30c4b8e935ac023c8ac3870d0a2efc8.jpg "ZigZag - SharpCharts")

![ZigZag - SharpCharts](../Images/950acc8018316dd367477e78e1aa0913.jpg "ZigZag - SharpCharts")

## 进一步学习

| **艾略特波浪理论** 罗伯特·普雷克特 |
| --- |
| [![](../Images/74272f03b0af5bf3b0ba902aa0a7b2bf.jpg)](http://store.stockcharts.com/products/elliott-wave-principle-key-to-market-behavior "http://store.stockcharts.com/products/elliott-wave-principle-key-to-market-behavior") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/elliott-wave-principle-key-to-market-behavior "http://store.stockcharts.com/products/elliott-wave-principle-key-to-market-behavior") |

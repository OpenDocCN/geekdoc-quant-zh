# 标准差（波动性）[图表学校]

### 目录

+   [标准差（波动性）](#standard_deviation_volatility)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [标准差数值](#standard_deviation_values)

    +   [衡量期望](#measuring_expectations)

    +   [结论](#conclusions)

    +   [与 SharpCharts 一起使用](#using_with_sharpcharts)

    +   [建议的扫描](#suggested_scans)

        +   [排除高波动性](#weeding_out_high_volatility)

## 介绍

标准差是一个统计术语，用于衡量围绕平均值的变异性或离散度。标准差也是波动性的一种度量。一般来说，离散度是实际值与平均值之间的差异。这种离散度或变异性越大，标准差就越高。这种离散度或变异性越小，标准差就越低。图表分析师可以使用标准差来衡量预期风险，并确定某些价格变动的重要性。

## 计算

StockCharts.com 计算的是整体数据集的标准差，这意味着所涉及的周期代表整个数据集，而不是来自更大数据集的样本。计算步骤如下：

1.  计算一定周期或观察次数的平均（均值）价格。

1.  确定每个周期的偏差（收盘价减去平均价格）。

1.  对每个周期的偏差进行平方。

1.  求平方偏差的总和。

1.  将这个总和除以观察次数。

1.  然后标准差等于该数字的平方根。

![标准差 Excel 电子表格](../Images/827d70a25b78c87bbc4fd2ce5240e301.jpg "标准差 Excel 电子表格")

上面的电子表格显示了使用 QQQQ 数据进行 10 期标准差的示例。请注意，10 期[平均值](/school/doku.php?id=chart_school:technical_indicators:moving_averages "chart_school:technical_indicators:moving_averages")是在第 10 期之后计算的，并且这个平均值适用于所有 10 期。使用这个公式构建一个运行标准差会非常耗时。Excel 有一个更简单的方法，使用 STDEVP 公式。下表显示了使用这个公式的 10 期标准差。这里有一个显示标准差计算的[Excel 电子表格](/school/lib/exe/fetch.php?media=chart_school:technical_indicators_and_overlays:std_dev_volatility:cs-stddev.xls "chart_school:technical_indicators_and_overlays:std_dev_volatility:cs-stddev.xls (23 KB)")。

![标准差 - Excel 电子表格](../Images/20acae58150f68d328f7e669eb5eeb35.jpg "标准差 - Excel 电子表格")

![标准差图表 1](../Images/2bd5601c884e6b166edd1d5d763cfb12.jpg "标准差图表 1")

## 标准差数值

标准差值取决于底层证券的价格。价格高的证券，如谷歌（±550），其标准差值会高于价格低的证券，如英特尔（±22）。这些较高的值并不反映更高的波动性，而是反映实际价格。标准差值以直接与底层证券价格相关的术语显示。如果一种证券在一段时间内经历了大幅价格变动，历史标准差值也会受到影响。一种从10变到50的证券在50时很可能具有比10时更高的标准差。

![标准差图表 2](../Images/b15fb064ddd009c33e95e4a2feb59e98.jpg "标准差图表 2")

在上面的图表中，左侧刻度与标准差相关。谷歌的标准差范围从2.5到35，而英特尔的范围从0.10到0.75。谷歌的平均价格变动（偏差）范围从$2.5到$35，而英特尔的平均价格变动（偏差）范围从10美分到75美分。

尽管范围不同，图表分析师可以直观地评估每种证券的波动性变化。英特尔的波动性从四月到六月有所增加，因为标准差多次超过了0.70。谷歌在十月经历了波动性的激增，因为标准差飙升至30以上。要直接比较这两种证券的波动性，必须将标准差除以收盘价。

## 期望值的测量

当前标准差值可用于估计移动的重要性或设定期望。这假设价格变动符合经典的钟形曲线正态分布。尽管证券的价格变动并不总是正态分布，图表分析师仍然可以使用正态分布准则来衡量价格变动的重要性。在正态分布中，68%的观察值落在一个标准差内。95%的观察值落在两个标准差内。99.7%的观察值落在三个标准差内。使用这些准则，交易员可以估计价格变动的重要性。超过一个标准差的变动将显示出高于平均水平的强度或弱势，取决于变动的方向。

![标准差图表 3](../Images/f7c32e5b52d1b30aadb7c56f4542ef0b.jpg "标准差图表 3")

上图显示了微软（MSFT）的21天标准偏差在指标窗口中。一个月大约有21个交易日，月标准偏差在最后一天为0.88。在正态分布中，21个观察值中有68%应该显示价格变动小于88美分。21个观察值中有95%应该显示价格变动小于1.76美分（2 x 0.88或两个标准偏差）。99.7%的观察值应该显示价格变动小于2.64（3 x 0.88或三个标准偏差）。超过1、2或3个标准偏差的价格波动将被视为值得注意。

![标准偏差图表 4](../Images/75f8e377509bdf6de0b3f18e8d55dbc0.jpg "标准偏差图表 4")

21天标准偏差仍然相当变化，从8月中旬到12月中旬在0.32和0.88之间波动。可以应用250天移动平均线来平滑指标并找到一个平均值，大约是68美分。大于68美分的价格波动大于21天标准偏差的250天SMA。这些高于平均水平的价格波动表明了可能预示趋势变化或标志突破的兴趣。

## 结论

标准偏差是波动性的统计度量。这些值为图表分析者提供了预期价格波动的估计。大于标准偏差的价格波动显示出高于平均水平的强度或弱势。标准偏差也与其他指标一起使用，如[Bollinger Bands](/school/doku.php?id=chart_school:technical_indicators:bollinger_bands "chart_school:technical_indicators:bollinger_bands")。这些带状线设置在移动平均线的2个标准偏差之上和之下。超过带状线的波动被认为足够显著，值得关注。与所有指标一样，标准偏差应与其他分析工具一起使用，如[动量振荡器](/school/doku.php?id=chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators#momentum_oscillators "chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators")或[图表模式](/school/doku.php?id=chart_school:chart_analysis:chart_patterns "chart_school:chart_analysis:chart_patterns")。

## 使用SharpCharts

标准偏差在SharpCharts中作为一个指标可用，默认参数为10。根据分析需求可以更改此参数。粗略地说，21天相当于一个月，63天相当于一个季度，250天相当于一年。标准偏差也可以用于周线或月线图表。可以通过点击高级选项然后添加叠加来将指标应用于标准偏差。[点击这里](http://stockcharts.com/h-sc/ui?s=QQQ&p=D&yr=0&mn=6&dy=0&id=p80789045093&listNum=30&a=217969334 "http://stockcharts.com/h-sc/ui?s=QQQ&p=D&yr=0&mn=6&dy=0&id=p80789045093&listNum=30&a=217969334")查看带有标准偏差的实时图表。

![标准差图表 5](../Images/7337c0f649f6341a85e587d7fdf3a381.jpg "标准差图表 5")

![标准差SharpCharts](../Images/98f43a0592a70f119e0718bd3ab5bd75.jpg "标准差SharpCharts")

## 建议的扫描

### 淘汰高波动性

标准差指标通常用于扫描以淘汰波动性极高的证券。这个简单的扫描搜索处于上升趋势的S&P 600股票。最终的扫描条款排除了高波动性股票的结果。请注意，标准差被转换为一种百分比，以便可以在相同的比例上比较不同股票的标准差。

```py
[group is SP600]
AND [Daily EMA(50,close) > Daily EMA(200,close)]  

AND [Std Deviation(250) / SMA(20,Close) * 100 < 20] 
```

有关使用标准差扫描的语法的更多详细信息，请参阅我们的[扫描指标参考](http://stockcharts.com/docs/doku.php?id=scans:indicators#standard_deviation_std_deviation "http://stockcharts.com/docs/doku.php?id=scans:indicators#standard_deviation_std_deviation")在支持中心。

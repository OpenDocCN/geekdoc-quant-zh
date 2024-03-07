# DecisionPoint价格动量振荡器（PMO）[ChartSchool]

### 目录

+   [DecisionPoint价格动量振荡器（PMO）](#decisionpoint_price_momentum_oscillator_pmo)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [解释](#interpretation)

    +   [超买/超卖指标](#overbought_oversold_indicator)

    +   [动量指标](#momentum_indicator)

    +   [信号生成器](#signal_generator)

    +   [PMO配置](#pmo_configurations)

    +   [结论](#conclusion)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [建议的扫描](#suggested_scans)

        +   [PMO上涨但尚未跨越信号线](#pmo_rising_but_not_yet_crossed_over_signal_line)

        +   [PMO下跌但尚未跌破信号线](#pmo_falling_but_not_yet_crossed_below_signal_line)

## 介绍

DecisionPoint价格动量振荡器（PMO）是基于[变化率（ROC）](/school/doku.php?id=chart_school:technical_indicators:rate_of_change_roc_and_momentum "chart_school:technical_indicators:rate_of_change_roc_and_momentum")计算的振荡器，该计算通过使用自定义平滑过程两次平滑指数移动平均线。由于PMO是标准化的，因此它也可以用作相对强度工具。因此，股票可以根据其PMO值排名，作为相对强度的表达。

## 计算

DecisionPoint价格动量振荡器是通过采用一个周期变化率并使用两个自定义平滑函数对其进行平滑而导出的。这些自定义平滑函数与指数移动平均线非常相似，但是与真正的EMA不同，它们不是将时间周期设置加一来创建平滑乘数（如真正的EMA中那样），而是只使用周期本身。

```py
Smoothing Multiplier = (2 / Time period)

Custom Smoothing Function = {Close - Smoothing Function(previous day)} *
 Smoothing Multiplier + Smoothing Function(previous day) 

PMO Line = 20-period Custom Smoothing of
(10 * 35-period Custom Smoothing of
 ( ( (Today's Price/Yesterday's Price) * 100) - 100) )

PMO Signal Line = 10-period EMA of the PMO Line
```

![](../Images/fcf273d3319262ef16792bc1bc61ab3d.jpg)

下表显示了亚马逊的PMO计算：

![](../Images/848e8a353e052ece6f3bcd60d6a8d12d.jpg)

要下载包含这些计算的Excel电子表格，请[点击这里](/school/lib/exe/fetch.php?media=chart_school:technical_indicators_and_overlays:dp_price_momentum_osc:cs-dp-pmo.xls "chart_school:technical_indicators_and_overlays:dp_price_momentum_osc:cs-dp-pmo.xls (387 KB)")。

## 解释

PMO在与零线相关的振荡。通常，PMO方向指示强度是增加还是减少，趋势角度的陡峭程度显示了动力的强度。由于这是一个内部比率计算（与外部相比，如标准相对强度计算，它将一个价格除以另一个价格指数），它返回一个经过标准化的结果，并且可以与任何其他证券或指数的PMO结果进行比较。因此，图表分析师可以通过使用它们的PMO值简单地对证券或指数列表进行相对强度排序。列表不必是同质的 - PMO可以用来对市场指数、股票和共同基金进行排名。

一个与PMO非常相似的指标是由杰拉尔德·阿普尔（Gerald Appel）发明的MACD（移动平均线收敛-发散）指标。PMO和MACD之间的主要区别是每个指标的绝对值。MACD基于移动平均计算，一个MACD读数与另一个毫无关系；而正如上面所解释的，PMO是一个内部比率。下面的图表显示了PMO和MACD在一起。

![](../Images/457845a6ea2559fed652cafacd582514.jpg)

尽管在短期图表上，PMO和MACD的形状相似，但是在长期图表上，PMO的比率型计算的优势是显而易见的，因为PMO相对稳定，不像MACD。请参见下面的周度和月度图表。

![](../Images/a08bcced80290d35246987d59e81dc54.jpg)

![](../Images/20c4ca5aa0b58aeca3a430277fa2a5e4.jpg)

## 超买/超卖指标

如下所示，PMO可以帮助确定价格指数是否超买或超卖。下面是标普500指数的五年图表，显示了各种极端市场条件。该指数的正常PMO范围约为+2.5（超买）至-2.5（超卖），当PMO接近或突破这些限制时，通常会发出价格反转的信号。当PMO在或超出其正常范围的极端位置改变方向时，这往往是价格方向发生中期变化的相当可靠的指示。

![](../Images/b239a0f4276f4700c25ce232f3e93497.jpg)

虽然+2.5至-2.5是广泛股市指数的通常范围，但每个价格指数都将有其自己的“特征”范围。例如，下面的微软（MSFT）图表显示了+5.0至-5.0的范围。始终检查长期图表以验证您正在分析的指数的正常范围。

![](../Images/5d9d22230c2bc2b87a50c7f89a529be1.jpg)

此外，请记住，技术指标是根据在所讨论的时间范围内的特定时间段计算的，因此月度PMO看起来完全不同于日常PMO。请参见下面基于相同七年期间的月度图表，该图表与上面的日常MSFT图表相同。

![](../Images/10dfebd3a39e9bfd5a8df9dd956a17e4.jpg)

## 动量指标

作为动量指标，PMO表达价格运动的方向和速度。在这方面，它类似于其他动量指标。在下面的黄金ETF（GLD）图表中，任一方向上最强烈的移动都以直线、陡峭、平滑的PMO运动为特征。更为停滞的趋势通常伴随着频繁的PMO方向变化。PMO的底部和顶部表明价格动量已经转向，因此它们可以提供价格顶部和底部的早期信号。当PMO处于超买或超卖区域时，它们通常更可靠。

![](../Images/1d6878b0e6c3cd294add5976d7cb3b69.jpg)

最后，与其他振荡器一样，PMO通过形成与价格指数的背离来提示重要方向变化的迹象。下面突出显示了三个独立的背离。两个负面背离（红线）警告着重要的顶部，因为价格指数创造了一个更高的高点，而PMO创造了一个更低的高点。正面背离（绿线）信号着重要的底部，价格创造了一个更低的低点，而PMO创造了一个更高的低点。

![](../Images/89a082a88c19e71ee85e527a1a1b4b27.jpg)

## 信号生成器

当PMO穿过其10周期EMA时，PMO会产生交叉信号。这些信号往往持续时间较短，但可能持续几周。不要直接接受它们，因为它们可能会频繁震荡。它们应该用于提醒您可能的交易机会，而不是作为机械交易模型使用。始终检查图表以验证价格模式和PMO的配置。当价格看起来过度，接近支撑或阻力，并且PMO非常超买或超卖时，信号效果最佳。这些信号也可以与DecisionPoint [趋势分析](/school/doku.php?id=chart_school:trading_strategies:decisionpoint_trend_model "chart_school:trading_strategies:decisionpoint_trend_model")一起使用，使用20/50/200-EMA交叉确定长期、中期和短期的牛市或熊市偏好。

当PMO接近其正常范围的极端位置时，或者在一个强烈、清晰、直线的PMO移动之后发生方向变化和交叉时，最可靠的信号会被产生。在零线周围和PMO在相对平坦模式中移动时，会产生相当多的“噪音”。下图突出显示了交叉信号：

![](../Images/952d8b706d469bae41b4c1a63a297b3b.jpg)

## PMO配置

**横向摆动**

以下图表展示了一个常见的PMO形态，强调了为什么所有PMO交叉信号不能被字面接受。红色圈出的区域是在价格稳步上涨趋势中典型的PMO运动。价格波动很小，所以PMO横向移动。PMO保持在零线以上的事实证明了价格走势的强劲；然而，价格波动中的小波动导致PMO在其10-EMA上下震荡，产生许多无利润的交叉牛市信号。这张图还展示了横向摆动最终会结束以及如何提供微妙线索表明趋势即将结束。

![](../Images/a267835c9e58dc8c96412576062c795f.jpg)

**熊市之吻**

“熊市之吻”是PMO经常显示的三个明显顶部动作中的最后一部分。当我们看到这种经典形态时，它提供了额外的保证，表明可交易的顶部已经形成。当PMO相对超买且价格指数经历了大幅上涨时，我们开始寻找这种形态。这种形态并不总是出现在顶部，但是当出现时，它有助于增强我们对信号可靠性的信心。

第一个动作是一个虚假的PMO顶部。主要顶部总是伴随着一个超买的PMO顶部，但并非所有PMO顶部都预示着主要价格顶部。虚假顶部提醒我们，价格顶部可能只有几周的时间。

接下来我们会看到一个略高的PMO顶部，随后是一个交叉卖出信号，当PMO（蓝线）穿过其10-EMA（绿线）向下交叉时生成。当这些信号发生在非常超买的水平时，它们可能暂时被视为准确，但是，当它们之前有非常强劲的价格行动时，价格可能再次创造新高，这会导致PMO再次开始上升。

最后，随着价格从最终顶部开始回落，PMO再次上涨，这次仅在勉强“吻”到10-EMA的下侧后达到顶峰。有些人称之为“死亡之吻”，但这似乎有点夸张，因此熊市之吻似乎更合适。此外，在重要底部还有一个相反的形态，术语“公牛之吻”似乎比“生命之吻”更贴切。

请注意，这一分析的一个重要方面是，价格指数已经突破了一个上升趋势线，并伴随着熊市之吻。

![](../Images/4a5c4d6de8e91a0cca696d0531374246.jpg)

**公牛之吻**

“公牛之吻”发生在PMO交叉买入信号之后不久，是在产生交叉信号后的初始向上推力后价格回撤的结果。虽然公牛之吻和熊市之吻本质上是相等但相反的形态，但两者之间的价格行为是不同的。通常情况下，熊市之吻是一个不确认信号，与一次上涨中的最终价格高点相一致；而公牛之吻通常与新一轮上涨中的更高价格低点相一致。

![](../Images/f366d38c3af656f556528191e87cdcb8.jpg)

**清晰信号**

虽然公牛和熊市之吻形态相当常见，但也有可能出现非常清晰的PMO反转和交叉，而没有与爆发和重新测试相关的摆动，因为价格趋势的变化相对平稳。关键是，反转和交叉行为可以涵盖各种配置。对图表的研究将有助于更好地理解导致某种类型PMO行为的价格行为。PMO行为还提供了关于可以预期的价格行为类型的线索。

![](../Images/3b9d93e56c554d2b93239a87ad899bde.jpg)

## 结论

决策点价格动量振荡器（PMO）可用作相对强度、动量和超买/超卖条件的衡量标准。它还可以用于通过牛市和熊市交叉确定价格反转。

## 使用 SharpCharts

决策点 PMO 可作为 SharpCharts 的指标使用。默认设置使用35期和20期EMA，带有10期EMA信号线，但用户可以选择更短的时间框架以产生更敏感的振荡器，或选择更长的时间框架以产生更不敏感的振荡器。一旦选择，指标可以放置在基础价格图表的上方、下方或后方。

![](../Images/9fbde43fe23bd887d872262f67faf3c8.jpg)

## 建议的扫描

### PMO 上升但尚未穿越信号线

这个扫描从过去60天至少平均价格为$10和每日交易量为100,000的股票基础开始。股票的 PMO 必须在过去三天内上升，但尚未穿过其信号线。此外，20日EMA高于50日EMA，50日EMA高于200日EMA，表明股票处于中期或长期牛市。这个扫描旨在作为进一步分析和尽职调查的起点。

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

这个扫描从过去60天至少平均价格为$10和每日交易量为100,000的股票基础开始。股票的 PMO 必须在过去三天内下降，但尚未跌破其信号线。此外，20日EMA低于50日EMA，50日EMA低于200日EMA，表明股票处于中期或长期熊市。这个扫描旨在作为进一步分析和尽职调查的起点。

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

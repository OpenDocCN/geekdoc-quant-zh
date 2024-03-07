# Aroon [图表学校]

### 目录

+   [Aroon](#aroon)

    +   [介绍](#introduction)

    +   [计算](#calculation)

    +   [解释](#interpretation)

    +   [新趋势出现](#new_trend_emerging)

    +   [整理期](#consolidation_period)

    +   [结论](#conclusions)

    +   [使用 SharpCharts](#using_with_sharpcharts)

    +   [建议扫描](#suggested_scans)

        +   [Aroon-Up 和 Aroon-Down 低于 20](#aroon-up_and_aroon-down_are_below_20)

## 介绍

由 Tushar Chande 在 1995 年开发，Aroon 是一个指标系统，用于确定股票是否处于趋势状态以及趋势强度如何。“Aroon” 在梵文中意为“黎明的第一缕光”。Chande 选择这个名字是因为这些指标旨在揭示新趋势的开始。Aroon 指标衡量自价格记录 x 天高点或低点以来的周期数。有两个独立的指标：Aroon-Up 和 Aroon-Down。25 天 Aroon-Up 衡量自 25 天高点以来的天数。25 天 Aroon-Down 衡量自 25 天低点以来的天数。在这个意义上，Aroon 指标与典型的[动量振荡器](/school/doku.php?id=chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators#momentum_oscillators "chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators")有很大不同，后者侧重于价格相对于时间。Aroon 是独特的，因为它侧重于时间相对于价格。图表分析师可以使用 Aroon 指标来发现新兴趋势，识别整理期，定义修正期，并预测逆转。

## 计算

Aroon 指标以百分比形式显示，并在 0 到 100 之间波动。Aroon-Up 基于价格高点，而 Aroon-Down 基于价格低点。这两个指标并排绘制，便于比较。SharpCharts 中的默认参数设置为 25，下面的示例基于 25 天。

```py
Aroon-Up = ((25 - Days Since 25-day High)/25) x 100
Aroon-Down = ((25 - Days Since 25-day Low)/25) x 100

```

![Aroon - 图表 1](../Images/3ab84ab991d5385d78051ec79cb27ba4.jpg "Aroon - 图表 1")

随着新高点或新低点之间经过的时间增加，Aroon 会下降。50 是分界点。因为 12.5 天标记着确切的中点，在日线图上不可能出现恰好为 50 的读数。在其他时间框架上是可能的。在日线图上，Aroon 要么低于 50（48），要么高于 50（52）。高于 50 的读数意味着在过去的 12 天或更短时间内记录了新高点或新低点。这是最近一半的回顾期。低于 50 的读数意味着在过去的 13 天或更长时间内记录了新高点或新低点（（25-13）/25 x 100 = 48）。这是回顾期的后一半。下表显示了 25 天 Aroon-Up 和 25 天 Aroon-Down 的数值范围。

![Aroon - 表格 1](../Images/8612b00403ab9e3c3934c406586ae5cb.jpg "Aroon - 表格 1")

## 解释

Aroon 指标在中心线（50）上下波动，并在 0 到 100 之间。这三个水平对于解释很重要。在最基本的情况下，当 Aroon-Up 在 50 以上，Aroon-Down 在 50 以下时，多头占优势。这表示新 x 天的高点比低点更多。对于下降趋势，情况相反。当 Aroon-Up 低于 50，Aroon-Down 高于 50 时，空头占优势。

Aroon 指标达到 100 表示可能出现新趋势。这可以通过另一个 Aroon 指标的下降来确认。例如，Aroon-Up 达到 100，同时 Aroon-Down 降至 30 以下，显示上涨力量。持续高读数意味着价格定期达到指定期间的新高或新低。当 Aroon-Up 在 70-100 范围内持续一段时间时，价格持续上涨。相反，持续低读数表明价格很少达到新高或新低。当 Aroon-Down 在 0-30 范围内持续一段时间时，价格不会下降。但这并不意味着价格在上涨。为此，我们需要检查 Aroon-Up。

## 新趋势的出现

新趋势信号有三个阶段。首先，Aroon 线会交叉。其次，Aroon 线会在 50 以上/以下交叉。第三，Aroon 线中的一条将达到 100。例如，上升趋势信号的第一阶段是当 Aroon-Up 移动到 Aroon-Down 之上。这显示新高比新低更近。请记住，Aroon 衡量的是经过的时间，而不是价格。第二阶段是当 Aroon-Up 移动到 50 以上，Aroon-Down 移动到 50 以下。第三阶段是当 Aroon-Up 达到 100，而 Aroon-Down 保持在相对较低水平。第一和第二阶段并不总是按照这个顺序发生。有时 Aroon-Up 会突破 50，然后突破 Aroon-Down。逆向工程上升趋势阶段将给出新兴下降趋势信号。Aroon-Down 突破 Aroon-Up，突破 50，并达到 100。

![Aroon - 图表 2](../Images/ea3beba1b1659579a7ce335a49d2db50.jpg "Aroon - 图表 2")

上图显示了 CSX Corp（CSX）的周线和 25 周 Aroon。首先，请注意，随着 Aroon-Down 在 2007 年底（最左侧）下降至 50 以下，下降趋势开始减弱。上升趋势的第一阶段是在 2008 年初 Aroon-Up 移动到 Aroon-Down 之上时发出的（第一个橙色圆圈）。Aroon-Up 继续保持在 50 以上，并在 Aroon-Down 保持在相对较低水平时达到 100。请注意，随着上涨的持续，Aroon-Up 保持接近 100。这种新兴上升趋势信号持续到 2008 年 9 月，当 Aroon-Down 突破 Aroon-Up，超过 50 并激增至 100 时（第二个橙色圆圈）。请注意，随着下降趋势的延伸，Aroon-Down 保持接近 100。这张图上的第三个趋势是在 2009 年 6 月 Aroon-Up 激增至 100 并连续一年以上保持在 50 以上时发出的信号（第三个橙色圆圈）。另外，请注意，Aroon-Down 保持在 50 以下一年以上。

## 巩固期

当两条线都低于 50 和/或平行下降时，Aroon 指标会发出巩固信号。一致低于 50 的读数表明平稳交易。对于 25 天 Aroon，低于 50 的读数意味着在 13 天或更长时间内没有记录到 25 天的高点或低点。当没有记录到新高点或新低点时，价格显然是平稳的。同样，当 Aroon-Up 和 Aroon-Down 齐头并进地平行下降，且两条线之间的距离非常小时，通常会形成巩固。这种狭窄的平行下降表明某种交易范围正在形成。第一个突破 50 并达到 100 的 Aroon 指标将触发下一个信号。

![Aroon - 图表 3](../Images/ab449227af3b97ad603c42c6cfb97a72.jpg "Aroon - 图表 3")

上图显示了 Omnicom (OMC) 的 Aroon 指标在平行下降中移动至 50 以下。通道的宽度可能较窄，但我们可以在价格图表上看到巩固形成的迹象。Aroon-Up 和 Aroon-Down 都在黄色区域低于 50。随后，Aroon-Up 突破并飙升至 100，这是在突破之前发生的。另一个 Aroon-Up 在突破点再次飙升，进一步确认了巩固结束和上涨开始的信号。

![Aroon - 图表 4](../Images/b3cf47fd93a5a65bcfa27032edb514f7.jpg "Aroon - 图表 4")

下图显示了 Lifepoint Hospitals (LPNT) 的 25 天 Aroon 指标。五月份，两条线同时下降，呈平行下降趋势。在整个下降过程中，两条线之间的距离大约为 25 点。六月份，Aroon-Up 和 Aroon-Down 趋于平缓，两者在三角形巩固期间都保持在 50 以下约两周时间。Aroon-Down（红色）首先突破 50，正好在价格图表上的三角形突破之前。随着价格突破三角形支撑位，Aroon-Down 达到 100，预示着继续下跌。

## 结论

**Aroon-Up 和 Aroon-Down 是互补指标，分别衡量新 x 天高点和低点之间经过的时间。** 它们一起显示，以便图表分析师可以轻松识别两者中更强的，并确定趋势偏好。 Aroon-Up 的激增伴随着 Aroon-Down 的下降，表明***上升趋势***的出现。相反，Aroon-Down 的激增伴随着 Aroon-Up 的下降，表明***下降趋势***的开始。当两者以平行方式下降或保持在低水平（低于 30）时，就会出现整理。图表分析师可以使用 Aroon 指标来确定某个证券是处于趋势还是横盘交易，然后使用其他指标生成适当的信号。例如，图表分析师可能使用[动量振荡器](/school/doku.php?id=chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators#momentum_oscillators "chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators")来识别超卖水平，当 25 周 Aroon 表明长期趋势向上时。

## 使用 SharpCharts

Aroon 指标在 SharpCharts 上作为一个指标可用。简单地选择“Aroon”将显示 Aroon-Up 和 Aroon-Down。这些指标可以放置在基础证券的价格图之上、之下或之后。用户可以点击指标右侧的绿色箭头查看高级选项，并在 50 处添加水平线。用户甚至可以将另一个指标应用于 Aroon 指标。**[点击这里](http://stockcharts.com/h-sc/ui?s=DIA&p=D&yr=0&mn=8&dy=0&id=p93531652664&listNum=30&a=191771207 "http://stockcharts.com/h-sc/ui?s=DIA&p=D&yr=0&mn=8&dy=0&id=p93531652664&listNum=30&a=191771207")** 查看带有 Aroon 指标的实时图表。

![Aroon - 图表 5](../Images/5639c1604f4256b51c609e45acd66e8e.jpg "Aroon - 图表 5")

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

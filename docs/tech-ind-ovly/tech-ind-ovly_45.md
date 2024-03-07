# RRG相对强度[ChartSchool]

### 目录

+   [RRG相对强度](#rrg_relative_strength)

    +   [介绍](#introduction)

    +   [标准化](#normalization)

    +   [JdK RS-Ratio](#jdk_rs-ratio)

    +   [JdK RS-Momentum](#jdk_rs-momentum)

    +   [周线对比日线](#weekly_versus_daily)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [常见问题](#frequently_asked_questions)

## 介绍

RRG相对强度是一对设计用于衡量相对表现和相对表现动量的指标。JdK RS-Ratio是用于衡量一种证券相对于另一种证券的相对表现的指标。它的伴侣，JdK RS-Momentum衡量RS-Ratio的动量，这意味着它衡量相对表现的动量。RS-Ratio和RS-Momentum被用于相对旋转图（RRGs），但这对指标也可以在SharpCharts上绘制。本文将重点介绍RS-Ratio和RS-Momentum作为SharpCharts上的指标。还有另一篇[ChartSchool文章](/school/doku.php?id=chart_school:chart_analysis:rrg_charts "chart_school:chart_analysis:rrg_charts")详细介绍了它们在相对旋转图中的使用。

***注意:** “相对旋转图™”和“RRG图表™”是[RRG Research](https://www.relativerotationgraphs.com "https://www.relativerotationgraphs.com")的注册商标。*

## 标准化

RS-Ratio和RS-Momentum是“标准化”的，这意味着这些指标以相同的计量单位表示，并在相同水平（100）上下波动。这个标准化过程意味着不同证券的RS-Ratio值可以进行比较，只要使用相同的基准。例如，图表分析师可以绘制九个Sector SPDRs的RS-Ratio，并使用S&P 500作为基准。具有最高RS-Ratio的部门将显示最大的相对强度，而具有最低RS-Ratio的部门将显示最大的相对弱势。

## JdK RS-Ratio

RS-Ratio是一种衡量相对表现趋势的指标。类似于价格相对性，RS-Ratio使用比率分析来比较一种证券与另一种证券（通常是基准）的表现。它旨在定义相对表现的趋势并衡量该趋势的强度。

下图显示了主窗口中的Technology SPDR（XLK），中间窗口中的价格相对性（XLK:$SPX比率）以及底部窗口中的RRG指标。我们将首先关注RS-Ratio（红色）。RS-Momentum（绿色）将在下一节中介绍。

![](../Images/2a0dc50b78fb0963a6c32a93675df51e.jpg)

RS-Ratio 为图表分析师提供了一个清晰的工具来定义相对表现的趋势。当指标高于 100 时（相对强势），反映了相对表现的上升趋势；当指标低于 100 时（相对弱势），反映了相对表现的下降趋势。指标越高于 100，相对表现的上升趋势就越强。指标越低于 100，相对表现的下降趋势就越强。

与所有追随趋势的指标一样，如移动平均线，驱动 RS-Ratio 的趋势跟踪模型包括滞后期。这意味着在 RS-Ratio 穿过 100 之前，价格相对会有上涨。相反，在 RS-Ratio 穿过 100 之前，价格相对会有下降。请注意上图中价格相对（XLK:$SPX 比率）在八月初达到峰值，但 RS-Ratio 直到十月中旬才跌破 100。同样，价格相对在七月中旬触底，但 RS-Ratio 直到九月中旬才突破 100。这对于设计忽略波动并专注于趋势的趋势跟踪指标来说是典型的。下图显示了另一个例子，消费者自由 SPDR（XLY）。

![](../Images/01807eb150ee32efaafc287e0d19ffff.jpg)

请记住，当使用相同的基准证券时，RS-Ratio 的值可以进行比较。假设我们正在比较四个行业 SPDR 与标普 500 的相对表现，RS-Ratio 的值如下：XLK=102.04，XLI=101.41，XLF=100.2，XLV=103.66。首先，所有四个都有高于 100 的 RS-Ratio，这意味着所有四个显示出相对强势（相对于标普 500）。其次，XLV 显示出最强的相对强势，因为它的 RS-Ratio 是四个中最高的。XLF 是四个中最弱的，因为它的 RS-Ratio 是最低的。

## JdK RS-Momentum

在详细查看 RS-Momentum 之前，让我们回顾一下动量的概念以及它与趋势的关系。与价格图表一样，图表分析师应该记住，动量在趋势实际逆转之前就会改变方向。然而，并非所有动量变化都会导致趋势逆转。

以价格和移动平均线为例。价格首先朝向移动平均线移动，然后在延伸时穿过移动平均线。然而，价格并不总是穿过移动平均线来信号趋势反转。激进的交易者更可能在价格朝向移动平均线移动时建仓，因为这意味着动量正在改善。保守的投资者更可能等待价格上涨到移动平均线之上，因为趋势尚未完全逆转。

RS-Momentum 是一个衡量 RS-Ratio 动量（变化率）的指标。作为一个动量指标，它领先于 RS-Ratio，并可用于预测 RS-Ratio 的转折点。通常，当 RS-Ratio 形成低谷并开始上升时，RS-Momentum 会上穿 100。相反，当 RS-Ratio 形成高峰并开始下降时，RS-Momentum 会下穿 100。

下面的图表显示了公用事业 SPDR（XLU），绿色表示 RS-Momentum，红色表示 RS-Ratio。RS-Momentum 在十二月中旬上穿 100，并在四周内大部分时间保持在 100 以上。请注意，RS-Ratio 在 RS-Momentum 上穿 100 时触底，而 RS-Ratio 在一月下旬后期上穿 100。

![](../Images/1c2136a1291063b6fac86347c59630de.jpg)

请记住，RS-Momentum 是 RS-Ratio 的指标。此外，它是一个动量指标，这意味着它经常会在 100 以上/以下波动。图表分析师可能希望专注于持续在 100 以上/以下的波动，以预测 RS-Ratio 中类似的交叉。

下面的图表显示了生物科技 SPDR（XBI），突出显示了 RS-Momentum 和 RS-Ratio 之间关系的两个示例。灰色阴影显示了二月至三月六周中有四周 RS-Momentum 低于 100。尽管指标短暂上升到 100 以上，但这种上升并没有持续很长时间，很快又回落到 100 以下。这表明 RS-Ratio 的动量转为负面，最终在三月下半月 RS-Ratio 下穿 100。

![](../Images/eb9a2b0fa5088363104d13e9c54c5335.jpg)

蓝色阴影显示了从四月中旬到五月下旬 RS-Momentum 在 100 以上的情况。RS-Ratio 在 RS-Momentum 超过 100 时触底，但直到五月底才上穿 100。顺便说一句，RS-Ratio 在上穿 100 之前，正好在 XBI 于六月初大幅上涨之前。

## 周线与日线

与常规柱状图一样，选择的时间范围会影响 RS-Ratio，并导致不同的结论。在下面的示例中，左侧图表显示了标普500指数两个月的日常数据，两个月的趋势是下降的。右侧图表显示了一年的周数据，总体趋势明显向上。黄色阴影区域突出显示了日常图表上显示的两个月数据，以便将这种下降放入透视中。显然，这是长期上升趋势中的短期下降趋势（回撤）。

![](../Images/b0be3ac4a89fc5eb7a961ac87f75e3f6.jpg)

现在让我们看看使用周线和日线图表的 RS-Ratio 和 RS-Momentum 的示例。第一个图表使用周时间范围，两个指标都低于 100，表明相对表现处于下降趋势且动量为负。这周线图表捕捉了长期趋势。第二个图表使用日时间范围，两个指标都高于 100，表明相对表现处于上升趋势且动量为正。这日线图表捕捉了比周线图表更小的趋势。

![](../Images/1660cf159293a87aa73cc050e704b22d.jpg) ![](../Images/97b1216f8ef8cf70d0c2c8b736cce38c.jpg)

如果我们假设长期趋势在这里占主导地位，那么我们也可以推断长期相对表现的下降趋势最终将战胜短期相对表现的上升趋势。换句话说，日线图上的相对表现上升趋势只是周线图上的一个小波动，不足以扭转相对表现的更大下降趋势。

与技术分析的所有方面一样，研究不同的时间框架以获得完整的图片是一个非常好的习惯。电信部门在周线图上明显表现不佳，动量为负。RS-Momentum的上升显示了在周线图上负动量的减少，这反映在日线图上，其中RS-Ratio和RS-Momentum移动超过100。

## 结论

RS-Ratio和RS-Momentum为图表分析师提供了一个四方面的方法来衡量相对表现。首先，RS-Ratio根据另一个证券（通常是基准）来衡量相对表现。简单来说，当证券高于100时显示相对强势，低于100时显示相对弱势。其次，RS-Ratio值告诉我们相对强势或相对弱势的程度。值越高于100，相对强势越大。值越低于100，相对弱势越大。第三，图表分析师可以比较RS-Ratio值以确定组内最强的证券。第四，RS-Momentum衡量RS-Ratio的动量，这可以用来预测RS-Ratio的转折点。与所有指标一样，图表分析师应该将相对表现与其他技术工具结合起来，以获得完整的图片。

## 使用SharpCharts

RS-Ratio和RS-Momentum在SharpCharts中作为指标可用。它们在指标下拉列表中被分组为“RRG相对强度”。一旦选择，用户可以通过在“参数”框中输入其符号来设置基准证券。下面的示例显示了消费者自由支出SPDR（XLY）与标普500作为基准的情况。请记住，任何符号都可以用来衡量相对表现。如果您想比较消费者自由支出SPDR（XLY）与技术SPDR（XLK）的表现，请简单地输入XLK作为参数并单击更新。[点击这里](http://stockcharts.com/h-sc/ui?s=XLY&p=D&yr=0&mn=6&dy=0&id=p07575376366&a=399188908 "http://stockcharts.com/h-sc/ui?s=XLY&p=D&yr=0&mn=6&dy=0&id=p07575376366&a=399188908") 查看RRG相对强度实际运行的实例。

![](../Images/cd94b164ca4ebceabb5fce240ff2ccfa.jpg)

## 常见问题

**问：绘制RRG需要多少数据？**

答：您至少需要大约50个数据点，因此对于每日RRG，您需要超过50天的数据。对于每周RRG，您将需要大约250天的数据。

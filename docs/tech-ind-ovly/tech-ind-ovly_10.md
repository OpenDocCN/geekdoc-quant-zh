# 枢轴点 [ChartSchool]

### 目录

+   [枢轴点](#pivot_points)

    +   [介绍](#introduction)

    +   [时间框架](#timeframes)

    +   [标准枢轴点](#standard_pivot_points)

    +   [斐波那契枢轴点](#fibonacci_pivot_points)

    +   [Demark枢轴点](#demark_pivot_points)

    +   [设定基调](#setting_the_tone)

    +   [支撑和阻力](#support_and_resistance)

    +   [结论](#conclusions)

    +   [与SharpCharts一起使用](#using_with_sharpcharts)

    +   [进一步研究](#further_study)

    +   [额外资源](#additional_resources)

        +   [股票与商品杂志文章](#stocks_commodities_magazine_articles)

## 介绍

**枢轴点是图表分析师可以用来确定方向运动和潜在支撑/阻力水平的重要水平。** 枢轴点使用先前时期的最高、最低和收盘价来估计未来的支撑和阻力水平。在这方面，枢轴点是预测性或领先指标。至少有五种不同版本的枢轴点。本文将重点介绍标准枢轴点、Demark枢轴点和斐波那契枢轴点。

枢轴点最初是由地板交易员用来设定关键水平的。地板交易员是最初的日间交易员。他们在一个快节奏的环境中进行短期关注的交易。在交易日开始时，地板交易员会查看前一天的最高、最低和收盘价，以计算当天的枢轴点。以此枢轴点为基础，进一步的计算用于设定支撑1、支撑2、阻力1和阻力2。这些水平将在整天交易中用于辅助他们的交易。

## 时间框架

1、5、10和15分钟图表的枢轴点使用前一天的最高、最低和收盘价。换句话说，今天的盘内图表的枢轴点将仅基于昨天的最高、最低和收盘价。一旦设置了枢轴点，它们将不会改变，并在整天内保持有效。

![枢轴点 - 图表1](../Images/7340af632f63d7a16d9d588e81bcd18a.jpg "枢轴点 - 图表1")

30、60和120分钟图表的枢轴点使用前一周的最高、最低和收盘价。这些计算是基于日历周的。一旦周开始，30、60和120分钟图表的枢轴点将在整个周内保持不变。**直到周结束并且可以计算新的枢轴点，它们才会改变。**

![枢轴点 - 图表2](../Images/f30afd69e1c419d1411f744d3bf22f97.jpg "枢轴点 - 图表2")

每日图表的枢轴点使用前一个月的数据。6月1日的枢轴点将基于5月的最高、最低和收盘价。它们在整个6月保持不变。新的枢轴点将在7月的第一个交易日计算。这些将基于6月的最高、最低和收盘价。

![枢轴点 - 图表3](../Images/f1307519517eaed9943f7edc6e82b43f.jpg "枢轴点 - 图表3")

每周和每月图表的枢轴点使用前一年的数据。

## 标准枢轴点

标准 Pivot Points 从基准 Pivot Point 开始。这是高、低和收盘价的简单平均值。中间 Pivot Point 在支撑和阻力 Pivot 之间显示为实线。请记住，高、低和收盘价都是来自前一时期的数据。

```py
Pivot Point (P) = (High + Low + Close)/3

Support 1 (S1) = (P x 2) - High

Support 2 (S2) = P  -  (High  -  Low)

Resistance 1 (R1) = (P x 2) - Low

Resistance 2 (R2) = P + (High  -  Low)

```

下图显示了纳斯达克100 ETF（QQQ）在15分钟图表上的标准 Pivot Points。在6月9日交易开始时，Pivot Point 处于中间位置，阻力水平在上方，支撑水平在下方。这些水平在一天内保持不变。

![Pivot Points  -  图表 4](../Images/ad17543763434c2aee7ef6ea34c715f6.jpg "Pivot Points  -  图表 4")

## 斐波那契 Pivot Points

斐波那契 Pivot Points 与标准 Pivot Points 开始方式相同。从基准 Pivot Point 开始，将高低差的斐波那契倍数加到形成阻力水平，减去形成支撑水平。

```py
Pivot Point (P) = (High + Low + Close)/3

Support 1 (S1) = P - {.382 * (High  -  Low)}

Support 2 (S2) = P - {.618 * (High  -  Low)}

Support 3 (S3) = P - {1 * (High  -  Low)}

Resistance 1 (R1) = P + {.382 * (High  -  Low)}

Resistance 2 (R2) = P + {.618 * (High  -  Low)}

Resistance 3 (R3) = P + {1 * (High  -  Low)}

```

下图显示了道琼斯工业平均指数 SPDR（DIA）在15分钟图表上的斐波那契 Pivot Points。R1 和 S1 基于38.2%。R2 和 S2 基于61.8%。R3 和 S3 基于100%。

![Pivot Points  -  图表 5](../Images/e925733240b3aadf2248df1742e43705.jpg "Pivot Points  -  图表 5")

## Demark Pivot Points

Demark Pivot Points 以不同的基准开始，并使用不同的支撑和阻力公式。这些 Pivot Points 取决于收盘价和开盘价之间的关系。

```py
If Close < Open, then X = High + (2 x Low) + Close

If Close > Open, then X = (2 x High) + Low + Close

If Close = Open, then X = High + Low + (2 x Close)

Pivot Point (P) = X/4

Support 1 (S1) = X/2 - High

Resistance 1 (R1) = X/2 - Low

```

下图显示了罗素2000 ETF（IWM）在15分钟图表上的 Demark Pivot Points。请注意，只有一个阻力（R1）和一个支撑（S1）。Demark Pivot Points 没有多个支撑或阻力水平。

![Pivot Points  -  图表 6](../Images/928b04e318a922cff8e25944b23732c0.jpg "Pivot Points  -  图表 6")

## 设定基调

Pivot Point 为价格走势设定了一般基调。这是标记为 (P) 的一组中间线。突破 Pivot Point 是积极的，显示出力量。请记住，这个 Pivot Point 基于前一时期的数据。它在当前时期被提出作为第一个重要水平。突破 Pivot Point 表明有力量，目标是第一个阻力。突破第一个阻力显示出更多力量，目标是第二个阻力水平。

![Pivot Points  -  图表 7](../Images/c18b966dd0e88dac6656de827f61d945.jpg "Pivot Points  -  图表 7")

相反的情况发生在下行。突破 Pivot Point 表明弱势，目标是第一个支撑水平。突破第一个支撑水平显示出更多弱势，目标是第二个支撑水平。

## 支撑和阻力

基于枢纽点的支撑和阻力水平可以像传统的支撑和阻力水平一样使用。关键是当这些水平发挥作用时密切关注价格走势。如果价格下跌到支撑然后企稳，交易者可以寻找对支撑的成功测试和反弹。通常有助于寻找一个看涨的图表模式或指标信号来确认从支撑处的上升。同样，如果价格上涨到阻力然后停滞，交易者可以寻找在阻力处的失败和下跌。同样，图表分析师应该寻找一个看跌的图表模式或指标信号来确认从阻力处的下降。

![枢纽点 - 图表 8](../Images/4cbb1c5fda781895b5ede3f217bd15f2.jpg "枢纽点 - 图表 8")

第二支撑和阻力水平也可以用来识别潜在的超买和超卖情况。突破第二阻力水平将显示出力量，但也会表明一种可能导致回调的超买情况。同样，跌破第二支撑将显示出弱势，但也会暗示一种可能导致反弹的短期超卖状态。

![枢纽点 - 图表 9](../Images/c766087fcdce05932d61a0c4a0d1c9e3.jpg "枢纽点 - 图表 9")

## 结论

**枢纽点为图表分析师提供了一种确定价格走势然后设定支撑和阻力水平的方法。** 它通常从枢纽点的交叉开始。有时市场在枢纽点之上或之下开始。支撑和阻力在交叉后发挥作用。虽然最初是为地板交易者设计的，但枢纽点背后的概念可以应用于各种时间框架。与所有指标一样，重要的是用技术分析的其他方面来确认枢纽点信号。一个看跌的蜡烛图反转模式可以确认在第二阻力处的反转。超卖的相对强弱指标可以确认在第二支撑处的超卖情况。MACD的上升可以用来确认成功的支撑测试。最后，有时第二或第三支撑/阻力水平在图表上看不到。这仅仅是因为它们的水平超过了右侧的价格刻度。换句话说，它们在图表之外。

## 使用 SharpCharts

枢纽点可以在 SharpCharts 工作台上作为“覆盖层”找到。标准枢纽点是默认设置，参数框为空。图表分析师可以通过在参数框中放置“F”来应用斐波那契枢纽点，通过在框中放置“D”来应用 Demark 枢纽点。甚至可以同时显示所有三个。[点击这里](http://stockcharts.com/h-sc/ui?s=$SPX&p=D&b=5&g=0&id=p75918574596&listNum=30&a=236469237 "http://stockcharts.com/h-sc/ui?s=$SPX&p=D&b=5&g=0&id=p75918574596&listNum=30&a=236469237") 查看带有所有三个枢纽点的实时图表。然后您可以删除您不想要的那些。

[![枢轴点  -  SPY示例](../Images/5248548a8301aea1cb689fbbcf1f9757.jpg "枢轴点  -  SPY示例")](http://stockcharts.com/h-sc/ui?s=$SPX&p=D&b=5&g=0&id=p75918574596&listNum=30&a=236469237 "http://stockcharts.com/h-sc/ui?s=$SPX&p=D&b=5&g=0&id=p75918574596&listNum=30&a=236469237")

![枢轴点 - SharpCharts](../Images/a95df3dd4dd05d885bcc146d39c0d9eb.jpg "枢轴点 - SharpCharts")

## 进一步研究

本书专门有一整章介绍如何使用标准枢轴点进行交易。Person向图表分析师展示如何将枢轴点支撑和阻力水平与技术分析的其他方面结合起来，生成买入和卖出信号。

| **技术交易战术完全指南** 约翰·珀森 |
| --- |
| [![](../Images/c3544022b2f24f16e18c19a16b6207ff.jpg)](http://store.stockcharts.com/products/a-complete-guide-to-technical-trading-tactics "http://store.stockcharts.com/products/a-complete-guide-to-technical-trading-tactics") |
| [![立即购买](../Images/1c93f62bf2e6d9151c2861b04ef09d52.jpg "立即购买")](http://store.stockcharts.com/products/a-complete-guide-to-technical-trading-tactics "http://store.stockcharts.com/products/a-complete-guide-to-technical-trading-tactics") |

* * *

## 其他资源

### 股票与商品杂志文章

**[John Devcic撰写的利用枢轴点预测逆转](http://stockcharts.com/h-mem/tascredirect.html?artid=\V24\C03\054DEVC.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V24\C03\054DEVC.pdf")**

2006年2月 - 股票与商品 V. 24:3 (72-73)

**[Jayanthi Gopalakrishnan撰写的枢轴点文章](http://stockcharts.com/h-mem/tascredirect.html?artid=\V18\C02\010PIV.pdf "http://stockcharts.com/h-mem/tascredirect.html?artid=\V18\C02\010PIV.pdf")**

2000年1月 - 股票与商品 V. 18:2 (16-22)

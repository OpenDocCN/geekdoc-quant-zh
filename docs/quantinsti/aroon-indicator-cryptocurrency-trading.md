# Aroon 指标:如何将其用于加密货币交易

> 原文：<https://blog.quantinsti.com/aroon-indicator-cryptocurrency-trading/>

由[瓦伦·迪瓦卡](https://www.linkedin.com/in/varun-divakar-b862a667/)

在这篇博客中，我们将了解 Aroon 指标，也称为 Aroon 振荡器。

### **什么是 Aroon 指标？**

1995 年，Tuscarora 资本管理公司的负责人,《新技术交易者》( 1994 年)和《超越技术分析》( 2001 年)的作者 Tushar Chande 开发了 Aroon 指标。这对于捕捉趋势和识别区间市场非常有用。

### **如何计算 Aroon 指标？**

首先让我们了解一下 Aroon 是如何计算的。Aroon 指示器由两部分组成。

1.  阿龙努普
2.  阿龙当

**AroonUp** 用于衡量上涨趋势，**aroondow**用于衡量下跌趋势。通常，AroonUp 是使用高点计算的，AroonDown 是使用低点计算的，但您也可以仅使用收盘价来计算它们。

要计算 AroonUp 值，您需要知道两件事:

1.  回顾时期
2.  自最高价形成以来的时期

假设你选择了一个 14 周期的回顾，那么我们需要检查过去 14 个周期的最高价/收盘价。

![14-period lookback](img/8b8bf9f26b0534bdfed322af79773863.png)

让我们说最高的顶点出现在第四根蜡烛上。则 AroonUp 计算如下:

AroonUp =(回看-(自最高高点以来的周期))/(回看)

因此，aro NUP =(14-4)/14

即。 **AroonUp = 0.7142**

你一定注意到了，Aroon 指标是一个百分比值。它只是表示在过去的“X”周期中，最高/最低价格有多近。上面计算的 AroonUp 值乘以 100，以百分比形式表示。

AroonUp = 0.7142*100

即。 **AroonUp = 71.42**

同样，AroonDown 是使用过去 X 个周期中的最低低点计算的。

**AroonUp =(回看-(自最低低点以来的周期))/(回看)**

![Calculate Aroon Indicator](img/55c0d945ba9966ab617556d490313a45.png)

减去两个 Aroon 指标，计算 Aroon 振荡器。

**AroonOscillator = AroonUp-AroonDown**

虽然 Aroon 振荡器是表示这两种指标的简单方法。让我们来详细了解一下如何解读这些指标。

### **Aroon 指示器的解释**

当 AroonUp 值大于 AroonDown 值时，市场被称为趋势上升。

但 Aroon 指标的这种交叉并不被认为是一个强烈的信号，相反，它被视为趋势的开始。只有当 AroonUp 值超过 50 时，才会确认上升趋势。

![Aroon line](img/87e4f2d8297919d6e7c4448fd57ba6c3.png)

在上图中，绿色的 Aroon 线代表 aroonp 值，它高于红线或 AroonDown 线，每当市场趋势向上时。

你也可以用 Aroon 振荡指标来解释这一点，如果 Aroon 振荡指标高于零，它表示上升趋势，如果它高于 100，你认为它是上升趋势的确认，如果它低于-100，那么我们可以确认它是下降趋势。

![Aroon oscillator](img/7d96c497d22d99bc7795a3db88c79818.png)

Aroon 指标也可以用来识别区间市场。当 AroonUp 和 AroonDown 指标平行时，或者当 Aroon 振荡指标持平时，它表明市场在区间波动。如果你是一个日内黄牛党，那么这个平坦的区间是你交易的理想选择。

和所有技术指标一样，Aroon 也是一个滞后指标。因此，它容易受到突然峰值的影响。为了防止这种波动，交易者应该有有效的退出标准。

[加密货币交易商](https://quantra.quantinsti.com/course/crypto-trading-strategies-advanced)总是在寻找最可靠的经纪和交易平台。你可以参考这篇列出了 [9 个最佳加密货币交易所](https://blog.quantinsti.com/top-9-cryptocurrency-trading-platforms/)的文章。

在我们的[加密货币交易](https://quantra.quantinsti.com/course/crypto-trading-strategies-intermediate)课程中，我们已经成功应用 Aroon 指标结合 RSI 生成交易信号。

*免责声明:股票市场的所有投资和交易都有风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。*
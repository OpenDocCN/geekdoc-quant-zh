# ADX 指标的数学直觉:Python 方法

> 原文：<https://blog.quantinsti.com/adx-indicator-python/>

以[重香重香](https://www.linkedin.com/in/rekhit/)

如果要确定趋势的强度，可以使用平均方向指数(ADX)指标。但是你为什么想要找到趋势的强度呢？如果你在较弱的趋势中交易，那么与较强的趋势相比，反转的可能性很大。所以把你的方向性交易和更强的趋势结合起来会帮助你获得更高的命中率和更高的平均盈利能力。

这里有一个有趣的事实，虽然名称是平均方向指数(ADX)，但它并没有告诉我们趋势的方向。虽然这听起来令人担忧，但原因很简单，ADX 指标总是与正方向指标和负方向指标一起使用，它们分别表示上升和下降趋势。我们将在本博客中了解 ADX 指标及其用途。

我们将讨论以下主题:

*   [什么是 ADX 指标？](#What)
*   [ADX 指标的计算](#Calculation)
*   [使用 Python 使用 ADX 指标交易策略](#Use)

## ![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")什么是 ADX 指标

威尔斯·怀尔德创造了方向移动指标和 ADX 指标来确定趋势的方向和强度。根据 Welles Wilder 的说法，方向移动指示器据说由以下部分组成:真实范围、平滑的正方向指示器(+DI)和平滑的负方向指示器(-DI)。

ADX 指标计算为+DI 指标和-DI 指标之差的平滑平均值，从而告诉我们趋势的强度。

ADX 指示器的值介于 0 和 100 之间。人们普遍认为，如果 ADX 高于 25，这是一个强劲趋势的迹象。

在我们继续讨论基于 ADX 指标的策略之前，让我们看一个小例子，看看 ADX 指标是如何计算的。

## ![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")ADX 指标的计算

我们将此部分分为以下步骤:

*   真实范围
*   正向运动
*   负向运动
*   平滑值
*   正指数指示器和负指数指示器
*   ADX 指标:最终计算

假设我们有以下数据。

| **日期** | **高** | **低** | **关闭** |
| 11/29/2019 | Ninety | Eighty-two | Eighty-seven |
| 12/2/2019 | Ninety-five | eighty-five | Eighty-seven |
| 12/3/2019 | One hundred and five | Ninety-three | Ninety-seven |
| 12/4/2019 | One hundred and twenty | One hundred and six | One hundred and fourteen |
| 12/5/2019 | One hundred and forty | One hundred and twenty-four | One hundred and thirty-three |
| 12/6/2019 | One hundred and sixty-five | One hundred and forty-seven | One hundred and fifty-seven |
| 12/9/2019 | One hundred and ninety-five | One hundred and seventy-five | One hundred and eighty-six |
| 12/10/2019 | Two hundred and thirty | Two hundred and eight | Two hundred and twenty-three |
| 12/11/2019 | Two hundred and seventy | Two hundred and forty-six | Two hundred and sixty-four |
| 12/12/2019 | Three hundred and fifteen | Two hundred and eighty-nine | Three hundred and eleven |
| 12/13/2019 | Three hundred and sixty-five | Three hundred and thirty-seven | Three hundred and fifty |

在我们实际使用 ADX 指标之前，我们还必须了解一些其他变量。我们已经将博客的这一部分分成了许多小部分，我们从寻找股票价格的真实范围开始。我们走吧！

### 真实范围

第一行的范围是上限和下限之间的差值。那是 90 - 82，8。只有真理才能让你自由！虽然前面的陈述是武断的，但它在某种程度上也是正确的。如果你看高低点数据，你可能会错过连续几天的价格变化。这就是真正的范围。

简单地说，我们取以下三个分量的最大值:

(当前高电平-当前低电平)

(当前高点-前一收盘点)的绝对值

(当前低点-前一收盘点)的绝对值

在这方面，我们发现了不同日期之间价格波动的实际范围。

如果我们必须计算上述值的真实范围，那么对于 12 月 2 日，这三个值将是:

(当前高-当前低)= 95 - 85 = 10

(当前高点-前一收盘点)的绝对值= 95 - 87 = 8

(当前低点-前一收盘点)的绝对值= (85 - 87) =绝对值(-2) = 2

因此，因为真实范围是三个值中的最大值，所以它应该是 10。

现在让我们来填桌子吧。

| **日期** | **高** | **低** | **关闭** | **(高-低)****【1】** | **(今日高点-昨日收盘)****【2】** | **(今日低点-昨日收盘)****【3】** | **真实范围** |
| 11/29/2019 | Ninety | Eighty-two | Eighty-seven | - | - | - | - |
| 12/2/2019 | Ninety-five | eighty-five | Eighty-seven | Ten | eight | Two | Ten |
| 12/3/2019 | One hundred and five | Ninety-three | Ninety-seven | Twelve | Eighteen | six | Eighteen |
| 12/4/2019 | One hundred and twenty | One hundred and six | One hundred and fourteen | Fourteen | Twenty-three | nine | Twenty-three |
| 12/5/2019 | One hundred and forty | One hundred and twenty-four | One hundred and thirty-three | Sixteen | Twenty-six | Ten | Twenty-six |
| 12/6/2019 | One hundred and sixty-five | One hundred and forty-seven | One hundred and fifty-seven | Eighteen | Thirty-two | Fourteen | Thirty-two |
| 12/9/2019 | One hundred and ninety-five | One hundred and seventy-five | One hundred and eighty-six | Twenty | Thirty-eight | Eighteen | Thirty-eight |
| 12/10/2019 | Two hundred and thirty | Two hundred and eight | Two hundred and twenty-three | Twenty-two | forty-four | Twenty-two | forty-four |
| 12/11/2019 | Two hundred and seventy | Two hundred and forty-six | Two hundred and sixty-four | Twenty-four | Forty-seven | Twenty-three | Forty-seven |
| 12/12/2019 | Three hundred and fifteen | Two hundred and eighty-nine | Three hundred and eleven | Twenty-six | Fifty-one | Twenty-five | Fifty-one |
| 12/13/2019 | Three hundred and sixty-five | Three hundred and thirty-seven | Three hundred and fifty | Twenty-eight | Fifty-four | Twenty-six | Fifty-four |

好吧。让我们继续前进。

### 正向运动

我们一路向上，我的朋友。顾名思义，积极的方向指标是用来帮助我们衡量市场的上升趋势。当然，我们将它与负方向指标配对，以从指标中获得真正的意义。

但是我怎么知道哪条路是向上的？

直觉上，如果每天的新高是与前一天的新高相比，那么我们可以说价格在上升。

![](img/0561ae0b2401628ad2fa6c018d496749.png)

对此我们有一个简单的公式，它使用了在英语和编程中都能找到的著名的“if-else”语句。

如果(今日高点-昨日高点)>(昨日低点-今日低点)，那么

+DM =(今日高点-昨日高点)

否则就是 0。

但是我们为什么要这样做呢？我们正在检查两个“高点”的价格差是否大于两个低点的价格差。这表明对该股票有需求，并愿意以高于前一高点的价格买入。

让我们进入下一部分。

### 负向运动

就像人生一样，有起有落，总会有股票下跌的时候。正如我们在上一节中讨论的，我们正在检查抛售压力，如果投资者准备以低于前一天的价格出售股票，这种压力就会出现。

因此，在负方向指示器的情况下，公式为:

如果(昨日低点-今日低点)>(今日高点-昨日高点)，那么

-DM =(昨日低点-今日低点)

否则就是 0。

我们将使用上述公式计算桌子的正向移动和反向移动。

| **日期** | **高** | **低** | **关闭** | **真实范围** | **阳性糖尿病** | **负 DM** |
| 11/29/2019 | Ninety | Eighty-two | Eighty-seven | - | - | - |
| 12/2/2019 | Ninety-five | eighty-five | Eighty-seven | Ten | five | Zero |
| 12/3/2019 | One hundred and five | Ninety-three | Ninety-seven | Eighteen | Ten | Zero |
| 12/4/2019 | One hundred and twenty | One hundred and six | One hundred and fourteen | Twenty-three | Fifteen | Zero |
| 12/5/2019 | One hundred and forty | One hundred and twenty-four | One hundred and thirty-three | Twenty-six | Twenty | Zero |
| 12/6/2019 | One hundred and sixty-five | One hundred and forty-seven | One hundred and fifty-seven | Thirty-two | Twenty-five | Zero |
| 12/9/2019 | One hundred and ninety-five | One hundred and seventy-five | One hundred and eighty-six | Thirty-eight | Thirty | Zero |
| 12/10/2019 | Two hundred and thirty | Two hundred and eight | Two hundred and twenty-three | forty-four | Thirty-five | Zero |
| 12/11/2019 | Two hundred and seventy | Two hundred and forty-six | Two hundred and sixty-four | Forty-seven | Forty | Zero |
| 12/12/2019 | Three hundred and fifteen | Two hundred and eighty-nine | Three hundred and eleven | Fifty-one | Forty-five | Zero |
| 12/13/2019 | Three hundred and sixty-five | Three hundred and thirty-seven | Three hundred and fifty | Fifty-four | Fifty | Zero |

因此，通过这种方式，我们理解了方向性运动。

在我们转向方向指数指标之前，我们必须弄清楚什么是真实范围的平滑版本，正方向移动和负方向移动。

### 平滑值

我们应该注意，平滑版本有点类似于移动平均，因为它用于平滑数据中的波动(如果有的话)。

我们将周期定义为 5。这是任意选择的。

我们将做正向运动的平滑值。第一个值的计算方法是取前 5 个值的和，即(5 + 10 +15 + 20 + 25) = 75。

下一个值是通过取前一个平滑值并从中减去平均值来计算的。最后，加上正向移动的当前值。

迷茫？别担心，我们有下面的例子。

第一次平滑的正向移动值= 75。

平滑正向移动值的平均值= 75/5 = 15。

当前正向移动= 30°(回想一下，这是第六个值)

因此，第二个平滑的真实范围值= 75 - (75/5) + 30 = 75 - 15 + 30 = 90。

让我们为以下内容创建表格:

| **日期** | **真实范围** | **DM 阳性** | **负 DM** | **平滑的正 DM** |
| 11/29/2019 | - | - | - | - |
| 12/2/2019 | Ten | five | Zero | - |
| 12/3/2019 | Eighteen | Ten | Zero | - |
| 12/4/2019 | Twenty-three | Fifteen | Zero | - |
| 12/5/2019 | Twenty-six | Twenty | Zero | - |
| 12/6/2019 | Thirty-two | Twenty-five | Zero | Seventy-five |
| 12/9/2019 | Thirty-eight | Thirty | Zero | Ninety |
| 12/10/2019 | forty-four | Thirty-five | Zero | One hundred and seven |
| 12/11/2019 | Forty-seven | Forty | Zero | One hundred and twenty-five point six |
| 12/12/2019 | Fifty-one | Forty-five | Zero | One hundred and forty-five point five |
| 12/13/2019 | Fifty-four | Fifty | Zero | One hundred and sixty-six point four |

我们注意到，由于负 DM 为 0，平滑后的负 DM 也为 0。

类似地，平滑的真实范围值被计算并填入下表:

| **日期** | **真实范围** | **阳性糖尿病** | **负 DM** | **平滑的正 DM** | **平滑负 DM** | **平滑后的真实范围** |
| 11/29/2019 | - | - | - | - | - | - |
| 12/2/2019 | Ten | five | Zero | - | - | - |
| 12/3/2019 | Eighteen | Ten | Zero | - | - | - |
| 12/4/2019 | Twenty-three | Fifteen | Zero | - | - | - |
| 12/5/2019 | Twenty-six | Twenty | Zero | - | - | - |
| 12/6/2019 | Thirty-two | Twenty-five | Zero | Seventy-five | Zero | One hundred and nine |
| 12/9/2019 | Thirty-eight | Thirty | Zero | Ninety | Zero | One hundred and twenty-five point two |
| 12/10/2019 | forty-four | Thirty-five | Zero | One hundred and seven | Zero | One hundred and forty-four point two |
| 12/11/2019 | Forty-seven | Forty | Zero | One hundred and twenty-five point six | Zero | One hundred and sixty-two point three |
| 12/12/2019 | Fifty-one | Forty-five | Zero | One hundred and forty-five point five | Zero | One hundred and eighty point nine |
| 12/13/2019 | Fifty-four | Fifty | Zero | One hundred and sixty-six point four | Zero | One hundred and ninety-eight point seven |

太好了！我们已经计算了相当多的变量。我们现在来看三位一体，正方向指数指标，负方向指数指标和最后一个 boss，即平均方向指数(ADX)指标。我们继续吧，好吗？

### 正向指标指示器和负向指标指示器

我们发现了平滑的正向运动和负向运动。就其本身而言，这两个指标的用途都有限。但是怀尔德同时使用了这两种信号，因此它们的交叉可以被归类为一种信号。

现在，由于每一个都可能有不同的幅度，我们通过除以真实范围并将其表示为百分比来对其进行归一化。

因此，对于正方向指示器，我们取平滑的正 DM ie 75 的值，并将其除以真实范围 70，得到值 75/70 = 1.07，作为百分比，它将是 107。

这里，我们应该注意，平滑的负 DM 总是 0，因此负方向指数指示器将是 0。

太好了！我们离这个故事的要点，即 ADX 指标，只有几步之遥了。

### ADX 指标:最终计算

记得我们说过 ADX 指标告诉我们趋势的强度，而不是方向。简单回顾一下情况，到目前为止，我们发现了正向指标和负向指标。这些会告诉我们趋势的方向。

但是，让我们退一步，看看我们是否能从指标中获得更多信息。我们需要检查的是这两个指标之间的差距，这将让我们对市场的表现有一个公平的想法。

如果我们有两个指标彼此接近的情况，那么这意味着可能有一个疲软的趋势，如果有的话。

但如果两者相差很大，就说明我们有很强的趋势。怀尔德通过给出方向指数(DX)指标的公式对此进行了量化。内容如下:

DX =(正负方向指标之差)/(正负方向指标之和)

因此，12 月 6 日的 DX 值为:

DX = (75 - 0) / (75 + 0) = 1。

因为我们用百分比表示它们，所以它将乘以 100 得到值:1 * 100 = 100。

现在，由于我们必须消除任何波动，我们采用 DX 的移动平均线来获得平均方向指数(ADX)指标。

因为我们将时间段设为 5，所以我们取这五个值的平均值。

因此，更新后的表格如下:

| **日期** | **真实范围** | **阳性糖尿病** | **负 DM** | **平滑的正 DM** | **平滑负 DM** | **平滑后的真实范围** | **正向指示灯** | **负方向指示灯** | **DX** | **ADX** |
| 11/29/2019 | - | - | - | - | - | - | - | - | - | - |
| 12/2/2019 | Ten | five | Zero | - | - | - | - | - | - | - |
| 12/3/2019 | Eighteen | Ten | Zero | - | - | - | - | - | - | - |
| 12/4/2019 | Twenty-three | Fifteen | Zero | - | - | - | - | - | - | - |
| 12/5/2019 | Twenty-six | Twenty | Zero | - | - | - | - | - | - | - |
| 12/6/2019 | Thirty-two | Twenty-five | Zero | Seventy-five | Zero | One hundred and nine | 68.80733945 | Zero | One hundred | - |
| 12/9/2019 | Thirty-eight | Thirty | Zero | Ninety | Zero | One hundred and twenty-five point two | 71.88498403 | Zero | One hundred | - |
| 12/10/2019 | forty-four | Thirty-five | Zero | One hundred and seven | Zero | One hundred and forty-four point two | 74.22308546 | Zero | One hundred | - |
| 12/11/2019 | Forty-seven | Forty | Zero | One hundred and twenty-five point six | Zero | One hundred and sixty-two point three | 77.37420531 | Zero | One hundred | - |
| 12/12/2019 | Fifty-one | Forty-five | Zero | One hundred and forty-five point five | Zero | One hundred and eighty point nine | 80.43684038 | Zero | One hundred | One hundred |
| 12/13/2019 | Fifty-four | Fifty | Zero | One hundred and sixty-six point four | Zero | One hundred and ninety-eight point seven | 83.74053399 | Zero | One hundred | One hundred |

由于该值为 100，我们可以说 ADX 指标呈现出非常强劲的趋势。这也可以通过上面显示的数据的蜡烛图直观地证实。

考虑到我们之前举了一个简单的例子，我们在下面添加了另一个表，该表给出了苹果的股价及其相应的 ADX 指标。

| **日期** | **真实范围** | **阳性糖尿病** | **负 DM** | **平滑后的真实范围** | **平滑的正 DM** | **平滑负 DM** | **正向指示灯** | **负方向指示灯** | **DX** | **ADX** |
| 2017-04-28 | One point zero three | Zero point one four | Zero | Six point one | One | Zero point three eight | Sixteen point four five | Six point two five | Forty-four point nine six | Thirty-two point three six |
| 2017-05-01 | Three point five five | Two point nine | Zero | Eight point four three | Three point seven | Zero point three | Forty-three point nine three | Three point six two | Eighty-four point seven nine | Forty-two point eight five |
| 2017-05-02 | One point five one | Zero | One point eight eight | Eight point two five | Two point nine six | Two point one two | Thirty-five point eight nine | Twenty-five point seven four | Sixteen point four eight | Thirty-seven point five seven |
| 2017-05-03 | Three point two four | Zero | Zero | Nine point eight four | Two point three seven | One point seven | Twenty-four point zero eight | Seventeen point two six | Sixteen point four eight | Thirty-three point three five |
| 2017-05-04 | One point three three | Zero | One point five four | Nine point two | One point nine | Two point nine | Twenty point six | Thirty-one point five | Twenty point nine three | Thirty point eight seven |
| 2017-05-05 | Two point four five | One point eight four | Zero | Nine point eight one | Three point three six | Two point three two | Thirty-four point two one | Twenty-three point six four | Eighteen point two seven | Twenty-eight point three five |
| 2017-05-08 | Four point seven four | Four point seven two | Zero | Twelve point five nine | Seven point four one | One point eight six | Fifty-eight point eight two | Fourteen point seven four | Fifty-nine point nine three | Thirty-four point six seven |
| 2017-05-09 | One point eight seven | Zero | Four point four two | Eleven point nine four | Five point nine two | Five point nine | Forty-nine point six one | Forty-nine point four four | Zero point one seven | Twenty-seven point seven seven |
| 2017-05-10 | One point eight eight | Zero | Zero | Eleven point four three | Four point seven four | Four point seven two | Forty-one point four five | Forty-one point three one | Zero point one seven | Twenty-two point two five |
| 2017-05-11 | One point seven six | Zero | Zero | Ten point nine one | Three point seven nine | Three point seven eight | Thirty-four point seven six | Thirty-four point six five | Zero point one seven | Seventeen point eight three |
| 2017-05-12 | Two point four seven | Zero | Two point three six | Eleven point two | Three point zero three | Five point three eight | Twenty-seven point zero nine | Forty-eight point zero eight | Twenty-seven point nine two | Nineteen point eight five |
| 2017-05-15 | One point six | Zero | Zero point three eight | Ten point five six | Two point four three | Four point six nine | Twenty-two point nine nine | Forty-four point three nine | Thirty-one point seven seven | Twenty-two point two three |
| 2017-05-16 | One point three four | Zero | Zero | Nine point seven nine | One point nine four | Three point seven five | Nineteen point eight four | Thirty-eight point three one | Thirty-one point seven seven | Twenty-four point one four |
| 2017-05-17 | Five point seven six | Zero | Zero | Thirteen point five nine | One point five five | Three | Eleven point four three | Twenty-two point zero seven | Thirty-one point seven seven | Twenty-five point six seven |
| 2017-05-18 | Three point zero nine | Zero | Zero | Thirteen point nine six | One point two four | Two point four | Eight point nine | Seventeen point one nine | Thirty-one point seven seven | Twenty-six point eight nine |
| 2017-05-19 | One point four four | Zero | One point five | Twelve point six one | Zero point nine nine | Three point four two | Seven point eight eight | Twenty-seven point one two | Fifty-four point nine six | Thirty-two point five |
| 2017-05-22 | One point six seven | Zero point six | Zero | Eleven point seven six | One point four | Two point seven four | Eleven point eight seven | Twenty-three point two seven | Thirty-two point four five | Thirty-two point four nine |
| 2017-05-23 | One point five nine | Zero | Zero point four | Eleven | One point one two | Two point five nine | Ten point one five | Twenty-three point five four | Thirty-nine point seven five | Thirty-three point nine four |
| 2017-05-24 | One point five | Zero | Zero | Ten point three | Zero point eight nine | Two point zero seven | Eight point six seven | Twenty point one one | Thirty-nine point seven five | Thirty-five point one |
| 2017-05-25 | One point three two | Zero | Zero | Nine point five six | Zero point seven one | One point six six | Seven point four seven | Seventeen point three three | Thirty-nine point seven five | Thirty-six point zero three |

![](img/209744c692be9407d44f57f0c78b6a27.png)

这里我们可以看到正方向指标多次从负方向指标下方穿过。但是，正如我们上面提到的，我们也检查 ADX 指标水平来确定趋势的强度。

让我们举几个例子，我们可以使用 ADX 指标作为交易策略的一部分。

## ![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")使用 Python 使用 ADX 指标交易策略

前面，我们看到了使用简单的表格查找 ADX 指标的过程。现在，为了处理真实世界的数据，我们将借助 Python 来简化工作。

我们将通过以下方式从 yahoo finance 获取数据。

```py
import yfinance as yf
aapl = yf.download('AAPL', '2017-1-1','2019-12-18')
```

我们随机选取了苹果公司的股票，从 2017 年 1 月 1 日到 2018 年 12 月 18 日。我们将在下面的代码中使用调整后的值。

```py
aapl['Adj Open'] = aapl.Open * aapl['Adj Close']/aapl['Close']
aapl['Adj High'] = aapl.High * aapl['Adj Close']/aapl['Close']
aapl['Adj Low'] = aapl.Low * aapl['Adj Close']/aapl['Close']
aapl.dropna(inplace=True)
```

您可以使用以下代码在 Python 中轻松计算 ADX 指标

```py
from ta.trend import ADXIndicator
adxI = ADXIndicator(aapl['Adj High'],aapl['Adj Low'],aapl['Adj Close'],14,False)
aapl['pos_directional_indicator'] = adxI.adx_pos()
aapl['neg_directional_indicator'] = adxI.adx_neg()
aapl['adx'] = adxI.adx()
aapl.tail()
```

输出如下所示:

| **日期** | **打开** | **高** | **低** | **关闭** | **调整关闭** | **体积** | **可调开启** | **可调高** | **调整低电平** | **位置 _ 方向 _ 指示器** | **负方向指示器** | **adx** |
| **2019 年 12 月 11 日** | Two hundred and sixty-nine | Two hundred and seventy-one | Two hundred and sixty-nine | Two hundred and seventy-one | Two hundred and seventy-one | Nineteen million six hundred and eighty-nine thousand two hundred | Two hundred and sixty-nine | Two hundred and seventy-one | Two hundred and sixty-nine | Thirty-one | Twenty-one | Twenty-six |
| **2019 年 12 月 12 日** | Two hundred and sixty-eight | Two hundred and seventy-three | Two hundred and sixty-seven | Two hundred and seventy-one | Two hundred and seventy-one | Thirty-four million three hundred and twenty-seven thousand six hundred | Two hundred and sixty-eight | Two hundred and seventy-three | Two hundred and sixty-seven | Thirty-one | Nineteen | Twenty-six |
| **2019 年 12 月 13 日** | Two hundred and seventy-one | Two hundred and seventy-five | Two hundred and seventy-one | Two hundred and seventy-five | Two hundred and seventy-five | Thirty-three million three hundred and ninety-six thousand nine hundred | Two hundred and seventy-one | Two hundred and seventy-five | Two hundred and seventy-one | Thirty-three | Eighteen | Twenty-six |
| **2019 年 12 月 16 日** | Two hundred and seventy-seven | Two hundred and eighty-one | Two hundred and seventy-seven | Two hundred and eighty | Two hundred and eighty | Thirty-two million forty-six thousand five hundred | Two hundred and seventy-seven | Two hundred and eighty-one | Two hundred and seventy-seven | Thirty-nine | Sixteen | Twenty-eight |
| **2019 年 12 月 17 日** | Two hundred and eighty | Two hundred and eighty-two | Two hundred and seventy-nine | Two hundred and eighty | Two hundred and eighty | Twenty-eight million five hundred and thirty-nine thousand six hundred | Two hundred and eighty | Two hundred and eighty-two | Two hundred and seventy-nine | Thirty-nine | Fifteen | Twenty-nine |

在 Python 中，我们使用“matplotlib”库以下列方式绘制图形:

```py
import matplotlib.pyplot as plt
def plot_graph(data,ylabel,xlabel):
plt.figure(figsize=(10,7))
plt.grid()
plt.plot(data)
plt.ylabel(ylabel)
plt.xlabel(xlabel)
plot_graph(aapl['Adj Close'], 'Price', 'Date')
plot_graph(aapl['adx'], 'Price', 'Date')
```

输出如下所示:

![](img/6e95b0b5d0a614fc9d461030d66b1a49.png)

![](img/77d9f890367a636178116a59d26cf8c6.png)

通过这种方式，我们可以比较 ADX 指标和价格，并制定您的交易策略。

但是看起来很混乱！

别担心，我们会掩护你的。在下面的代码中，我们将绘制价格数据，并突出显示 ADX 指标高于 25 的部分，这表明趋势强劲。

```py
aapl['trend'] = np.where(aapl.adx>25,aapl['Adj Close'],np.nan)

aapl['trend_signal'] = np.where(aapl.adx>25,1,0)
plt.figure(figsize=(10,7))
plt.grid()
plt.plot(aapl['Adj Close'])
plt.plot(aapl['trend'])
plt.ylabel('Price')
plt.xlabel('Date')
```

![](img/04f9a9773217bff203261feee84a899a.png)

As we had mentioned earlier, The ADX indicator tells us the strength of the trend and not the direction. Thus, if we take the example of the data from Oct 2018 to Jan 1, 2019, the ADX indicator has highlighted the price data signifying that there is a strong trend present. Further, when we see the price chart, we can see it is a downtrend and can take a short position.

但我们看到从 2019 年 1 月开始的数据，直到 2019 年 5 月，价格上涨，ADX 指标高于 25，表明上涨趋势，我们可以将此作为做多的信号。

如果我们使用 ADX 指标作为交易策略，回报将按以下方式绘制。

```py
aapl['direction'] = np.where(aapl.pos_directional_indicator>aapl.neg_directional_indicator,1,-1) * aapl['trend_signal']
aapl['daily_returns'] = aapl['Adj Close'].pct_change()
aapl['strategy_returns'] = aapl.daily_returns.shift(-1) * aapl.direction
plot_graph((aapl['strategy_returns']+1).cumprod(), 'Returns', 'Date')
```

![](img/de43e9bc888d57226709c581ade4e6ab.png)

这些只是我们在交易策略中使用方向指标和 ADX 指标的几种方法。当然，没有一个指标是完美的，总是建议和其他[指标](https://blog.quantinsti.com/indicators-build-trend-following-strategy/)一起使用，来确认你的行动。

## 结论

我们今天已经走了很长的路，从理解 ADX 指标的计算以及实现它的 python 代码，到在您的交易策略中使用该指标。我们也知道 ADX 指标执行起来相对简单，有助于我们识别市场中的强劲[趋势](https://blog.quantinsti.com/indicators-build-trend-following-strategy/)。虽然它有自己的局限性，但将它与其他指标结合起来，将会产生强大的交易策略。

如果你想学习算法交易和自动交易系统的各个方面，那就去查查[算法交易(EPAT )](https://www.quantinsti.com/epat/) 的高管课程。课程涵盖统计学&计量经济学、金融计算&技术和算法&定量交易等培训模块。EPAT 教你在算法交易中建立一个有前途的职业所需的技能。[现在报名](https://www.quantinsti.com/epat/)！

*免责声明:本文中提供的所有数据和信息仅供参考。QuantInsti 对本文中任何信息的准确性、完整性、现时性、适用性或有效性不做任何陈述，也不对这些信息中的任何错误、遗漏或延迟或因其显示或使用而导致的任何损失、伤害或损害承担任何责任。所有信息均按原样提供。*
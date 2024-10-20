# 抛物面合成孔径雷达-简介

> 原文：<https://blog.quantinsti.com/parabolic-sar/>

由[维布·辛格](https://www.linkedin.com/in/vibhu-singh-1b76b6105/)

在市场中，发现趋势是至关重要的，但发现趋势何时结束也同样重要。退出交易比进入交易更难。在这篇博客中，我们将讨论一个这样的技术指标，抛物线 SAR 指标，它有助于确定趋势何时结束。

抛物线 SAR 或抛物线停止和反转是由 J. Welles Wilder 开发的。抛物线 SAR 被交易者用来预测资产的方向，并帮助确定进场点和出场点。在本文中，我们将讨论以下几点:

*   [抛物线 SAR 计算](#calculation)
*   [如何用抛物线 SAR 交易](#trade)
*   [Python 中抛物线 SAR 的交易策略](#strategy)
*   [抛物面 SAR 的利与弊](#pros)

抛物线 SAR 显示为价格标记上方或下方的一系列点，如图所示。

![](img/6965b7667f4f6c46554d47d210497b50.png)

价格水平上方的点被认为是下降趋势。相反，低于价格水平的点被认为是上升趋势。圆点方向的变化表明价格方向的潜在变化。例如，你可以在开始时观察到这些点低于价格水平。当它在价格上方翻转时，它可能是价格进一步下跌的信号。当价格和点之间有很大的差距时，趋势是强劲的，你可以在图表的末尾观察到。在横盘行情中，价格和点之间频繁互动。

## 抛物线 SAR 计算

抛物线 SAR (PSAR)指示器使用:

1.  当前趋势中的最高价和最低价
2.  加速系数:加速系数决定了抛物线 SAR 的灵敏度。

### 默认设置

AF 从 0.02 开始，每次极值点产生新的高/低时增加 0.02。AF 最大可达 0.2，无论趋势延续多久。

增加步长和最大步长的值会增加指示器的灵敏度，但会降低其准确性。降低步长和最大步长的值会降低指示器的灵敏度，但会提高其精度。我们需要在这两个值之间找到一个平衡点，以产生高质量的信号。在我们的策略中，我们将使用(0.02，0.2)的值

### 上升抛物面 SAR 的计算

当前 SAR =先前 SAR +先前 AF(先前 EP -先前 SAR)

其中，
前期 SAR =前期 SAR 值
EP =当前上升趋势的最高高点
AF =加速因子

### 下落抛物面 SAR 的计算

当前 SAR =先前 SAR -先前 AF(先前 SAR -先前 EP)

其中，
前期 SAR =前期 SAR 值
EP =当前下跌趋势的最低低点
AF =加速因子

在我们的策略中，我们将使用 TA-Lib 库(技术指标的 Python 库)来直接计算抛物线 SAR 值。

## 如何用抛物线 SAR 交易

### 趋势市场

抛物线 SAR 最好在市场趋势时使用；这是当市场在两个方向上都有长时间的反弹，并且有小幅度的修正。建议不要在横盘时用抛物线 SAR 交易。

### 更高的时间框架

如果时间范围很小，抛物面 SAR 将产生太多的信号，并可能提供相互矛盾的信号。在更高的时间框架内，交易将缓慢进行，这将避免错误信号，因为大部分市场噪音已经消除。

### 最好用作退出指示器

抛物线 SAR 主要用作出口指示器。当价格低于抛物线 SAR 时平仓买入，当价格高于抛物线 SAR 时平仓卖出。它还提供了一个止损水平，无论市场方向如何，止损水平都会向市场价格靠拢。

### 将抛物线 SAR 与其他指标相结合

抛物线 SAR 是一个滞后指标，因为它跟随价格，在其他指标的帮助下，我们将能够产生高质量的信号。可以和很多指标结合。但是，需要注意的是，抛物线 SAR 的作用是确定趋势的方向和改变趋势的方向。将抛物线 SAR 与另一个趋势跟踪指标相结合并没有多大用处，因为它将提供两个趋势确认信号。在策略中，我们将 Ichimoku 指标与抛物线 SAR 一起使用。想了解更多关于 Ichimoku cloud 的内容，可以参考这个[链接](https://blog.quantinsti.com/ichimoku-cloud-trading-strategy/)。抛物线 SAR 可用于确定最佳进入和退出点，Ichimoku 云提供当前和未来潜在的支持和阻力点。

## Python 中抛物线 SAR 的交易策略

既然你对抛物面 SAR 有了了解。让我们用 Python 实现交易策略。

### 输入数据

导入 2014 年 1 月 1 日至 2019 年 10 月 1 日的亚马逊(AMZN)数据。数据从雅虎财经导入。

In [2]:

```py
# Import pandas
import pandas as pd
# Import yfinance
import yfinance as yf
# Import data from yahoo finance
data = yf.download(tickers='AMZN', start='2014-01-01', end='2019-10-01')
# Drop the NaN values
data = data.dropna()
data.head()

```

```py
[*********************100%***********************] 1 of 1 downloaded

```

Out[2]:

| 日期 | 打开 | 高的 | 低的 | 关闭 | 接近的 | 卷 |
| --- | --- | --- | --- | --- | --- | --- |
| 2013-12-31 | Three hundred and ninety-four point five eight | Three hundred and ninety-eight point eight three | Three hundred and ninety-three point eight | Three hundred and ninety-eight point seven nine | Three hundred and ninety-eight point seven nine | One million nine hundred and ninety-six thousand five hundred |
| 2014-01-02 | Three hundred and ninety-eight point eight | Three hundred and ninety-nine point three six | Three hundred and ninety-four point zero two | Three hundred and ninety-seven point nine seven | Three hundred and ninety-seven point nine seven | Two million one hundred and thirty-seven thousand eight hundred |
| 2014-01-03 | Three hundred and ninety-eight point two nine | Four hundred and two point seven one | Three hundred and ninety-six point two two | Three hundred and ninety-six point four four | Three hundred and ninety-six point four four | Two million two hundred and ten thousand two hundred |
| 2014-01-06 | Three hundred and ninety-five point eight five | Three hundred and ninety-seven | Three hundred and eighty-eight point four two | Three hundred and ninety-three point six three | Three hundred and ninety-three point six three | Three million one hundred and seventy thousand six hundred |
| 2014-01-07 | Three hundred and ninety-five point zero four | Three hundred and ninety-eight point four seven | Three hundred and ninety-four point two nine | Three hundred and ninety-eight point zero three | Three hundred and ninety-eight point zero three | One million nine hundred and sixteen thousand |

In [4]:

```py
# Import matplotlib
import matplotlib.pyplot as plt
plt.style.use('fast')
# Plot the closing price
data.Close.plot(figsize=(10,5))
plt.grid()
plt.show()

```

![](img/ba3bf31edc7d24eb3cff801446d209e2.png)

### 抛物面 SAR

使用 Ta-Lib 库中的`SAR`函数计算抛物线。输入参数是高价、低价、加速系数(AF)和最大步长。

正如已经讨论过的，每当极值点形成一个新的高点/低点，加速因子增加 0.02，它可以达到 0.2 的最大值，不管上升趋势/下降趋势持续多长时间。

In [5]:

```py
# Import talib
import talib
# Calculate parabolic sar
data['SAR'] = talib.SAR(data.High, data.Low, acceleration=0.02, maximum=0.2)

```

In [6]:

```py
# Plot Parabolic SAR with close price
data[['Close', 'SAR']][:500].plot(figsize=(10,5))
plt.grid()
plt.show()

```

![](img/1b244a5b33908a4bb9603456144d75f0.png)

### 市云

市云，也称为市云 Kino Hyo，由五个地块和一片云组成。

Ichimoku Cloud 的默认参数是 9，26，52，26。

1.  Tenkan-sen(转换线):(9 期高+ 9 期低)/2
2.  Kijun-sen(底线):(26 期高点+ 26 期低点)/2
3.  森口跨度 A(领先跨度 A): (Tenkan-sen + Kijun-sen)/2
4.  森口跨度 B(领先跨度 B): (52 期高+ 52 期低)/2
5.  池口跨度(滞后跨度):过去 26 天的收盘图

In [7]:

```py
# Calculate Tenkan-sen
high_9 = data.High.rolling(9).max()
low_9 = data.Low.rolling(9).min()
data['tenkan_sen_line'] = (high_9 + low_9) /2
# Calculate Kijun-sen
high_26 = data.High.rolling(26).max()
low_26 = data.Low.rolling(26).min()
data['kijun_sen_line'] = (high_26 + low_26) / 2
# Calculate Senkou Span A
data['senkou_spna_A'] = ((data.tenkan_sen_line + data.kijun_sen_line) / 2).shift(26)
# Calculate Senkou Span B
high_52 = data.High.rolling(52).max()
low_52 = data.High.rolling(52).min()
data['senkou_spna_B'] = ((high_52 + low_52) / 2).shift(26)
# Calculate Chikou Span B
data['chikou_span'] = data.Close.shift(-26)

```

In [8]:

```py
data.head()

```

Out[8]:

| 日期 | 打开 | 高的 | 低的 | 关闭 | 接近的 | 卷 | 特别行政区 | tenkan_sen_line | kijun_sen_line | (西班牙语) | 森口 | 赤口 _span |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 2013-12-31 | Three hundred and ninety-four point five eight | Three hundred and ninety-eight point eight three | Three hundred and ninety-three point eight | Three hundred and ninety-eight point seven nine | Three hundred and ninety-eight point seven nine | One million nine hundred and ninety-six thousand five hundred | 圆盘烤饼 | 圆盘烤饼 | 圆盘烤饼 | 圆盘烤饼 | 圆盘烤饼 | Three hundred and sixty-one point zero eight |
| 2014-01-02 | Three hundred and ninety-eight point eight | Three hundred and ninety-nine point three six | Three hundred and ninety-four point zero two | Three hundred and ninety-seven point nine seven | Three hundred and ninety-seven point nine seven | Two million one hundred and thirty-seven thousand eight hundred | 393.8000 | 圆盘烤饼 | 圆盘烤饼 | 圆盘烤饼 | 圆盘烤饼 | Three hundred and sixty point eight seven |
| 2014-01-03 | Three hundred and ninety-eight point two nine | Four hundred and two point seven one | Three hundred and ninety-six point two two | Three hundred and ninety-six point four four | Three hundred and ninety-six point four four | Two million two hundred and ten thousand two hundred | 393.9112 | 圆盘烤饼 | 圆盘烤饼 | 圆盘烤饼 | 圆盘烤饼 | Three hundred and sixty-one point seven nine |
| 2014-01-06 | Three hundred and ninety-five point eight five | Three hundred and ninety-seven | Three hundred and eighty-eight point four two | Three hundred and ninety-three point six three | Three hundred and ninety-three point six three | Three million one hundred and seventy thousand six hundred | 402.7100 | 圆盘烤饼 | 圆盘烤饼 | 圆盘烤饼 | 圆盘烤饼 | Three hundred and forty-nine point two five |
| 2014-01-07 | Three hundred and ninety-five point zero four | Three hundred and ninety-eight point four seven | Three hundred and ninety-four point two nine | Three hundred and ninety-eight point zero three | Three hundred and ninety-eight point zero three | One million nine hundred and sixteen thousand | 402.7100 | 圆盘烤饼 | 圆盘烤饼 | 圆盘烤饼 | 圆盘烤饼 | Three hundred and fifty-seven point two |

### Plot komu Cloud

Komu 云是在森口跨度 A 和寇森跨度 b 之间的空间。云的边缘提供了潜在的当前和未来的支持和阻力点。我们用收盘价和抛物线 SAR 来绘制 komu cloud。当先科跨度 A 大于先科跨度 B 时，我们用浅绿色绘制云。当先科跨度 B 大于先科跨度 A 时，我们用浅珊瑚色绘制云

In [9]:

```py
# Plot closing price and parabolic SAR
komu_cloud = data[['Close','SAR']][:500].plot(figsize=(12, 7))
# Plot Komu cloud
komu_cloud.fill_between(data.index[:500], data.senkou_spna_A[:500], data.senkou_spna_B[:500],
 where=data.senkou_spna_A[:500] >= data.senkou_spna_B[:500], color='lightgreen')
komu_cloud.fill_between(data.index[:500], data.senkou_spna_A[:500], data.senkou_spna_B[:500],
 where=data.senkou_spna_A[:500] < data.senkou_spna_B[:500], color='lightcoral')
plt.grid()
plt.legend()
plt.show()

```

![](img/739ee713cb6810d17ead1dd87c8a8605.png)

### 购买信号

当价格高于 Komu 云，抛物线 SAR 低于价格时，我们买入。

In [10]:

```py
data['signal'] = 0
data.loc[(data.Close > data.senkou_spna_A) & (data.Close >
 data.senkou_spna_B) & (data.Close > data.SAR), 'signal'] = 1

```

### 卖出信号

当价格低于 Komu 云，抛物线 SAR 高于价格时，我们卖出。

In [11]:

```py
data.loc[(data.Close < data.senkou_spna_A) & (data.Close <
 data.senkou_spna_B) & (data.Close < data.SAR), 'signal'] = -1

```

In [12]:

```py
data['signal'].value_counts()

```

Out[12]:

```py
 0 1037
 1 270
-1 140
Name: signal, dtype: int64
```

### 计算策略回报

我们计算每日收益。然后，我们通过将每日回报乘以前一天的信号来计算策略回报。此外，我们还计算了策略收益的累积积。

In [13]:

```py
# Calculate daily returns
daily_returns = data.Close.pct_change()
# Calculate strategy returns
strategy_returns = daily_returns *data['signal'].shift(1)

```

In [14]:

```py
# Calculate cumulative returns
(strategy_returns+1).cumprod().plot(figsize=(10,5))
# Plot the strategy returns
plt.xlabel('Date')
plt.ylabel('Strategy Returns (%)')
plt.grid()
plt.show()

```

![](img/08bd63f7a3563b71fa174ceb8e77720f.png)

### 交易策略概要

这是一个基于抛物线 SAR 和 Ichimoku 云的简单策略。然而，它能产生超过 5 年的良好回报。但是在后验测试中你需要注意一些事情，比如止损，滑点。现在轮到您调整代码，使其更接近真实环境。

## 抛物面 SAR 的利与弊

抛物线 SAR 的优点是它在市场趋势强劲时最有效。此外，与其他[趋势指标](https://blog.quantinsti.com/indicators-build-trend-following-strategy/)相比，它提供了更好的退出信号。主要的缺点是，当没有趋势或市场起伏不定时，抛物线 SAR 的虚线会在价格上方或下方连续回转。这通常会导致错误的信号。

## 结论

这样，我们已经看到了如何计算抛物线 SAR 以及它在交易中的应用。我们也了解了抛物线 SAR 指示器的优点和缺点

请在下面的评论中告诉我们你是否喜欢这篇文章和任何其他反馈。

您可以通过注册 Quantra 上的量化交易策略和模型课程，了解更多关于技术指标的信息，并建立自己的交易策略。

如果你想学习算法交易的各个方面，那么看看我们在算法交易 (EPAT)的[执行项目。课程涵盖统计学&计量经济学、金融计算&技术和算法&定量交易等培训模块。EPAT 旨在让你具备成为成功交易者的正确技能。立即注册！](https://www.quantinsti.com/)

*免责声明:本文中提供的所有数据和信息仅供参考。QuantInsti 对本文中任何信息的准确性、完整性、现时性、适用性或有效性不做任何陈述，也不对这些信息中的任何错误、遗漏或延迟或因其显示或使用而导致的任何损失、伤害或损害承担任何责任。所有信息均按原样提供。*

**文件下载中:**抛物线 SAR Python 代码
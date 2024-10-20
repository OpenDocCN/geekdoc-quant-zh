# 交易选项:Python 中的铁秃鹰交易策略

> 原文：<https://blog.quantinsti.com/iron-condor-options-trading-strategy/>

![Trading Options Iron Condor Trading Strategy In Python](img/70a27132566b013eb260db96a7c8f68f.png)

由尼廷·塔帕尔

### **简介**

我一直在试图涵盖一些最简单的期权策略，包括期权扼杀策略和看涨期权价差策略，这些策略对于期权新手来说很容易实施。如果你是期权交易的新手，那么你可以查看 Quantra 上的[虚拟期权交易](https://quantra.quantinsti.com/course/options-trading-strategies-python-basic)免费课程。这一次我将涵盖铁秃鹰交易策略。

任何进行期权交易的人都很清楚，他们一直在和时间衰减做斗争，尤其是当你是买方的时候。许多正在实施的策略都是为了让时间因素为他们服务而设计的，而不是相反。“铁秃鹰”就是这样一种策略，它可以让时间衰减对你有利。

### **什么是铁鹰交易策略？**

铁鹰策略是最简单的策略之一，即使是小账户交易者也可以采用。对于熟悉其他[基本期权交易策略](https://blog.quantinsti.com/basics-options-trading/)的人来说，铁神鹰策略基本上是牛看跌价差和熊看涨价差期权交易策略的组合。

对于不了解上述策略的人来说，另一个更简单的解释是，Iron Condor strategy 是一种四足交易，它以卖出相同基础证券和到期日的价外看跌期权和价外看涨期权开始。交易者希望股票价格在到期时保持在这些位置之间。但做空期权可能涉及很多风险，任何不利的情况都可能导致巨大的损失。因此，为了保护这种风险，交易者进一步买入价外看跌期权，这四种期权统称为铁鹰策略。

重要的是要明白，铁秃鹰战略是一个有限的风险策略，在稳定的市场，低波动性，可以帮助交易者赚取有限的利润。

#### **策略特征**

**期权的价格:**

卖出 1 份 OTM 看跌期权(较高的执行价格)卖出 1 份 OTM 看涨期权(较低的执行价格)买入 1 份 OTM 看跌期权(较低的执行价格)买入 1 份 OTM 看涨期权(较高的执行价格)

**最大利润**:收到的净保费

**最大损失**:

看涨期权的执行价格-看跌期权的执行价格-收到的净溢价或看跌期权的执行价格-看跌期权的执行价格-收到的净溢价，以较高者为准

**盈亏平衡:**

上侧:卖空看涨期权的执行价格+收到的净溢价下侧:卖空看跌期权的执行价格-收到的净溢价

#### 这个策略是如何运作的？

让我们假设一只股票 ABC 的交易价格是 100 印度卢比，为了执行一个铁鹰交易策略，我们将:卖出 80 印度卢比 2.5 的执行卖出 120 印度卢比 2.5 的执行买入

希望价格保持在我们预定的这两个执行价格范围内，这样我们就能获利。但是，由于无限损失的风险，我们将通过以下方式保护我们的头寸:买入 60 印度卢比看跌期权，买入 140 印度卢比看跌期权

![Call Strike and Put](img/97f981e3cfd8451c018a36190a54151b.png)

这四个位置将共同构成我们的铁鹰:

![Formation of Iron Condor](img/96b8010cbc23c36e48c9fff7654ae17c.png)

#### **如何实施这一战略？**

让我们看看如何在真实的市场场景中执行这一策略。

为此，我将选择 Yes Bank Limited(股票代号:Yes Bank)的期权，到期日为 2018 年 3 月 28 日，当前股价为 323.40 印度卢比

过去 1 个月的股价走势(来源——谷歌财经)

![1-month stock price movement](img/84140487ac09b12f50277cbf53aeafa4.png)

以下是 YESBANK 截止日期为 2018 年 3 月 28 日的期权链。

![Option Chain](img/0600d50efd861f3a9db3cf249c31e375.png)

我将持有以下头寸:以印度卢比 3.30 卖出 350 看涨期权，以印度卢比 3.40 卖出 300 看跌期权，以印度卢比 1.30 买入 370 看涨期权，以印度卢比 1.20 买入 280 看跌期权

![Call Options](img/5b1822a5bd3ee2c88989121b165b5818.png)

![Put Options](img/b36311aea4fbf661ff6dd745c6c2b46e.png)

资料来源:nseindia.com

##### **最大利润:**

以防股票反弹不多，停留在我的预定头寸之间，即价格在 300 印度卢比和 350 印度卢比之间。我的收益如下:

![Max Profit](img/77ad73c28812c4351e6d82fdf83e203c.png)

因此，我们通过出售期权在最初的头寸上赚了钱，但在我们为了保护而预订的头寸上却亏损了。总收益是 4.2 个点。

##### **最大损失:**

让我们假设有一个重大的波动或市场颠簸，由于一个不确定的事件，使股票上升到印度卢比 390。所以这意味着我们的多头和空头头寸是亏本的。这是这种情况下的回报:

![Max Loss](img/fcc410438d9d1034dcb7fd1d914e6fea.png)

我们在短推时赚了 3.4 卢比，在长推时损失了 1.2 卢比。短期看涨期权价值 40 点，因此我们亏损了 36.7 印度卢比(3.30-40)，长期看涨期权价值 20 点，使我们亏损了 18.7 印度卢比(20-1.30)。总计我们损失了 15.8 卢比。记住，我们买入的多头看涨期权帮助我们将总交易的损失最小化。

另一个需要注意的重要事情是，无论股票涨跌，这都是我们在这笔交易中的最大损失。

现在让我们看看一系列潜在价格的收益:

![Payoff chart](img/9f1c075c0888029e878444c72f66f659.png)

**我们现在将使用 [Python 代码](https://quantra.quantinsti.com/course/options-trading-strategies-python-basic)向您展示收益汇总:**

### **导入库**

```py
import numpy as np
import matplotlib.pyplot as plt
import seaborn
```

#### **电话支付**

```py
def call_payoff(sT, strike_price, premium):
return np.where(sT > strike_price, sT - strike_price, 0) – premium
# Stock price
spot_price = 323.40
# Long call
strike_price_long_call = 370
premium_long_call = 1.30
# Short call
strike_price_short_call = 350
premium_short_call = 3.30
# Stock price range at expiration of the call
sT = np.arange(0.5*spot_price,2*spot_price,1)

payoff_long_call = call_payoff(sT, strike_price_long_call, premium_long_call)

fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT,payoff_long_call,label='Long 370 Strike Call',color='g')
plt.xlabel('Stock Price')
plt.ylabel('Profit and loss')
plt.legend()
#ax.spines['top'].set_visible(False) # Top border removed
#ax.spines['right'].set_visible(False) # Right border removed
#ax.tick_params(top=False, right=False) # Removes the tick-marks on the RHS
plt.grid()
plt.show()
```

![Strike Call](img/2ac98a8a2c6ef044272bb167469edc4f.png)

```py
payoff_short_call = call_payoff(sT, strike_price_short_call, premium_short_call) * -1.0

fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT,payoff_short_call,label='Short 350 Strike Call',color='r')
plt.xlabel('Stock Price')
plt.ylabel('Profit and loss')
plt.legend()
plt.grid()
plt.show()
```

![Strike Call](img/d5337186fe1c80df3c5cb007a54a348a.png)

#### **放收益**

```py
def put_payoff(sT, strike_price, premium):
return np.where(sT < strike_price, strike_price - sT, 0) – premium
# Stock price
spot_price = 323.40
# Long put
strike_price_long_put = 280
premium_long_put = 1.20
# Short put
strike_price_short_put = 300
premium_short_put = 3.40
# Stock price range at expiration of the put
sT = np.arange(0.5*spot_price,2*spot_price,1)

payoff_long_put = put_payoff(sT, strike_price_long_put, premium_long_put)

fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT,payoff_long_put,label='Long 280 Strike Put',color='y')
plt.xlabel('Stock Price')
plt.ylabel('Profit and loss')
plt.legend()
plt.grid()
plt.show()
```

![Short Put](img/4c7614821a535620c529a9e6b631bc6d.png)

```py
payoff_short_put = put_payoff(sT, strike_price_short_put, premium_short_put) * -1.0

fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT,payoff_short_put,label='Short 300 Strike Put',color='m')
plt.xlabel('Stock Price')
plt.ylabel('Profit and loss')
plt.legend()
plt.grid()
plt.show()
```

![Strike Put](img/70a385a1dfe1e5b08645fb69167d3267.png)

#### **铁血秃鹰战略成效**

```py
payoff = payoff_long_call + payoff_short_call + payoff_long_put + payoff_short_put

fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT,payoff_long_call,'--',label='Long 370 Strike Call',color='g')
ax.plot(sT,payoff_short_call,'--',label='Short 350 Strike Call',color='r')
ax.plot(sT,payoff_long_put,'--',label='Long 280 Strike Put',color='y')
ax.plot(sT,payoff_short_put,'--',label='Short 300 Strike Put',color='m')
ax.plot(sT,payoff,label='Iron Condor')
plt.xlabel('Stock Price')
plt.ylabel('Profit and loss')
plt.legend()
plt.grid()
plt.show()
```

![Iron Condor](img/093f4c75dfec1de98ef8e27d6a31ee4d.png)

### **下一步**

使用 Black Scholes 期权定价模型学习[期权定价的建模，并为各种期权的组合绘制相同的图。您可以在该模型中放入任意数量的看涨和/或看跌期权，并使用内置宏(名为“BS”)来计算每个期权的基于 BS 模型的期权定价。](https://blog.quantinsti.com/options-trading-excel-model/)

***更新:**我们注意到一些用户在从雅虎和谷歌金融平台下载市场数据时面临挑战。如果你正在寻找市场数据的替代来源，你可以使用 [Quandl](https://www.quandl.com/) 来获得同样的信息。*

*免责声明:股票市场的所有投资和交易都有风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。*

### **下载 Python 代码**

*   铁秃鹰交易策略 Python 代码文件
# 看涨期权传播策略

> 原文：<https://blog.quantinsti.com/bull-call-spread-strategy/>

![Bull Call Spread Strategy Preview](img/2ed4209067320f1becd93358312dea47.png)

由尼廷·塔帕尔

### **简介**

在我的上一篇博客中，我解释了[扼杀策略](https://blog.quantinsti.com/long-strangle-option-strategy-in-python/)是如何运作的。这一次，我将带您了解看涨期权的传播策略。这种策略在新手交易者中很受欢迎，因为它简单易行，风险有限，但如果你选择了正确的机会，就有很大的潜力获得可观的投资回报。

这种策略是希望最小化风险并获得适度投资回报的交易者的首选。

### **什么是看涨期权传播策略？**

看涨期权价差策略包括相同基础证券的[期权](http://s.bl-1.com/h/cgFQDB8B?url=https://quantra.quantinsti.com/course/options-trading-strategies-python-basic)，到期日相同，但执行价格不同。因此，这种战略也被称为**【垂直传播】**。

### **战略亮点**

**期权的价格:**

1.  购买 1 OTM 罢工呼吁
2.  卖出 1 个 OTM 买入期权

**最大利润:**短期看涨期权的执行价格-长期看涨期权的执行价格-已支付的净溢价

**最大损失:**已付净保费

**盈亏平衡:**看涨期权的执行价格+已支付的净溢价

### **如何实施这一战略？**

让我们通过一个例子来学习这个策略。如果印孚瑟斯有限公司(INFY)的股票交易价格为 1130 印度卢比，作为一名交易员，如果我预计印孚瑟斯有限公司在 2018 年 3 月 28 日到期日将小幅上涨至 1200 印度卢比，那么，为了从这一观点中获利，我将购买 20 印度卢比的 1160 印度卢比执行看涨期权。

![Infy Option Chain](img/26a3f66611a9d50148eee203a4e84edc.png)

资料来源:nseindia.com

如果我的观点是正确的，股票涨到 1200 印度卢比，那么 1160 执行看涨期权将会获利 40 点，扣除溢价后，净利润大约为 20 印度卢比，但是如果我的观点是错误的，那么我将失去 20 印度卢比的溢价。为了区区 10 卢比的奖励而冒 20 卢比的风险，看起来并不是正确的做法。

这就是看涨期权价差策略发挥作用的时候了。为了提高我的风险回报比，我可以做的是，除了以 20 印度卢比购买 1160 执行看涨期权，我还可以卖出 1200 印度卢比执行看涨期权，并收取 11 印度卢比的溢价。

*   购买 1160 罢工电话@ 20
*   卖 1200 打电话@ 11

![Buy and Sell](img/f039ccdb6d3fcdc241e274ddc6d2b3e8.png)

资料来源:nseindia.com

这使得净应付溢价为 9 印度卢比，这仅仅是为长期看涨期权支付的溢价和从短期看涨期权收取的溢价之间的差额。

根据我的观点，如果 INFY 股票在到期日达到 1200 印度卢比，那么 1160 执行看涨期权的价格为 40 点，1200 执行看涨期权没有价值，在扣除 9 印度卢比的净溢价后，净利润为 31 印度卢比。

考虑不同的情况，如果 INFY 保持在 1160 的长期看涨期权执行价格以下。我们已经知道，如果期权在到期日没有价值，那么期权到期时就没有价值了。因此，执行价格为 1160 和 1200 的看涨期权都是无价值的，到期时一文不值。我将损失 20 印度卢比，即为 1160 罢工看涨期权支付的溢价，但从 1200 罢工看跌期权收取的溢价为 11 印度卢比。所以净损失是 9 卢比。

现在，如果 INFY 股票价格在到期日结束于 1160，多头看涨期权执行价格和 1200，空头看涨期权执行价格之间。那么，1200 执行看涨期权就不赚钱，没有价值，而 1160 执行看涨期权是赚钱的，值 INFY 股价和 1160 之间的差价。

这是我对 INFY 股票价格变化的收益的简单表示:

![Payoff Chart](img/ff40c5cf6a08f0f08f90bb5c52024e53.png)

*   LS–IV–下限–内在价值(1160 CE)
*   PP–已付保费
*   LS 收益–较低的罢工收益
*   HS-IV–更高的冲击–内在价值(1200 CE)
*   PR-收到的溢价
*   HS 回报–更高的罢工回报

你可以点击博客底部的下载按钮下载报告单。你只需要在这张表上输入你的期权价值，就可以得到你的收益。

### **Python 中如何计算策略收益？**

现在，让我用 Python 编程代码带你看一下收益图。

#### **导入库**

```py
import numpy as np
import matplotlib.pyplot as plt
import seaborn
```

#### **电话支付**

我们定义一个函数来计算购买看涨期权的收益。该函数将 sT 作为输入，sT 是到期时股票价格、认购期权的执行价格和认购期权的溢价的可能值的范围。它返回看涨期权的收益。

```py
def call_payoff(sT, strike_price, premium):
return np.where(sT > strike_price, sT - strike_price, 0) – premium
```

##### **定义参数**

```py
# Infosys stock price
spot_price = 1130
# Long call
strike_price_long_call = 1160
premium_long_call = 20
# Short call
strike_price_short_call = 1200
premium_short_call = 11
# Stock price range at expiration of the call
sT = np.arange(0.95*spot_price,1.1*spot_price,1)
```

**多头 1160 击看涨期权平仓**

```py
payoff_long_call = call_payoff(sT, strike_price_long_call, premium_long_call)
# Plot
fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT,payoff_long_call,label='Long 1160 Strike Call',color='g')
plt.xlabel('Infosys Stock Price')
plt.ylabel('Profit and loss')
plt.legend()
plt.show()
```

![Long Call](img/879bd1d79c848eda0451de8b322653a0.png)

**做空 1200 份看涨期权的回报**

```py
payoff_short_call = call_payoff(sT, strike_price_short_call, premium_short_call) * -1.0
# Plot
fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT,payoff_short_call,label='Short 1200 Strike Call',color='r')
plt.xlabel('Infosys Stock Price')
plt.ylabel('Profit and loss')
plt.legend()
plt.show()
```

![Short Call](img/5299c68d3745b4ee6d38b1e76bfccf06.png)

**看涨期权价差收益**

```py
payoff_bull_call_spread = payoff_long_call + payoff_short_call

print "Max Profit:", max(payoff_bull_call_spread)
print "Max Loss:", min(payoff_bull_call_spread)
# Plot
fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT,payoff_long_call,'--',label='Long 1160 Strike Call',color='g')
ax.plot(sT,payoff_short_call,'--',label='Short 1200 Strike Call ',color='r')
ax.plot(sT,payoff_bull_call_spread,label='Bull Call Spread')
plt.xlabel('Infosys Stock Price')
plt.ylabel('Profit and loss')
plt.legend()
plt.show()
```

![Payoff](img/b43772af15279a44cf57c576ff03e7f3.png)

### **下一步**

如果你想学习算法交易的各个方面，那就去看看算法交易(EPAT)中的 T2 高管课程。该课程涵盖了统计学&计量经济学、金融计算&技术和算法&定量交易等培训模块。EPAT 让你具备成为成功交易者所需的技能。[现在报名](https://www.quantinsti.com/epat/)！

***免责声明**:股票市场的所有投资和交易都有风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。*

### **下载数据文件**

*   公牛呼叫传播- Python 代码
*   看涨期权价差-收益 Excel 表
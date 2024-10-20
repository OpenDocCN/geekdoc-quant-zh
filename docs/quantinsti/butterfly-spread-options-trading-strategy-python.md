# Python 中的蝴蝶差价期权交易策略

> 原文：<https://blog.quantinsti.com/butterfly-spread-options-trading-strategy-python/>

由[维拉伊·巴加](https://www.linkedin.com/in/virajbhagat/)

交易员和投资者认为市场的波动是赚取利润的机会。

如果股票上涨= >买入股票+买入看涨期权没有上涨太多= >应用多头价差下跌= >卖空股票+应用空头价差保持稳定= >应用蝴蝶期权策略

### **关于蝴蝶期权交易策略**

蝴蝶期权策略是牛价差和熊价差的组合，是一种中性的交易策略，因为它的风险选项有限，利润潜力也有限。这种方法适用于其潜在价格在其生命周期内变化很小的股票。

它有利于方向性交易，可以在上涨或下跌时交易，在非方向性市场中也最有效。交易价值较大的股票风险相对较小，因此使用的保证金较少。当基础资产的未来波动性预期高于/低于多头/空头时，IV 蝴蝶价差很有可能赚取有限的利润。

### **蝴蝶战略的组成部分**

蝴蝶[选项策略](https://quantra.quantinsti.com/course/options-trading-strategies-python-intermediate)由身体(中间双选项位置)和翅膀(两个相对的末端位置)组成。其属性如下所示:

*   这是一个三足战略
*   涉及买入或卖出看涨/看跌期权(不同于[备兑买入策略](https://blog.quantinsti.com/write-covered-call-strategy-in-python/)买入股票并卖出 OTM 看涨期权)
*   可以使用看涨或看跌期权来构造
*   在同一到期日的 4 份期权合约
*   拥有相同的基础资产
*   涉及 3 个不同的执行价格(2 个具有相同的执行价格)
*   用这些电话创建 2 笔交易

#### **购买 1 ITM 电话**

*   以较低的执行价格买入
*   到期时关闭
*   提供最大利润

#### **卖出 2 个 ATM 电话**

*   以中等成交价格出售
*   创造收入
*   过期无效

#### **购买 1 OTM 电话**

*   以更高的执行价买入
*   过期无效

**该策略在理想情况下应该是这样的:**

![Butterfly-Spread-graph](img/77e89c2896891a06622d799016df2bb8.png)

#### **条件**

*   中、上、下执行价的差价必须相同。
*   中间执行价格应介于较高的执行价格和较低的执行价格之间。

### **蝴蝶扩散策略的计算**

由此产生的净借方被用于交易。

#### **有限利润**

最大利润在以下情况下获得:

*   相关股票价格在到期时保持不变
*   只有较低的罢工呼吁到期的钱
*   现金价格等于到期日的中间执行价格

#### **最大利润**

*   最大利润=短期看涨期权的执行价格-较低的长期看涨期权的执行价格-支付的净溢价
*   标的价格=卖空期权的执行价格

#### **有限风险**

用于进入交易的初始借方限制了最大值。长蝴蝶传播的损失。

#### **最大损失**

*   最大损失=已付保费净额+已付佣金
*   标的价格= Strike Price of Lower Strike Long Call Price of Underlying > /=较高的执行看涨期权的执行价格

#### **盈亏平衡点**

蝶式价差头寸有 2 个盈亏平衡点:

*   上盈亏平衡点=最高执行价-支付的净溢价(即借方)
*   较低的盈亏平衡点=最低执行价格+支付的净溢价(即借方)

到期时，如果标的股票的价格等于这两个值中的任何一个，蝴蝶将会盈亏平衡。

### **实施战略**

在这个例子中，我将使用阿达尼电力有限公司(股票代码:Adani Power Ltd)。

阿达尼电力有限公司的股价在本月下半月稳步运行。最高为 38.20，最低为 31.05，这是根据谷歌金融的当前值。

为了这个例子的目的；我会买 1 个价内看涨期权，2 个价内看涨期权和 1 个价外看涨期权。

这是阿达尼电力有限公司的期权链，截止日期为 2018 年 3 月 28 日。

![Adani Option Chain](img/3ac4b72ac7c76a80b470b6e8b6a23208.png)

资料来源:nseindia.com

![Adani Calls](img/d91145e363aafa7a03e6fb1274dc1827.png)

资料来源:nseindia.com

我将为行使价为 32.50 的两个自动柜员机看涨期权支付 3.60 印度卢比，行使价为 30.00 的 ITM 看涨期权支付 3.15 印度卢比，行使价为 35 的 OTM 看涨期权支付 0.85 印度卢比。期权将于 2018 年 3 月 28 日到期。为了获利，市场应该在到期前上涨。发起这项交易支付的净保费将为 10.10 印度卢比。

如果蝶式价差得到适当实施，收益可能会高于潜在损失，两者都将受到限制。

### **计算** **蝴蝶价差期权交易策略****Python 中的收益**

现在，让我用 Python 编程代码和调用，带你看一下收益图。

```py
import numpy as np
import matplotlib.pyplot as plt
import seaborn
```

#### **电话支付**

```py
def call_payoff (sT, strike_price, premium):
return np.where(sT> strike_price, sT-strike_price, 0)-premium
# Spot Price
s0 = 40
​
# Long Call
higher_strike_price_long_call = 35
lower_strike_price_long_call=30
​
premium_higher_strike_long_call = 0.85
premium_lower_strike_long_call = 3.15
​
# Short Call
​
strike_price_short_call = 32.5
premium_short_call = 1.80
​
# Range of call option at expiration
sT = np.arange(10,60,1)
```

#### **长期买入回报**

```py
# OTM Strike Long Call Payoff
lower_strike_long_call_payoff = call_payoff(sT, lower_strike_price_long_call, premium_lower_strike_long_call)
​
fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT,lower_strike_long_call_payoff, color='g')
ax.set_title('LONG 30 Strike Call')
plt.xlabel('Stock Price')
plt.ylabel('Profit & Loss')
​
plt.show()
```

![OTM Strike Long Call Payoff](img/5795874315c06eed291c92fe5f8d9d11.png)

#### **更高的看涨期权收益**

```py
# Higher Strike Long Call Payoff
​
higher_strike_long_call_payoff = call_payoff(sT, higher_strike_price_long_call, premium_higher_strike_long_call)
​
fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT,higher_strike_long_call_payoff, color='g')
ax.set_title('LONG 35 Strike Call')
plt.xlabel('Stock Price (sT)')
plt.ylabel('Profit & Loss')
​
plt.show()
```

![Higher Strike Long Call Payoff](img/1cd02c3614b56f26e33e68f339082716.png)

#### **短期买入回报**

```py
# Short Call Payoff
​
Short_call_payoff = call_payoff(sT, strike_price_short_call, premium_short_call)*-1.0
​
fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT, Short_call_payoff, color='r')
ax.set_title('Short 32.5 Strike Call')
plt.xlabel('Stock Price')
plt.ylabel('Profit & Loss')
​
plt.show()
```

![Strike Call Payoff](img/a37660c58b010806ec453c9f2c6162c2.png)

#### **蝴蝶价差收益**

```py
Butterfly_spread_payoff = lower_strike_long_call_payoff + higher_strike_long_call_payoff + 2 *Short_call_payoff
​
fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT,Butterfly_spread_payoff ,color='b', label= 'Butterfly Spread')
ax.plot(sT, lower_strike_long_call_payoff,'--', color='g',label='Lower Strike Long Call')
ax.plot(sT, higher_strike_long_call_payoff,'--', color='g', label='Higher Strike Long Call')
ax.plot(sT, Short_call_payoff, '--', color='r', label='Short call')
plt.legend()
plt.xlabel('Stock Price')
plt.ylabel('Profit & Loss')
plt.show()
```

![Butterfly Spread Payoff](img/74c4ef671cd7c7e3e748d61a871c8683.png)

```py
Butterfly_spread_payoff = lower_strike_long_call_payoff + higher_strike_long_call_payoff + 2 *Short_call_payoff
​
fig, ax = plt.subplots()
ax.spines['bottom'].set_position('zero')
ax.plot(sT,Butterfly_spread_payoff ,color='b', label= 'Butterfly Spread')
plt.legend()
plt.xlabel('Stock Price')
plt.ylabel('Profit & Loss')
plt.show()
```

![Butterfly Spread Payoff](img/ce700f4e5628949d9c6313a39afe07d7.png)

```py
profit = max(Butterfly_spread_payoff)
loss = min(Butterfly_spread_payoff)
​
print ("%.2f" %profit)
print ("%.2f" %loss)

Max. Profit: 1.60
Max. Loss: 0.40 
```

### **一些相关术语**

**短蝴蝶:**与长蝴蝶相反，在股票价格可能向两个方向变动时使用

****长蝶泳:**使用看跌期权练习长蝶泳**

****断了翅膀的蝴蝶:**执行价格之间的距离是不相等的**

****秃鹰:**机体有不同的执行价格**

****翼展:**成员以各种飞行生物命名的翼展家族**

### ****结论****

**蝴蝶差价是一种利用期权合约时间溢价侵蚀的策略，但仍允许投资者承担有限的已知风险。预测基础证券交易范围狭窄的投资者使用它(因为他们感觉舒服)，那些不喜欢空头的无限风险的投资者也使用它。

您可以报名参加 Quantra 上的[期权交易课程](https://quantra.quantinsti.com/course/options-trading-strategies-python-advanced)，在您的交易中创造成功的策略和运用知识。它涵盖了零售和机构交易策略。**

### ****下一步****

**如果你想学习算法交易的各个方面，那就去看看算法交易(EPAT)的高管课程。课程涵盖统计学&计量经济学、金融计算&技术和算法&定量交易等培训模块。EPAT 让你具备成为成功交易者所需的技能。[现在报名](https://www.quantinsti.com/epat/)！**

***免责声明:股票市场的所有投资和交易都有风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。***

### ****下载数据文件****

*   **蝴蝶期权交易策略- Python 代码**
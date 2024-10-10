示例交易程序 - 步骤指南

示例交易程序 1 - 通用

步骤 1：导入库并设置环境

让我们首先导入必要的库。

python

import pandas as pd

import numpy as np

import matplotlib.pyplot as plt

from sklearn.ensemble import RandomForestClassifier

from sklearn.metrics import accuracy_score

from sklearn.model_selection import train_test_split

步骤 2：导入和预处理数据

在这个例子中，我们使用苹果公司（AAPL）的历史股票数据。你可以从不同来源获取这些数据，例如雅虎财经或专用 API。

python

# 假设 df 是一个包含历史数据的 DataFrame

# df = pd.read_csv('AAPL_data.csv')

# 计算移动平均线

df['SMA_50'] = df['Close'].rolling(window=50).mean()

df['SMA_200'] = df['Close'].rolling(window=200).mean()

步骤 3：特征工程

让我们添加一些可能与交易相关的特征，如波动率和动量。

python

# 波动率

df['Volatility'] = df['Close'].rolling(window=50).std()

# 动量

df['Momentum'] = df['Close'].diff(4)

步骤 4：创建标签

让我们为监督学习标记数据。如果接下来的 5 天价格上涨，标记为 1；否则，标记为 0。

python

df['Future_Close'] = df['Close'].shift(-5)

df['Label'] = np.where(df['Future_Close'] >= df['Close'], 1, 0)

步骤 5：为模型准备数据

python

features = ['SMA_50', 'SMA_200', '波动率', '动量']

X = df[features].dropna()

y = df['Label'][df.index.isin(X.index)]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

步骤 6：构建和训练模型

我们将使用随机森林分类器进行此示例。

python

model = RandomForestClassifier(n_estimators=100)

model.fit(X_train, y_train)

步骤 7：评估模型

python

y_pred = model.predict(X_test)

print('准确率:', accuracy_score(y_test, y_pred))

步骤 8：实施策略和回测

如果模型预测为 1（价格将上涨），则买入；否则，卖出。

python

df['Predicted_Label'] = model.predict(df[features].dropna())

df['Strategy_Returns'] = df['Close'].pct_change() * df['Predicted_Label'].shift()

cumulative_strategy_returns = (1 + df['Strategy_Returns']).cumprod()

cumulative_market_returns = (1 + df['Close'].pct_change()).cumprod()

plt.figure(figsize=(10,5))

plt.plot(cumulative_market_returns, label='市场收益')

plt.plot(cumulative_strategy_returns, label='策略收益')

plt.legend()

plt.show()

这是一个简单的例子，可以帮助你入门。在实际应用中，你需要通过广泛的回测验证你的策略，优化特征，并可能实施风险管理策略。

Python - 完整程序

# 导入库

import pandas as pd

import numpy as np

from sklearn.ensemble import RandomForestClassifier

from sklearn.metrics import accuracy_score

from sklearn.model_selection import train_test_split

import matplotlib.pyplot as plt

# 步骤 2：导入和预处理数据

# 假设你有一个名为'AAPL_data.csv'的CSV文件，其中包含历史数据

# df = pd.read_csv('AAPL_data.csv')

# 为演示，我们生成一些虚拟数据

df = pd.DataFrame({

'收盘': np.random.rand(1000) * 1000  # 生成随机收盘价格

})

# 计算移动平均

df['SMA_50'] = df['收盘'].rolling(window=50).mean()

df['SMA_200'] = df['收盘'].rolling(window=200).mean()

# 第3步：特征工程

# 波动率

df['波动率'] = df['收盘'].rolling(window=50).std()

# 动量

df['动量'] = df['收盘'].diff(4)

# 第4步：创建标签

df['未来收盘'] = df['收盘'].shift(-5)

df['标签'] = np.where(df['未来收盘'] >= df['收盘'], 1, 0)

# 第5步：为模型准备数据

特征 = ['SMA_50', 'SMA_200', '波动率', '动量']

X = df[features].dropna()

y = df['标签'][df.index.isin(X.index)]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# 第6步：构建和训练模型

模型 = RandomForestClassifier(n_estimators=100)

model.fit(X_train, y_train)

# 第7步：评估模型

y_pred = model.predict(X_test)

print(f'准确率: {accuracy_score(y_test, y_pred)}')

# 第8步：实施策略并进行回测

df['预测标签'] = model.predict(df[features].dropna())

df['策略收益'] = df['收盘'].pct_change() * df['预测标签'].shift()

累计策略收益 = (1 + df['策略收益']).cumprod()

累计市场收益 = (1 + df['收盘'].pct_change()).cumprod()

plt.figure(figsize=(10,5))

plt.plot(累计市场收益, label='市场收益')

plt.plot(累计策略收益, label='策略收益')

plt.legend()

plt.show()

请注意，您需要通过取消注释读取CSV文件的行来将随机虚拟数据替换为实际历史数据。请记住，这只是一个示例，并非实际交易建议。在考虑任何策略进行实时交易之前，请确保彻底回测。

示例交易程序2 - 通用

第1步：导入库 我们将使用Pandas进行数据处理，Matplotlib进行图表绘制，NumPy进行数值运算。

python

import pandas as pd

import numpy as np

import matplotlib.pyplot as plt

第2步：导入和预处理数据 假设你有一个CSV文件，其中包含历史数据（比如AAPL股票）。

python

# df = pd.read_csv('AAPL_data.csv')

# 为演示目的，我们生成一些随机数据

df = pd.DataFrame({

'收盘': np.random.rand(1000) * 1000

})

第3步：特征工程 计算20个周期的滚动均值和标准差。

python

df['滚动均值'] = df['收盘'].rolling(window=20).mean()

df['滚动标准差'] = df['收盘'].rolling(window=20).std()

第4步：创建布林带 上带是滚动均值 + (2 * 滚动标准差)，下带是滚动均值 - (2 * 滚动标准差)。

python

df['上带'] = df['滚动均值'] + (df['滚动标准差'] * 2)

df['下带'] = df['滚动均值'] - (df['滚动标准差'] * 2)

第5步：创建标签 如果收盘价高于上轨，我们将卖出（-1），如果低于下轨，我们将买入（1）。

python

df['Signal'] = 0

df.loc[df['Close'] > df['Upper_Band'], 'Signal'] = -1

df.loc[df['Close'] < df['Lower_Band'], 'Signal'] = 1

第6步：实施策略 计算每日收益。

python

df['Daily_Return'] = df['Close'].pct_change()

df['Strategy_Return'] = df['Signal'].shift() * df['Daily_Return']

第7步：回测 计算策略和市场的累计收益。

python

df['Cumulative_Market_Returns'] = (1 + df['Daily_Return']).cumprod()

df['Cumulative_Strategy_Returns'] = (1 + df['Strategy_Return']).cumprod()

第8步：绘制策略与市场收益

python

plt.figure(figsize=(10,5))

plt.plot(df['Cumulative_Market_Returns'], label='市场收益')

plt.plot(df['Cumulative_Strategy_Returns'], label='策略收益')

plt.legend()

plt.show()

这里是完整的代码。你需要将虚拟数据替换为你的真实历史数据。

Python

import pandas as pd

import numpy as np

import matplotlib.pyplot as plt

# 第2步：导入和预处理数据

# df = pd.read_csv('AAPL_data.csv')

# 演示用的虚拟数据

df = pd.DataFrame({

'Close': np.random.rand(1000) * 1000

})

# 第3步：特征工程

df['Rolling_Mean'] = df['Close'].rolling(window=20).mean()

df['Rolling_STD'] = df['Close'].rolling(window=20).std()

# 第4步：创建布林带

df['Upper_Band'] = df['Rolling_Mean'] + (df['Rolling_STD'] * 2)

df['Lower_Band'] = df['Rolling_Mean'] - (df['Rolling_STD'] * 2)

# 第5步：创建标签

df['Signal'] = 0

df.loc[df['Close'] > df['Upper_Band'], 'Signal'] = -1

df.loc[df['Close'] < df['Lower_Band'], 'Signal'] = 1

# 第6步：实施策略

df['Daily_Return'] = df['Close'].pct_change()

df['Strategy_Return'] = df['Signal'].shift() * df['Daily_Return']

# 第7步：回测

df['Cumulative_Market_Returns'] = (1 + df['Daily_Return']).cumprod()

df['Cumulative_Strategy_Returns'] = (1 + df['Strategy_Return']).cumprod()

# 第8步：绘制

plt.figure(figsize=(10,5))

plt.plot(df['Cumulative_Market_Returns'], label='市场收益')

plt.plot(df['Cumulative_Strategy_Returns'], label='策略收益')

plt.legend()

plt.show()

示例交易程序3 – Interactive Brokers

from ib_insync import IB, Stock, util, MarketOrder

# 第1步：连接到Interactive Brokers

ib = IB()

ib.connect('127.0.0.1', 7497, clientId=1)

# 第2步：定义合约并请求历史K线

contract = Stock('AAPL', 'SMART', 'USD')

ib.qualifyContracts(contract)

bars = ib.reqHistoricalData(

contract,

endDateTime='',

durationStr='30天',

barSizeSetting='1小时',

whatToShow='MIDPOINT',

useRTH=True)

# 转换为DataFrame

df = util.df(bars)

# 第3步：定义简单移动平均策略

sma_short = df['close'].rolling(window=5).mean()

sma_long = df['close'].rolling(window=20).mean()

# 第4步：基于策略生成交易信号

signals = []

for short, long in zip(sma_short, sma_long):

if short > long:

signals.append(1)  # 买入

else:

signals.append(0)  # 卖出

# 第 5 步：执行交易

for i in range(1, len(signals)):

if signals[i] > signals[i - 1]:

# 执行一个买入订单

order = MarketOrder('BUY', 10)

trade = ib.placeOrder(contract, order)

ib.sleep(1)

print(f"买入订单状态: {trade.orderStatus.status}")

elif signals[i] < signals[i - 1]:

# 执行一个卖出订单

order = MarketOrder('SELL', 10)

trade = ib.placeOrder(contract, order)

ib.sleep(1)

print(f"卖出订单状态: {trade.orderStatus.status}")

ib.disconnect()

示例交易程序 4 – Meta Trader

//+------------------------------------------------------------------+

//|                                              MovingAverage.mq4   |

//|                        版权 2023, 公司名称                     |

//+------------------------------------------------------------------+

#property copyright "MetaQuotes Software Corp."

#property link      "https://www.mql5.com"

#property version   "1.00"

// 声明外部变量（可从 MetaTrader 调整）

extern int TakeProfit = 100;

extern int StopLoss = 50;

extern int FastMA = 5;

extern int SlowMA = 20;

//+------------------------------------------------------------------+

//| 专家初始化函数                                           |

//+------------------------------------------------------------------+

int OnInit()

{

// 在这里初始化你的交易算法

return(INIT_SUCCEEDED);

}

//+------------------------------------------------------------------+

//| 专家去初始化函数                                         |

//+------------------------------------------------------------------+

void OnDeinit(const int reason)

{

// 在这里去初始化你的交易算法

}

//+------------------------------------------------------------------+

//| 专家每次报价函数                                             |

//+------------------------------------------------------------------+

void OnTick()

{

double fastMA = iMA(NULL, 0, FastMA, 0, MODE_SMA, PRICE_CLOSE, 0);

double slowMA = iMA(NULL, 0, SlowMA, 0, MODE_SMA, PRICE_CLOSE, 0);

if(fastMA > slowMA)

{

// 买入逻辑在这里

if(OrderSend(Symbol(), OP_BUY, 1, Ask, 3, 0, Ask + TakeProfit * Point, "", 0, Green) > 0)

{

// 成功下单买入

}

}

else if(fastMA < slowMA)

{

// 卖出逻辑在这里

if(OrderSend(Symbol(), OP_SELL, 1, Bid, 3, 0, Bid - StopLoss * Point, "", 0, Red) > 0)

{

// 成功下单卖出

}

}

}

//+------------------------------------------------------------------+

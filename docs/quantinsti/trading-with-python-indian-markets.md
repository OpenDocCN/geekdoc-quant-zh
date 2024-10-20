# 使用 Zerodha Kite Connect API 在印度市场与 Python 进行交易

> 原文：<https://blog.quantinsti.com/trading-with-python-indian-markets/>

## ![Algorithmic Trading in Indian Markets using Python](img/20040e030709d93ce616fc6296d74c8c.png)

我们已经在本文的[中告诉你为什么 Python 是进行算法交易的首选语言之一。我们也告诉过你在印度的程序化 T2 交易。我们还成功举办了一场关于使用 python 在印度市场进行交易的网上研讨会(](/python-best-programming-language-algorithmic-trading/)[点击此处](https://www.youtube.com/watch?v=9vzd289Eedk)观看网上研讨会)，我们应该向您介绍一下这个交易平台，它将使您能够使用 Python 实现您的算法交易策略。

为了使用 Python 在印度市场进行交易，我们将利用 Zerodha Kite Connect API，这是印度第一个面向零售客户的市场 API。我们将在网络研讨会中详细讨论这一点。我们涵盖了[EPAT](https://www.quantinsti.com/epat/)的大多数交易平台，这是我们广受欢迎的算法交易和量化金融课程。在之前的一篇文章中，我们还介绍了 python 中可用于编程交易的各种[库](/python-trading-library/)，在这篇文章中，我们还将讨论用于与 Zerodha Kite Connect API 通信的官方 Python 客户端。

### 什么是 Zerodha Kite Connect？

Kite Connect 是类似 REST 的基于超文本传输协议的 API 的汇编，这些 API 缓解了构建投资和交易平台所需的众多能力。它建立在 Zerodha 的在线交易平台之上。用户只能是 Zerodha 的客户，他们可以通过编程方式访问有关经纪业务的所有信息。您还可以将 Kite Connect API 用于:

*   实时执行订单
*   管理投资组合
*   流式实时市场数据
*   异地订单执行
*   获得订单的可靠更新
*   当然，获取历史数据

现在，如果你还记得，在我们关于交互式经纪人交易的文章中，我们提到了使用 IB API 进行算法交易的一些优势。对于印度市场来说，Zerodha Kite Connect 是使用 Python 实现算法交易策略的绝佳选择，这在我们的[网络研讨会](https://www.youtube.com/watch?v=9vzd289Eedk)中有进一步解释。

### Zerodha 风筝会的目标

散户投资者远离资本市场的日子已经一去不复返了，因为他们没有任何务实地进入交易账户的选择。Zerodha Kite Connect 致力于为印度的交易方式带来革命性的变化，承诺:

*   降低在印度进行交易的成本
*   将来完全没有经纪业务
*   使过程更加透明
*   提供一个更好的交易平台
*   保持客户至上的态度。
*   支持多种编程语言，包括 Python、Java、C#、Excel VBA 等。你也可以在 Kite Connect 上使用命令行控制台。

除了下订单和管理订单，Kite Connect 还承诺让用户建立:

*   多资产风险建模系统
*   股票筛选员
*   量化策略
*   股票选择模型
*   期权希腊计算器
*   回溯测试，机器学习
*   个人风筝或 Pi。

Zerodha Kite Connect 的一个关键优势是，您将拥有并控制您的交易账户和与之相关的数据，并且您将不会被限制在您的经纪人提供的平台上。

### 用于 Kite Connect 中程序化交易的 Python

我们已经在标题为[为什么 Python 程序化交易是交易者的首选的文章中告诉了你为什么 Python 足以成为程序化交易的最佳选择？](/python-best-programming-language-algorithmic-trading/)

Zerodha 的 Kite Connect 拥有多种编程语言的客户端库，包括 PHP、JS，当然还有 Python。Python 的官方库可从以下网址获得:

[https://github.com/rainmattertech/pykiteconnect](https://github.com/rainmattertech/pykiteconnect)

#### 要求

Zerodha 是印度第一家折扣经纪商，Kite Connect 的所有交易都通过 Zerodha 执行。所以，你需要做的第一件事是[在 Zerodha](https://zerodha.com/?c=RAINMT&leadsrc=kite.trade) 上创建一个交易账户，这样你就可以访问 API 了。一旦你有了这些，接下来要做的就是[注册一个开发者账户](https://developers.kite.trade/login)。就是这样！你可以马上开始。在我们的网络研讨会中，Zerodha 的创始人&兼首席执行官 Nithin Kamat、&zero DHA 的软件开发人员 Satyajit Sarangi 将以循序渐进的方式解释这一切。

因为 Zerodha 已经为 Kite Connect API 的用户获得了所有必要的批准，所以作为 Kite Connect 的用户，你不需要获得任何其他的批准。

### Python 客户端的安装

从 github 资源库下载资源后，您必须安装这些文件。要安装客户端，您必须使用以下命令:

```py
pip install kiteconnect
```

#### API 用法

您也可以在 github 存储库中找到以下代码。然而，为了方便起见，我们在这里给出它:

```py
from kiteconnect import KiteConnect

kite = KiteConnect(api_key="your_api_key")

# Redirect the user to the login url obtained
# from kite.login_url(), and receive the request_token
# from the registered redirect url after the login flow.
# Once you have the request_token, obtain the access_token
# as follows.

data = kite.request_access_token("request_token_here", secret="your_secret")
kite.set_access_token(data["access_token"])

# Place an order
try:
    order_id = kite.order_place(tradingsymbol="INFY",
                    exchange="NSE",
                    transaction_type="BUY",
                    quantity=1,
                    order_type="MARKET",
                    product="NRML")

    print("Order placed. ID is", order_id)
except Exception as e:
    print("Order placement failed", e.message)

# Fetch all orders
print(kite.orders())
```

#### WebSocket 用法

```py
from kiteconnect import WebSocket

# Initialise.
kws = WebSocket("your_api_key", "your_public_token", "logged_in_user_id")

# Callback for tick reception.
def on_tick(tick, ws):
    print tick

# Callback for successful connection.
def on_connect(ws):
    # Subscribe to a list of instrument_tokens (RELIANCE and ACC here).
    ws.subscribe([738561, 5633])

    # Set RELIANCE to tick in `full` mode.
    ws.set_mode(ws.MODE_FULL, [738561])

# Assign the callbacks.
kws.on_tick = on_tick
kws.on_connect = on_connect

# Infinite loop on the main thread. Nothing after this will run.
# You have to use the pre-defined callbacks to manage subscriptions.
kws.connect()
```

你可以在这里进一步阅读所有支持方法的列表[。Zerodha 的精英们将在我们关于使用 Python 在印度市场进行交易的网络研讨会上详细介绍这一点。如果你没有参加，那么请点击这里](https://kite.trade/docs/pykiteconnect/)观看[的录音。](https://www.youtube.com/watch?v=9vzd289Eedk)

### 最后

得益于 Zerodha 的 Kite Connect API，使用 Python 在印度市场进行算法交易变得更加有趣和简单。你现在要做的就是:

*   向 Zerodha 注册一个交易账户
*   注册一个 Kite Connect 帐户
*   登录你的 kite connect 开发者账户
*   开始创造你的策略

就是这样！享受 Kite Connect 提供的程序化交易

### 下一步

Python 算法交易在 quant finance 社区中获得了牵引力，因为它可以轻松地建立复杂的统计模型，这是因为有足够的科学库可用，如 Pandas、NumPy、PyAlgoTrade、Pybacktest 等。

如果您希望掌握使用 Python 生成交易策略、回溯测试、处理时间序列、生成交易信号、预测分析等艺术，您可以注册我们的 [Python for Trading 课程！](https://quantra.quantinsti.com/course/python-for-trading)

*免责声明:股票市场的所有投资和交易都涉及风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。T3】*

来源: [https://kite.trade](https://kite.trade)
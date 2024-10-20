# 与算法交易者的坦诚对话(第二部分)

> 原文：<https://blog.quantinsti.com/candid-conversations-algorithmic-trader-2/>

#### ![Candid Conversation with Algorithmic Trader part 2](img/74513e1ee92847ce05fcf2638fff9e97.png)

#### 如果你不知道自己是谁，股市是一个寻找答案的昂贵地方- **乔治·古德曼**

在 [上一篇](/candid-discussion-algorithmic-trader/) 中，我和几位算法交易领域的专家进行了一次对话，对这个看似“黑箱”的东西有所感悟。那次谈话不仅帮助我打消了对算法交易的一些疑虑，还增强了我一头扎进一个由复杂数学模型、股票市场头寸管理和编程灾难主宰的世界的愿望。

所以，我站在这里，准备冒险一试。有人告诉我，要成为自动交易者，我不需要金融或计算机科学的大学学位。当然，要想在这个领域取得成功，我知道正规的教育是非常有益的，但是现在，我只是触及了表面。虽然，我的工程背景确实让我在理解金融数学模型和编程方面有了一定的余地。

然而，这条路似乎并不平坦。我脑子里还有一卡车的问题。有多少市场知识足以让我们开始使用算法进行交易？我可以在哪里验证我的交易策略？我怎样才能让我的策略盈利？我需要遵循的领域的*【必须做的事情】*和*【经验法则】*是什么？

我想我需要再次和专家坐下来，喝一杯热气腾腾的拿铁，消除误会。

> #### Therefore, I read some literatures about algorithmic trading, and finally want to set up my own trading platform. What path do you recommend?

如果你的想法是最终拥有自己的设置，你将需要在量化和/或编程方面积累专业知识。首先，我建议你至少掌握一门 Quants 和 Algo 交易者常用的编程语言(Matlab/Python/R)，因为这是必不可少的要素。当然，你在任何一种语言中发展的技能对其他人也是有用的。最好的办法就是尽快把手弄脏。开始了解市场。建立你的图表知识。阅读交易者在市场中使用的不同策略。或许，重要的是理解市场无效率的基本原理，并通过围绕市场无效率制定策略来利用市场无效率。一旦制定了策略，就用历史数据对其进行回溯测试，以消除你可能有的不准确的假设。如果一切顺利，你应该可以在真实市场中用这个策略交易。

> #### What do you mean by market inefficiency?

股票或证券的实时价格不能准确反映其真实价值的情况。在一个无效率的市场中，一些证券定价过高，而另一些定价过低。这给了交易者一定的风险，或者在某些情况下，给了他们赚钱的机会。听说过 [统计套利](/statistical-arbitrage/) 这个术语吗？

> #### Yes. Isn't this a buzzword for pairing transactions? I want to know more about it.

那只是部分真实。配对交易是众多统计套利中的一种。 这也是市场无效率的一种类型。在算法和高频交易者中非常流行，它实际上是 [配对交易策略](/incorrect-notions-statistical-arbitrage/) 的进化版本，其中股票根据基本面或基于市场的相似性被配对。当一对股票中的一只表现优于另一只时，表现较差的股票被买入，同时预期它会超过表现较好的股票，另一只被卖空。这对冲了整个市场波动的风险。

> #### This does seem logical. So, what do you think is the most important thing when designing a trading strategy?

这个问题没有直接的答案，因为它是几种事物的混合。你需要了解市场如何运作，并据此确定进场点和出场点。就我的经验来说， 识别何时退出市场，识别止损比进场位 更难。每种策略都是独一无二的，因此需要有自己定制的定位。

一旦你的策略准备好了，最好是[](/backtesting/)对照历史数据进行回溯测试。然而，在进行回溯测试时，有一点需要注意。例如，一名交易员希望测试一项基于互联网 IPO 表现优于整体市场这一概念的策略。如果你在上世纪 90 年代末互联网繁荣时期测试这一策略，该策略的表现将远远超过市场。然而，在泡沫破裂后尝试同样的策略将导致惨淡的回报。

因此，准备一个应急计划是很重要的，因为没有一个策略会在所有的市场条件下都有效。提款是不可避免的，应该纳入交易策略。记住，好的战略不是技术的奴隶。你可以雇一个程序员来执行你的交易策略，但反之则不行。

如果你想测试你的算法，NinjaTrader 是一个免费使用的平台。如果你想了解更多信息，有很多其他的免费回溯测试工具可以研究。

> #### I like your point about exit, because I know that any trading strategy is not without risks. How does Algo trading system deal with risks?

你应该明白 [风险管理](/changing-trends-in-trading-risk-management/) 及其降低是算法交易最关键的领域之一。市场充满了奇怪的东西，一旦你意识到你正处于亏损的边缘，你的算法应该会检查出这笔交易。这就是算法的出口点比入口点更重要的原因。

算法风险可以分为几类:一致性、质量、可伸缩性等等。一致性意味着输入系统的数据不是旧的或过时的。 市场数据包中嵌入了时间戳。世界上先进的交易所正在采用像原子钟时间同步这样的概念。你的算法交易系统应该能够跟踪这些时间戳，以确保你得到的数据确实是新的。

对于任何正常的交易活动，您必须注意市场风险、金融风险、监管风险、流动性风险和信贷/交易对手风险。此外，算法交易员还需要做好法定风险的准备。 在算法交易系统中，有两个地方需要处理风险:在应用程序内部和在订单管理系统中生成订单之前。 印度是监管环境最严格的国家之一，在订单流出之前，许多算法交易相关的风险都必须在系统中强制检查。

> #### **Wow! This is a lot of risk management that we are talking about here. But I want to take a step back and ask about the order management system**

[订单管理系统](/automated-trading-order-management-system/) 或被称为 OMS，是将订单发送到正确目的地的路径。订单需要包含证券标识符、订单大小、价格限制、订单类型和条件、使用的算法类型等等。 该信息通常由最终用户通过 winform 输入，但对于全自动系统，不需要 winform，然而，在这两种情况下，建议将每个订单对象存储在关系数据库中以备记录。

一旦订单被系统捕获，它需要被发送到所需的目的地。由于大多数接收订单的系统都有自己的专有协议，订单路由要求每个订单都以正确的格式编码。

为了确保订单信息被正确发送和接收，需要进行多项检查。场馆将运行各种校验和以及订单长度，以便 FIX 引擎可以确认收到的订单与发送的预期订单相匹配。订单经理还会在发出订单前进行风险检查。

> #### **Mm-hmm. I think I will stop my inquiry now. I got some very profound insights from your speech. Maybe I should start with some programming tutorials.** T3】

这是个好主意。这里有一些你可以寻找的资源。算法交易的汇总[阅读列表](/essential-books-algorithmic-trading/)

### **向前一步**

如果你和算法交易者或市场专家有过这样的对话，请在下面的评论区和我们分享。

如果你是一名程序员或科技专业人士，想开始自己的自动化交易平台。从每日从业者的现场互动讲座中学习算法交易。我们的 [Algo 交易课程](https://www.quantinsti.com/epat/)，算法交易的执行程序涵盖了统计&计量经济学、金融计算&技术和算法&量化交易等培训模块。
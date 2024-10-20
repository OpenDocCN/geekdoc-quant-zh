# 延迟战争——为什么低延迟很重要？

> 原文：<https://blog.quantinsti.com/latency-war-why-is-low-latency-important/>

[https://www.youtube.com/embed/6RiHCH5IPr4?rel=0](https://www.youtube.com/embed/6RiHCH5IPr4?rel=0)

是潜伏的愚蠢！大卫·谢瑞登曾经说过，如果你有一个低带宽的网络链路，那么很容易将几个并联起来，形成一个具有更高带宽的组合链路，但如果你有一个延迟很差的网络链路，那么再多的钱也不能将它们变成一个延迟很好的链路。

让我们看一个例子来分解延迟的技术术语。波音 747 运载 500 名乘客，而波音 737 运载 150 名乘客。你会说 747 比 737 快 3 倍吗？波音 747 比 737 大 3 倍，并不比 737 快，因为两者的时速都是 500 英里。等待时间在算法交易中起着至关重要的作用，在算法交易中，速度是执行交易的关键因素。传统系统架构与[自动化系统架构](https://blog.quantinsti.com/algorithmic-trading-system/)的简单比较。

![System Architecture of a Traditional Trading System](img/f936ebb95001db48ff58f634924befbe.png)传统交易系统的系统架构

传统的交易系统包括一个读取数据的系统、一个历史数据仓库、一个分析历史数据的工具、一个提交交易输入的系统和一个将订单发送到交易所的系统。Exchange 逐个发送滴答数据。服务器主要用于数据存储，是个人桌面的同义词。市场数据从服务器被检索到交易者的工具中，在那里发生可操作的情报(买、卖、不交易)。然后，这些操作通过订单管理器传递给交易所。这些动作是连续的。交易员的工具只能在收到市场数据后处理和生成订单。

直接市场访问(DMA)的出现给交易系统的架构带来了巨大的变化。

![System Architecture of an Automated Trading System](img/8a53ec4a2941f8060c6496a737cb0585.png)自动交易系统的系统架构

在传统系统中，数据流将从经纪人流向交易者的工具。这在通过 DMA 的自动交易系统中得到改善。这大大减少了数据从交易所流向交易工具所需的时间。即使在自动交易系统中，数据流和交易生成的这些动作仍然是连续的。可以减少交易工具(事件发生)和订单生成之间的延迟，以实现更高的效率。这可以通过将等待时间减少到毫秒级或更低来实现。风险管理必须在没有人工干预的情况下实时实施。

为什么低延迟首先如此重要？要回答这个问题，把交易想象成一场赛跑。比你的竞争对手速度更快，你赢的机会就更大。交易的目标是以有竞争力的价格执行交易。希望改善延迟以防止被竞争对手选中。必须实施正确的技术来减少延迟，因为低延迟系统成本很高。因此，必须在低延迟投资和低延迟投资回报率之间取得平衡。

下面的快照提供了不同策略的延迟。

![latencies for different strategies](img/d0ab1cd84e5b523ad559c42d88be8202.png)

延迟可以用等式的形式来表示。

**L=P+N+S+I+AP**

这里 P 是沿线路发送比特的传播时间，N 是网络分组处理-路由、交换和保护，S 是串行化时间-将比特拉进/拉出线路，I 是中断处理时间-在服务器上接收分组，API 是应用处理时间。

如前所述，必须采取果断措施来平衡复杂性水平，以减少延迟并优化投资决策。

![Costs in Time (Years) for Time Reduction (micro-seconds)](img/026ae32ccad731fd24b6e718860f6be1.png)

![Technology Mix](img/56f99dfe3098e262368d778db6e2a300.png)

总而言之，低延迟是算法交易的一个重要因素。低延迟导致交易执行具有竞争力的价格。

### **演示文稿**

[//www.slideshare.net/slideshow/embed_code/key/DahrBRyeRBVdsL](//www.slideshare.net/slideshow/embed_code/key/DahrBRyeRBVdsL)
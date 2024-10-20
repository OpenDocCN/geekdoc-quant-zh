# 利用二次判别分析优化日内动量策略

> 原文：<https://blog.quantinsti.com/quadratic-discriminant-analysis-optimize-intraday-momentum-strategy/>

拉马克·科尔曼

在本帖中，我们将创建一个日内动量策略，并使用 QDA 作为优化策略的手段。我们将首先回顾线性判别分析(LDA)及其与 QDA 的关系，了解 QDA，以及何时可以用这种技术代替线性判别分析。然后，我们将使用埃米尼标准普尔 500 期货的数据创建我们的日内动量策略，并应用我们的 QDA 分析来改进我们的交易策略。

我们开始吧！

## **线性判别分析综述**

回想一下，使用机器学习技术的目的是为了让我们能够从数据中做出更好的推断和预测。因此，机器学习的目的类似于实现量化交易工作流程的目的。在定量交易中，我们的目标是消除认知偏差，最终将我们的决策建立在合理的证据或逻辑上。换句话说，我们的目标是用量化交易提供的客观性来取代手工交易固有的主观性。机器学习是实现这一目标的手段。

分类是机器学习问题的一种类型。在一个标准分类问题中，我们有一些***【y】***或包含 ***k*** 水平或可能类别的响应。我们可以使用定量或数字、定性或分类，或者两种数据类型的混合作为我们的**或特征来预测我们的数据的类别。**

**在交易环境中，分类问题的一个例子是试图预测下一个价格的方向。在回归设置中，我们将尝试构建一个模型，使我们能够预测实际价格或数字响应。所以回归问题处理数字预测，分类处理分类预测。**

**当我们实现机器学习算法时，我们对***【f(X)***进行近似，这是一个表示 ***X*** 或我们的预测器和 ***y*** (我们的响应)之间关系的方程。参数模型为我们提供的优势是专注于估计一个方程的特定系数，而不是估计整个方程。**

**这意味着，我们可以对我们的数据做出一些假设，并基于现有的方程构建我们的模型，并求解该方程的系数，而不是试图构建一个完整的方程来表示我们的输入和输出之间的关系。这种模型有优点也有缺点，我们不会深入探讨，但本质上，为了有效地提供预测，模型需要反映或“模拟”现实中的数据。模型具有固有的假设，如果这些假设与现实不一致，模型的准确性或预测能力就会很低。**

**从它的名字，你可能已经猜到 LDA 假设线性。**

**在 LDA 中，我们从我们的观察可以落入的 ***k*** 类开始。该模型为每个 ***k*** 类创建概率分布。与直接估计观察值在特定类别中的概率的逻辑回归不同，LDA 使用 Bayes 定理并间接地估计这个后验概率。**

**例如，从代数上回忆一下，直线的方程是 ***y=mx+b*** 。**

**有了这个等式，我们可以简单地通过估计 ***m*** 和 ***b*** 来拟合我们的数据，其中 ***m*** 是给定**x*中一个单位变化的 ***y*** 的斜率或导数(即变化率),而*是截距这个等式允许我们，给定一些 ***x*** 值，来估计系数***【m】***和***【b】***，并对***【y】***进行预测。******

******此过程类似于实现参数模型的过程。我们有一个关于数据结构的假设，通过我们的线性方程来说明，因此我们可以简单地估计我们的系数来进行预测。******

******LDA 的等式如下:******

******![LDA equation](img/ef54437bb93eef15315323f243e57a6c.png)******

******在这个等式中，我们寻求估计**或每个 ***k*** 、 ***π <sub>k</sub>*** ，或***k***类和*<sup>σ</sup>*的先验概率，或每个类之间的公共协方差矩阵一旦我们有了这些系数，我们就可以把它们代入我们的方程进行预测。********

******我们将在下一篇题为“使用线性判别分析进行[量化投资组合管理](https://quantra.quantinsti.com/course/quantitative-portfolio-management)”的文章中介绍更多关于 LDA 的内容这个帖子将很快上线。******

## ********什么是二次判别分析？********

******二次判别分析是另一种机器学习分类技术。像 LDA 一样，它试图估计一些系数，将这些系数代入一个方程，作为进行预测的手段。实际上，LDA 和 QDA 非常相似。两者都假设 k 类可以从高斯分布中提取。QDA 也像 LDA 一样，使用 Baye 定理来估计方程的参数。QDA 的方程式如下:******

******![QDA 1](img/2e2f830bc372254e4a35490346be2066.png)******

******等于:******

******![QDA 2](img/880187b10f09b926e04c4d5c5af66e57.png)******

******因此我们可以看到，我们的 QDA 方程看起来与我们的 LDA 方程有些相似，只是在 LDA 中我们估计***<sub>k</sub>**T5、 ***π <sub>k</sub>*** 和 ***σ <sup>2</sup>*** ，但在 QDA 我们估计***μ<sub>k</sub>**********

*******在 LDA 中，我们假设每个***k<sub>th</sub>**T5】类有一个共享协方差矩阵， ***σ <sup>2</sup>*** 。但是在 QDA，这个假设已经改变了，我们现在假设每个***k***类都有自己的协方差矩阵， ***∑ <sub>k</sub>*** 。********

*****好了，现在你可能在想，如果 LDA 和 QDA 有相似之处，我们为什么要用 QDA。难道我们不能只关注 LDA 吗？因为很明显，QDA 更复杂一些，并且包含了矩阵乘法。*****

*****虽然 LDA 和 QDA 很相似，但也存在应该使用 QDA 的情况，并且可能优于 LDA，反之亦然。例如，LDA 假设 k 个类共享一个协方差矩阵。如果这种假设是无效的，那么 QDA 将优于 LDA。模型的另一个考虑是它们的灵活性。模型的灵活性可以直接转化为偏差-方差的权衡。模型越灵活，就越有可能过度拟合数据，并具有低偏差但高方差。相比之下，模型越不灵活，它就越有可能具有高偏差但低方差，因此并不真正类似于真实的总体。*****

*****伦敦发展署远没有 QDA 灵活。如果公共协方差矩阵的假设不正确，则 LDA 将具有高偏差，或者不代表现实。如果这个假设是正确的，那么使用 LDA 进行分类可能比使用 QDA 更好。*****

*****此外，特征的数量在模型选择中起着重要的作用。如果有很多预测器，使用 QDA 将比 LDA 的计算效率更低。这是因为在 QDA，你有更多的参数要估计，而且自然地，这在某种程度上是基于预测因子的数量而增长的。如果有很多训练观察，QDA 可能是更好的选择。*****

## *******日内动量策略开发*******

*****好吧。现在我们已经回顾了 LDA 和 QDA，让我们为发展我们的日内动量策略制定一个框架。我们将使用 eMini 标准普尔 500 的日内数据，并将 RSI 作为我们的动量指标。我们的目标是构建我们的策略，评估其性能，然后通过使用二次判别分析来改进我们的策略的性能。*****

*****让我们导入一些我们常用的库。*****

```py
*****#data analysis and manipulation
import numpy as np
import pandas as pd
#data visualization
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style('whitegrid')*****
```

*****现在我们已经导入了初始库，让我们导入数据。我们将使用 pandas 读取 csv 文件格式的数据。*****

```py
*****#initializing our data variable as our eMini data
data=pd.read_csv('ESPostData.csv')*****
```

*****现在我们有了数据，让我们对它进行一些探索性的数据分析。我们将从使用信息和描述方法以及检查数据头开始。*****

```py
*****data.info()*****
```

```py
*****<class 'pandas.core.frame.DataFrame'>
RangeIndex: 28027 entries, 0 to 28026
Data columns (total 10 columns):
Date            28027 non-null object
Time            28027 non-null object
Open            28027 non-null float64
High            28027 non-null float64
Low             28027 non-null float64
Close           28027 non-null float64
Volume          28027 non-null int64
NumberOfTrades  28027 non-null int64
BidVolume       28027 non-null int64
AskVolume       28027 non-null int64
dtypes: float64(4), int64(4), object(2)
memory usage: 2.1+ MB*****
```

*****通过应用这种方法，我们可以看到数据帧中的数据类型以及列。现在让我们对我们的数据调用所描述的方法。*****

```py
*****data.describe()*****
```

*****![Statistical information](img/36b9da739cdb12fcfbbc081867c94e6e.png)*****

*****这个方法给了我们一些关于数据的统计信息。我们现在可以检查数据的头部。*****

```py
*****data.head()*****
```

*****![Data Head](img/c6251fdd4dad6309c0708f404e0f7ab9.png)*****

*****我们将创建一个基于动力的战略。我们可以看到每隔 3 分钟就有一次数据。买入和卖出的交易量可以提供一些短期动力的信息。让我们创建一个 delta 柱，我们的出价量减去我们的要价量，并将其与收盘价进行比较，看看是否有一些关系。我们将首先复制我们的数据，然后添加我们的 delta 列。*****

```py
*****#making copy of our data
es=data.copy()
#creating delta column
es['Delta']=es[' BidVolume']-es[' AskVolume']*****
```

*****现在让我们重新检查我们的数据头部，并创建一个回归图。*****

```py
*****es.head()*****
```

*****![Recheck head of data](img/f4d8dab084e03beed5e03ef7ba4837c0.png)*****

```py
*****#creating regression plot
sns.lmplot('Delta',' Close',data=es)
plt.title('ES Regression Delta to Close')*****
```

```py
*****<matplotlib.text.Text at 0x16b7bae3080>*****
```

*****![ES Regression Delta to Close](img/663bbc04d227c41674d0c3cb616c1c8f.png)*****

*****现在我们已经了解了我们的 delta 和收盘价之间的关系，让我们画一个 delta 的分布图。*****

```py
*****#creating distribution of delta
sns.distplot(es['Delta'])
plt.title('ES Delta Distribution')*****
```

```py
*****<matplotlib.text.Text at 0x16b7bbb3550>*****
```

*****![ES Delta Distribution](img/ba3f02395a20906aa1e12d3fcfeaa599.png)*****

*****现在，我们将向数据中添加一个范围列，并查看每个条形的范围与增量之间的关系。*****

```py
*****#adding our range column
es['Range']=es[' High']-es[' Low']*****
```

```py
*****#rechecking the head of our data
es.head()*****
```

*****![Add range column](img/c09aaae834fd67fbca9e8181652db3e0.png)*****

*****现在我们可以创建一个 delta 和数据范围的散点图。*****

```py
*****sns.jointplot(es['Delta'], es['Range'])*****
```

```py
*****<seaborn.axisgrid.JointGrid at 0x16b7ee09470>*****
```

*****![Scatter Plot](img/e6f571f464e224c58cf4d2b991651e34.png)*****

*****现在我们来看看每根棒线交易次数的分布。*****

```py
*****#creating number of trades distribution
sns.distplot(es[' NumberOfTrades'],bins=100)*****
```

```py
*****<matplotlib.axes._subplots.AxesSubplot at 0x16b7ef2bc18>*****
```

*****![Distribution of Trades](img/6bea858e88cbc53f7abefd024db6da3c.png)*****

*****现在我们已经从探索性数据分析中获得了一些数据，我们准备使用 RSI 指标创建我们的日内动量策略。我们将把我们的策略包装在一个类中，该类允许我们创建策略的不同实例，而不必重写相同的逻辑。*****

```py
*****class rsi_strategy(object):

 def __init__(self,data,n,data_name,start,end):

   self.data=data #the dataframe
   self.n=n #the moving average
   self.data_name=data_name #the name that will appear on plots
   self.start=start #the beginning date of the sample period
   self.end=end #the ending date of the sample period

def generate_signals(self):

   delta=self.data[' Close'].diff()
   dUp,dDown=delta.copy(),delta.copy()
   dUp[dUp<0]=0
   dDown[dDown>0]=0
   RolUp=dUp.rolling(self.n).mean()
   RolDown=dDown.rolling(self.n).mean()

   #assigning indicator to the dataframe
   self.data['RSI']=np.where(RolDown!=0, RolUp/RolDown,1)
   self.data['RSI_Slow']=self.data['RSI'].rolling(self.n).mean()

   #creating signals
   self.data=self.data.assign(Signal=pd.Series(np.zeros(len(self.data))).values)
   self.data.loc[self.data['RSI']<self.data['RSI_Slow'],'Signal']=1
   self.data.loc[self.data['RSI']>self.data['RSI_Slow'], 'Signal']=-1

   return

def plot_performance(self,allocation):
    #intializing a variable for initial allocation
    #to be used to create equity curve
    self.allocation=allocation

    #creating returns and portfolio value series
    self.data['Return']=np.log(self.data[' Close']/self.data[' Close'].shift(1))
    self.data['S_Return']=self.data['Signal'].shift(1)*self.data['Return']
    self.data['Market_Return']=self.data['Return'].expanding().sum()
    self.data['Strategy_Return']=self.data['S_Return'].expanding().sum()
    self.data['Portfolio Value']=((self.data['Strategy_Return']+1)*self.allocation)

    #creating metrics
    self.data['Wins']=np.where(self.data['S_Return'] > 0,1,0)
    self.data['Losses']=np.where(self.data['S_Return']<0,1,0)
    self.data['Total Wins']=self.data['Wins'].sum()
    self.data['Total Losses']=self.data['Losses'].sum()
    self.data['Total Trades']=self.data['Total Wins'][0]+self.data['Total Losses'][0]
    self.data['Hit Ratio']=round(self.data['Total Wins']/self.data['Total Losses'],2)
    self.data['Win Pct']=round(self.data['Total Wins']/self.data['Total Trades'],2)
    self.data['Loss Pct']=round(self.data['Total Losses']/self.data['Total Trades'],2)

    #Plotting the Performance of the RSI Strategy

    plt.plot(self.data['Market_Return'],color='black', label='Market Returns')
    plt.plot(self.data['Strategy_Return'],color='blue', label= 'Strategy Returns')
    plt.title('%s RSI Strategy Backtest'%(self.data_name))
    plt.legend(loc=0)
    plt.tight_layout()
    plt.show()

    plt.plot(self.data['Portfolio Value'])
    plt.title('%s Portfolio Value'%(self.data_name))
    plt.show()*****
```

*****好吧。现在让我们试试我们的 *rsi_strategy* 类。*****

```py
*****#creating an instance of our strategy class
strat1=rsi_strategy(es,10,'ES',es['Date'][0],es['Date'].iloc[-1])*****
```

*****既然我们有了 RSI 策略的实例，我们现在可以调用生成信号和绘制性能方法来查看我们的策略的执行情况。*****

```py
*****#generating signals
strat1.generate_signals()*****
```

```py
*****#plotting performance of our strat1 strategy
#passing in an allocation amount of $10,000
strat1.plot_performance(10000)*****
```

*****![ES RSI Strategy Backtest](img/91ba65a8980b77119e26d36e11cacf87.png)*****

*****![ES Portfolio Value](img/0768873dd555613ef1579432df9a929d.png)*****

*****现在我们已经构建了策略，我们可以使用编码到策略类中的功能来检查它的一些指标。我们将检查我们的命中率、胜率和失败率。*****

```py
*****#checking our Hit Ratio
strat1.data['Hit Ratio'][0]*****
```

```py
*****0.93000000000000005*****
```

*****这个命中率告诉我们，我们的策略目前的胜败比不到 1 比 1。现在让我们检查我们的赢输百分比。*****

```py
*****#checking our win percentage
print('Strategy Win Percentage')
strat1.data['Win Pct'][0]*****
```

```py
*****Strategy Win Percentage
0.47999999999999998*****
```

```py
*****#checking our loss percentage
print('Strategy Loss Percentage')
strat1.data['Loss Pct'][0]*****
```

```py
*****Strategy Loss Percentage
0.52000000000000002*****
```

*****我们还可以检查我们的总盈亏数，以及我们的策略的总交易数。*****

```py
*****#checking total number of wins
strat1.data['Total Wins'][0]*****
```

```py
*****10818*****
```

```py
*****#checking total number of losses
strat1.data['Total Losses'][0]*****
```

```py
*****11613*****
```

```py
*****#checking total number of trades
strat1.data['Total Trades'][0]*****
```

```py
*****22431*****
```

*****在这一点上，我们已经对我们的数据进行了探索性的数据分析，创建了我们的日内动量策略，并查看了我们策略的指标。我们的策略目前的命中率不到 1。我们的胜率约为 48%，亏损率为 52%。从表面上看，这并不令人印象深刻。*****

*****我们如何改进我们的战略，以便我们能够从中获利？*****

*****即使我们输的比赢的稍微多一点，如果我们能有效地消除一些亏损的交易，我们就能反过来重新调整我们的盈亏百分比和命中率。换句话说，我们的成功交易不是问题。实际上，赢得 48%的时间比赢得少于 48%的金额要好。问题是，考虑到我们总交易的分布，我们赢的不够多。如果我们几乎消除了所有亏损的交易，会怎么样？我们的交易会少很多，但我们的胜率会飙升，这样我们就可以交易策略获利。*****

*****正确识别问题或任务是任何机器学习应用程序的关键技能。我们将利用 QDA 来改进我们现有的战略。我们的目标是能够预测我们的策略何时可能在亏损交易发生之前进行亏损交易，以便我们能够消除亏损交易，从而重新平衡我们的盈亏百分比。听起来很有趣！我们开始吧！*****

## *******使用 QDA 优化日内动量策略*******

*****现在我们将使用 QDA 作为改进我们日内动量策略的一种手段。我们先从 sklearn 导入必要的库开始。*****

```py
*****from sklearn.discriminant_analysis import QuadraticDiscriminantAnalysis
from sklearn.metrics import confusion_matrix, classification_report*****
```

*****我们需要一种方法来确定我们什么时候可能进行亏损交易。嗯……我们给数据添加一个分类返回列怎么样。然后我们可以做一点[特征工程](https://quantra.quantinsti.com/course/data-and-feature-engineering-for-trading)并使用我们的 QDA 分类器来预测分类返回值。一旦我们完成了这个，我们就可以通过把我们的预测反馈给我们的策略来测试我们的想法，看看这是否能提高我们策略的性能。*****

*****我们将从复制我们的战略数据框架开始。回想一下，这是我们构建战略的初始实施时创建的数据框架。*****

```py
*****df=strat1.data*****
```

*****让我们检查一下数据帧的头部。*****

```py
*****df.head()*****
```

*****![Head of dataframe](img/94db624b2555398cc1df502731485afe.png)*****

*****现在让我们添加我们的分类返回列。*****

```py
*****#adding column to hold the direction of returns
df['Return Direction']=np.where(df['Strategy_Return']>0,'Up',np.where(df['Strategy_Return']<0,'Down',"Flat"))*****
```

*****让我们在返回方向列上调用我们的 head 和 tail 方法。*****

```py
*****df['Return Direction'].head()*****
```

```py
*****0 Flat
1 Flat
2 Flat
3 Flat
4 Flat
Name: Return Direction, dtype: object*****
```

```py
*****df['Return Direction'].tail()*****
```

```py
*****28022 Down
28023 Down
28024 Down
28025 Down
28026 Down
Name: Return Direction, dtype: object*****
```

*****现在我们已经添加了返回方向列，我们可以开始考虑我们应该使用什么特征来预测我们的策略亏损的概率。我们可以利用标的的波动性，因为它应该对我们的策略有一些影响。我们还可以使用不同的波动滞后来捕捉动量的演变。我们也可以使用我们的 RSI 指标。好吧。让我们把这些加到我们的数据框里。*****

*****你可能想知道为什么我们不用我们的信号发生器。我们希望以一种可以应用于任何市场环境的方式来训练我们的模型。在任何给定的时间，在各种市场条件下，我们的多头和空头可能会有不同的分布。例如，如果我们在牛市中，我们更有可能得到做多信号而不是做空信号。与我们的短期交易相比，我们的长期交易也更有可能获得更大程度的盈利。如果我们训练我们的模型来预测我们的信号发生器在此期间的亏损交易，它会将长信号与收益递增相关联，将短信号与收益递减相关联。虽然目前这可能是真的，但将来当我们进入熊市时，这个模型会有很大的偏差，不能预测我们亏损的交易。*****

```py
*****#adding our features
#creating volatility
strat1.data['Vol']=strat1.data[' Close'].rolling(window=5).std()
#creating lags of volatility
strat1.data['Vol Lag 3']=strat1.data['Vol'].shift(3)
strat1.data['Vol Lag 4']=strat1.data['Vol'].shift(4)
strat1.data['Vol Lag 5']=strat1.data['Vol'].shift(5)*****
```

*****好吧，让我们暂停一下，确保我们明白这里发生了什么。我们首先对日内数据进行了一些探索性的数据分析。我们的目标是使用 RSI 指标创建一个日内交易策略。我们创建了一个类，允许我们创建动量策略的实例。我们对我们战略的表现并不感到兴奋，但我们确实认识到它有一些潜力。*****

*****我们的策略目前的赢亏比不到 1。它目前赢了 48%的时间，输了 52%的时间。我们的前提是，如果我们可以消除一些亏损的交易，从而减少一些交易，我们就可以将我们的策略盈利的可能性转变为对我们有利。事实上，我们只赢了 48%的时间不是真正的问题。如果我们只进行这些交易，同时将总交易量减半，我们就有了一个完美的(理论上的)策略。换句话说，我们需要一种定量的方法来改进我们的策略，以便它可以实际用于生产。*****

*****为了实现我们的目标，我们必须能够预测何时我们的策略可能会进行可能会亏损的交易。因此，我们创建了回报方向栏来跟踪我们的交易是赢了还是输了。我们需要可以在我们的训练模型中使用的特征，这些特征可以提供一些亏损交易概率的指示。我们选择了波动性滞后和我们的 RSI，在上面的代码块中，我们添加了波动性及其滞后。请注意，我们是在“ *strat1.data* ”而不是“ *es* ”数据帧上做的。strat1.data 是我们在制作动量策略的 strat1 实例时创建的数据框架。我们简单地将在我们的类中创建的“*数据*”数据帧命名为 dataframe，并将我们的特征存储在其中。这样做的目的是因为我们正在优化保持我们回报的战略 1 动量策略。回想一下，我们的 es 数据框架只保存我们传递到策略中的数据。*****

*****一旦我们创建了 QDA 模型，我们可以将其预测存储在 es 数据框架的副本中，然后创建第二个动量策略实例并比较结果。我们需要稍微改变一下我们的类，这样它就可以在交易之前读取我们的预测。所以本质上，只有当我们的 QDA 模型预测交易不太可能是亏损交易时，我们的策略才会交易。*****

*****现在我们有了我们的特性，我们可以初始化我们的 X 和 y 变量，并进行我们的训练测试分割。让我们复制我们的 strat1.data 数据帧并检查它的头。*****

```py
*****#copying our strategy dataframe
df=strat1.data.copy()*****
```

```py
*****#checking the head of our df dataframe
df.head()*****
```

*****![Check Head of dataframe](img/cec1df617b035698e994fb8a04aa2183.png)*****

*****为了确保我们使用所有适当的列，让我们在 dataframe 上调用 info 方法。*****

```py
*****df.info()*****
```

```py
*****<class 'pandas.core.frame.DataFrame'>
RangeIndex: 28027 entries, 0 to 28026
Data columns (total 33 columns):
Date              28027 non-null object
 Time             28027 non-null object
 Open             28027 non-null float64
 High             28027 non-null float64
 Low              28027 non-null float64
 Close            28027 non-null float64
 Volume           28027 non-null int64
 NumberOfTrades   28027 non-null int64
 BidVolume        28027 non-null int64
 AskVolume        28027 non-null int64
Delta             28027 non-null int64
Range             28027 non-null float64
RSI               28017 non-null float64
RSI_Slow          28008 non-null float64
Signal            28027 non-null float64
Return            28026 non-null float64
S_Return          28026 non-null float64
Market_Return     28026 non-null float64
Strategy_Return   28026 non-null float64
Portfolio Value   28026 non-null float64
Wins              28027 non-null int32
Losses            28027 non-null int32
Total Wins        28027 non-null int64
Total Losses      28027 non-null int64
Total Trades      28027 non-null int64
Hit Ratio         28027 non-null float64
Win Pct           28027 non-null float64
Loss Pct          28027 non-null float64
Return Direction  28027 non-null object
Vol               28023 non-null float64
Vol Lag 3         28020 non-null float64
Vol Lag 4         28019 non-null float64
Vol Lag 5         28018 non-null float64
dtypes: float64(20), int32(2), int64(8), object(3)
memory usage: 6.8+ MB*****
```

*****现在，我们可以清楚地看到我们所有的列。我们的 X 或特征将是我们的波动和 RSI 的滞后，我们的 y 或响应将是我们的回报方向柱。我们现在可以初始化变量了。*****

```py
*****#initializing features
X=df[['Vol Lag 3','Vol Lag 4','Vol Lag 5', 'RSI']]*****
```

```py
*****#initialing our response
y=df['Return Direction']*****
```

```py
*****#checking the head of our features
X.head()*****
```

*****![Check Head of Features](img/b5a5edbd9ca48dd65a933d630d667b24.png)*****

*****我们现在可以将数据分成训练集和测试集。我们将从 sklearn 导入*训练*测试*分割*来做这件事。*****

```py
*****from sklearn.model_selection import train_test_split*****
```

*****现在我们准备使用我们的训练*测试*分割方法。*****

```py
*****#initializing training and testing variables
X_train,X_test,y_train,y_test=train_test_split(X,y,test_size=0.2)*****
```

*****既然我们已经将我们的数据分割成 80/20 的训练测试分割，我们可以初始化我们的 QDA 模型并使其适合我们的数据。*****

```py
*****model=QuadraticDiscriminantAnalysis()*****
```

*****在拟合训练数据之前，我们需要填充空值。*****

```py
*****#fitting model to our training data
#and filling null values with 0
model.fit(X_train.fillna(0),y_train)*****
```

```py
*****QuadraticDiscriminantAnalysis(priors=None, reg_param=0.0,
     store_covariances=False, tol=0.0001)*****
```

*****现在我们已经拟合了我们的模型，我们可以通过传递我们的 *X *测试*数据来使用它进行预测。这些数据是我们的模型还没有看到的特征。然后，我们可以将我们的模型做出的预测与 *y* 测试*数据，或者我们反应的实际值进行比较。*****

```py
*****#creating predictions
predictions=model.predict(X_test.fillna(0))*****
```

*****现在，我们将使用混淆矩阵和分类报告来评估我们的模型表现如何。*****

```py
*****#initializing confusion matrix
print('Confusion Matrix:')
print(confusion_matrix(y_test,predictions))*****
```

```py
*****Confusion Matrix:
[[4902 6 242]
[ 2 0 0]
[ 399 0 55]]*****
```

```py
*****#initializing classification report
print('Classification Report')
print(classification_report(y_test,predictions))*****
```

```py
*****Classification Report
      precision recall f1-score support
Down     0.92    0.95    0.94    5150
Flat     0.00    0.00    0.00       2
Up       0.19    0.12    0.15     454
avg / total 0.86 0.88 0.87 5606*****
```

*****哇！我们的模型能够以 92%的准确率预测亏损交易。*****

*****我们现在可以将我们的预测添加回我们的 es 数据帧，然后将其传递回我们的 rsi_strategy 类，以创建一个 strat2 实例，并将我们的指标与我们的 strat1 指标进行比较。*****

*****在将我们的预测添加到我们的 es 数据框架之前，让我们重新检查一下。我们将在数据帧上调用 head 方法。*****

```py
*****#rechecking the head of our es data
es.head()*****
```

*****![Rechecking Head of ES Data](img/32d607acf263b50ae2533256f2c67c67.png)*****

*****现在让我们把我们的预测添加到我们的 es 数据框架中。*****

*****回想一下，为了构建我们的 QDA 模型，我们必须进行 80-20 列车测试划分。这意味着我们在 80%的 es 数据上训练我们的模型，并在 20%上测试它。这也意味着我们只对 20%的数据进行了预测，因此我们预测的长度与 es 数据帧的长度不匹配。*****

*****假设我们从分类报告和混淆矩阵中知道我们的模型是有效的，我们要做的是使我们的模型适合我们所有的 es 数据，这样我们就可以得到对另外 80%数据的预测，并能够将它们添加到我们的 es 数据框架中。*****

*****我们将初始化第二个预测变量，并将整个 X 传递给我们的模型。*****

```py
*****#initializing second predictions variable for es dataframe
predictions_2=model.predict(X.fillna(0))*****
```

*****现在，我们准备将我们的预测添加到 es 数据框架中，以便将其传递到我们的 *rsi_strategy* 中。*****

```py
*****#adding our QDA model's predictions to our es dataframe
es['Predictions']=predictions_2*****
```

*****好了，现在我们已经把我们的预测存储在我们的 es 数据框架中了。现在我们可以重新调整我们的策略，这样如果我们预测“*下跌*”，或者换句话说，如果我们的模型预测亏损，我们就不交易。让我们将这个额外的逻辑添加到我们的类中。*****

```py
*****class optimized_rsi(object):

def __init__(self,data,n,data_name,start,end):

    self.data=data #the dataframe
    self.n=n #the moving average
    self.data_name=data_name #the name that will appear on plots
    self.start=start #the beginning date of the sample period
    self.end=end #the ending date of the sample period

def generate_signals(self):

    delta=self.data[' Close'].diff()
    dUp,dDown=delta.copy(),delta.copy()
    dUp[dUp<0]=0 dDown[dDown>0]=0
    RolUp=dUp.rolling(self.n).mean()
    RolDown=dDown.rolling(self.n).mean()

    #assigning indicator to the dataframe
    self.data['RSI']=np.where(RolDown!=0, RolUp/RolDown,1)
    self.data['RSI_Slow']=self.data['RSI'].rolling(self.n).mean()

    #creating signals;
    #altering the signal generator by going through our predictions
    #and reinitializing signals to 0 whose prediction is down
    self.data=self.data.assign(Signal=pd.Series(np.zeros(len(self.data))).values)
    self.data['QDA Signal']=np.zeros(len(self.data))

    self.data.loc[self.data['RSI']<self.data['RSI_Slow'],'Signal']=1 self.data.loc[self.data['RSI']>self.data['RSI_Slow'], 'Signal']=-1

    self.data['QDA Signal']=np.where(self.data['Predictions']=="Down",0,self.data['Signal'])

    return

def plot_performance(self,allocation):
    #intializing a variable for initial allocation
    #to be used to create equity curve
    self.allocation=allocation

    #creating returns and portfolio value series
    self.data['Return']=np.log(self.data[' Close']/self.data[' Close'].shift(1))
    #using our signal 2 column to calcuate returns instead of signal 1 column
    self.data['S_Return']=self.data['QDA Signal'].shift(1)*self.data['Return']
    self.data['Market_Return']=self.data['Return'].expanding().sum()
    self.data['Strategy_Return']=self.data['S_Return'].expanding().sum()
    self.data['Portfolio Value']=((self.data['Strategy_Return']+1)*self.allocation)

    #creating metrics
    self.data['Wins']=np.where(self.data['S_Return'] > 0,1,0)
    self.data['Losses']=np.where(self.data['S_Return']<0,1,0)
    self.data['Total Wins']=self.data['Wins'].sum()
    self.data['Total Losses']=self.data['Losses'].sum()
    self.data['Total Trades']=self.data['Total Wins'][0]+self.data['Total Losses'][0]
    self.data['Hit Ratio']=round(self.data['Total Wins']/self.data['Total Losses'],2)
    self.data['Win Pct']=round(self.data['Total Wins']/self.data['Total Trades'],2)
    self.data['Loss Pct']=round(self.data['Total Losses']/self.data['Total Trades'],2)

    #Plotting the Performance of the RSI Strategy

    plt.plot(self.data['Market_Return'],color='black', label='Market Returns')
    plt.plot(self.data['Strategy_Return'],color='blue', label= 'Strategy Returns')
    plt.title('%s RSI Strategy Backtest'%(self.data_name))
    plt.legend(loc=0)
    plt.tight_layout()
    plt.show()

    plt.plot(self.data['Portfolio Value'])
    plt.title('%s Portfolio Value'%(self.data_name))
    plt.show()*****
```

*****既然我们已经改变了我们的信号发生器来解释我们的 QDA 模型的预测，让我们初始化我们的 strat2 对象，并将我们的性能与我们的 strat1 策略进行比较。*****

```py
*****#initializing our strat2 strategy
strat2=optimized_rsi(es,10,'ES',es.iloc[0]['Date'],es.iloc[-1]['Date'])*****
```

```py
*****#generating signals
strat2.generate_signals()*****
```

*****既然我们有了基于 QDA 模型预测的信号，我们可以调用 plot_performance 方法来创建我们的权益曲线，然后比较我们两个策略实施的指标。*****

```py
*****#plotting performance
strat2.plot_performance(10000)*****
```

*****![ES RSI Strategy Backtest 2](img/801ff0f41e48f86fb80e9957e28e9bc9.png)*****

*****![ES Portfolio Value 2](img/7728fccef38cc02ab7abee1ade96a4ed.png)*****

*****现在，我们已经创建了动量策略的第二个实例，我们可以计算我们的指标并比较我们的 strat1 策略。*****

```py
*****#generating metrics
strat2_trades=strat2.data['Total Trades'][0]
strat2_hit_ratio=strat2.data['Hit Ratio'][0]
strat2_win_pct=strat2.data['Win Pct'][0]
strat2_loss_pct=strat2.data['Loss Pct'][0]*****
```

```py
*****#printing strat2 metrics
print('Strat 2 Hit Ratio:',strat2_hit_ratio)
print('Strat 2 Win Percentage:',strat2_win_pct)
print('Strat 2 Loss Percentage:',strat2_loss_pct)
print('Strat 2 Total Trades:',strat2_trades)*****
```

```py
*****Strat 2 Hit Ratio: 0.97
Strat 2 Win Percentage: 0.49
Strat 2 Loss Percentage: 0.51
Strat 2 Total Trades: 1323*****
```

*****让我们回顾一下我们的战略 1 指标。*****

```py
*****#getting strat1 metrics
strat1_trades=strat1.data['Total Trades'][0]
strat1_hit_ratio=strat1.data['Hit Ratio'][0]
strat1_win_pct=strat1.data['Win Pct'][0]
strat1_loss_pct=strat1.data['Loss Pct'][0]*****
```

```py
*****#printing our strat1 metrics
print('Strat 1 Hit Ratio:',strat1_hit_ratio)
print('Strat 1 Win Percentage:',strat1_win_pct)
print('Strat 1 Loss Percentage:',strat1_loss_pct)
print('Strat 1 Total Trades:',strat1_trades)*****
```

```py
*****Strat 1 Hit Ratio: 0.93
Strat 1 Win Percentage: 0.48
Strat 1 Loss Percentage: 0.52
Strat 1 Total Trades: 22431*****
```

*****好吧，有趣的事情发生了。回想一下，我之前说过，我们只赢了 48%的概率并不是问题，问题是转移概率，限制我们的亏损交易。这就是我们建立 QDA 模型的原因，这样我们就可以很有把握地预测什么时候我们可能会进行亏损的交易。*****

*****请注意，我们的指标略有变化。*****

*   *****我们的 strat2 命中率确实有所提高，从 strat1 的. 93 提高到了. 97。*****
*   *****我们的战略 2 的盈利百分比从战略 1 的 0.48 增加到了 0.49，这也相当于战略 2 的亏损百分比为 0.51，战略 1 的亏损百分比为 0.52。*****

*****注意我们交易数量的显著差异。与我们的 strat2 实例相比，我们在 strat1 实例中进行了更多的交易。*****

*****这直接影响到我们的策略成功生产的可能性。我们使用 QDA 模型有效地消除了许多对我们的策略构成问题的交易。另外，看看我们的 strat1 和 strat2 实例的权益曲线。*****

*   *****我们的 strat1 实例结束时的投资组合价值约为 9600。*****
*   *****我们的 strat2 实例在期末的投资组合价值为 10，200 英镑，这低于它的启动阶段，但仍然是对 strat1 实例的重大改进。*****

*****考虑到我们的盈利和亏损百分比的微小变化，这是很重要的，并表明还有其他因素在交易策略的盈利能力中发挥着重要作用。如果你仔细观察这一时期的末期，你可以看到我们的 QDA 模型的真实效果。在我们的 strat1 实例中，接近期末时，我们只是直线抛售。但是看一下我们在同一时间段的 strat2 实例，我们实际上显著改进了我们的交易。*****

*****当然，相对于这一策略，在我们所学的基础上还可以做更多的事情。但是，这个实验已经证明，这里提出的框架是一个可行的优化日内交易策略。不可否认，这篇文章中提出的策略被设计成有缺陷，以测试使用 QDA 进行优化的想法。换句话说，我并没有试图优化这个策略，只是想要一个显示出一些潜力的策略，就像你现在正在做的一样。所以想象一下，你可以用这个框架和一个你实际上正在尝试投入生产的策略做些什么。*****

## *******回顾*******

*****我们在这篇文章中已经介绍了很多，希望你能从中获得一些有助于你制定战略的见解。*****

*****我们首先了解了什么是 QDA，并研究了模型背后的一些数学原理。我们回顾了之前在 LDA 上的 [**帖子中所学到的内容，并与 QDA 的帖子进行了比较。我们导入了一些 eMini S & P 500 的日内数据，目的是创建一个日内动量策略，并使用 QDA 来改进我们的策略。在构建我们的策略之前，我们做了一些探索性的数据分析，以更多地了解我们的数据集。**](/linear-discriminant-analysis-quantitative-portfolio-management/)*****

*****我们使用面向对象编程来设计我们的 RSI 策略，这种方式允许我们重用我们的代码并创建多个策略实例。在创建了我们的第一个策略实例之后，我们发现我们的策略还没有准备好投入生产，但是显示出了一些潜在的迹象。然后，我们的目标是建立一个 QDA 模型来预测我们可能在什么时候进行亏损交易，以努力将我们的策略转化为对我们有利的策略。*****

*****我们在数据中增加了一个分类栏“回报方向”,并设计了波动率的特征“滞后 3”、“滞后 4”、“滞后 5 ”,以及用于 QDA 模型的相对强弱指数。我们的 QDA 模型显示，预测亏损交易的准确率为 92%。然后，我们将预测应用到数据中，并创建了一个 strat2 实例。虽然我们的盈利和亏损百分比变化不大，但我们的回报增加了 600 美元，而且我们的 strat2 实例，与我们的 strat1 实例不同，实际上是正的。*****

*****我们的研究表明，我们的日间机器学习优化框架对于增加我们的策略投入生产的可能性是可行的。我们还可以做更多的事情来改进这一策略，但我们已经传达了总体想法。*****

## *******挑战:在 Twitter 上给我们发一张你的股票曲线快照*******

*****See if you can further build upon the framework presented in this post. Play with the code to see how you might improve this model. Be sure to download the data used in this post via the CSV file below.**********As a bonus, review the post "**[Using Linear Discriminant Analysis For Quantitative Portfolio Management](https://blog.quantinsti.com/linear-discriminant-analysis-quantitative-portfolio-management/)**" and see if you can incorporate that framework into what was covered in this post.**********We'd love to see what you create. Tweet us a snapshot of your strategy's equity curve at [@QuantInsti on Twitter](https://twitter.com/QuantInsti). Be sure and use the hashtag **#QDA**.*****

## *******接下来的步骤*******

*****If you're interested in learning more about Machine Learning for Trading, Quantinsti offers both a self-paced option, via our Quantra Online Learning Portal, and a comprehensive quantitative trading regimen, the Executive Program in Algorithmic Trading (EPAT).**********The EPAT program is administered over the course of 6months and covers topics such as Statistics and Econometrics, Quantitative Trading Strategies, Programming in Python and R, as well as Machine Learning. The faculty of the program are current quants with different backgrounds and thus ensures participants that the content will be relevant to the current market and industry environment. If you would like to learn more you may visit us [**here**](https://www.quantinsti.com/).**********If you prefer to learn on your own time and at your own pace, [Quantra](https://www.quantra.quantinsti.com) is a good learning option for you. Through Quantra you'll can lifetime access to courses such as Introduction to Machine Learning for Trading, Trading with Machine Learning: Classification and SVM, and more. To learn more you can visit us [**here**](https://www.quantra.quantinsti.com).*****

******免责声明:股票市场的所有投资和交易都有风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。******

### *******下载数据文件*******

*   *****数据 CSV 文件*****
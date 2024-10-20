# Python 中用于对选择的 k 均值聚类算法

> 原文：<https://blog.quantinsti.com/k-means-clustering-pair-selection-python/>

拉马克斯·科尔曼

从在你浏览过的文章末尾显示相关文章，到根据你的浏览习惯创建个性化推荐，你会惊讶于你已经与 K-means 算法交互了多少次，而你甚至没有意识到。上面的例子只是日常生活中的例子。当你把目光转向庞大的行业本身时，你会发现这种算法无处不在。定制新闻源、使用相似模式的 bot 或欺诈检测、基于需求和供应预测的库存管理、图像识别，这些只是使用 K-means 算法的几个例子。

[![Python Basics Handbook](img/740388889e6405dfac04c53fbf13b051.png)T4】](https://www.quantinsti.com/python-basics-handbook)

在本文中，我们将涵盖以下几点:

*   [什么是 K 均值聚类](#what)
*   [没有 K-Means 的生活](#life)
*   [理解 K-Means](#und)
*   [使用 K-Means 构建 StatArb 策略](#bul)
*   [K-表示 StatArb 实现](#imp)

我们开始吧！

## 什么是 K-Means 聚类？

K-Means 聚类是一种无监督的机器学习，它根据相似性对数据进行分组。回想一下，在监督机器学习中，我们为算法提供了我们希望它与标签或我们希望它预测或分类的结果相关联的特征或变量。在无监督的机器学习中，我们只为模型提供特征，然后它自己“学习”关联。

K-Means 是一种在数据集中寻找子组的技术。K-Means 与其他聚类方法的一个区别是，在 K-Means 中，我们有预定数量的聚类，而其他一些技术不需要我们预先定义聚类的数量。

该算法首先将每个数据点随机分配到一个特定的聚类中，任何两个聚类中都没有一个数据点。然后，它计算这些点的质心或平均值。

该算法的目的是减少总的组内变化。换句话说，我们希望将每个点放入一个特定的聚类中，测量距该聚类质心的距离，然后取这些距离的平方和，以获得总的聚类内变化。我们的目标是降低这个值。

分配数据点和计算平方距离的过程继续进行，直到聚类的组成不再有变化，或者换句话说，我们已经最佳地减少了聚类内的变化。

在交易界，如果你想知道 k-means 的重要性，除了统计套利的实现，你不必看得更远。

[统计套利](/statistical-arbitrage/)是最具辨识度的[量化交易策略量化模型](https://quantra.quantinsti.com/course/quantitative-trading-strategies-models)之一。虽然存在几种变化，但基本前提是，尽管两种证券是随机游走的，但它们的关系不是随机的，因此产生了交易机会。实施任何形式的统计套利的一个关键问题是对选择的过程。

先不使用 k-means 尝试实现统计套利。

## 没有 K 均值的生活

为了理解为什么我们可能想要使用 K-均值来解决配对选择的问题，我们将尝试实现一个统计套利，就好像没有 K-均值一样。这意味着我们将尝试开发一个强力解决方案来解决我们的配对选择问题，然后在我们的统计套利策略中应用这个解决方案。

让我们花点时间想想为什么 k 线可以用来交易。使用 K-Means 形成可能对的子群有什么好处？我是说我们不能自己想出一对吗？

**推荐阅读:** [配对交易基础知识:相关性、协整性和策略](https://blog.quantinsti.com/pairs-trading-basics/)

**这是一个很好的问题，毫无疑问，你可能想知道。为了更好地理解使用像 K-Means 这样的技术进行统计套利的优势，如果没有 K-Means，我们将演练一次交易统计套利策略。可以这么说，我将是你过去交易的幽灵。**

**首先，让我们确定任何统计套利交易策略的关键组成部分。**

1.  **我们必须识别具有可交易关系的资产**
2.  **我们必须计算这些资产分布的 Z 值，以及头寸规模的对冲比率**
3.  **当 Z 分数超过某个上限或下限时，我们会做出买卖决定**

**首先，我们需要一些对子进行交易。但是我们不能在不知道我们选择的货币对是否协整的情况下进行统计套利交易。协整仅仅意味着我们的两个资产之间的统计性质是稳定的。即使这两种资产随机移动，我们也可以指望它们之间的关系是恒定的，或者至少在大多数时间是恒定的。**

**传统上，在解决配对选择问题时，在没有 K-Means 的世界中，我们必须通过蛮力，或者试错法来找到配对。这通常是通过将仅仅属于同一部门或行业的股票组合在一起实现的。这个想法是，如果这些股票属于相似行业的公司，因此它们的经营有相似之处，它们的股票也应该有相似的走势。但是，正如我们将要看到的，情况并不一定如此。**

**第一步是想出一些应该产生交易关系的股票对。我们将使用标准普尔 500 的股票，但这一过程可以应用于任何指数中的任何股票。嗯，沃尔玛和塔吉特怎么样？他们都是零售商和直接竞争对手。当然，它们应该是协整的，这样我们就可以用统计套利策略进行交易。**

**让我们从导入必要的库以及我们将需要的数据开始。我们将 2014-2016 年作为我们的分析期。**

```py
#importing necessary libraries
#data analysis/manipulation
import numpy as np
import pandas as pd
#importing pandas datareader to get our data
import pandas_datareader as pdr
#importing the Augmented Dickey Fuller Test to check for cointegration
from statsmodels.tsa.api import adfuller
```

**现在我们有了自己的图书馆，让我们获取数据。**

```py
#setting start and end dates
start='2014-01-01'
end='2916-01-01'
#importing Walmart and Target using pandas datareader
wmt=pdr.get_data_yahoo('WMT',start,end)
tgt=pdr.get_data_yahoo('TGT',start,end)
```

**在测试我们两只股票的协整性之前，让我们看看它们在这段时间的表现。我们将创建一个沃尔玛和塔吉特的情节。**

```py
#Creating a figure to plot on
plt.figure(figsize=(10,8))
#Creating WMT and TGT plots
plt.plot(wmt["Close"],label='Walmart')
plt.plot(tgt[‘Close'],label='Target')
plt.title('Walmart and Target Over 2014-2016')
plt.legend(loc=0)
plt.show()
```

**![](img/e619daf89858034c9974092375a0b27f.png)**

**在上面的剧情中，我们可以看到 2014 年年初的一点关联。但这并没有真正让我们清楚沃尔玛和塔吉特之间的关系。为了明确这两只股票之间的关系，我们将创建一个关联热图。**

**为了开始创建我们的关联[热图](/creating-heatmap-using-python-seaborn/)，我们必须首先将沃尔玛和目标价格放在同一个数据框架中。让我们为我们的股票创建一个新的数据框架。**

```py
#initializing newDF as a pandas dataframe
newDF=pd.DataFrame()
#adding WMT closing prices as a column to the newDF
newDF['WMT']=wmt['Close']
#adding TGT closing prices as a column to the newDF
newDF['TGT']=tgt['Close']
```

**现在我们已经创建了一个新的数据框架来保存我们的沃尔玛和目标股票价格，让我们来看看它。**

```py
newDF.head()
```

**![](img/6667236d90f7c73300a838bf0442ea58.png)**

**我们可以看到，我们有两个股票的价格在一个地方。我们现在准备创建我们股票的关联热图。为此，我们将使用 [python 的 Seaborn](https://blog.quantinsti.com/creating-heatmap-using-python-seaborn/) 库。回想一下，我们之前将 Seaborn 作为 sns 导入。**

```py
#using seaborn as sns to create a correlation heatmap of WMT and TGT
sns.heatmap(newDF.corr())
```

**![](img/56a08158ebd6c53d2eb3a321bd7fa6b0.png)**

**在上面的图中，我们在 newDF 上调用了 corr()方法，并将其传递给了 [Seaborn 的](https://blog.quantinsti.com/creating-heatmap-using-python-seaborn/)热图对象。从这个图像中，我们可以看到我们的两只股票没有那么相关。让我们创建一个最终的可视化来评估这种关系。我们将为此使用散点图。**

**前面我们使用了 Matplotlibs 散点图方法。所以现在我们来介绍一下 Seaborn 的散点图法。请注意，Seaborn 构建在 Matplotlib 之上，因此 Matplotlib 的功能可以应用于 Seaborn。**

```py
#Creating a scatter plot using Seaborn
plt.figure(figsize=(15,10))
sns.jointplot(newDF['WMT'],newDF['TGT'])
plt.legend(loc=0)
plt.show()
```

**![](img/5a9bbb36ebd221f888b856f055381ebf.png)**

**我喜欢使用 Seaborn 散点图的一个特点是它提供了相关系数和 P 值。从这个皮尔森值，我们可以看到，WMT 和 TGT 在这段时间内并不正相关。现在我们对我们的两只股票有了更好的了解，让我们来看看是否存在可交易的关系。**

**我们将使用[增强的 Dickey Fuller 测试](https://blog.quantinsti.com/augmented-dickey-fuller-adf-test-for-a-pairs-trading-strategy/)来确定我们的哪些股票可以在统计套利策略中交易。**

**回想一下，我们之前从 statsmodels.tsa.api 包中导入了 adfuller 测试。**

**要执行 ADF 测试，我们必须首先创建我们股票的价差。我们将它添加到现有的 newDF 数据帧中。**

```py
#adding the spread column to the nemDF dataframe
newDF['Spread']=newDF['WMT']-newDF['TGT']
#instantiating the adfuller test
adf=adfuller(newDF['Spread'])
```

**我们现在已经对我们的价差进行了 ADF 测试，需要确定我们的股票是否是协整的。让我们写一些逻辑来确定我们的测试结果。**

```py
#Logic that states if our test statistic is less than
#a specific critical value, then the pair is cointegrated at that
#level, else the pair is not cointegrated
if adf[0] < adf[4]['1%']:
print('Spread is Cointegrated at 1% Significance Level')
elif adf[0] < adf[4]['5%']:
print('Spread is Cointegrated at 5% Significance Level')
elif adf[0] < adf[4]['10%']:
print('Spread is Cointegrated at 10% Significance Level')
else:
print('Spread is not Cointegrated')
```

****价差未被协整****

**扩展的 Dickey Fuller 检验的结果显示，沃尔玛和塔吉特没有协整关系。这由不小于临界值之一的测试统计确定。如果您想查看 ADF 测试的实际打印结果，可以键入 ADF。在上面的例子中，我们使用索引来解释 t 统计量和临界值之间的关系。statsmodels ADF 测试为您提供了其他有用的信息，如 p 值。您可以在此了解更多关于 ADF 测试的信息**

```py
#printing out the results of the adf test
adf
(-0.38706825965317432,
0.91223562790079438,
0,
503,
{'1%': -3.4434175660489905,
'10%': -2.5698395516760275,
'5%': -2.8673031724657454},
1190.4266834075452)
```

**好吧，我们再试一次。也许我们会有更好的运气，以一种蛮力的方式来识别一种可交易的关系。美元树和美元将军怎么样？他们都是折扣零售商，看起来他们的名字里都有一美元。既然我们已经掌握了窍门，我们就直接进入 ADF 测试。让我们首先导入 DLTR 和 DG 的数据。**

```py
#importing dltr and dg
dltr=pdr.get_data_yahoo('DLTR',start, end)
dg=pdr.get_data_yahoo('DG',start, end)
```

**现在我们已经获得了数据，让我们将这些股票添加到我们的 newDF 中，并创建它们的价差。**

```py
#adding dltr and dg to our newDF dataframe
newDF['DLTR']=dltr['Close']
newDF['DG']=dg['Close']
#creating the dltr and dg spread as a column in our newDF dataframe
newDF['Spread_2']=newDF['DLTR']-newDF['DG']
```

**我们现在已经将 DLTR 和 DG 股票以及它们的价差添加到我们的 newDF 数据框架中。让我们快速看一下我们的数据框架。**

```py
newDF.head()
```

**![](img/77343b6ad66cb6ee41ca7d3560bec6f0.png)

现在我们有了 Spread_2 或 DLTR 和 DG 的价差，我们可以为这两只股票创建 ADF2 或第二个 ADF 测试。

```py
#Creating another adfuller instance
adf2=adfuller(newDF['Spread_2'])
```

我们刚刚对 DLTR 和 DG 的差价进行了 ADF 测试。我们现在可以重复我们先前的逻辑来确定差价是否产生可交易的关系。

```py
if adf2[0] < adf2[4]['1%']:
print('Spread is Cointegrated at 1% Significance Level')
elif adf2[0] < adf2[4]['5%']:
print('Spread is Cointegrated at 5% Significance Level')
elif adf2[0] < adf2[4]['10%']:
print('Spread is Cointegrated at 10% Significance Level')
else:
print('Spread is not Cointegrated')
```

**Spread is not Cointegrated**

要查看 ADF2 测试的完整打印结果，我们可以调用 adf2。

```py
adf2
(-1.9620694402101162,
0.30344784824995258,
1,
502,
{'1%': -3.4434437319767452,
'10%': -2.5698456884811351,
'5%': -2.8673146875484368},
1305.4559226426163)
```

不如我们在这里休息一下，复习一下我们到目前为止学到的东西。在这一节中，我们试图在一个没有 K-Means 的世界中开发一个统计套利策略，从而开始了理解 K-Means 对配对选择和统计套利的功效的旅程。

我们了解到，在一个没有 K 均值的统计套利交易世界里，我们只能靠自己的方法来解决配对选择的历史性问题。我们已经知道，尽管两只股票在基本面上相关，但这并不一定暗示它们将提供可交易的关系。

在下一节中，我们将更好地理解 K-Means，然后准备将其应用到我们自己的统计套利策略中。

## 理解 K 均值

在我们开始实现用于统计套利的 K-means 聚类算法之前，让我们看看 K-Means 是如何工作的。

我们将从导入我们常用的数据分析和操作库开始。Sci-kit learn 提供了内置的数据集，您可以使用这些数据集来熟悉各种算法。你可以在这里看看 sklearn [提供的一些数据集。](http://scikit-learn.org/stable/datasets/index.html)

为了理解 K-Means 是如何工作的，我们将创建自己的玩具数据并可视化聚类。然后，我们将使用 sklearn 的 K-Means 算法来评估它识别我们创建的聚类的能力。我们开始吧！

```py
#importing necessary libraries
#data analysis and manipulation libraries
import numpy as np
import pandas as pd
#visualization libraries
import matplotlib.pyplot as plt
import seaborn as sns
#machine learning libraries
#the below line is far making fake data far illustration purposes
from sklearn.datasets import make_blobs
```

现在我们已经从 sklearn 导入了我们的数据分析、可视化和 make_blobs 方法，我们准备创建我们的玩具数据来开始我们的分析。

```py
#creating fake data
data=make_blobs(n_samples=500, n_features=8,centers=5, cluster_std=1.5, random_state=201)
```

在上面的代码行中，我们创建了一个名为 data 的变量，并使用从 sklearn 导入的 make_blobs 对象对其进行了初始化。make blobs 对象允许我们创建和指定与我们将要创建的数据相关联的参数。我们能够分配样本的数量，或在聚类之间平均分配的观察值的数量，特征、聚类、聚类标准偏差和随机状态的数量。使用 centres 变量，我们可以确定我们希望从玩具数据中创建的聚类数。

现在我们已经初始化了我们的方法，让我们看看我们的数据。

```py
#Let's take a look at our fake data
data[0] #produces an array of our samples
```

![](img/2ee08363ad1a3b9f82ed571dac67b407.png)

打印数据[0]返回我们的样本数组。这些是我们在 make_blobs 对象中初始化 n_samples 参数时创建的玩具数据点。我们还可以查看我们创建的集群分配。

```py
#viewing the clusters of our data
data[1]
```

![](img/1d99eac589800595cf6c6d9f7a791f16.png)

打印数据[1]允许我们查看创建的集群。

注意，虽然我们在初始化中指定了五个集群，但是我们的集群分配范围是从 0 到 4。这是因为 python 索引从 0 开始，而不是从 1 开始。所以集群计数，可以这么说，从 0 开始，持续五步。

我们已经查看了我们的数据和集群，但是查看阵列并不能给我们提供很多信息。这就是我们可视化库的用武之地。Python 的 matplotlib 是一个很棒的可视化数据库，这样我们就可以对它进行推断。让我们创建一个散点图，或一个视觉识别我们的数据内在的关系。

```py
#creating a scatter plot of our data in features 1 and 2
plt.scatter(data[0][:,0],data[0][:,1])
```

![](img/04ed64ff4b29d178655fb29332752e38.png)

上面的情节给了我们更多的信息。更不用说它更容易阅读。我们已经使用前面创建的两个特征创建了样本数据的散点图。我们可以看到一些不同的集群。图表右上角的组是最明显的。图表左侧的数据也有一定程度的分离。但是，我们不是给数据分配了五个集群吗？我们还看不到这五个星团，但我们知道它们就在那里。

我们可以改善视觉效果的一个方法是用我们创建的集群来给它上色。

```py
#the above plot doesn't give us much information
#Let's recreate it using our clusters
plt.scatter(data[0][:,0],data[0][:,1],c=data[1])
```

![](img/accafb960b07c58f0c655de109786f9d.png)

上面的情节是一个进步。我们现在可以看到，原始图左下角的分组实际上是多个重叠的集群。如果我们添加更多不同的颜色，让我们能够识别每个集群中的特定点，那么这种可视化效果会更好。我们可以通过在散点图中添加另一个名为 cmap 的参数来做到这一点。cmap 参数将允许我们设置 matplotlib 内置的颜色映射，以便根据我们的聚类对数据重新着色。了解更多关于 matplotlib 的色彩映射。

```py
#we can improve the above visualization by adding a color map to our plot
plt.scatter(data[0][:,0],data[0][:,1],c=data[1],cmap=‘gist_rainbow')
```

![](img/03b79641c553f101c29967bfd4991114.png)

回顾一下，在这一点上，我们已经使用 sklearn 内置的 make_blobs 方法创建了一些玩具数据。然后，我们查看了前两个特征的行，随后是玩具数据的实际聚类。接下来，我们绘制了基于聚类的带颜色和不带颜色的数据。

为了展示 K-Means 是如何实现的，我们现在可以创建 K-Means 对象，并使其适合我们的玩具数据，然后比较结果。

```py
#importing K-Means
from sklearn.cluster import KMeans
```

每次我们在 sklearn 中导入一个模型，要使用它，必须创建它的一个实例。模型是对象，因此我们创建对象的实例，并为我们的特定对象指定参数。

自然，这允许我们创建各种不同的模型，每个模型都有不同的分析规范。在本例中，我们将创建 K-Means 对象的单个实例，并指定分类的数量。

```py
#instantiating K-means
model=KMeans(n_clusters=5) #n_clusters represents # of clusters; we know this because we created this dataset
KMeans(algorithm='auto', copy_x=True, init='k-means++', max_iter=300,
n_clusters=5, n_init=10, n_jobs=1, precompute_distances='auto',
random_state=None, tol=0.0001, verbose=0)
```

在上面的代码行中，我们已经使我们的模型符合我们的数据。我们可以看到，它证实了我们的模型应用于我们的数据的参数。

接下来，现在我们已经有了玩具数据，并可视化了我们创建的聚类，我们可以将我们从玩具数据创建的聚类与我们的 K-Means 算法基于查看我们的数据创建的聚类进行比较。

我们将编写一个类似于我们之前创建的可视化代码，但是，我们将使用 matplotlibs subplot 方法创建两个图，我们的聚类和 K-Means 聚类，可以并排查看这两个图以进行分析。如果你想了解更多关于 matplotlibs 子情节的功能，你可以访问[这里](https://matplotlib.org/devdocs/api/_as_gen/matplotlib.pyplot.subplot.html)。

```py
#now we can compare our clustered data to that of K-means
#creating subplots
plt.figure(figsize=(10,8))
plt.subplot(121)
plt.scatter(data[0][:,0],data[0][:,1],c=data[1],cmap='gist_rainbow')
#in the above line of code, we are simply replotting our clustered data
#based on already knowing the labels(i.e. c=data[1])
plt.title('Our Clustering')
plt.tight_layout()
plt.subplot(122)
plt.scatter(data[0][:,0],data[0][:,1],c=model.labels_,cmap='gist_rainbow')
#notice that the above line of code differs from the first in that
#c=model.labels_ instead of data[1]...this means that we will be plotting
#this second plot based on the clusters that our model predicted
plt.title('K-Means Clustering')
plt.tight_layout()
plt.show()
```

![](img/8ce89a7922830fe5d07c1215a8855081.png)

上面的图显示 K-Means 算法能够识别我们数据中的聚类。颜色与聚类没有关系，只是区分聚类的一种方式。

实际上，我们没有数据所属的实际聚类，因此我们无法将 K-Means 的聚类与之前的聚类进行比较；但是本演练展示的是 K-Means 识别数据中是否存在子组的能力。

在我们更好地理解 K-Means 的应用和有用性的旅程中，我们已经从我们创建的数据中创建了我们自己的聚类，使用 K-Means 算法在我们的玩具数据中识别聚类，并及时回到没有 K-Means 的统计套利和[均值回归交易](https://quantra.quantinsti.com/course/python-mean-reversion-strategies-ernest-chan)世界

让我们暂停一会儿，理解一下到目前为止我们学到了什么。我们知道 K-Means 最初将数据点随机分配给聚类，然后计算质心或平均值。此外，它还计算每个聚类内的距离，对这些距离进行平方，然后求和，以获得误差平方和。

目标是减少这种误差或距离。该算法重复这个过程，直到不再有集群内变化，或者换句话说，集群组成停止变化。

太好了！现在，我们从这里去哪里？在下一节中，我们将进入一个统计套利交易的世界，在这个世界中，K-Means 是解决配对选择问题的一个可行的选择，并使用它来实现一个统计套利交易策略。

首先，我们需要收集一组股票的数据。我们将继续使用标准普尔 500。标准普尔 500 有 505 只股票。我们将为每只股票收集一些数据，并将这些数据用作 [K-Means](https://blog.quantinsti.com/k-means-clustering-pair-selection-python/) 的特征。然后，我们将在其中一个聚类中确定一个配对，使用 ADF 测试对其进行协整测试，然后使用该配对构建一个统计套利交易策略。

让我们开始吧！

## 使用 K-Means 构建 StatArb 策略

我们首先从 Excel 文件中读入一些数据，其中包含将要使用的股票和特性。

```py
#Importing Our Stock Data From Excel
file=pd.ExcelFile('KMeansStocks.xlsx')
#Parsing the Sheet from Our Excel file
stockData=file.parse('Example')
```

既然我们已经从 Excel 中导入了股票数据，让我们来看看我们将使用哪些特性来构建我们基于 [K 均值](https://blog.quantinsti.com/k-means-clustering-pair-selection-python-part-2/)的统计套利策略。

```py
#Looking at the head of our Stock Data
stockData.head()
```

![](img/60035d32476e56a328369795b07a0b96.png)

```py
#Looking at the tail of our Stock Data
stockData.tail()
```

![](img/849489c5ce172f649995a2a8fad5b56a.png)

我们将使用股息收益率、P/E、EPS、市值和 EBITDA 作为在标准普尔 500 创建集群的特征。从我们数据的尾部来看，我们可以看到雅虎没有股息率，并且没有达到市盈率。这带来了一个很好的教学时刻。在现实世界中，数据并不总是干净的，因此需要您清理和准备数据，以便适合分析并最终用于构建策略。

实际上，导入的数据已经做了一些预处理，因为我已经从中删除了一些不必要的列。

### **实现机器学习算法的过程**

让我们花一点时间来思考实现机器学习算法的过程。

1.  我们从收集数据开始
2.  接下来，我们希望确保我们的数据是干净的，随时可以使用
3.  在某些情况下，根据我们实现的算法，我们进行训练测试分割(对于 K-意味着这是不必要的)
4.  在进行训练-测试分离之后，我们接着在我们的训练数据上训练我们的算法，然后在我们的测试数据上测试它
5.  然后我们调查我们模型的精确度

### **实施**

让我们从进一步清理数据开始。让我们将索引更改为 Symbols 列，这样我们就可以将集群与相应的符号相关联。此外，让我们删除名称列，因为它没有任何用途。

在对我们的数据进行其他更改之前，让我们制作一份原始数据的副本。这是一个很好的实践，因为如果我们使用的是原件的副本而不是原件，我们可能会在以后出错，并且能够重置我们的实现。

```py
#Making a copy of our stockdata
stockDataCopy=stockData.copy()
#Dropping the Name column from our stockData
stockDataCopy.drop('Name', inplace=True,axis=1)
```

在做出更改后，最好回去检查您的数据。让我们看一下我们的 stockData，确认我们正确地删除了 Name 列。此外，在上面的代码行中，我们希望确保包含 inplace=True。这表明更改将持续存在于我们的数据中。

```py
#Checking the head of our stockData
stockDataCopy.head()
```

![](img/4d5cea758cd554185feb25cea79f3f98.png)

好了，现在我们已经正确地删除了 Name 列，我们可以将数据的索引改为 Symbol 列的索引。

```py
stockDataCopy.reindex(index=stockDataCopy['Symbol'],columns=stockDataCopy.columns)
```

![](img/7a19788f3b1325969df5fb1613ab052e.png)

我们已经重新索引了我们的股票数据，但是这个视图并不是我们所期望的。让我们通过将值添加回我们的列来解决这个问题。我们之所以能够做到这一点，是因为我们使用的是原件的副本。

```py
#Adding back the values to our Columns
stockDataCopy['Symbol']=stockData['Symbol'].values
stockDataCopy['Dividend Yield']=stockData['Dividend Yield'].values
stockDataCopy['P/E']=stockData['P/E'].values
stockDataCopy['EPS']=stockData['EPS'].values
stockDataCopy['MarketCap']=stockData['MarketCap'].values
stockDataCopy['EBITDA']=stockData['EBITDA'].values
```

我们已经将数据添加回我们的 stockDataCopy 数据帧。注意，在上面的代码中，我们能够做到这一点，因为我们可以简单地从原始数据帧中移植值。让我们再来看看我们的股票数据。

```py
#Viewing the head of our stockDataCopy dataframe
stockDataCopy.head()
```

![](img/5cde6241ddc38a151b644c4106fd081c.png)

似乎 [Jupyter Notebook](https://blog.quantinsti.com/jupyter-notebook-tutorial-installation-components-magic-commands/) 对我们的数据帧(即 Spyder IDE 的数据帧)进行重新索引和重新赋值的反应不同。我们现在不会担心这个问题，但将来可能需要创建一个解决方法。现在，我们将重点关注数据的聚类。我们从实例化另一个 K-Means 对象开始。

```py
stock_kmeans=KMeans()
```

等等，我们怎么找到 K？？？

这让我们看到了我们战略发展的另一个重要组成部分。回想一下，在我们的 K 均值聚类示例中，我们创建了自己的玩具数据，因此能够确定我们想要多少个聚类。在测试 K-Means 算法时，我们能够将 K 指定为 5，因为我们知道它应该尝试创建多少个聚类。

然而，使用实际数据，我们不知道在我们的股票数据中实际存在多少子群。这意味着我们必须找到一种方法来确定要使用的适当的聚类数量或 K 值。

一种这样的技术被称为“肘”技术。我们之前提到过这一点，但我将简要回顾一下。我们绘制了聚类数与误差平方和(SSE)的关系图。图中倾向于弯曲的地方，形成一个肘状的形状，是我们应该选择的聚类的值。

因此，我们的任务是为 K 创建一个值范围，在该范围内迭代，并在每次迭代中使我们的 stock_kmeans 模型适合我们的数据。我们还需要存储 K 值，并有一种方法来计算每次迭代的质心距离，这样我们就可以计算 SSE 或误差平方和。

为了找到我们的距离，我们将使用 scipy。现在就导入吧。

从 scipy.spatial.distance 导入 cdist

如果您想了解更多关于 cdist 对象的信息，您可以访问此[链接](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.cdist.html)。

K-Means 中使用的距离是欧几里德距离，这是我们将在该方法中使用的距离。

让我们创建肘图来确定 k 的值。

```py
#creating an object to determine the value for K
class Get_K(object):
def __init__(self,start,stop,X):
self.start=start
self.stop=stop
self.X=X
#in our example, we found out that there were some NaN
#values in our data, thus we must fill those with 0
#before passing our features into our model
self.X=self.x.fillna(e)
def get_k(self):
#this method will iterate through different
#values of K and create the SSE
#initializing a list to hold our error terms
self.errors=[ ]
#intializing a range of values for K
Range=range(self.start,self.stop)
#iterating over range of values far K
#and calculating our errors
for i in Range:
self.k_means=KMeans(n_clusters=i)
self.k_means.fit(self.X)
self.errors.append(sum(np.min(cdist(self.X[0:200],self.k_means.cluster_centers_,'euclidean'),axis=1))/200)
return
 def plot_elbow(self):
with plt.style.context(['seaborn-notebook','ggplot‘]):
plt.figure(figsize=(10,8))
#we have multiple features, thus we will use the
#P/E to create our elbow
plt.plot(self.X['P/E'][0:200],self.errors[0:200])
plt.xlabel('Clusters')
plt.ylabel('Errors')
plt.title('K-Means Elbow Plot')
plt.tight_layout()
plt.show()
Return
```

我们现在有了一个对象来确定我们应该为 k 使用的值。我们将创建这个对象的一个实例，传入我们的 stockData，并确定我们应该为 k 使用的值。

让我们首先创建一个特性列表。

```py
features=stockDataCopy[[‘Dividend Yield','P/E','EPS','MarketCap','EBITDA']]
```

现在我们已经设置了我们的特征，我们可以将它们传递到我们的 K-Means 算法中。

```py
#Creating an instance of our Get_K object
#we are setting our range of K from 1 to 266
#note we pass in the first 200 features values in this example
#this was done because otherwise, to plot our elbow, we would
#have to set our range max at 500\. To avoid the computational
#time associated with the for loop inside our method
#we pass in a slice of the first 200 features
#this is also the reason we divide by 200 in our class
Find_K=Get_K(1, 200,features [1:200]
```

至此，我们已经创建了我们的特性列表，并创建了 Get_K 类的一个实例，K 的可能范围是从 1 到 200。

现在我们可以调用 get_k 方法来查找错误。

```py
#Calling get_k method on our Find_K object
Find_K.get_k()
```

可视化 K-Means 肘图

现在我们已经使用 get_k 方法计算了 K 的误差和范围，我们可以调用 plot_elbow 方法来可视化这种关系，然后为 K 选择适当的值。

```py
#Visualizing our K-Means Elbow Plot
Find_K.plot_elbow()
```

![](img/88889914dbe055332150bc944f8357f6.png)

我们现在可以使用上面的图来设置我们的 K 值。一旦我们设置了 K，我们就可以将我们的模型应用于我们的股票数据，然后解析出我们的聚类并将它们添加回我们的 stock data 数据框架。从这里，我们可以操作我们的数据框架，这样我们就可以确定哪些股票在哪个集群中。之后，我们可以选择成对的股票，并通过检查它们是否是协整的来完成我们的分析，如果是这样，就建立一个统计套利策略。

让我们在这里休息一下，回顾一下到目前为止我们所学到的知识。我们继续在理解 K-Means 如何改进我们的统计套利策略的基础上发展。我们了解到实现 K-Means 要解决的一个重要问题是确定我们应该为 K 使用什么值。

我们已经涵盖了很多，现在我们几乎到了我们一直在等待的点，编码我们的战略。我们马上开始吧！

## k-均值 StatArb 实现

我们将创建一个类，它将允许我们清理数据、测试协整，并通过调用我们的[统计套利](https://blog.quantinsti.com/statistical-arbitrage/)对象的方法来运行我们的策略。

![](img/b53689b3b6125f4a4fc9ef11aab148a3.png)

![](img/20fbbcc3b225bd63c15e8b17438c5d0f.png)

![](img/e0894ac747054ba6941688707616fce1.png)

![](img/8fa8c7186fdf21f127483635b13e1b20.png)

让我们简单地看一下上面的代码是做什么的。

我们首先创建一个 statarb 类的实例。我们传入我们想要交易的两只股票的两个数据框架，以及移动平均线的参数、z 得分的下限或买入水平、z 得分的上限或卖出水平、我们对冲比率的 beta 回望期和我们 z 得分的出场水平。默认情况下，此级别设置为 0。

一旦我们创建了 stat arb 对象，我们就可以访问它的方法了。我们首先像前面一样在 create spread 方法中清理数据。一旦我们的数据被清除，我们就可以调用我们的协整检验方法。该方法将获取在我们的 create spread 方法中创建的价差，然后将其传递给 ADF 测试，并返回这两只股票是否协整。

如果我们的股票是协整的，那么我们可以调用我们的生成信号方法来实现[统计套利](https://blog.quantinsti.com/fx-market-pairs-trading-strategy/) [策略](https://quantra.quantinsti.com/course/statistical-arbitrage-trading)。从这里我们可以调用我们的 create returns 方法。这个方法要求我们传递一个分配量。这是我们假设投资组合的金额，将用于创建我们的权益曲线。在我们的权益曲线创建后，我们将可以访问其他数据，如命中率、输赢和我们的[夏普比率](https://blog.quantinsti.com/sharpe-ratio-applications-algorithmic-trading/)。

为了实现该策略，我们必须在迭代数据帧以检查信号时跟踪我们的当前位置。对于如何实施统计套利策略的一个很好的演练，请访问 Quantstart.com。这里是[文章](https://www.quantstart.com/articles/Backtesting-An-Intraday-Mean-Reversion-Pairs-Strategy-Between-SPY-And-IWM)的链接。Michael 做得很好，为实施的每一步提供了深入的见解。

我们将 K 设为 100。让我们从实例化 K-Means 对象开始。

![](img/cc581efc35230783517dada08950e1b1.png)

现在，让我们根据数据的特征来拟合我们的模型。

![](img/2d1df0f1704e2bd30036b3bcc121b84b.png)

![](img/36bf8ac60f712620922820746e338f71.png)

现在，我们已经使我们的模型适合了我们的特性，我们可以获得我们的集群并将它们添加到我们的 stockDataCopy 数据帧中。另外，请注意，我们在特性上调用了 fillna()方法。这样做是因为我们注意到我们的一些特性有 NaN 值，而这不能传递到我们的模型中。我们没有调用 dropna()来删除这些值，因为这会改变我们的特征的长度，并且在将集群添加回我们的数据帧时会出现问题。

让我们来看看我们的集群。

![](img/47b596fc1906d155ef038993e47e2002.png)

![](img/ed6cc46c1f5fc923a48840b671692ef4.png)

好了，现在我们有了聚类，我们可以将它们添加回我们的数据中。让我们先来看看我们的数据框架。

![](img/a3d60b8c12bbade429c08698293613a7.png)

![](img/cee4b7061339ce0ac247b3123787449a.png)

让我们为我们的集群添加一列到我们的数据框架中。

![](img/47a78bc7265fd3a34901a7ad518635e6.png)

让我们再次回顾我们的数据框架。

![](img/3768edac48202e37668ce59021df32b1.png)

![](img/e2cb0ea25749d6619127de26fb898b71.png)

既然我们的数据框架中已经有了我们的聚类，我们的下一个任务是在我们的聚类中识别可交易对。

让我们看看每个聚类中放了多少只股票。为此，我们将从集合库中导入计数器方法。

![](img/c2dc7881937bf26da18e994be9492a72.png)

![](img/3517308d4b834ec21adcc98c39741b3e.png)

现在我们已经创建了一个变量来计算每个簇中的符号数，我们可以打印它了。

![](img/bbd8787b264dac85990b406eaa3a4a14.png)

![](img/e187011c6943fee99224aef89f8c658c.png)

现在，我们准备将集群添加到数据框架中。但是，请注意上面的内容，当查看每个聚类中有多少个值时，我们可以看到一些聚类只有 1 个符号。我们希望消除这些，只查看包含 2 个或更多符号的聚类。我们还想通过聚类来排序我们的数据，以便我们可以查看各个聚类中的每个符号。

为此，我们将创建一个新的数据帧，并使用 pandas concat 方法将其与根据 Clusters 列分组的 stockDataCopy 数据帧连接起来，但过滤掉包含少于 2 个符号的集群。

![](img/84e6a21e51d4a1b69812aa768eae0c53.png)

![](img/2ee700d2bcdc02fde7cae59efd00c8cd.png)

我们可以将我们的连接保存到一个变量中，这个变量将允许我们对它执行操作。

![](img/696184a60021bac4cebc304cdd167c8f.png) ![](img/57b8986f6ca5c41b011db39c915af0a7.png)

![](img/3653b14cdf4129a32e3bb7a70134ccf6.png)

上面的数据帧向我们展示了簇 0 中的五个符号。我们可以看到该指数代表了它们在股票数据框架中的原始位置。我们还可以对它们的特征做一个简单的比较。

我们现在可以看到滚动或迭代我们的数据帧，并看到哪些符号在每个集群中，最少至少有两个符号。让我们使用我们的 statarb 方法来测试一对符号的协整性，并开发一个统计套利策略。

我们将从创建 statarb 对象的实例开始。我们将从集群 0 中随机选择两只股票进行分析。我们必须首先导入测试期间每个符号的数据。

![](img/2d02f1a089654cb8a920e027d224a165.png)

现在我们已经导入了数据，让我们快速查看一下。

![](img/dc47c5b5837eb84660d0135a8d40a948.png)

![](img/e16889c2e54fc4d66a5fd7641df5cca0.png)

好了，现在让我们来测试我们的 statarb 类，以测试符号的协整性，并建立一个策略。

![](img/95bdfe622e0058583d8268c2f2d5f448.png)

在上面的代码行中，我们刚刚创建了 statarb 策略类的一个实例。我们现在可以调用 create_spread 方法来创建数据的分布。我们传入 bbby 和 gt 的整个数据框架，因为这个方法将解析收盘价并为我们创建价差。之后，我们可以调用剩下的方法来完成我们的统计套利分析。

![](img/ec959cd0c2107a6f717638f0bf903c41.png)

![](img/1a776335a8daace1822f80f621764808.png)

在上面的数据框架中，我们可以看到我们已经增加了我们的传播。头部的值是 NaN，它反映了我们正在使用的回看。我们可以向下滚动，查看每一列的值都已填充。

![](img/d0a98e0be6a17cc1aad9a2a31d74ba64.png)

现在，我们已经创建了我们的货币对的利差，让我们来看看它们是否是协整的。

![](img/466fe4188622a40ca805a53ab0e41294.png) ![](img/10f250be5e7b8a248fa0e29ec38789d3.png)

我们的组合是高度整合的。现在我们已经确认了这一点，我们可以调用我们的 generate signals 并创建回报，以查看我们的策略在测试期间的表现。

![](img/3505962fc5929c0b6946e157d94bf2b9.png)

![](img/f62fea25d3e5c851d39756bf55e494bc.png)

我们可以看到，我们已经将信号添加到数据帧中。

现在我们已经为我们的组合生成了信号，让我们使用创建回报方法来计算我们的回报并打印我们的权益曲线。回想一下，这个方法接受一个分配量。这是我们投资组合的起始价值。这个方法还要求我们为我们的 pair 传入一个名称，作为包含在我们的绘图中的字符串。

![](img/61c7b7560aafee1708b733a86169dfd3.png)

![](img/032d24b5e8a52d06b19813caa017d38f.png)

我们可以看到，在似乎不再是协整之前，我们的策略在一段时间内表现良好。让我们来看看我们的夏普比率。

![](img/a67434c0657166142e7d23e9f025cbde.png)

![](img/10b742ff9b7a1a76112e445ed193417a.png)

挑战:看看你是否能改进这个策略

尝试改进这个策略。我们的分析显示，这两只股票高度协整。然而，在我们测试期的大部分时间里表现良好之后，该策略似乎出现了损失协整。

这说明了几件事。

*   说明[统计套利](https://blog.quantinsti.com/incorrect-notions-statistical-arbitrage/)不是无风险的交易策略。
*   它强调了交易时使用的参数的重要性。这些才是真正的专利。

## 结论

哇！我们在短时间内涵盖了大量的信息。概括地说，我们从理解 K-Means 开始。我们也走过了一个没有 K 均值的统计套利世界。我们强行创造了一些配对，并了解到识别可交易的关系比在同一领域找到配对要复杂一些。然后，我们使用标准普尔 500 的真实股票数据，即股息收益率、P/E、MarketCap、EPS 和 EBITDA，作为特征，开始为交易统计套利创建真实世界的 K 均值分析。

然后，我们将我们的聚类添加到我们的数据框架中，并对其进行操作，以便我们可以通过 ADF 测试来测试每个聚类中的配对的协整性。我们从分析的第 0 类中随机选择了 BBBY 和 GT，发现它们在 99%的显著性水平上是协整的。之后，我们使用我们创建的 statarb 类对我们新发现的 pair 进行回溯测试。咻！

这个分析也显示了 K-Means 在寻找非传统的统计套利交易中的优势。BBBY 是 Bed Bath 和 Beyond 的股票代码，GT 是固特异轮胎和橡胶公司的股票代码。这两只股票表面上看起来没有任何共同之处，但在过去一直在 1%的临界值进行协整。

## 下一步

如果你想学习算法交易的各个方面，那就去看看算法交易(EPAT)的高管课程。课程涵盖统计学&计量经济学、金融计算&技术和算法&定量交易等培训模块。EPAT 让你具备成为成功交易者所需的技能。[现在报名](https://www.quantinsti.com/epat/)！

*免责声明:股票市场的所有投资和交易都有风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。*

### **下载 Python 代码**

*   使用 K-Means 构建 StatArb 策略的 Python 代码**
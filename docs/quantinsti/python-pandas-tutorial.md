# Python 熊猫教程:安装、系列和数据框架

> 原文：<https://blog.quantinsti.com/python-pandas-tutorial/>

杰伊·帕尔马

**Pandas** 是一个处理顺序数据和表格数据的 Python 库。它包括许多工具，以方便有效的方式管理、分析和操作数据。我们可以认为它的数据结构类似于数据库表或电子表格。

Pandas 构建在 Numpy 库之上，有两个主要的数据结构，即。系列(一维)和数据框架(二维)。它可以处理同构和异构数据，其众多功能包括:

*   ETL 工具(提取、转换和加载工具)
*   处理缺失数据(NaN)
*   处理数据文件(csv、xls、db、hdf5 等。)
*   时间序列操作工具

在 Python 生态系统中，Pandas 是检索、操作、分析和转换金融数据的最佳选择。

在这个 Python 熊猫教程中，我们将学习 Python 熊猫模块的基础知识，并理解一些代码。这篇博客文章是从 [Python 基础手册](https://www.quantinsti.com/python-basics-handbook)中摘录的，其创建的简单目的是让读者理解 [Python 语言](/getting-started-python-trading/)的美丽和简单。

本文的内容包括:

*   [安装 Python 熊猫](#installing)
*   [Python 熊猫解决什么问题？](#problem)
*   [蟒蛇熊猫系列](#series)
*   [Python 熊猫数据帧](#dataframe)
*   [在 Python 熊猫中导入数据](#import)
*   [索引和子集化](#indexing)
*   [操纵 Python 熊猫数据帧](#manipulating)
*   [统计探索性数据分析](#statistical)
*   [过滤 Python 熊猫数据帧](#filtering)
*   [迭代 Python 熊猫数据帧](#iterating)
*   [合并、追加和连接 Python 熊猫数据帧](#merge)
*   [熊猫的时间序列](#timeseries)

## 安装 Python 熊猫

在 Python Pandas 教程的这一部分，我们将开始浏览官方文档，其中有关于安装 Pandas 的详细解释。我们总结如下。

### 和皮普一起

最简单的安装熊猫的方法是从 PyPI。

在终端窗口中，运行以下命令。

```py
pip install pandas

```

在您的代码中，您可以使用转义符'**！从你的 Python 控制台直接安装 pandas。**

```py
!pip install pandas

```

Pip 是管理 Python 包的有用工具，值得花些时间更好地了解它。

```py
pip help

```

### 对于康达环境

对于喜欢在每个项目中使用 Python 环境的高级用户，您可以创建一个新环境并安装 pandas，如下所示。

```py
conda create -n EPAT python
source activate EPAT
conda install pandas

```

### 测试熊猫装置

为了检查安装，Pandas 附带了一个测试套件来测试几乎所有的代码库，并验证一切正常。

```py
import pandas as pd
pd.test()

```

## Python 熊猫解决什么问题？

在 Python 熊猫教程的这一节，我们将了解 Python 熊猫的用法。

Python Pandas 处理同质数据系列(一维)和异质表格数据系列(二维)。它包括许多处理这些数据类型的工具，例如:

*   索引和标签。
*   元素搜索。
*   元素的插入、删除和修改。
*   应用集合技术，如分组、连接、选择等。
*   数据处理和清理。
*   使用时间序列。
*   进行统计计算
*   绘制图形
*   多种数据文件格式的连接器，如 csv、xlsx、hdf5 等。

[熊猫纪录片:与熊猫共度 10 分钟](https://pandas.pydata.org/pandas-docs/stable/10min.html)

## 蟒蛇熊猫系列

我们将在 Python 熊猫教程中学习的第一个数据结构是 Series。

Python Pandas 系列是同构的一维对象，也就是说，所有数据都是同一类型的，并且隐式地用一个索引来标记。

例如，我们可以有一系列整数、实数、字符、字符串、字典等。我们可以方便地操纵这些系列执行操作，如添加、删除、排序、连接、过滤、矢量化操作、统计分析、绘图等。

让我们看一些如何创建和操作 Python 熊猫系列的例子:

*   我们将从创建一个空的 Python 熊猫系列开始:

```py
import pandas as pd
s = pd.Series()
print(s)

Out[]: 

Series([], dtype: float64)

```

*   让我们创建一个 Python 熊猫系列的整数:

```py
import pandas as pd
s = pd.Series([1, 2, 3, 4, 5, 6, 7])
print(s)

Out[]:
        0    1
        1    2
        2    3
        3    4
        4    5
        5    6
        6    7
        dtype: int64

```

*   让我们创建一个 Python 熊猫系列角色:

```py
import pandas as pd
s = pd.Series(['a', 'b', 'c', 'd', 'e'])
print(s)

Out[]: 
        0    1
        1    2
        2    3
        3    4
        4    5
        5    6
        6    7
        dtype: int64

```

*   让我们创建一个随机的 Python 熊猫系列浮点数:

```py
import pandas as pd
import numpy as np
s = pd.Series(np.random.randn(5))
print(s)

Out[]:  
 0    0.383567
        1    0.869761
        2    1.100957
        3   -0.259689
        4    0.704537
        dtype: float64

```

在我们在 Python Pandas 教程中看到的所有例子中，我们都允许默认显示索引标签(没有显式编程)。它从 0 开始，我们可以这样检查索引:

```py
In[]: 

s.index

Out[]: 

RangeIndex(start=0, stop=5, step=1)

```

但是我们也可以指定我们需要的索引，例如:

```py
In[]: 

s = pd.Series(np.random.randn(5), index=['a', 'b', 'c', 'd', 'e'])

Out[]:
      a    1.392051
      b    0.515690
      c   -0.432243
      d   -0.803225
      e    0.832119
      dtype: float64

```

*   让我们根据字典创建一个 Python 熊猫系列:

```py
import pandas as pd
dictionary = {'a' : 1, 'b' : 2, 'c' : 3, 'd': 4, 'e': 5}
s = pd.Series(dictionary)
print(s)

Out[]:

        a    1
        b    2
        c    3
        d    4
        e    5
        dtype: int64

```

在这种情况下，除非我们指定任何其他索引，否则 Python Pandas 系列是使用字典键作为索引创建的。

### Python 熊猫系列的简单操作

当我们有一个 Python 熊猫系列时，我们可以对它执行几个简单的操作。

例如，在 Python 熊猫教程的这一部分，让我们创建两个系列。一个来自字典，另一个来自整数数组:

```py
In[]: 
 import pandas as pd
      dictionary = {'a' : 1, 'b' : 2, 'c' : 3, 'd': 4, 'e': 5}
      s1 = pd.Series(dictionary)

      array = [1, 2, 3, 4, 5]
      s2 = pd.Series(array)

Out[]:  
 a    1
        b    2
        c    3
        d    4
        e    5
        dtype: int64

        0    1
        1    2
        2    3
        3    4
        4    5
        dtype: int64

```

我们可以执行类似于 Numpy 数组的操作:

*   通过索引从 Python Pandas 系列中选择一个项目:

```py
In[]: 
s1[0] # Select the first element

Out[]: 
1

In[]: 
s1['a'] 

Out[]: 
1

In[]: 
s2[0] 

Out[]: 
1

```

*   通过索引从 Python Pandas 系列中选择几个项目:

```py
In[]: 
s1[[1,4]]

Out[]:
        b    2
        e    5
        dtype: int64

In[]: s1[['b', 'e']]

Out[]:  
 b    2
        e    5
        dtype: int64

In[]: 
s2[[1,4]]

Out[]:  
 b    2
        e    5
        dtype: int64

```

*   从一个元素开始获取 Python 熊猫系列:

```py
In[]: 
s1[2:]

Out[]:  
 c    3
        d    4
        e    5
        dtype: int64

In[]: 
s2[2:]

Out[]:  
 2    3
        3    4
        4    5
        dtype: int64

```

*   让 Python 熊猫系列达到一个元素:

```py
In[]: 
s1[:2]

Out[]:  
 c    3
        d    4
        e    5
        dtype: int64

In[]: 
s2[:2]

Out[]:  
 2    3
        3    4
        4    5
        dtype: int64

```

我们可以像字典一样执行操作:

*   分配一个值:

```py
In[]: 
 s1[1] = 99
      s1['a'] = 99

Out[]:  
 a     1
        b    99
        c     3
        d     4
        e     5
        dtype: int64

In[]: 
s2[1] = 99
print(s2)

Out[]:  
 0     1
        1    99
        2     3
        3     4
        4     5
        dtype: int64

```

*   通过索引获取值(如字典键):

```py
In[]: 
s.get('b')

Out[]: 
2

```

下面是一些强大的矢量化运算，可以让我们快速执行计算，例如:

*   加、减、乘、除、幂，以及几乎任何接受 NumPy 数组的 NumPy 函数。

```py
s1 + 2
s1 - 2
s1 * 2
s1 / 2
s1 ** 2
np.exp(s1)

```

*   我们可以对两个 Python 熊猫系列执行相同的操作，尽管它们必须对齐，也就是说，要有相同的索引，在其他情况下，执行联合操作。

```py
In[]: 
s1 + s1 # The indices are aligned

Out[]:  
 a     2
        b     4
        c     6
        d     8
        e    10
        dtype: int64

In[]: 
s1 + s2 # The indices are unaligned

Out[]:  
 a   NaN
        b   NaN
        c   NaN
        d   NaN
        e   NaN
        0   NaN
        1   NaN
        2   NaN
        3   NaN
        4   NaN
        dtype: float64

```

## 蟒蛇熊猫数据框

我们将要看到的 Python Pandas 中的第二个数据结构是 DataFrame。

Python Pandas DataFrame 是一个异构的二维对象，也就是说，每一列中的数据都是相同的类型，但每一列的数据类型可能不同，并且用索引隐式或显式地标记。

我们可以把 Python Pandas DataFrame 想象成一个数据库表，我们在其中存储异构数据。例如，Python Pandas 数据框架有一列用于名，另一列用于姓，第三列用于电话号码，或者 Python Pandas 数据框架有多列用于存储开盘价、收盘价、最高价、最低价、成交量等。

索引可以是隐式的，从零开始，或者我们可以自己指定它，甚至还可以使用日期和时间作为索引。

让我们看一些如何创建和操作 Python 熊猫数据框架的例子。

*   创建一个空的 Python 熊猫数据框架:

```py
In[]: 
 import pandas as pd
      s = pd.DataFrame()
      print(s)

Out[]:  
 Empty DataFrame
        Columns: []
        Index: []

```

*   创建空结构 Python 熊猫数据帧:

```py
In[]: 
 import pandas as pd
      s = pd.DataFrame(columns=['A','B','C','D','E'])
      print(s)

Out[]:  
 Empty DataFrame
        Columns: [A, B, C, D, E]
        Index: []

In[]: 
 import pandas as pd
      s = pd.DataFrame(columns=['A','B','C','D','E'], index=range(1, 6))
      print(s)

Out[]:
             A    B    C    D    E
        1  NaN  NaN  NaN  NaN  NaN
        2  NaN  NaN  NaN  NaN  NaN
        3  NaN  NaN  NaN  NaN  NaN
        4  NaN  NaN  NaN  NaN  NaN
        5  NaN  NaN  NaN  NaN  NaN

```

*   通过 NumPy 数组创建 Python Pandas 数据帧:

```py
In[]: 
 array =  {'A' : [1, 2, 3, 4],
                'B' : [4, 3, 2, 1]}

      pd.DataFrame(array)

Out[]: 
        A   B
      0 1   4
      1 2   3
      2 3   2
      3 4   1

```

*   创建 Python Pandas 数据帧，传递 NumPy 数组，日期时间索引为:

```py
In[]: 
 import pandas as pd
      array =  {'A' : [1, 2, 3, 4],'B' : [4, 3, 2, 1]}
      index = pd.DatetimeIndex(['2018-12-01', '2018-12-02','2018-12-03', '2018-12-04'])
      pd.DataFrame(array, index=index)

Out[]:
                 A B
    2018-12-01  1   4
    2018-12-02  2   3
    2018-12-03  3   2
    2018-12-04  4   1

```

*   创建 Python 熊猫数据帧传递字典:

```py
In[]: 
 import pandas as pd
      dictionary = {'a' : 1, 'b' : 2, 'c' : 3, 'd': 4, 'e': 5}
      pd.DataFrame([dictionary])

Out[]:
        a   b   c   d   e
      0 1   2   3   4   5

```

*   查看 Python 熊猫数据框架:我们可以使用一些方法来探索熊猫数据框架:

首先，我们创建一个 Python 熊猫数据框架来使用它。

```py
In[]: 
 import pandas as pd
      pd.DataFrame({'A' : np.random.randn(10), 'B' : np.random.randn(10), 'C' : np.random.randn(10)})

Out[]:
            A         B           C
    0   0.164358    1.689183    1.745963
    1   -1.830385   0.035618    0.047832
    2   1.304339    2.236809    0.920484
    3   0.365616    1.877610    -0.287531
    4   -0.741372   -1.443922   -1.566839
    5   -0.119836   -1.249112   -0.134560
    6   -0.848425   -0.569149   -1.222911
    7   -1.172688   0.515443    1.492492
    8   0.765836    0.307303    0.788815
    9   0.761520    -0.409206   1.298350

```

*   获取前三行:

```py
In[]: 
 import pandas as pd
      df=pd.DataFrame({'A' : np.random.randn(10), 'B' : np.random.randn(10), 'C' : np.random.randn(10)})

      df.head(3)

Out[]:
            A         B           C
    0   0.164358    1.689183    1.745963
    1   -1.830385   0.035618    0.047832
    2   1.304339    2.236809    0.920484

```

*   获取最后三行:

```py
In[]: 
 import pandas as pd
      df=pd.DataFrame({'A' : np.random.randn(10), 'B' : np.random.randn(10), 'C' : np.random.randn(10)})

      df.tail(3)

Out[]:
           A         B           C
    7   -1.172688   0.515443    1.492492
    8   0.765836    0.307303    0.788815
    9   0.761520    -0.409206   1.298350

```

*   获取 Python 熊猫数据框架的索引:

```py
In[]: 
 import pandas as pd
      df=pd.DataFrame({'A' : np.random.randn(10), 'B' : np.random.randn(10), 'C' : np.random.randn(10)})

      df.index

Out[]: 
RangeIndex(start=0, stop=10, step=1)

```

*   获取 Python 熊猫数据框架的列:

```py
In[]: 
 import pandas as pd
      df=pd.DataFrame({'A' : np.random.randn(10), 'B' : np.random.randn(10), 'C' : np.random.randn(10)})

      df.columns

Out[]: 
Index(['A', 'B', 'C'], dtype='object')

```

*   获取 Python 熊猫数据帧的值:

```py
In[]: 
 import pandas as pd
      df=pd.DataFrame({'A' : np.random.randn(10), 'B' : np.random.randn(10), 'C' : np.random.randn(10)})

      df.values

Out[]: 
array([[ 0.6612966 , -0.60985049,  1.11955054],
       [-0.74105636,  1.42532491, -0.74883362],
       [ 0.10406892,  0.5511436 ,  2.63730671],
       [-0.73027121, -0.11088373, -0.19143175],
       [ 0.11676573,  0.27582786, -0.38271609],
       [ 0.51073858, -0.3313141 ,  0.20516165],
       [ 0.23917755,  0.55362   , -0.62717194],
       [ 0.25565784, -1.4960713 ,  0.58886377],
       [ 1.20284041,  0.21173483,  2.0331718 ],
       [ 0.62247283,  2.18407105,  0.02431867]])

```

## 在 Python Pandas 中导入数据

Python Pandas DataFrame 能够读取几种数据格式，一些最常用的是:CSV、JSON、Excel、HDF5、SQL 等。

### CSV 到数据帧

最有用的功能之一是`read_csv`,它允许我们读取几乎任何格式的 csv 文件，并将其加载到我们的 Python Pandas 数据框架中进行处理。让我们看看如何处理 csv 文件:

```py
import pandas as pd
df=pd.read_csv('Filename.csv')
type(df)

Out[]: 
pandas.core.frame.DataFrame

```

这个简单的操作将 csv 文件加载到 Python Pandas 数据帧中，之后我们就可以像前面看到的那样研究它了。

### 定制熊猫进口

有时 csv 文件的格式带有特定的分隔符，或者我们需要特定的列或行。在 Python 熊猫教程的这一部分，我们现在将看到一些处理这种情况的方法。

在本例中，我们希望加载一个以空格作为分隔符的 csv 文件:

```py
import pandas as pd
df=pd.read_csv('Filename.csv', sep=' ')

```

在本例中，我们希望加载 0 和 5 列以及前 100 行:

```py
import pandas as pd
df=pd.read_csv('Filename.csv', usecols=[0,1,2,3,4,5], nrows=100)

```

可以定制标题、转换列名或行名，以及执行许多其他操作。

查看 Pandas 文档中的 IO 工具。

### 从 Excel 文件导入工作表

与我们处理 csv 文件的方式相同，我们可以使用`read_excel`函数处理 Excel 文件，让我们看一些例子:

在本例中，我们希望从 Excel 文件中加载工作表 1:

```py
import pandas as pd
df=pd.read_excel('Filename.xls', sheet_name='Sheet1')

```

这个简单的操作将工作表 1 从 Excel 文件加载到 Pandas 数据框架中。

## 索引和子集

一旦我们准备好 Python Pandas 数据框架，独立于我们的数据源(csv、Excel、hdf5 等)。)我们可以使用它，就像它是一个数据库表一样，选择我们感兴趣的元素。我们将使用一些例子来说明如何索引和提取数据子集。

让我们从加载一个包含市场工具详细信息的 csv 文件开始。

```py
In[]: 
 import pandas as pd
      df=pd.read_csv('MSFT.csv' , usecols=[0,1,2,3,4,5])
      df.head()
      df.shape

Out[]:
          Date        Open  High     Low    Close   Volume
    0   2008-12-29  19.1500 19.21   18.64   18.96   58512800.0
    1   2008-12-30  19.0100 19.49   19.00   19.34   43224100.0
    2   2008-12-31  19.3100 19.68   19.27   19.44   46419000.0
    3   2009-01-02  19.5328 20.40   19.37   20.33   50084000.0
    4   2009-01-05  20.2000 20.67   20.06   20.52   61475200.0

    (1000, 6)

```

这里，我们已经读取了一个 csv 文件，其中我们只需要日期、开盘、收盘、高、低和成交量(前 6 列)等列，我们检查了具有 1000 行和 6 列的数据帧的形式。

### 选择单个列

在前面的代码中，我们直接从 csv 文件中读取了前 6 列。这是我们应用的过滤器，因为我们只对那些列感兴趣。

我们可以对 Python Pandas 数据帧本身应用选择过滤器，以选择一列进行处理。例如，我们可能需要`Close`列:

```py
In[]: 
close=df['Close']
close.head()

Out[]:
        Close
    0   18.96   
    1   19.34   
    2   19.44   
    3   20.33   
    4   20.52

```

### 选择多列

我们也可以选择多个列:

```py
In[]: 
closevol=df[['Close', 'Volume']]
closevol.head()

Out[]:
        Close  Volume
    0   18.96   58512800.0
    1   19.34   43224100.0
    2   19.44   46419000.0
    3   20.33   50084000.0
    4   20.52   61475200.0

```

### 通过[]选择行。

我们可以通过索引选择一组行:

```py
In[]: 
 import pandas as pd
      df=pd.read_csv('TSLA.csv' )

      df[100:110]

Out[]:

```

| 
 | 日期 | 打开 | 高的 | 低的 | 关闭 | 卷 | 除息 | 分流比 | adopen | 和高 | AdjLow | 接近的 | AdjVolume | 名字 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| One hundred | 2017-10-30 | Three hundred and nineteen point one eight | 323.7800 | Three hundred and seventeen point two five | Three hundred and twenty point zero eight | Four million two hundred and thirty-six thousand and twenty-nine | Zero | One | Three hundred and nineteen point one eight | 323.7800 | Three hundred and seventeen point two five | Three hundred and twenty point zero eight | Four million two hundred and thirty-six thousand and twenty-nine | TSLA |
| One hundred and one | 2017-10-27 | Three hundred and nineteen point seven five | 324.5900 | Three hundred and sixteen point six six | Three hundred and twenty point eight seven | Six million nine hundred and forty-two thousand four hundred and ninety-three | Zero | One | Three hundred and nineteen point seven five | 324.5900 | Three hundred and sixteen point six six | Three hundred and twenty point eight seven | Six million nine hundred and forty-two thousand four hundred and ninety-three | TSLA |
| One hundred and two | 2017-10-26 | Three hundred and twenty-seven point seven eight | 330.2300 | Three hundred and twenty-three point two | Three hundred and twenty-six point one seven | Four million nine hundred and eighty thousand three hundred and sixteen | Zero | One | Three hundred and twenty-seven point seven eight | 330.2300 | Three hundred and twenty-three point two | Three hundred and twenty-six point one seven | Four million nine hundred and eighty thousand three hundred and sixteen | TSLA |
| One hundred and three | 2017-10-25 | Three hundred and thirty-six point seven | 337.5000 | Three hundred and twenty-three point five six | Three hundred and twenty-five point eight four | Eight million five hundred and forty-seven thousand seven hundred and sixty-four | Zero | One | Three hundred and thirty-six point seven | 337.5000 | Three hundred and twenty-three point five six | Three hundred and twenty-five point eight four | Eight million five hundred and forty-seven thousand seven hundred and sixty-four | TSLA |
| One hundred and four | 2017-10-24 | Three hundred and thirty-eight point eight | 342.8000 | Three hundred and thirty-six point one six | Three hundred and thirty-seven point three four | Four million four hundred and sixty-three thousand eight hundred and seven | Zero | One | Three hundred and thirty-eight point eight | 342.8000 | Three hundred and thirty-six point one six | Three hundred and thirty-seven point three four | Four million four hundred and sixty-three thousand eight hundred and seven | TSLA |
| One hundred and five | 2017-10-23 | Three hundred and forty-nine point eight eight | 349.9500 | Three hundred and thirty-six point two five | Three hundred and thirty-seven point zero two | Five million seven hundred and fifteen thousand eight hundred and seventeen | Zero | One | Three hundred and forty-nine point eight eight | 349.9500 | Three hundred and thirty-six point two five | Three hundred and thirty-seven point zero two | Five million seven hundred and fifteen thousand eight hundred and seventeen | TSLA |
| One hundred and six | 2017-10-20 | Three hundred and fifty-two point six nine | 354.5500 | Three hundred and forty-four point three four | Three hundred and forty-five point one | Four million eight hundred and eighty-eight thousand two hundred and twenty-one | Zero | One | Three hundred and fifty-two point six nine | 354.5500 | Three hundred and forty-four point three four | Three hundred and forty-five point one | Four million eight hundred and eighty-eight thousand two hundred and twenty-one | TSLA |
| One hundred and seven | 2017-10-19 | Three hundred and fifty-five point five six | 357.1465 | Three hundred and forty-eight point two | Three hundred and fifty-one point eight one | Five million thirty-two thousand eight hundred and eighty-four | Zero | One | Three hundred and fifty-five point five six | 357.1465 | Three hundred and forty-eight point two | Three hundred and fifty-one point eight one | Five million thirty-two thousand eight hundred and eighty-four | TSLA |
| One hundred and eight | 2017-10-18 | Three hundred and fifty-five point nine seven | 363.0000 | Three hundred and fifty-four point one three | Three hundred and fifty-nine point six five | Four million eight hundred and ninety-eight thousand eight hundred and eight | Zero | One | Three hundred and fifty-five point nine seven | 363.0000 | Three hundred and fifty-four point one three | Three hundred and fifty-nine point six five | Four million eight hundred and ninety-eight thousand eight hundred and eight | TSLA |
| One hundred and nine | 2017-10-17 | Three hundred and fifty point nine one | 356.2200 | Three hundred and fifty point zero seven | Three hundred and fifty-five point seven five | Three million two hundred and eighty thousand six hundred and seventy | Zero | One | Three hundred and fifty point nine one | 356.2200 | Three hundred and fifty point zero seven | Three hundred and fifty-five point seven five | Three million two hundred and eighty thousand six hundred and seventy | TSLA |

或者我们可以选择一组行和列:

```py
In[]: 
df[100:110][['Close', 'Volume']]

Out[]: 
        Close   Volume
100 320.08  4236029.0
101 320.87  6942493.0
102 326.17  4980316.0
103 325.84  8547764.0
104 337.34  4463807.0
105 337.02  5715817.0
106 345.10  4888221.0
107 351.81  5032884.0
108 359.65  4898808.0
109 355.75  3280670.0

```

### 通过选择。loc[](按标签)

使用`df.loc`,我们可以使用标签进行相同的选择:

要选择一组行，我们可以使用索引号作为标签编写以下代码:

```py
In[]: 
df.loc[100:110]

Out[]:

```

| 
 | 日期 | 打开 | 高的 | 低的 | 关闭 | 卷 | 除息 | 分流比 | adopen | AdjHigh | AdjLow | 接近的 | AdjVolume | 名字 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| One hundred | 2017-10-30 | Three hundred and nineteen point one eight | 323.7800 | Three hundred and seventeen point two five | Three hundred and twenty point zero eight | Four million two hundred and thirty-six thousand and twenty-nine | Zero | One | Three hundred and nineteen point one eight | 323.7800 | Three hundred and seventeen point two five | Three hundred and twenty point zero eight | Four million two hundred and thirty-six thousand and twenty-nine | TSLA |
| One hundred and one | 2017-10-27 | Three hundred and nineteen point seven five | 324.5900 | Three hundred and sixteen point six six | Three hundred and twenty point eight seven | Six million nine hundred and forty-two thousand four hundred and ninety-three | Zero | One | Three hundred and nineteen point seven five | 324.5900 | Three hundred and sixteen point six six | Three hundred and twenty point eight seven | Six million nine hundred and forty-two thousand four hundred and ninety-three | TSLA |
| One hundred and two | 2017-10-26 | Three hundred and twenty-seven point seven eight | 330.2300 | Three hundred and twenty-three point two | Three hundred and twenty-six point one seven | Four million nine hundred and eighty thousand three hundred and sixteen | Zero | One | Three hundred and twenty-seven point seven eight | 330.2300 | Three hundred and twenty-three point two | Three hundred and twenty-six point one seven | Four million nine hundred and eighty thousand three hundred and sixteen | TSLA |
| One hundred and three | 2017-10-25 | Three hundred and thirty-six point seven | 337.5000 | Three hundred and twenty-three point five six | Three hundred and twenty-five point eight four | Eight million five hundred and forty-seven thousand seven hundred and sixty-four | Zero | One | Three hundred and thirty-six point seven | 337.5000 | Three hundred and twenty-three point five six | Three hundred and twenty-five point eight four | Eight million five hundred and forty-seven thousand seven hundred and sixty-four | TSLA |
| One hundred and four | 2017-10-24 | Three hundred and thirty-eight point eight | 342.8000 | Three hundred and thirty-six point one six | Three hundred and thirty-seven point three four | Four million four hundred and sixty-three thousand eight hundred and seven | Zero | One | Three hundred and thirty-eight point eight | 342.8000 | Three hundred and thirty-six point one six | Three hundred and thirty-seven point three four | Four million four hundred and sixty-three thousand eight hundred and seven | TSLA |
| One hundred and five | 2017-10-23 | Three hundred and forty-nine point eight eight | 349.9500 | Three hundred and thirty-six point two five | Three hundred and thirty-seven point zero two | Five million seven hundred and fifteen thousand eight hundred and seventeen | Zero | One | Three hundred and forty-nine point eight eight | 349.9500 | Three hundred and thirty-six point two five | Three hundred and thirty-seven point zero two | Five million seven hundred and fifteen thousand eight hundred and seventeen | TSLA |
| One hundred and six | 2017-10-20 | Three hundred and fifty-two point six nine | 354.5500 | Three hundred and forty-four point three four | Three hundred and forty-five point one | Four million eight hundred and eighty-eight thousand two hundred and twenty-one | Zero | One | Three hundred and fifty-two point six nine | 354.5500 | Three hundred and forty-four point three four | Three hundred and forty-five point one | Four million eight hundred and eighty-eight thousand two hundred and twenty-one | TSLA |
| One hundred and seven | 2017-10-19 | Three hundred and fifty-five point five six | 357.1465 | Three hundred and forty-eight point two | Three hundred and fifty-one point eight one | Five million thirty-two thousand eight hundred and eighty-four | Zero | One | Three hundred and fifty-five point five six | 357.1465 | Three hundred and forty-eight point two | Three hundred and fifty-one point eight one | Five million thirty-two thousand eight hundred and eighty-four | TSLA |
| One hundred and eight | 2017-10-18 | Three hundred and fifty-five point nine seven | 363.0000 | Three hundred and fifty-four point one three | Three hundred and fifty-nine point six five | Four million eight hundred and ninety-eight thousand eight hundred and eight | Zero | One | Three hundred and fifty-five point nine seven | 363.0000 | Three hundred and fifty-four point one three | Three hundred and fifty-nine point six five | Four million eight hundred and ninety-eight thousand eight hundred and eight | TSLA |
| One hundred and nine | 2017-10-17 | Three hundred and fifty point nine one | 356.2200 | Three hundred and fifty point zero seven | Three hundred and fifty-five point seven five | Three million two hundred and eighty thousand six hundred and seventy | Zero | One | Three hundred and fifty point nine one | 356.2200 | Three hundred and fifty point zero seven | Three hundred and fifty-five point seven five | Three million two hundred and eighty thousand six hundred and seventy | TSLA |

或者我们可以像前面一样选择一组行和列:

```py
In[]: 
df.loc[100:110, ['Close', 'Volume']]

Out[]:
    Close   Volume
100 320.08  4236029.0
101 320.87  6942493.0
102 326.17  4980316.0
103 325.84  8547764.0
104 337.34  4463807.0
105 337.02  5715817.0
106 345.10  4888221.0
107 351.81  5032884.0
108 359.65  4898808.0
109 355.75  3280670.0
110 350.60  5353262.0

```

### 通过选择。iloc[](按职位)

通过`df.iloc`,我们可以使用整数位置进行相同的选择:

```py
In[]: 
df.iloc[100:110]

Out[]:

```

| 
 | 日期 | 打开 | 高的 | 低的 | 关闭 | 卷 | 除息 | 分流比 | adopen | 和高 | AdjLow | 接近的 | AdjVolume | 名字 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| One hundred | 2017-10-30 | Three hundred and nineteen point one eight | 323.7800 | Three hundred and seventeen point two five | Three hundred and twenty point zero eight | Four million two hundred and thirty-six thousand and twenty-nine | Zero | One | Three hundred and nineteen point one eight | 323.7800 | Three hundred and seventeen point two five | Three hundred and twenty point zero eight | Four million two hundred and thirty-six thousand and twenty-nine | TSLA |
| One hundred and one | 2017-10-27 | Three hundred and nineteen point seven five | 324.5900 | Three hundred and sixteen point six six | Three hundred and twenty point eight seven | Six million nine hundred and forty-two thousand four hundred and ninety-three | Zero | One | Three hundred and nineteen point seven five | 324.5900 | Three hundred and sixteen point six six | Three hundred and twenty point eight seven | Six million nine hundred and forty-two thousand four hundred and ninety-three | TSLA |
| One hundred and two | 2017-10-26 | Three hundred and twenty-seven point seven eight | 330.2300 | Three hundred and twenty-three point two | Three hundred and twenty-six point one seven | Four million nine hundred and eighty thousand three hundred and sixteen | Zero | One | Three hundred and twenty-seven point seven eight | 330.2300 | Three hundred and twenty-three point two | Three hundred and twenty-six point one seven | Four million nine hundred and eighty thousand three hundred and sixteen | TSLA |
| One hundred and three | 2017-10-25 | Three hundred and thirty-six point seven | 337.5000 | Three hundred and twenty-three point five six | Three hundred and twenty-five point eight four | Eight million five hundred and forty-seven thousand seven hundred and sixty-four | Zero | One | Three hundred and thirty-six point seven | 337.5000 | Three hundred and twenty-three point five six | Three hundred and twenty-five point eight four | Eight million five hundred and forty-seven thousand seven hundred and sixty-four | TSLA |
| One hundred and four | 2017-10-24 | Three hundred and thirty-eight point eight | 342.8000 | Three hundred and thirty-six point one six | Three hundred and thirty-seven point three four | Four million four hundred and sixty-three thousand eight hundred and seven | Zero | One | Three hundred and thirty-eight point eight | 342.8000 | Three hundred and thirty-six point one six | Three hundred and thirty-seven point three four | Four million four hundred and sixty-three thousand eight hundred and seven | TSLA |
| One hundred and five | 2017-10-23 | Three hundred and forty-nine point eight eight | 349.9500 | Three hundred and thirty-six point two five | Three hundred and thirty-seven point zero two | Five million seven hundred and fifteen thousand eight hundred and seventeen | Zero | One | Three hundred and forty-nine point eight eight | 349.9500 | Three hundred and thirty-six point two five | Three hundred and thirty-seven point zero two | Five million seven hundred and fifteen thousand eight hundred and seventeen | TSLA |
| One hundred and six | 2017-10-20 | Three hundred and fifty-two point six nine | 354.5500 | Three hundred and forty-four point three four | Three hundred and forty-five point one | Four million eight hundred and eighty-eight thousand two hundred and twenty-one | Zero | One | Three hundred and fifty-two point six nine | 354.5500 | Three hundred and forty-four point three four | Three hundred and forty-five point one | Four million eight hundred and eighty-eight thousand two hundred and twenty-one | TSLA |
| One hundred and seven | 2017-10-19 | Three hundred and fifty-five point five six | 357.1465 | Three hundred and forty-eight point two | Three hundred and fifty-one point eight one | Five million thirty-two thousand eight hundred and eighty-four | Zero | One | Three hundred and fifty-five point five six | 357.1465 | Three hundred and forty-eight point two | Three hundred and fifty-one point eight one | Five million thirty-two thousand eight hundred and eighty-four | TSLA |
| One hundred and eight | 2017-10-18 | Three hundred and fifty-five point nine seven | 363.0000 | Three hundred and fifty-four point one three | Three hundred and fifty-nine point six five | Four million eight hundred and ninety-eight thousand eight hundred and eight | Zero | One | Three hundred and fifty-five point nine seven | 363.0000 | Three hundred and fifty-four point one three | Three hundred and fifty-nine point six five | Four million eight hundred and ninety-eight thousand eight hundred and eight | TSLA |
| One hundred and nine | 2017-10-17 | Three hundred and fifty point nine one | 356.2200 | Three hundred and fifty point zero seven | Three hundred and fifty-five point seven five | Three million two hundred and eighty thousand six hundred and seventy | Zero | One | Three hundred and fifty point nine one | 356.2200 | Three hundred and fifty point zero seven | Three hundred and fifty-five point seven five | Three million two hundred and eighty thousand six hundred and seventy | TSLA |

在最后一个例子中，我们使用索引作为整数位置，而不是标签。

我们可以像前面一样选择一组行和列:

```py
In[]: 
df.iloc[100:110, [3, 4]]

Out[]:
      Low   Close
100 317.25  320.08
101 316.66  320.87
102 323.20  326.17
103 323.56  325.84
104 336.16  337.34
105 336.25  337.02
106 344.34  345.10
107 348.20  351.81
108 354.13  359.65
109 350.07  355.75

```

### 布尔索引

到目前为止，在 Python Pandas 教程中，我们已经按照标签或位置对数据子集进行了切片。现在让我们看看如何选择符合某些标准的数据。我们通过布尔索引来实现这一点。我们可以使用与 Numpy 数组相似的标准。这里我们只向您展示两个说明性的例子。这并不足以让你熟悉它，所以鼓励你去查阅文档和本章末尾的进一步阅读来了解更多。

*   我们可以过滤大于(小于)一个数字的数据。

```py
In[]: 
df[df.Close > 110]

Out[]:

```

| 
 | 日期 | 打开 | 高的 | 低的 | 关闭 | 卷 | 除息 | 分流比 | adopen | 和高 | AdjLow | 接近的 | AdjVolume | 名字 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Zero | 2018-03-27 | Three hundred and four | 304.2700 | 277.1800 | 279.1800 | Thirteen million six hundred and ninety-six thousand one hundred and sixty-eight | Zero | One | Three hundred and four | 304.2700 | 277.1800 | 279.1800 | Thirteen million six hundred and ninety-six thousand one hundred and sixty-eight | TSLA |
| one | 2018-03-26 | Three hundred and seven point three four | 307.5900 | 291.3600 | 304.1800 | Eight million three hundred and twenty-four thousand six hundred and thirty-nine | Zero | One | Three hundred and seven point three four | 307.5900 | 291.3600 | 304.1800 | Eight million three hundred and twenty-four thousand six hundred and thirty-nine | TSLA |
| Two | 2018-03-23 | Three hundred and eleven point two five | 311.6100 | 300.4500 | 301.5400 | Six million six hundred thousand five hundred and thirty-eight | Zero | One | Three hundred and eleven point two five | 311.6100 | 300.4500 | 301.5400 | Six million six hundred thousand five hundred and thirty-eight | TSLA |
| 
 | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |
| One thousand and eighty | 2013-12-09 | One hundred and thirty-seven | 141.7000 | 134.2100 | 141.6000 | Nine million sixty-one thousand five hundred | Zero | One | One hundred and thirty-seven | 141.7000 | 134.2100 | 141.6000 | Nine million sixty-one thousand five hundred | TSLA |
| One thousand and eighty-one | 2013-12-06 | One hundred and forty-one point five one | 142.4900 | 136.3000 | 137.3600 | Seven million nine hundred and nine thousand six hundred | Zero | One | One hundred and forty-one point five one | 142.4900 | 136.3000 | 137.3600 | Seven million nine hundred and nine thousand six hundred | TSLA |
| One thousand and eighty-two | 2013-12-05 | One hundred and forty point one five | 143.3500 | 139.5000 | 140.4800 | Nine million two hundred and eighty-eight thousand four hundred | Zero | One | One hundred and forty point one five | 143.3500 | 139.5000 | 140.4800 | Nine million two hundred and eighty-eight thousand four hundred | TSLA |

1083 行× 14 列

```py
In[]: 
df[(df['Close'] > 110) | (df['Close'] < 120)]

Out[]:
`

```

| 
 | 日期 | 打开 | 高的 | 低的 | 关闭 | 卷 | 除息 | 分流比 | adopen | 和高 | AdjLow | 接近的 | AdjVolume | 名字 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Zero | 2018-03-27 | Three hundred and four | 304.2700 | 277.1800 | 279.1800 | Thirteen million six hundred and ninety-six thousand one hundred and sixty-eight | Zero | One | Three hundred and four | 304.2700 | 277.1800 | 279.1800 | Thirteen million six hundred and ninety-six thousand one hundred and sixty-eight | TSLA |
| one | 2018-03-26 | Three hundred and seven point three four | 307.5900 | 291.3600 | 304.1800 | Eight million three hundred and twenty-four thousand six hundred and thirty-nine | Zero | One | Three hundred and seven point three four | 307.5900 | 291.3600 | 304.1800 | Eight million three hundred and twenty-four thousand six hundred and thirty-nine | TSLA |
| Two | 2018-03-23 | Three hundred and eleven point two five | 311.6100 | 300.4500 | 301.5400 | Six million six hundred thousand five hundred and thirty-eight | Zero | One | Three hundred and eleven point two five | 311.6100 | 300.4500 | 301.5400 | Six million six hundred thousand five hundred and thirty-eight | TSLA |
| 
 | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |
| One thousand and eighty | 2013-12-09 | One hundred and thirty-seven | 141.7000 | 134.2100 | 141.6000 | Nine million sixty-one thousand five hundred | Zero | One | One hundred and thirty-seven | 141.7000 | 134.2100 | 141.6000 | Nine million sixty-one thousand five hundred | TSLA |
| One thousand and eighty-one | 2013-12-06 | One hundred and forty-one point five one | 142.4900 | 136.3000 | 137.3600 | Seven million nine hundred and nine thousand six hundred | Zero | One | One hundred and forty-one point five one | 142.4900 | 136.3000 | 137.3600 | Seven million nine hundred and nine thousand six hundred | TSLA |
| One thousand and eighty-two | 2013-12-05 | One hundred and forty point one five | 143.3500 | 139.5000 | 140.4800 | Nine million two hundred and eighty-eight thousand four hundred | Zero | One | One hundred and forty point one five | 143.3500 | 139.5000 | 140.4800 | Nine million two hundred and eighty-eight thousand four hundred | TSLA |

1083 行× 14 列

## 操纵 Python 熊猫数据帧

当我们处理数据时，最常见的结构是数据帧。我们已经在 Python 熊猫教程中看到了如何创建它们、进行选择和查找数据。我们现在将看到如何操作 Python Pandas 数据帧，以将其转换为另一个 Python Pandas 数据帧，该数据帧具有我们的问题所需的形式。

我们将看到如何对它进行排序、重新索引、消除不需要的(或虚假的)数据、添加或删除列以及更新值。

### 。移调

Python Pandas 数据帧转置函数`T`允许我们将行转置为列，逻辑上将列转置为行:

```py
In[]: import pandas as pd
      df=pd.read_csv('TSLA.csv' )
      df2=df[100:110][['Close', 'Volume']]

      df2.T

Out[]:

```

| 
 | One hundred | One hundred and one | One hundred and two | One hundred and three | One hundred and four | One hundred and five | One hundred and six | One hundred and seven | One hundred and eight | One hundred and nine |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 关闭 | Three hundred and twenty point zero eight | Three hundred and twenty point eight seven | Three hundred and twenty-six point one seven | Three hundred and twenty-five point eight four | Three hundred and thirty-seven point three four | Three hundred and thirty-seven point zero two | Three hundred and forty-five point one | Three hundred and fifty-one point eight one | Three hundred and fifty-nine point six five | Three hundred and fifty-five point seven five |
| 卷 | Four million two hundred and thirty-six thousand and twenty-nine | Six million nine hundred and forty-two thousand four hundred and ninety-three | Four million nine hundred and eighty thousand three hundred and sixteen | Eight million five hundred and forty-seven thousand seven hundred and sixty-four | Four million four hundred and sixty-three thousand eight hundred and seven | Five million seven hundred and fifteen thousand eight hundred and seventeen | Four million eight hundred and eighty-eight thousand two hundred and twenty-one | Five million thirty-two thousand eight hundred and eighty-four | Four million eight hundred and ninety-eight thousand eight hundred and eight | Three million two hundred and eighty thousand six hundred and seventy |

### 。排序索引()

当我们使用 Python Pandas Dataframe 时，通常会添加或删除行，按列排序等。这就是为什么拥有一个能够让我们轻松舒适地按照索引对 Python Pandas 数据帧进行排序的函数非常重要。我们用 Pandas DataFrame 的`sort_index`函数来做这件事。

```py
In[]:
 df.sort_index()

Out[]:

```

| 
 | 日期 | 打开 | 高的 | 低的 | 关闭 | 卷 | 除息 | 分流比 | adopen | 和高 | AdjLow | 接近的 | AdjVolume | 名字 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Zero | 2018-03-27 | Three hundred and four | 304.2700 | 277.1800 | 279.1800 | Thirteen million six hundred and ninety-six thousand one hundred and sixty-eight | Zero | One | Three hundred and four | 304.2700 | 277.1800 | 279.1800 | Thirteen million six hundred and ninety-six thousand one hundred and sixty-eight | TSLA |
| one | 2018-03-26 | Three hundred and seven point three four | 307.5900 | 291.3600 | 304.1800 | Eight million three hundred and twenty-four thousand six hundred and thirty-nine | Zero | One | Three hundred and seven point three four | 307.5900 | 291.3600 | 304.1800 | Eight million three hundred and twenty-four thousand six hundred and thirty-nine | TSLA |
| Two | 2018-03-23 | Three hundred and eleven point two five | 311.6100 | 300.4500 | 301.5400 | Six million six hundred thousand five hundred and thirty-eight | Zero | One | Three hundred and eleven point two five | 311.6100 | 300.4500 | 301.5400 | Six million six hundred thousand five hundred and thirty-eight | TSLA |
| 
 | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

### 。排序值()

有时，我们可能对按照某一列或者甚至几列作为标准对 Python Pandas 数据帧进行排序感兴趣。例如，按名字对列进行排序，按姓氏对第二个条件进行排序。我们用 Python Pandas DataFrame 的`sort_values`函数来做这件事。

```py
In[]: 
df.sort_values(by='Close')

Out[]:

```

| 
 | 日期 | 打开 | 高的 | 低的 | 关闭 | 卷 | 除息 | 分流比 | adopen | 和高 | AdjLow | 接近的 | AdjVolume | 名字 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| One thousand and eighty-one | 2013-12-06 | One hundred and forty-one point five one | 142.4900 | 136.3000 | 137.3600 | Seven million nine hundred and nine thousand six hundred | Zero | One | One hundred and forty-one point five one | 142.4900 | 136.3000 | 137.3600 | Seven million nine hundred and nine thousand six hundred | TSLA |
| One thousand and fifty-seven | 2014-01-13 | One hundred and forty-five point seven eight | 147.0000 | 137.8200 | 139.3400 | Six million three hundred and sixteen thousand one hundred | Zero | One | One hundred and forty-five point seven eight | 147.0000 | 137.8200 | 139.3400 | Six million three hundred and sixteen thousand one hundred | TSLA |
| One thousand and seventy-eight | 2013-12-11 | One hundred and forty-one point eight eight | 143.0500 | 139.4900 | 139.6500 | Seven million one hundred and thirty-seven thousand eight hundred | Zero | One | One hundred and forty-one point eight eight | 143.0500 | 139.4900 | 139.6500 | Seven million one hundred and thirty-seven thousand eight hundred | TSLA |
| 
 | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

```py
In[]: 
df.sort_values(by=['Open', 'Close'])

Out[]:

```

| 
 | 日期 | 打开 | 高的 | 低的 | 关闭 | 卷 | 除息 | 分流比 | adopen | 和高 | AdjLow | 接近的 | AdjVolume | 名字 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| One thousand and eighty | 2013-12-09 | One hundred and thirty-seven | 141.7000 | 134.2100 | 141.6000 | Nine million sixty-one thousand five hundred | Zero | One | One hundred and thirty-seven | 141.7000 | 134.2100 | 141.6000 | Nine million sixty-one thousand five hundred | TSLA |
| One thousand and seventy-seven | 2013-12-12 | One hundred and thirty-nine point seven | 148.2400 | 138.5300 | 147.4700 | Ten million seven hundred and sixty-seven thousand eight hundred | Zero | One | One hundred and thirty-nine point seven | 148.2400 | 138.5300 | 147.4700 | Ten million seven hundred and sixty-seven thousand eight hundred | TSLA |
| One thousand and seventy-nine | 2013-12-10 | One hundred and forty point zero five | 145.8700 | 139.8600 | 142.1900 | Ten million seven hundred and forty-eight thousand two hundred | Zero | One | One hundred and forty point zero five | 145.8700 | 139.8600 | 142.1900 | Ten million seven hundred and forty-eight thousand two hundred | TSLA |
| 
 | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

### 。reindex()

Python Pandas 的 reindex 函数让我们重新排列系列或数据帧的索引，当我们需要重新组织索引以满足某些标准时，这很有用。

例如，我们可以使用之前创建的序列或数据帧来改变原始索引。例如，当索引是一个标签时，我们可以根据需要进行重组:

```py
In[]: import pandas as pd
      import numpy as np
      df = pd.DataFrame(np.random.randn(5), index=['a', 'b', 'c', 'd', 'e'])

      df

Out[]:

```

| 
 | Zero |
| --- | --- |
| a | -0.134133 |
| b | -0.586051 |
| c | 1.179358 |
| d | 0.433142 |
| e | -0.365686 |

现在，我们可以将索引重组如下:

```py
In[]: 
df.reindex(['b', 'a', 'd', 'c', 'e'])

Out[]:

```

| 
 | Zero |
| --- | --- |
| b | -0.586051 |
| a | -0.134133 |
| d | 0.433142 |
| c | 1.179358 |
| e | -0.365686 |

当索引是数字时，我们可以使用相同的函数来手动排序索引:

```py
In[]: 
 import pandas as pd
      import numpy as np
      df = pd.DataFrame(np.random.randn(5))
      df.reindex([4,3,2,1,0])

Out[]:

```

| 
 | Zero |
| --- | --- |
| four | 1.058589 |
| three | 1.194400 |
| Two | -0.645806 |
| one | 0.836606 |
| Zero | 1.288102 |

在本节的后面，我们将看到如何工作和重组日期和时间索引。

### 添加新列。例如，对于 df['新列'] = 1

Python Pandas 数据帧的另一个有趣特性是可以向现有数据帧添加新列。

例如，我们可以向之前创建的随机数据帧添加一个新列:

```py
In[]: 
import pandas as pd
import numpy as np
df = pd.DataFrame(np.random.randn(5))

Out[]:

```

| 
 | Zero |
| --- | --- |
| Zero | 0.238304 |
| one | 2.068558 |
| Two | 1.015650 |
| three | 0.506208 |
| four | 0.214760 |

要添加一个新列，我们只需要在数据帧中包含新列名并分配一个初始化值，或者给新列分配一个 Pandas 系列或其他数据帧中的另一列。

```py
In[]: 
df['new']=1
df

Out[]:

```

| 
 | 
 | Zero | 新的 |
| --- | --- | --- | --- |
| 
 | Zero | 0.238304 | one |
| 
 | one | 2.068558 | one |
| 
 | Two | 1.015650 | one |
| 
 | three | 0.506208 | one |
| 
 | four | 0.214760 | one |

### 删除现有列

同样，我们可以从 Python Pandas 数据帧中删除一个或多个列。让我们用随机值创建一个 5 行 4 列的数据帧来删除一列。

```py
In[]: 

import pandas as pd
import numpy as np
df = pd.DataFrame(np.random.randn(5, 4))
df

Out[]:

```

| 
 | 
 | Zero | one | Two | three |
| --- | --- | --- | --- | --- | --- |
| 
 | Zero | -1.171562 | -0.086348 | -1.971855 | 1.168017 |
| 
 | one | -0.408317 | -0.061397 | -0.542212 | -1.412755 |
| 
 | Two | -0.365539 | -0.587147 | 1.494690 | 1.756105 |
| 
 | three | 0.642882 | 0.924202 | 0.517975 | -0.914366 |
| 
 | four | 0.777869 | -0.431151 | -0.401093 | 0.145646 |

现在，我们可以删除通过索引或标签(如果有)指定的列:

```py
In[]: 
del df[0]

Out[]:

```

| 
 | 
 | one | Two | three |
| --- | --- | --- | --- | --- |
| 
 | Zero | -0.086348 | -1.971855 | 1.168017 |
| 
 | one | -0.061397 | -0.542212 | -1.412755 |
| 
 | Two | -0.587147 | 1.494690 | 1.756105 |
| 
 | three | 0.924202 | 0.517975 | -0.914366 |
| 
 | four | -0.431151 | -0.401093 | 0.145646 |

```py
In[]: 
df['new']=1
df

Out[]:

```

| 
 | 
 | Zero | 新的 |
| --- | --- | --- | --- |
| 
 | Zero | 0.238304 | one |
| 
 | one | 2.068558 | one |
| 
 | Two | 1.015650 | one |
| 
 | three | 0.506208 | one |

```py
In[]: 
del df['new']

Out[]:

```

| 
 | 
 | Zero |
| --- | --- | --- |
| 
 | Zero | 0.238304 |
| 
 | one | 2.068558 |
| 
 | Two | 1.015650 |
| 
 | three | 0.506208 |

### 。位于[](按标签)

使用`at`,我们可以通过行和列标签定位特定值，如下所示:

```py
In[]: 
import pandas as pd
import numpy as np
df=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
print(df)

df.at['a', 'A']

Out[]:

```

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 0.996496 | -0.165002 | 0.727912 | 0.564858 |
| b | -0.388169 | 1.171039 | -0.231934 | -1.124595 |
| c | -1.385129 | 0.299195 | 0.573570 | -1.736860 |
| d | 1.222447 | -0.312667 | 0.957139 | -0.054156 |
| e | 1.188335 | 0.679921 | 1.508681 | -0.677776 |

```py
In[]: 
df.at['a', 'A']

Out[]: 

0.9964957014209125

```

也可以用相同的功能分配一个新值:

```py
In[]: 
df.at['a', 'A'] = 0

Out[]:

```

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 0.000000 | -0.165002 | 0.727912 | 0.564858 |
| b | -0.388169 | 1.171039 | -0.231934 | -1.124595 |
| c | -1.385129 | 0.299195 | 0.573570 | -1.736860 |
| d | 1.222447 | -0.312667 | 0.957139 | -0.054156 |
| e | 1.188335 | 0.679921 | 1.508681 | -0.677776 |

### 。iat[](按职位)

使用`iat`,我们可以通过行和列索引定位特定值，如下所示:

```py
In[]: 
 import pandas as pd
      import numpy as np
      df=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
      print(df)

      df.iat[0, 0]

Out[]: 
0.996496

```

也可以用相同的功能分配一个新值:

```py
In[]: 
df.iat[0, 0] = 0

Out[]:

```

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 0.000000 | -0.165002 | 0.727912 | 0.564858 |
| b | -0.388169 | 1.171039 | -0.231934 | -1.124595 |
| c | -1.385129 | 0.299195 | 0.573570 | -1.736860 |
| d | 1.222447 | -0.312667 | 0.957139 | -0.054156 |
| e | 1.188335 | 0.679921 | 1.508681 | -0.677776 |

### 值的条件更新。例如，对于 df[df > 0] = 1

另一个有用的功能是更新符合某些标准的值，例如，更新值大于 0 的值:

```py
In[]: 
import pandas as pd
import numpy as np
df=pd.DataFrame(np.random.randn(5, 4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
print(df)

df[df > 0] = 1
df

Out[]:

```

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 1.000000 | -0.082466 | 1.000000 | -0.728372 |
| b | -0.784404 | -0.663096 | -0.595112 | 1.000000 |
| c | -1.460702 | -1.072931 | -0.761314 | 1.000000 |
| d | 1.000000 | 1.000000 | 1.000000 | -0.302310 |
| e | -0.488556 | 1.000000 | -0.798716 | -0.590920 |

我们还可以更新满足某些标准的特定列的值，甚至可以使用几个列作为标准并更新特定的列。

```py
In[]: 
df['A'][df['A'] < 0] = 1
print(df)

Out[]:

```

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | One | -0.082466 | 1.000000 | -0.728372 |
| b | One | -0.663096 | -0.595112 | 1.000000 |
| c | One | -1.072931 | -0.761314 | 1.000000 |
| d | One | 1.000000 | 1.000000 | -0.302310 |
| e | One | 1.000000 | -0.798716 | -0.590920 |

```py
In[]: 
df['A'][(df['B'] < 0 )& (df['C'] < 0)] = 9
print(df)

Out[]:

```

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | One | -0.082466 | 1.000000 | -0.728372 |
| b | Nine | -0.663096 | -0.595112 | 1.000000 |
| c | Nine | -1.072931 | -0.761314 | 1.000000 |
| d | One | 1.000000 | 1.000000 | -0.302310 |
| e | One | 1.000000 | -0.798716 | -0.590920 |

### 。德罗普纳()

偶尔，我们可能会有一个 Python Pandas 数据帧，出于某种原因，它包含 NA 值。当我们进行计算或运算时，这种类型的值通常是有问题的，必须在处理它们之前正确处理。

消除 NA 值的最简单方法是删除包含它的行。

```py
In[]: 
import pandas as pd
import numpy as np
df=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
print(df)

Out[]:

```

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 1.272361 | 1.799535 | -0.593619 | 1.152889 |
| b | -0.318368 | -0.190419 | 0.129420 | 1.551332 |
| c | 0.166951 | 1.669034 | -1.653618 | 0.656313 |
| d | 0.219999 | 0.951074 | 0.442325 | -0.170177 |
| e | 0.312319 | -0.765930 | -1.641234 | -1.388924 |

```py
In[]: 
df['A'][(df['B'] < 0 )& (df['C'] < 0)] = np.nan
print(df)

Out[]:

```

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 1.272361 | 1.799535 | -0.593619 | 1.152889 |
| b | -0.318368 | -0.190419 | 0.129420 | 1.551332 |
| c | 0.166951 | 1.669034 | -1.653618 | 0.656313 |
| d | 0.219999 | 0.951074 | 0.442325 | -0.170177 |
| e | 圆盘烤饼 | -0.765930 | -1.641234 | -1.388924 |

```py
In[]: 
df=df.dropna()
print(df)

Out[]:

```

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 1.272361 | 1.799535 | -0.593619 | 1.152889 |
| b | -0.318368 | -0.190419 | 0.129420 | 1.551332 |
| c | 0.166951 | 1.669034 | -1.653618 | 0.656313 |
| d | 0.219999 | 0.951074 | 0.442325 | -0.170177 |

在这里，我们删除了在其任何列中具有 NaN 值的整行，但是我们也可以指定删除其任何值为 NaN 的列:

```py
df=df.dropna(axis=1)
print(df)

```

我们可以指定单个 NaN 值是否足以删除行或列，或者是否整行或整列都必须有 NaN 才能删除。

```py
```thon
df=df.dropna(how='all')
print(df)

```py

### 。菲尔娜

通过前面的函数，我们已经看到了如何消除包含一个或所有值的完整行或列。如果行或列中有有效值，这个操作可能会有点激烈。

为此，使用`fillna`函数将 NaN 值替换为某个固定值是很有趣的。

```
In[]: 
import pandas as pd
import numpy as np
df=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
print(df)

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 1.272361 | 1.799535 | -0.593619 | 1.152889 |
| b | -0.318368 | -0.190419 | 0.129420 | 1.551332 |
| c | 0.166951 | 1.669034 | -1.653618 | 0.656313 |
| d | 0.219999 | 0.951074 | 0.442325 | -0.170177 |
| e | 0.312319 | -0.765930 | -1.641234 | -1.388924 |

```
In[]: 
df['A'][(df['B'] < 0 )& (df['C'] < 0)] = np.nan
print(df)

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 1.272361 | 1.799535 | -0.593619 | 1.152889 |
| b | -0.318368 | -0.190419 | 0.129420 | 1.551332 |
| c | 0.166951 | 1.669034 | -1.653618 | 0.656313 |
| d | 0.219999 | 0.951074 | 0.442325 | -0.170177 |
| e | 圆盘烤饼 | -0.765930 | -1.641234 | -1.388924 |

```
In[]: 
df=df.fillna(999)
print(df)

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 1.272361 | 1.799535 | -0.593619 | 1.152889 |
| b | -0.318368 | -0.190419 | 0.129420 | 1.551332 |
| c | 0.166951 | 1.669034 | -1.653618 | 0.656313 |
| d | 0.219999 | 0.951074 | 0.442325 | -0.170177 |
| e | Nine hundred and ninety-nine | -0.765930 | -1.641234 | -1.388924 |

### 。应用()

`apply`是一种非常有用的方法，可以在数据帧中使用函数或方法，而不必遍历它。

我们可以对系列或数据帧应用 apply 函数，以便对数据帧的所有行或列应用函数。让我们看一些例子。

假设我们正在处理随机生成的 Python 熊猫数据帧，并且需要应用一个函数。在这个例子中，为了简单起见，我们将创建一个自定义函数来计算一个数字的平方。

```
In[]: 
import pandas as pd
import numpy as np
df=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
print(df)

Out[]:
`

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | -0.633249 | -2.699088 | 0.574052 | 0.652742 |
| b | 0.060295 | -0.150527 | 0.149123 | -0.701216 |
| c | -0.052515 | 0.469481 | 0.899180 | -0.608409 |
| d | -1.352912 | 0.103302 | 0.457878 | -1.897170 |
| e | 0.088279 | 0.418317 | -1.102989 | 0.582455 |

```
def square_number(number):
  return number**2

# Test the function
In[]: 
square_number(2)

Out[]: 
4

```py

现在，让我们通过应用来使用自定义函数:

```
In[]: 
df.apply(square_number, axis=1)

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 0.401005 | 7.285074 | 0.329536 | 0.426073 |
| b | 0.003636 | 0.022658 | 0.022238 | 0.491704 |
| c | 0.002758 | 0.220412 | 0.808524 | 0.370161 |
| d | 1.830372 | 0.010671 | 0.209652 | 3.599253 |
| e | 0.007793 | 0.174989 | 1.216586 | 0.339254 |

这个方法`apply`将函数`square_number`应用于数据帧的所有行。

### 。shift()

`shift`功能允许我们向左或向右移动一行和/或向上或向下移动一列。让我们看一些例子。

首先，我们将向下移动列的值:

```
In[]: 
import pandas as pd
import numpy as np
df=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
print(df)

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | -0.633249 | -2.699088 | 0.574052 | 0.652742 |
| b | 0.060295 | -0.150527 | 0.149123 | -0.701216 |
| c | -0.052515 | 0.469481 | 0.899180 | -0.608409 |
| d | -1.352912 | 0.103302 | 0.457878 | -1.897170 |
| e | 0.088279 | 0.418317 | -1.102989 | 0.582455 |

```
In[]: 
df['D'].shift(1)

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | -0.633249 | -2.699088 | 0.574052 | 圆盘烤饼 |
| b | 0.060295 | -0.150527 | 0.149123 | 0.652742 |
| c | -0.052515 | 0.469481 | 0.899180 | -0.701216 |
| d | -1.352912 | 0.103302 | 0.457878 | -0.608409 |
| e | 0.088279 | 0.418317 | -1.102989 | -1.897170 |

我们将向上移动一列的值

```
In[]: 
df['shift'] = df['D'].shift(-1)

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | -0.633249 | -2.699088 | 0.574052 | -0.701216 |
| b | 0.060295 | -0.150527 | 0.149123 | -0.608409 |
| c | -0.052515 | 0.469481 | 0.899180 | -1.897170 |
| d | -1.352912 | 0.103302 | 0.457878 | 0.582455 |
| e | 0.088279 | 0.418317 | -1.102989 | 圆盘烤饼 |

这对于比较当前值和先前值非常有用。

## 统计探索性数据分析

Python Pandas DataFrame 允许我们进行一些描述性统计计算，这对我们处理的数据进行初步分析非常有用。来看看一些有用的函数。

### 信息()

了解我们的数据帧的结构和格式是一个很好的做法，`Info`函数正好为我们提供了这一点:

```
In[]: 
import pandas as pd
import numpy as np
df=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
print(df)

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | -0.633249 | -2.699088 | 0.574052 | 0.652742 |
| b | 0.060295 | -0.150527 | 0.149123 | -0.701216 |
| c | -0.052515 | 0.469481 | 0.899180 | -0.608409 |
| d | -1.352912 | 0.103302 | 0.457878 | -1.897170 |
| e | 0.088279 | 0.418317 | -1.102989 | 0.582455 |

```
In[]: 
df.info()

Out[]:
       <class 'pandas.core.frame.DataFrame'>
      Index: 5 entries, a to e
      Data columns (total 5 columns):
      A        5 non-null float64
      B        5 non-null float64
      C        5 non-null float64
      D        5 non-null float64
      shift    4 non-null float64
      dtypes: float64(5)
      memory usage: 240.0+ bytes

```py

### 描述()

我们可以通过“描述”功能获得数据框架的统计概览，它给出了平均值、中间值、标准偏差、最大值、最小值、四分位数等。每个数据帧列的。

```
In[]: 
import pandas as pd
import numpy as np
df=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
print(df)

Out[]:
`

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | -0.633249 | -2.699088 | 0.574052 | 0.652742 |
| b | 0.060295 | -0.150527 | 0.149123 | -0.701216 |
| c | -0.052515 | 0.469481 | 0.899180 | -0.608409 |
| d | -1.352912 | 0.103302 | 0.457878 | -1.897170 |
| e | 0.088279 | 0.418317 | -1.102989 | 0.582455 |

```
In[]: 
df.describe()

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| 数数 | 5.000000 | 5.000000 | 5.000000 | 5.000000 |
| 意思是 | -0.378020 | -0.371703 | 0.195449 | -0.394319 |
| 标准 | 0.618681 | 1.325046 | 0.773876 | 1.054633 |
| 部 | -1.352912 | -2.699088 | -1.102989 | -1.897170 |
| 25% | -0.633249 | -0.150527 | 0.149123 | -0.701216 |
| 50% | -0.052515 | 0.103302 | 0.457878 | -0.608409 |
| 75% | 0.060295 | 0.418317 | 0.574052 | 0.582455 |
| 最大 | 0.088279 | 0.469481 | 0.899180 | 0.652742 |

### 。值计数()

函数`value_counts`计算指定列的重复值:

```
In[]: 
df['A'].value_counts()

Out[]: 
 0.088279    1
      -0.052515    1
       0.060295    1
      -0.633249    1
      -1.352912    1
      Name: A, dtype: int64

```py

### 。平均值()

我们可以通过`mean`函数获得特定列或行的平均值。

```
In[]:
df['A'].mean() # specifying a column 
Out[]: 
-0.3780203497252693
`

```py

```
In[]: 
df.mean() # by column
df.mean(axis=0) # by column

Out[]:
        A       -0.378020
        B       -0.371703
        C        0.195449
        D       -0.394319
        shift   -0.638513
        dtype: float64
`

```py

```
In[]:
df.mean(axis=1) # by row

Out[]:
        a   -0.526386
        b    0.002084
        c    0.001304
        d   -0.659462
        e   -0.382222
        dtype: float64

```py

### 。标准()

我们可以通过`std`函数获得特定列或行的标准偏差。

```
In[]: 
df['A'].std() # specifying a column

Out[]: 
0.6186812554819784
`

```py

```
In[]: 
df.std() # by column
df.std(axis=0) # by column

Out[]:
        A        0.618681
        B        1.325046
        C        0.773876
        D        1.054633
        shift    1.041857
        dtype: float64
`

```py

```
In[]: 
df.std(axis=1) # by row

Out[]:  
 a    1.563475
        b    0.491499
        c    0.688032
        d    0.980517
        e    1.073244
        dtype: float64

```py

## 过滤 Python 熊猫数据帧

我们已经看到了如何在 Python Pandas 数据框架中过滤数据，包括使用一些逻辑标准过滤行或列的逻辑语句。让我们记住一些例子:

例如，我们将筛选列“A”大于零的行:

```
In[]: 
import numpy as np
df=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
print(df)

Out[]:
`

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | -0.633249 | -2.699088 | 0.574052 | 0.652742 |
| b | 0.060295 | -0.150527 | 0.149123 | -0.701216 |
| c | -0.052515 | 0.469481 | 0.899180 | -0.608409 |
| d | -1.352912 | 0.103302 | 0.457878 | -1.897170 |
| e | 0.088279 | 0.418317 | -1.102989 | 0.582455 |

```
In[]:
df_filtered = df[df['A'] > 0]
print(df_filtered)

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| b | 0.060295 | -0.150527 | 0.149123 | -0.701216 |
| e | 0.088279 | 0.418317 | -1.102989 | 0.582455 |

我们还可以组合逻辑语句，我们将过滤所有列‘A’和‘B’的值大于零的行。

```
In[]: 
df_filtered = df[(df['A'] > 0) & (df['B'] > 0)] print(df_filtered)

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| e | 0.088279 | 0.418317 | -1.102989 | 0.582455 |

## 迭代 Python 熊猫数据帧

我们可以逐行遍历 Python Pandas 数据帧，在每次迭代中进行操作，让我们看一些例子。

```
In[]: 
for item in df.iterrows():
          print(item)

Out[]:
('a', A       -0.633249
B       -2.699088
C        0.574052
D        0.652742
shift         NaN
Name: a, dtype: float64)
('b', A        0.060295
B       -0.150527
C        0.149123
D       -0.701216
shift    0.652742
Name: b, dtype: float64)
('c', A       -0.052515
B        0.469481
C        0.899180
D       -0.608409
shift   -0.701216
Name: c, dtype: float64)
('d', A       -1.352912
B        0.103302
C        0.457878
D       -1.897170
shift   -0.608409
Name: d, dtype: float64)
('e', A        0.088279
B        0.418317
C       -1.102989
D        0.582455
shift   -1.897170
Name: e, dtype: float64)

```py

## Python Pandas 数据帧上的合并、追加和连接操作

Python Pandas 数据帧的另一个有趣的特性是，我们可以合并、连接它们并添加新值，让我们在 Python Pandas 教程的这一部分看看如何进行这些操作。

*   `merge`函数允许我们按行合并两个 Python Pandas 数据帧:

```
In[]: 
 import numpy as np
      df1=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
      print(df1)

Out[]:
`

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 1.179924 | -1.512124 | 0.767557 | 0.019265 |
| b | 0.019969 | -1.351649 | 0.665298 | -0.989025 |
| c | 0.351921 | -0.792914 | 0.455174 | 0.170751 |
| d | -0.150499 | 0.151942 | -0.628074 | -0.347300 |
| e | -1.307590 | 0.185759 | 0.175967 | -0.170334 |

```
df2=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
print(df2)
`

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 2.030462 | -0.337738 | -0.894440 | -0.757323 |
| b | 0.475807 | 1.350088 | -0.514070 | -0.843963 |
| c | 0.948164 | -0.155052 | -0.618893 | 1.319999 |
| d | 1.433736 | -0.455008 | 1.445698 | -1.051454 |
| e | 0.565345 | 1.802485 | -0.167189 | -0.227519 |

```
In[]: 
 df3 = pd.merge(df1, df2)
      print(df3)

Out[]:  
 Empty DataFrame
        Columns: [A, B, C, D]
        Index: []

```py

*   `append`函数允许我们按行将一个 Python Pandas 数据帧中的行追加到另一个 Python Pandas 数据帧中:

```
In[] 
 import numpy as np
      df1=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
      print(df1)

      df2=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
      print(df2)

      df3 = df1.append(df2)
      print(df3)

Out[]

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 1.179924 | -1.512124 | 0.767557 | 0.019265 |
| b | 0.019969 | -1.351649 | 0.665298 | -0.989025 |
| c | 0.351921 | -0.792914 | 0.455174 | 0.170751 |
| d | -0.150499 | 0.151942 | -0.628074 | -0.347300 |
| e | -1.307590 | 0.185759 | 0.175967 | -0.170334 |
| a | 2.030462 | -0.337738 | -0.894440 | -0.757323 |
| b | 0.475807 | 1.350088 | -0.514070 | -0.843963 |
| c | 0.948164 | -0.155052 | -0.618893 | 1.319999 |
| d | 1.433736 | -0.455008 | 1.445698 | -1.051454 |
| e | 0.565345 | 1.802485 | -0.167189 | -0.227519 |

*   `concat`函数允许我们按行或列合并两个 Python Pandas 数据帧:

```
In[]: 
 import numpy as np
      df1=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
      print(df1)

      df2=pd.DataFrame(np.random.randn(5,4), index=['a','b','c','d','e'], columns=['A', 'B', 'C', 'D'])
      print(df2)

      df3 = pd.concat([df1, df2]) # concat by row
      print(df3)

Out[]:
`

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 1.179924 | -1.512124 | 0.767557 | 0.019265 |
| b | 0.019969 | -1.351649 | 0.665298 | -0.989025 |
| c | 0.351921 | -0.792914 | 0.455174 | 0.170751 |
| d | -0.150499 | 0.151942 | -0.628074 | -0.347300 |
| e | -1.307590 | 0.185759 | 0.175967 | -0.170334 |
| a | 2.030462 | -0.337738 | -0.894440 | -0.757323 |
| b | 0.475807 | 1.350088 | -0.514070 | -0.843963 |
| c | 0.948164 | -0.155052 | -0.618893 | 1.319999 |
| d | 1.433736 | -0.455008 | 1.445698 | -1.051454 |
| e | 0.565345 | 1.802485 | -0.167189 | -0.227519 |

```
In[]: 
df3 = pd.concat([df1, df2], axis=0) # concat by row
print(df3)

Out[]:
`

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| a | 1.179924 | -1.512124 | 0.767557 | 0.019265 |
| b | 0.019969 | -1.351649 | 0.665298 | -0.989025 |
| c | 0.351921 | -0.792914 | 0.455174 | 0.170751 |
| d | -0.150499 | 0.151942 | -0.628074 | -0.347300 |
| e | -1.307590 | 0.185759 | 0.175967 | -0.170334 |
| a | 2.030462 | -0.337738 | -0.894440 | -0.757323 |
| b | 0.475807 | 1.350088 | -0.514070 | -0.843963 |
| c | 0.948164 | -0.155052 | -0.618893 | 1.319999 |
| d | 1.433736 | -0.455008 | 1.445698 | -1.051454 |
| e | 0.565345 | 1.802485 | -0.167189 | -0.227519 |

```
In[]: 
df3 = pd.concat([df1, df2], axis=1) # concat by column
print(df3)

Out[]:

```py

| 
 | A | B | C | D | A | B | C | D |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| a | 1.179924 | -1.512124 | 0.767557 | 0.019265 | 2.030462 | -0.337738 | -0.894440 | -0.757323 |
| b | 0.019969 | -1.351649 | 0.665298 | -0.989025 | 0.475807 | 1.350088 | -0.514070 | -0.843963 |
| c | 0.351921 | -0.792914 | 0.455174 | 0.170751 | 0.948164 | -0.155052 | -0.618893 | 1.319999 |
| d | -0.150499 | 0.151942 | -0.628074 | -0.347300 | 1.433736 | -0.455008 | 1.445698 | -1.051454 |
| e | -1.307590 | 0.185759 | 0.175967 | -0.170334 | 0.565345 | 1.802485 | -0.167189 | -0.227519 |

## Python 熊猫中的时间序列

Python Pandas TimeSeries 包括一组工具，用于处理按时间索引的系列或数据帧。

通常，财务数据系列就是这种类型，因此，了解这些工具将使我们的工作更加轻松。

在 Python 熊猫教程的这一部分，我们将从头开始创建时间序列，然后我们将看到如何操作它们并将它们转换成不同的频率。

### 索引 Python 熊猫时间系列

用`date_range` Panda 的方法，我们可以创建一个有一定频率的时间范围。例如，创建一个从 2018 年 12 月 1 日开始的范围，每小时发生 30 次。

```
In[]: 
rng = pd.date_range('12/1/2018', periods=30, freq='H')
print(rng)

Out[]: 
DatetimeIndex(['2018-12-01 00:00:00', '2018-12-01 01:00:00',
               '2018-12-01 02:00:00', '2018-12-01 03:00:00',
               '2018-12-01 04:00:00', '2018-12-01 05:00:00',
               '2018-12-01 06:00:00', '2018-12-01 07:00:00',
               '2018-12-01 08:00:00', '2018-12-01 09:00:00',
               '2018-12-01 10:00:00', '2018-12-01 11:00:00',
               '2018-12-01 12:00:00', '2018-12-01 13:00:00',
               '2018-12-01 14:00:00', '2018-12-01 15:00:00',
               '2018-12-01 16:00:00', '2018-12-01 17:00:00',
               '2018-12-01 18:00:00', '2018-12-01 19:00:00',
               '2018-12-01 20:00:00', '2018-12-01 21:00:00',
               '2018-12-01 22:00:00', '2018-12-01 23:00:00',
               '2018-12-02 00:00:00', '2018-12-02 01:00:00',
               '2018-12-02 02:00:00', '2018-12-02 03:00:00',
               '2018-12-02 04:00:00', '2018-12-02 05:00:00'],
              dtype='datetime64[ns]', freq='H')

```py

我们可以做同样的事情来获得每日频率(或者任何其他的，[参见文档](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.date_range.html?highlight=date_range))。我们可以使用`freq`参数对此进行调整。

```
In[]: 
rng = pd.date_range('12/1/2018', periods=30, freq='D')
print(rng)

Out[]: 
DatetimeIndex(['2018-12-01', '2018-12-02', '2018-12-03', '2018-12-04',
               '2018-12-05', '2018-12-06', '2018-12-07', '2018-12-08',
               '2018-12-09', '2018-12-10', '2018-12-11', '2018-12-12',
               '2018-12-13', '2018-12-14', '2018-12-15', '2018-12-16',
               '2018-12-17', '2018-12-18', '2018-12-19', '2018-12-20',
               '2018-12-21', '2018-12-22', '2018-12-23', '2018-12-24',
               '2018-12-25', '2018-12-26', '2018-12-27', '2018-12-28',
               '2018-12-29', '2018-12-30'],
              dtype='datetime64[ns]', freq='D')

```py

现在，我们在`rng`对象中有了一个`DateTimeIndex`，我们可以用它来创建一个系列或数据帧:

```
In[]: 
ts = pd.DataFrame(np.random.randn(len(rng), 4), index=rng, columns=['A', 'B', 'C', 'D'])
print(ts)

Out[]:
`

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| 2018-12-01 | 0.048603 | 0.968522 | 0.408213 | 0.921774 |
| 2018-12-02 | -2.301373 | -2.310408 | -0.559381 | -0.652291 |
| 2018-12-03 | -2.337844 | 0.329954 | 0.289221 | 0.259132 |
| 2018-12-04 | 1.357521 | 0.969808 | 1.341875 | 0.767797 |
| 2018-12-05 | -1.212355 | -0.077457 | -0.529564 | 0.375572 |
| 2018-12-06 | -0.673065 | 0.527754 | 0.006344 | -0.533316 |
| 2018-12-07 | 0.226145 | 0.235027 | 0.945678 | -1.766167 |
| 2018-12-08 | 1.735185 | -0.604229 | 0.274809 | 0.841128 |

```
In[]: 
ts = pd.Series(np.random.randn(len(rng)), index=rng)
print(ts)

Out[]:  
 2018-12-01    0.349234
        2018-12-02   -1.807753
        2018-12-03    0.112777
        2018-12-04    0.421516
        2018-12-05   -0.992449
        2018-12-06    1.254999
        2018-12-07   -0.311152
        2018-12-08    0.331584
        2018-12-09    0.196904
        2018-12-10   -1.619186
        2018-12-11    0.478510
        2018-12-12   -1.036074

```py

有时，我们从互联网资源或 csv 文件中读取数据，我们需要将日期列转换为索引，以便正确处理系列或数据帧。

```
In[]: 
import pandas as pd
df=pd.read_csv('TSLA.csv')
df.tail()

Out[]:

```py

| 
 | 日期 | 打开 | 高的 | 低的 | 关闭 | 卷 | 除息 | 分流比 | adopen | 和高 | AdjLow | 接近的 | AdjVolume | 名字 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| One thousand and seventy-eight | 2013-12-11 | One hundred and forty-one point eight eight | One hundred and forty-three point zero five | One hundred and thirty-nine point four nine | One hundred and thirty-nine point six five | Seven million one hundred and thirty-seven thousand eight hundred | Zero | One | One hundred and forty-one point eight eight | One hundred and forty-three point zero five | One hundred and thirty-nine point four nine | One hundred and thirty-nine point six five | Seven million one hundred and thirty-seven thousand eight hundred | TSLA |
| One thousand and seventy-nine | 2013-12-10 | One hundred and forty point zero five | One hundred and forty-five point eight seven | One hundred and thirty-nine point eight six | One hundred and forty-two point one nine | Ten million seven hundred and forty-eight thousand two hundred | Zero | One | One hundred and forty point zero five | One hundred and forty-five point eight seven | One hundred and thirty-nine point eight six | One hundred and forty-two point one nine | Ten million seven hundred and forty-eight thousand two hundred | TSLA |
| One thousand and eighty | 2013-12-09 | One hundred and thirty-seven | One hundred and forty-one point seven | One hundred and thirty-four point two one | One hundred and forty-one point six | Nine million sixty-one thousand five hundred | Zero | One | One hundred and thirty-seven | One hundred and forty-one point seven | One hundred and thirty-four point two one | One hundred and forty-one point six | Nine million sixty-one thousand five hundred | TSLA |
| One thousand and eighty-one | 2013-12-06 | One hundred and forty-one point five one | One hundred and forty-two point four nine | One hundred and thirty-six point three | One hundred and thirty-seven point three six | Seven million nine hundred and nine thousand six hundred | Zero | One | One hundred and forty-one point five one | One hundred and forty-two point four nine | One hundred and thirty-six point three | One hundred and thirty-seven point three six | Seven million nine hundred and nine thousand six hundred | TSLA |
| One thousand and eighty-two | 2013-12-05 | One hundred and forty point one five | One hundred and forty-three point three five | One hundred and thirty-nine point five | One hundred and forty point four eight | Nine million two hundred and eighty-eight thousand four hundred | Zero | One | One hundred and forty point one five | One hundred and forty-three point three five | One hundred and thirty-nine point five | One hundred and forty point four eight | Nine million two hundred and eighty-eight thousand four hundred | TSLA |

在这里，我们可以看到数字索引和一个日期列，让我们将该列转换为索引，以便及时索引从 csv 文件中读取的数据帧。为此，我们将使用 Python Pandas `set_index`方法

```
In[]: 
df = df.set_index('Date')
df.tail()

Out[]:

```py

| 日期 | 打开 | 高的 | 低的 | 关闭 | 卷 | 除息 | 分流比 | adopen | 和高 | AdjLow | 接近的 | AdjVolume | 名字 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 2013-12-11 | One hundred and forty-one point eight eight | One hundred and forty-three point zero five | One hundred and thirty-nine point four nine | One hundred and thirty-nine point six five | Seven million one hundred and thirty-seven thousand eight hundred | Zero | One | One hundred and forty-one point eight eight | One hundred and forty-three point zero five | One hundred and thirty-nine point four nine | One hundred and thirty-nine point six five | Seven million one hundred and thirty-seven thousand eight hundred | TSLA |
| 2013-12-10 | One hundred and forty point zero five | One hundred and forty-five point eight seven | One hundred and thirty-nine point eight six | One hundred and forty-two point one nine | Ten million seven hundred and forty-eight thousand two hundred | Zero | One | One hundred and forty point zero five | One hundred and forty-five point eight seven | One hundred and thirty-nine point eight six | One hundred and forty-two point one nine | Ten million seven hundred and forty-eight thousand two hundred | TSLA |
| 2013-12-09 | One hundred and thirty-seven | One hundred and forty-one point seven | One hundred and thirty-four point two one | One hundred and forty-one point six | Nine million sixty-one thousand five hundred | Zero | One | One hundred and thirty-seven | One hundred and forty-one point seven | One hundred and thirty-four point two one | One hundred and forty-one point six | Nine million sixty-one thousand five hundred | TSLA |
| 2013-12-06 | One hundred and forty-one point five one | One hundred and forty-two point four nine | One hundred and thirty-six point three | One hundred and thirty-seven point three six | Seven million nine hundred and nine thousand six hundred | Zero | One | One hundred and forty-one point five one | One hundred and forty-two point four nine | One hundred and thirty-six point three | One hundred and thirty-seven point three six | Seven million nine hundred and nine thousand six hundred | TSLA |
| 2013-12-05 | One hundred and forty point one five | One hundred and forty-three point three five | One hundred and thirty-nine point five | One hundred and forty point four eight | Nine million two hundred and eighty-eight thousand four hundred | Zero | One | One hundred and forty point one five | One hundred and forty-three point three five | One hundred and thirty-nine point five | One hundred and forty point four eight | Nine million two hundred and eighty-eight thousand four hundred | TSLA |

现在，我们有熊猫时间系列准备工作。

### 重采样熊猫时间序列

Python Pandas TimeSeries 的一个非常有用的特性是重采样能力，这允许我们将当前频率传递到另一个更高的频率(我们不能传递到更低的频率，因为我们不知道数据)。

可以设想，当我们从一个频率传递到另一个频率时，数据可能会丢失，为此，我们必须使用一些函数来处理每个频率间隔的值，例如，如果我们从每小时一次的频率传递到每天一次的频率，我们必须指定我们想要对每个频率内的数据组做什么，我们可以做均值、求和，我们可以获得最大值或最小值等。

```
In[]: 
rng = pd.date_range('12/1/2018', periods=30, freq='H')
ts = pd.DataFrame(np.random.randn(len(rng), 4), index=rng, columns=['A', 'B', 'C', 'D'])
print(ts)

Out[]:
`

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| 2018-12-01 00:00:00 | 0.048603 | 0.968522 | 0.408213 | 0.921774 |
| 2018-12-01 01:00:00 | -2.301373 | -2.310408 | -0.559381 | -0.652291 |
| 2018-12-01 02:00:00 | -2.337844 | 0.329954 | 0.289221 | 0.259132 |
| 2018-12-01 03:00:00 | 1.357521 | 0.969808 | 1.341875 | 0.767797 |
| 2018-12-01 04:00:00 | -1.212355 | -0.077457 | -0.529564 | 0.375572 |
| 2018-12-01 05:00:00 | -0.673065 | 0.527754 | 0.006344 | -0.533316 |

```
In[]: 
ts = ts.resample("1D").mean()
print(ts)

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| 2018-12-01 | 0.449050 | 0.127412 | -0.154179 | -0.358324 |
| 2018-12-02 | -0.539007 | -0.855894 | 0.000010 | 0.454623 |

### 操纵时间序列

我们可以像现在一样操作 Python Pandas 时间序列，因为它们为我们提供了与 Pandas 系列和 Pandas 数据帧相同的容量。

此外，我们可以轻松处理所有与处理日期相关的工作。例如，获取某个日期的所有数据，获取某个日期范围内的数据，等等。

```
In[]: 
rng = pd.date_range('12/1/2018', periods=30, freq='D')
ts = pd.DataFrame(np.random.randn(len(rng), 4), index=rng, columns=['A', 'B', 'C', 'D'])
print(ts)

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| 2018-12-01 | 0.048603 | 0.968522 | 0.408213 | 0.921774 |
| 2018-12-02 | -2.301373 | -2.310408 | -0.559381 | -0.652291 |
| 2018-12-03 | -2.337844 | 0.329954 | 0.289221 | 0.259132 |
| 2018-12-04 | 1.357521 | 0.969808 | 1.341875 | 0.767797 |
| 2018-12-05 | -1.212355 | -0.077457 | -0.529564 | 0.375572 |
| 2018-12-06 | -0.673065 | 0.527754 | 0.006344 | -0.533316 |

获取特定日期的所有值:

```
In[]: 
ts['2018-12-15':]

Out[]:

```py

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| 2018-12-02 | 0.324689 | -0.413723 | 0.019163 | 0.385233 |
| 2018-12-03 | -2.198937 | 0.536600 | -0.540934 | -0.603858 |
| 2018-12-04 | -1.195148 | 2.191311 | -0.981604 | -0.942440 |
| 2018-12-05 | 0.621298 | -1.435266 | -0.761886 | -1.787730 |
| 2018-12-06 | 0.635679 | 0.683265 | 0.351140 | -1.451903 |

获取日期范围内的所有值:

```
In[]: 
ts['2018-12-15':'2018-12-20']

Out[]:

```

| 
 | A | B | C | D |
| --- | --- | --- | --- | --- |
| 2018-12-15 | 0.605576 | 0.584369 | -1.520749 | -0.242630 |
| 2018-12-16 | -0.105561 | -0.092124 | 0.385085 | 0.918222 |
| 2018-12-17 | 0.337416 | -1.367549 | 0.738320 | 2.413522 |
| 2018-12-18 | -0.011610 | -0.339228 | -0.218382 | -0.070349 |
| 2018-12-19 | 0.027808 | -0.422975 | -0.622777 | 0.730926 |
| 2018-12-20 | 0.188822 | -1.016637 | 0.470874 | 0.674052 |

## 摘要

让我们总结一下我们在 Python 熊猫教程中学到的几点

*   Python 熊猫数据帧和 Python 熊猫系列是一些最重要的数据结构。这是一个必须掌握流利的处理，因为我们会发现他们在几乎所有的问题，我们处理。
*   Python 熊猫数据帧是由行和列形成的数据结构，并且有一个索引。
*   我们必须把它们想象成数据表(对于只有一列的数组),我们可以通过行或列来选择、过滤、排序、添加和删除元素。
*   ETL 过程中的帮助(提取、转换和加载)
*   我们可以用简单的功能来选择、插入、删除和更新元素。
*   我们可以按行或列进行计算。
*   具有运行矢量化计算的能力。
*   我们可以同时处理几个数据帧。
*   索引和子集化是 Python 熊猫最重要的特性。
*   促进数据的统计探索。
*   它为我们处理 NaN 数据提供了多种选择。
*   另一个额外的优势是读写多种数据格式(CSV、Excel、HDF5 等)的能力。).
*   从外部来源(雅虎、谷歌、Quandl 等)检索数据。)
*   最后，它能够处理日期和时间索引，并为我们提供了一组处理日期的函数。

## 结论

重申一下，这篇文章是从 [Python 基础手册](https://www.quantinsti.com/python-basics-handbook)中摘录的，它是为这两者而创作的；刚开始使用 [Python](https://quantra.quantinsti.com/course/python-for-trading) 的新手，以及有成就的交易者，他们可以在编写策略时使用它作为方便的参考。

请在下面的评论中告诉我们你是否喜欢这篇文章以及其他反馈。

*<small>免责声明:股票市场的所有投资和交易都涉及风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。</small>T11】*
# r 每周简报第二卷

> 原文：<https://blog.quantinsti.com/r-weekly-bulletin-vol-ii/>

本周的 R 公告将涵盖函数调用、数据帧排序、创建时序对象，以及 is.na、na.omit、paste、help、rep 和 seq 函数等函数。希望你喜欢这个 R 周刊。享受阅读！

### 快捷键

1.  显示文件- Ctrl+5
2.  显示绘图- Ctrl+6
3.  要显示包- Ctrl+7

### **解题思路**

#### 在 R 脚本中调用函数

如果您想从另一个脚本调用您的 R 脚本中的自定义函数，可以使用“exists”函数和“source”函数。请参见下面的示例:

**举例:**

```py
if(exists("daily_price_data", mode="function")) source("Stock price data.R")
```

在这种情况下，表达式将检查“股票价格数据”中是否存在名为“每日*价格*数据”的函数。r”脚本，如果是这样，它将在当前脚本中加载该函数。然后，通过提供相关参数，我们可以在脚本中多次使用该函数。

#### 将日期从 Google finance 转换为时间序列对象

当我们从 Google finance 下载股票价格数据时,“DATE”列显示 yymmdd 格式的日期。这种格式在 r 中不被视为时间序列对象，要将 Google Finance 中的日期转换为时间序列对象，可以使用 lubridate 包中的 ymd 函数。ymd 函数接受年、月、日形式的日期。对于其他格式的日期，lubridate 包具有类似 ydm、mdy、myd、dmy 和 dym 的函数，这些函数可用于将其转换为时间序列对象。

**举例:**

```py
library(lubridate)
dt = ymd(20160523)
print(dt)
```

[1] "2016-05-23"

#### 按升序或降序对数据帧进行排序

dplyr 包中的排列函数可用于对数据框进行排序。第一个参数是 data.frame，下一个参数是排序所依据的变量，可以是升序，也可以是降序。

在下面的例子中，我们创建了一个两列数据框，由股票符号及其各自的价格变化百分比组成。然后，我们首先按升序对百分比变化列进行排序，然后再按降序对百分比变化列进行排序。

**举例:**

```py
library(dplyr)
# Create a dataframe
Ticker = c("UNITECH", "RCOM", "VEDL", "CANBK")
Percent_Change = c(2.3, -0.25, 0.5, 1.24)
df = data.frame(Ticker, Percent_Change)
print(df)
```

股票价格百分比变化 1 尤尼泰 2.30 2 RCOM 0.25 3 韦德 1.50 4 加拿大元 1.24

```py
# Sort in an ascending order
df_descending = arrange(df, Percent_Change)
print(df_descending)
```

1 RCOM -0.25 德国马克-0.50 德国马克-1.24 德国马克-2.30 德国马克

```py
# Sort in a descending order
df_descending = arrange(df, desc(Percent_Change))
print(df_descending)
```

股票价格百分比变化 1 欧元兑换 1 美元 2.30 加元 1.24 美元 3 欧元兑换 1.50 美元 4 RCOM 0.25 美元

### 功能去神秘化

#### 粘贴功能

粘贴是 R 中一个非常有用的函数，用于连接提供给它的参数。若要包含或删除参数之间的空格，请使用“sep”参数。

**示例 1:** 使用粘贴将一串单词和一个函数组合起来

```py
x = c(20:45)
paste("Mean of x is", mean(x), sep = " ")
```

[1]“x 的平均值是 32.5”

**示例 2:** 使用目录路径、符号和文件扩展名作为粘贴函数的参数来创建文件名。

```py
dirPath = "C:/Users/MyFolder/"
symbol = "INFY"
filename = paste(dirPath, symbol, ".csv", sep = "")
print(filename)
```

[1] "C:/Users/MyFolder/INFY.csv "

#### is.na 和 na.omit 函数

is.na 函数检查给定数据集中是否有 na 值，而 na.omit 函数将从给定数据集中删除所有 NA 值。

**示例:**考虑一个数据框架，该数据框架包括对应于每个日期的股票的开盘价和收盘价。

```py
date = c(20160501, 20160502, 20160503, 20160504)
open = c(234, NA, 236.85, 237.45)
close = c(236, 237, NA, 238)
df = data.frame(date, open, close)
print(df)
```

日期开盘收盘 1 20160501 234.00 236 2 20160502 北美 237 3 20160503 236.85 北美 4 20160504 237.45 238

让我们使用 is.na 函数检查数据帧是否有 NA 值。

```py
is.na(df)
```

日期打开关闭假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假假

从结果可以看出，它有两个 NA 值。现在让我们使用 na.omit 函数，并查看结果。

```py
na.omit(df)
```

日期开盘收盘 1 2016 05 01 234.00 236 4 2016 05 04 237.45 238

从结果中可以看出，具有 NA 值的行被省略，并且结果数据帧现在仅包括非 NA 值。

这些函数可用于检查我们希望对其应用一些计算的大型数据集中的任何 NA 值。NA 值的存在会导致计算给出不需要的结果，因此这种 NA 值需要被移除或者被相关值代替。

#### 重复和序列功能

rep 函数将参数重复指定的次数，而 sequence 函数用于形成所需的数字序列。请注意，在序列函数中，我们使用逗号，而不是冒号。

**例 1:**

```py
rep("Strategy", times = 3)
```

[1]“策略”“策略”“策略”

```py
rep(1:3, 2)
```

[1] 1 2 3 1 2 3

**例 2:**

```py
seq(1, 5)
```

[1] 1 2 3 4 5

```py
seq(1, 5, 0.5)
```

[1] 1.0 1.5 2.0 2.5 3.0 3.5 4.0 4.5 5.0

#### 帮助和示例功能

help 函数提供关于主题排序的信息，而 example 函数提供关于给定主题的示例。

帮助(汇总)示例(汇总)

要访问与特定包中的特定函数相关联的 R 帮助文件，请将函数名作为 help 函数的第一个参数，同时包含第二个参数中提到的包名。

**举例:**

```py
help(barplot, package="graphics")
```

或者，也可以键入一个问号，后跟函数名(例如？柱状图)并执行命令以了解关于该函数的更多信息。

### **下一步**

我们希望你喜欢这个公告。在[下一期每周简报](https://blog.quantinsti.com/r-weekly-bulletin-vol-iii)中，我们将为读者列出更多有趣的方式方法加上 R 函数。

**更新**

我们注意到一些用户在从雅虎和谷歌金融平台下载市场数据时面临挑战。如果你正在寻找市场数据的替代来源，你可以使用 [Quandl](https://www.quandl.com/) 来获得同样的信息。
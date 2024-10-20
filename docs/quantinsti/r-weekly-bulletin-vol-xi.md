# r 每周简报第一卷——Xi

> 原文：<https://blog.quantinsti.com/r-weekly-bulletin-vol-xi/>

![](img/4c2dd2c0f5a4e154695a761b95acd256.png)

本周的 R 公告将涵盖如何舍入到最接近的所需数字、转换和比较日期以及如何从元素中删除最后 x 个字符的主题。希望你喜欢这个 R 周刊。享受阅读！

### 快捷键

1.  注释/取消注释当前行/选择- Ctrl+Shift+C
2.  向上/向下移动行-Alt+向上/向下
3.  删除行- Ctrl+D

### 解决问题的想法

#### 舍入到最接近的所需数字

考虑这样一种情况，您想要将一个给定的数字四舍五入到最接近的 25。这可以通过以下方式完成:

```py
round(145/25) * 25
```

[1] 150

```py
floor(145/25) * 25
```

[1] 125

```py
ceiling(145/25) * 25
```

[1] 150

用法:假设您正在计算最小报价单位为 5 派息的 NSE 股票的止损或获利。在这种情况下，我们将除以并乘以 0.05，以获得所需的结果。

**举例:**

```py
Price = 566
Stop_loss = 1/100
# without rounding
SL = Price * Stop_loss
print(SL)
```

[1] 5.66

```py
# with rounding to the nearest 0.05
SL1 = floor((Price * Stop_loss)/0.05) * 0.05
print(SL1)
```

[1] 5.65

#### 如何移除每个元素的最后 n 个字符

为了删除最后 n 个字符，我们将使用 substr 函数和 nchr 函数。下面的例子说明了做这件事的方法。

**举例:**

```py
# In this case, we just want to retain the ticker name which is "TECHM"
symbol = "TECHM.EQ-NSE"
s = substr(symbol,1,nchar(symbol)-7)
print(s)
```

[1]“TECHM”

#### 转换和比较不同格式的日期

当我们从 Google finance 中提取股票数据时，日期显示为“YYYYMMDD”，它不能被识别为日期-时间对象。要将其转换为日期时间对象，我们可以使用 lubridate 包中的“ymd”函数。

**举例:**

```py
library(lubridate)
x = ymd(20160724)
print(x)
```

[1] "2016-07-24"

另一个数据提供程序提供股票数据，该数据具有美国格式(mm/dd/yyyy)的日期时间对象。当我们读取文件时，日期-时间列被作为字符读取。我们需要将它转换成一个日期时间对象。我们可以使用。日期函数，并通过指定格式。

```py
dt = "07/24/2016"
y = as.Date(dt, format = "%m/%d/%Y")
print(y)
```

[1] "2016-07-24"

```py
# Comparing the two date-time objects (from Google Finance and the data provider) after conversion
identical(x, y)
```

[1]正确

### 功能去神秘化

**等级函数**

rank 函数返回向量中值的样本等级。可以用几种方式处理平局(即相等的值)和缺失值。

**rank(x，** na **。last = TRUE，ties.method = c("average "，" first "，" random "，" max "，" min"))**

其中， **x:** 数值、复数、字符或逻辑向量 na **。最后:**用于控制 NAs 的治疗。如果为真，则数据中缺失的值被放在最后；如果为假，则放在第一位；如果 NA，它们被移除；如果“keep ”,它们将与秩 NA **ties 一起保存。方法:**指定如何处理 ties 的字符串

**例子:**

```py
x <- c(3, 5, 1, -4, NA, Inf, 90, 43)
rank(x)
```

[1] 3 4 2 1 8 7 6 5

```py
rank(x, na.last = FALSE)
```

[1] 4 5 3 2 1 8 7 6

#### 变异和改变功能

变异和转化函数是 dplyr 包的一部分。mutate 函数使用给定数据框的现有变量计算新变量。新变量被添加到现有数据框中。另一方面，转化函数将这些新变量创建为单独的数据框。

考虑下例中给出的数据帧“df”。假设我们对一只股票的 1 分钟价格数据进行了 5 次观察，我们希望通过从 1 分钟收盘价中减去平均值来创建一个新变量。这可以通过使用 mutate 函数以下面的方式完成。

**举例:**

```py
library(dplyr)
OpenPrice = c(520, 521.35, 521.45, 522.1, 522)
ClosePrice = c(521, 521.1, 522, 522.25, 522.4)
Volume = c(2000, 3500, 1750, 2050, 1300)
df = data.frame(OpenPrice, ClosePrice, Volume)
print(df)
```

![](img/a27a5570bfb4e8ffdade1530078193a7.png)

```py
df_new = mutate(df, cpmean_diff = ClosePrice - mean(ClosePrice, na.rm = TRUE))
print(df_new)
```

![](img/d3bbbf53b3b1d1fc66497ef57da4f85d.png)

```py
# If we want the new variable as a separate data frame, we can use the transmute function instead.
df_new = transmute(df, cpmean_diff = ClosePrice - mean(ClosePrice, na.rm = TRUE))
print(df_new)
```

![](img/976be0552d8040ad609ce0522d1fb7d8.png)

#### set.seed 函数

set.seed 函数有助于在程序每次运行时生成相同的随机数序列。它将随机数发生器设置为已知状态。该函数接受一个整数参数。为了得到相同的初始状态，需要使用相同的正整数。

**举例:**

```py
# Initialize the random number generator to a known state and generate five random numbers
set.seed(100)
runif(5)
```

[1] 0.30776611 0.25767250 0.55232243 0.05638315 0.46854928

```py
# Reinitialize to the same known state and generate the same five 'random' numbers
set.seed(100)
runif(5)
```

[1] 0.30776611 0.25767250 0.55232243 0.05638315 0.46854928

### **下一步**

我们希望你喜欢这个公告。在[下一期每周简报](https://blog.quantinsti.com/r-weekly-bulletin-vol-xii)中，我们将为读者列出更多有趣的方式方法加上 R 函数。

**更新**

我们注意到一些用户在从雅虎和谷歌金融平台下载市场数据时面临挑战。如果你正在寻找市场数据的替代来源，你可以使用 [Quandl](https://www.quandl.com/) 来获得同样的信息。
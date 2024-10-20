# 在交易中使用 Python Lambda 函数

> 原文：<https://blog.quantinsti.com/using-python-lambda-function-in-trading/>

由[查尼卡·塔卡](https://www.linkedin.com/in/chainika-bahl-thakar-b32971155/)

如果你是一个使用 Python 为交易头寸编码的交易者，lambda 是你想要探索的函数。Lambda 帮助你只使用一次函数，因此避免了函数定义使代码混乱。

简而言之，Python 的 lambda 关键字允许您在一行代码中定义一个函数，并立即使用它。

让我们通过这篇博客进一步了解有趣的 lambda 函数，它涵盖了:

*   [Python 中的 lambda 函数是什么？](#what-is-the-lambda-function-in-python)
*   [为什么叫 lambda 函数？](#why-is-it-called-the-lambda-function)
*   [λ参数和语法](#lambda-arguments-and-syntax)
*   [常规功能和λ功能的区别](#difference-between-the-conventional-function-and-lambda-function)
*   [什么时候使用 lambda 函数？](#when-to-use-the-lambda-function)
*   [lambda 函数是如何工作的？](#how-does-the-lambda-function-work)
*   [Python lambda 在交易](#python-lambda-in-trading)
*   [λ函数在交易中的好处](#benefits-of-lambda-function-in-trading)

* * *

## Python 中的 lambda 函数是什么？

首先进入我们的主题，让我们讨论一下简短的匿名 lambda 函数。

lambda 函数也称为匿名函数或内联函数，是计算表达式的一行 Python 代码。此外，lambda 函数可以接受任意数量的参数，并且总是返回值。

* * *

## 为什么叫 lambda 函数？

在 Python 中，lambda 是一个匿名函数，因此没有名字。在 Python 中，普通函数是使用“def”关键字定义的，而匿名函数是使用“lambda”关键字定义的。

* * *

## Lambda 参数和语法

让我们看看下面的 lambda 语法。

**舔着 num: num * num * num**

当插入实数值时，上述语法返回给定数字的立方。lambda 函数没有名字，这就是为什么你可能会看到它被称为匿名函数。

* * *

## 常规功能和 lambda 功能之间的差异

Lambda 用于构造 python 函数；它是一个内联函数，不像传统的 def 函数允许分块构造。让我们比较一下传统函数构造的语法和 lambda 函数的语法，以便弄清楚。

![Conventional vs lambda function](img/80504b05068494b52918610df85feff7.png)

Conventional function vs lambda function



在传统的 def 函数中可以有任意数量的语句，它从给函数命名开始。另一方面，lambda 是一个匿名函数。您不需要为 lambda 构造提供任何名称。

让我们举一些简单的例子来说明它们的用法。

![Conventional vs lambda function](img/574752eb9f92d058427d42cbe777a3bc.png)

Conventional vs lambda function



lambda 构造更多地是为了方便使用，而不是使用 lambda 可以执行的操作范围。当您需要构造 lambda 函数时，请记住以下几点。

*   Lambda 是一个表达式，而不是一个语句。它不支持表达式块。
*   Lambda 是在我们需要使用它的地方定义的，不需要命名
*   Lambda 不需要 return 语句。它总是在求值之后返回一些东西。

* * *

## 什么时候使用 lambda 函数？

嗯，使用 lambda 函数的最大好处是，它可以用来代替任何计算单个表达式并返回值的常规函数。

但是，如果你想让你的函数改变一个全局变量，从一个文件中读取，或者计算一个以上的表达式，它就不能作为一个 lambda 函数。然而，在 Python 编程中，lambda 函数在大多数情况下都很简单。

* * *

## lambda 函数是如何工作的？

**使用带有映射、过滤和减少功能的 Lambda**

### 地图功能

Lambda 函数通常与 map()、filter()和 reduce()等函数一起使用。让我们举例说明它们的用法。

map 函数用于将函数传递给 iterable 对象中的每一项。map 函数返回包含所有结果的列表，而不修改原始对象。

示例:

```py
score = [
(10, 5),
(20, 2),
(30, 4),
(40, 7)
]
result = map(lambda x: x[0] / x[1], score)
for item in result:
print(f"Lambda returned the answer: {item}")

```

在上面的代码中，我们定义了一个名为 score 的元组列表。然后，调用 map 函数，将 lambda 函数作为第一个参数，将 list 作为第二个参数。

Lambda 函数在代码中被编写为将元组作为参数。它返回存储在元组的元素 0 中的值除以存储在元素 1 中的值。

在 map 运行之后，我们将把结果存储在变量 result 中。然后，遍历结果列表并打印它们。在所有情况下，除法的结果都应该是 10。

### 滤波函数

filter 函数用于提取 iterable 对象中该函数返回 True 的每个元素。在这种情况下，我们将使用 lambda 构造来定义函数，并应用 filter 函数。

让我们看看如何使用 filter 来查找偶数编号的列表项。为此，我们需要写一个 lambda 函数，只有当我们传递给它的数满足我们的条件时，它才为真。

示例:

```py
data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
result = filter(lambda x: x % 2 == 0, data)
print(f"Lambda returned the answer: {list(result)}")

```

在上面的代码中，每个列表项被一分为二，并检查余数。如果余数为零，我们知道这个数是偶数。

### 减少功能

reduce 函数是一个独特的函数，它通过调用作为参数的一部分提供的函数，将输入列表缩减为单个值。默认情况下，reduce 函数从列表的第一个值开始，并将当前输出传递给列表中的下一个项目。

示例:

```py
from functools import reduce
score = [20, 30, 40, 50]
result = reduce(lambda x, y: x + y, score)
print(f"Lambda returned the answer: {result}")

```

在上面的例子中，我们在 lambda 表达式中一起添加了列表项。Reduce 从一个空累加器开始，并添加第一项。然后，它将累加器设置为第一次操作的结果，并重复该操作。

这些是我们使用 lambda 结构的一些方法。

* * *

## 交易中的 Python lambda

使用 Python 的 lambda 函数，我们可以为不同的贸易相关输入编写几个代码。让我们看看下面的交易例子。
# Python 数据类型和变量教程

> 原文：<https://blog.quantinsti.com/python-data-types-variables-tutorial/>

杰伊·帕尔马

简单地说，变量可以被认为是一个有名字的容器，用来保存值。变量可以接受各种格式的数据，如字符串、整数、带小数部分的数字(浮点数)等。前面提到的这些格式称为数据类型。

现在是时候更详细地研究这些概念了。在这篇博客中，我们将更详细地讨论 python 变量和 python 数据类型。这篇博客文章是从 [Python 基础手册](https://www.quantinsti.com/python-basics-handbook)中摘录的，其创建的简单目的是让读者理解 [Python 语言](https://blog.quantinsti.com/getting-started-python-trading/)的美丽和简单。

我们将在这个博客中讨论以下主题。

*   [Python 变量](#Variables)
*   [Python 数据类型](#Data-Types)
*   [Python 数据类型转换](#Type-Conversion)

## Python 变量

用编程术语来说，python 变量是用来存储值的保留内存位置。换句话说，Python 程序中的变量为计算机处理提供了必要的数据。

在本节中，我们将学习 python 变量及其类型。让我们从创建一个变量开始。

### 变量声明和赋值

在 Python 中，变量不需要像许多其他编程语言那样预先声明或定义。事实上，Python 没有声明变量的命令。为了创建一个 python 变量，我们给它赋值并开始使用它。使用单个等号`=`进行赋值，也称为赋值运算符。当我们给一个 python 变量赋予第一个值时，它就被创建了。

```py
# Creating a variable
In [1]: price = 226

```

上面的语句可以解释为 python 变量`price`被赋值`226`。它也被称为*初始化*变量。一旦这条语句被执行，我们就可以开始在其他语句或表达式中使用`price`，它的值将被替换。举个例子，

```py
In [2]: print(price)
226 # Output

```

稍后，如果我们更改`price`的值并再次运行`print`语句，新值将作为输出出现。这被称为 python 变量的*重声明*。

```py
In [3]: price = 230 # Assigning new value
In [4]: print(price) # Printing price
230 # Output

```

我们还可以将赋值操作链接到 python 变量，这使得同时为多个变量赋值成为可能。

```py
In [5]: x = y = z = 200 # Chaining assignment operation
In [6]: print(x, y, z) # Printing all variables
200 200 200 # Output

```

上例所示的链式赋值同时将值`200`赋给 python 变量`x`、`y`和`z`。

### Python 变量命名约定

在 python 中，我们到处都使用 Python 变量。python 变量可以有一个简称或更具描述性的名称。命名变量时应遵循以下规则列表。

*   python 变量名必须以字母或下划线字符开头。

    ```py
    stock = 'AAPL' # Valid name
    _name = 'AAPL' # Valid name

    ```

*   python 变量名不能以数字开头。

    ```py
    1stock = 'AAPL' # Invalid name
    1_stock = 'AAPL' # Invalid name

    ```

*   python 变量名只能包含字母数字字符(a-z、A-Z、0-9)和下划线(_)。

    ```py
    Stock = 'AAPL' # Valid name. It starts with a capital letter.
    stock_price = 226.41 # Valid name. It is a combination of alphabets and the underscore.
    stock_1 = 'AAPL' # Valid name. It is a combination of alphabets and a number.
    Stock_name_2 = 'MSFT' # Valid name. It is a combination of a capital letter, alphabets and a number.

    ```

*   python 变量名不能包含空格和符号，如+、-等。

    ```py
    stock name = 'AAPL' # Invalid name. It cannot contain the whitespace.
    stock-name = 'AAPL' # Invalid name. It cannot contain characters other than the underscore ( _ ).

    ```

*   Python 变量名区分大小写。

    ```py
    STOCK = 'AAPL'
    stock = 'MSFT'
    Stock = 'GOOG'
    # STOCK, stock and Stock all three are different variable names.

    ```

    > 记住在 Python 中**变量名是区分大小写的**。

*   Python 关键字不能用作变量名。

    ```py
    str = 'AAPL' # Invalid name.
    is = 'A Variable' # Invalid name.
    for = 'Dummy Variable' # Invalid name.
    # 'str', 'is', and 'for' cannot be used as the variable name as they are reserved keywords in Python.

    ```

以下几点是职业程序员遵循的*事实上的*做法。

*   使用描述用途的名称，而不要使用假名。换句话说，应该是有意义的。

    ```py
    a = 18 # Valid name but the variable does not describe the purpose.
    age = 18 # Valid name which describes it suitably

    ```

*   使用下划线字符`_`分隔两个单词。

    ```py
    stockname = 'AAPL' # Valid name.
    stock_name = 'AAPL' # Valid name. And it also provides concise readability.

    ```

*   变量名以一个小字母开始。

    ```py
    Stock_name = 'AAPL' # Valid name.
    stock_name = 'AAPL' # Valid name. Additionally, it refers to uniformity with other statements.

    ```

> 遵守这些规则可以增加代码的可读性。请记住，这些都是很好的编码实践(推荐但绝不是必须遵循的)，您可以将其应用到任何编程语言，而不仅仅是 Python。

## Python 数据类型

理解了什么是变量以及如何使用变量存储值之后，是时候学习 python 变量所包含的值的数据类型了。我们将学习 python 中内置的原始 Python 数据类型，如数字、字符串和布尔。Python 有四种基本数据类型:

*   整数
*   浮动
*   线
*   布尔代数学体系的

我们将在下面更详细地介绍这些 python 数据类型:

### 整数

在 python 数据类型中，整数可以被视为不带任何小数的数值。实际上是用来描述 Python 中任何一个*整数*如`7`、`256`、`1024`等。我们用一个整数值来表示一个从负无穷大到无穷大的数值数据。使用赋值运算符将这些数字赋给 python 变量。

```py
total_output_of_dice_roll = 6
days_elapsed = 30
total_months = 12
year = 2019

```

我们将整数`6`赋给变量`total_output_of_dice_roll`，因为掷骰子不可能有分数输出。类似地，我们有一个值为`30`的变量`days_elapsed`，值为`12`的变量`total_months`，值为`2019`的变量`year`。

### 浮动

在 python 数据类型中，float 代表*浮点数*，实质上是一个有小数部分的数字。也可用于有理数，通常以小数结尾如`6.5`、`100.1`、`123.45`等。下面是一些 python 数据类型示例，其中浮点值比整数更合适。

```py
stock_price = 224.61
height = 6.2
weight = 60.4

```

> 从统计学的角度来看，浮点值可以被认为是一个连续的值，而整数值可以相应地是一个离散的值。

通过这样做，我们可以很好地理解 python 数据类型和 python 变量名是如何结合在一起的。反过来，这可以在表达式中使用，以执行任何数学计算。

让我们简单地用变量来尝试一下作为计算器的 Python。

```py
# Assign an integer value
In [7]: x = 2
# Assign a float value
In [8]: y = 10.0
# Addition
In [9]: print(x + y)
Out[9]: 12.0
# Subtraction
In [10]: print(x - y)
Out[10]: -8.0
# Multiplication
In [11]: print(x * y)
Out[11]: 20.0
# Division
In [12]: print(x / y)
Out[12]: 0.2
# Modulo
In [13]: print(x % y)
Out[13]: 2.0
# Exponential / Power
In [14]: print(x ** y)
Out[14]: 1024.0

```

> 请注意代码片段中描述功能的*注释*的精确用法。另外，请注意，*输出的所有表达式的*都是作为输入中使用的文字之一的 *float* 数，是一个 float 值。

看看上面提到的 python 数据类型的例子，试着理解代码片段。如果你能感觉到发生了什么，那很好。您已经踏上了 python 数据类型之旅的正轨。尽管如此，让我们试着理解代码，以便更加清晰。这里，我们将整数值`2`赋给`x`，将浮点值`10.0`赋给`y`。然后，我们尝试对这些定义的变量进行各种数学运算，而不是使用直接值。明显的好处是我们通过使用这些 python 变量获得的灵活性。例如，考虑这样一种情况，我们想对不同的值如`3`和`15.0`执行上述操作，我们只需分别用新值重新声明变量`x`和`y`，其余代码保持不变。

### Boolean

这个内置的 python 数据类型可以有两个值之一，`True`或`False`。我们使用赋值操作符`=`将一个布尔值赋给变量，其方式类似于我们所看到的整型和浮点型值。例如:

```py
In [15]: buy = True
In [16]: print(buy)
Out[16]: True
In [17]: sell = False
In [18]: print(sell)
Out[18]: False

```

Python 中的表达式通常在布尔上下文中计算，这意味着它们被解释为表示它们的真值。布尔表达式广泛用于逻辑条件和控制流语句中。考虑下面的例子

```py
# Checking for equality between 1 and itself using comparison operator '=='
In [19]: 1 == 1
Out[19]: True
# Checking for equality between values 1 and -1
In [20]: 1 == -1
Out[20]: False
# Comparing value 1 with -1
In [21]: 1 > -1
Out[21]: True

```

上面的 python 数据类型示例是一些计算结果为`True`或`False`的最简单的布尔表达式。

> 我们不在引号内写`True`和`False`。写的时候需要不带引号。此外，第一个字母需要大写，其次是小写字母。以下列表不会被评估为布尔值
> 
> *   “真的”
> *   真实的
> *   真实的
> *   “错误”
> *   错误的
> *   错误的

### 字符串

在 python 数据类型中，字符串是写在单引号`'`或双引号`"`内的字母、数字和其他字符的集合。换句话说，它是引号内的字符序列。让我们借助一些例子来理解一个字符串是如何工作的。

```py
# Variable assignment with a string
In [22]: sample_string = '1% can also be expressed as 0.01'
# Print the variable sample_string
In [23]: sample_string
Out[23]: '1% can also be expressed as 0.01'

```

在上面的 python 数据类型示例中，我们定义了一个名为`sample_string`的字符串变量，并为其赋值`'1% can also be expressed as 0.01'`。有趣的是，我们使用了字母、数字和特殊字符的组合来定义变量。在 Python 中，引号内的任何东西都是字符串。考虑下面的例子，

```py
In [24]: stock_price = '224.61'
In [25]: stock_price
Out[25]: '224.61'

```

我们定义变量`stock_price`来分配字符串值`'224.61'`。有趣的是，变量的输出也是一个字符串。每当数值以字符串形式给出时，Python 不会隐式转换 python 数据类型。

我们可以使用`+`操作符连接两个或更多的字符串。

```py
In [26]: 'Price of AAPL is ' + stock_price
Out[26]: 'Price of AAPL is 224.61'

```

使用`+`操作符的串联操作只对字符串有效。它不适用于不同的 python 数据类型。如果我们尝试执行该操作，将会出现一个错误。

```py
In [27]: stock_price = 224.61 # Re-declaring the variable with an integer value
In [28]: 'Price of AAPL is ' + stock_price # Error line
Traceback (most recent call last):
 File "<ipython-input-28-1c5964ef305c>", line 1, in <module>
 'Price of AAPL is ' + stock_price
TypeError: must be str, not float

```

正如所料，当我们试图连接一个字符串和浮点文字时，Python 抛出了一个`TypeError`。类似于`+`操作符，我们可以使用带有字符串文字的`*`操作符多次产生相同的字符串。

```py
In [29]: string = 'Python! '
In [30]: string * 3
Out[30]: 'Python! Python! Python! '

```

在 python 数据类型中，我们可以使用 slice 操作选择一个子字符串或字符串的一部分。使用方括号`[]`进行切片。从字符串中切分单个元素的语法是`[index]`，它将在`index`返回一个元素。索引是指每个元素在字符串中的位置，它从 0 开始，对于每个下一个元素，它按时间顺序不断增加。

```py
In [29]: string = 'EPAT Handbook!'
In [30]: string[0] # 0 refers to an element E
Out[30]: 'E'
In [31]: string[1] # 1 refers to an element P
Out[31]: 'P'

```

在上面的 python 数据类型示例中，作为第一个字符的元素`E`属于索引`0`，紧挨着`E`的`P`属于索引`1`，以此类推。类似地，元素`b`的索引将是`9`。您能猜出上面例子中元素`k`的索引吗？

要从字符串中分割出一个子串，使用的语法是`[start index:end index]`，它将返回从位于`start index`的元素开始的子串，但不包括位于`end index`的元素。考虑下面的 python 数据类型示例，其中我们将字符串从索引`0`子串到`4`，产生输出`'EPAT'`。注意索引`4`处的元素`' '`没有包含在输出中。类似地，我们对子串进行切片，如下面的 python 数据类型示例所示。

```py
In [32]: string[0:4]
Out[32]: 'EPAT'
In [33]: string[4]
Out[33]: ' '
In [34]: string[5:13]
Out[34]: 'Handbook'
In [35]: string[13]
Out[35]: '!'

```

在 Python 中，我们不能对字符串中不存在的索引执行切片操作。每当遇到索引不正确的切片操作，Python 就会抛出`IndexError`。

```py
In [36]: string[14]
Traceback (most recent call last):
 File "<ipython-input-36-6a6fe155a0da>", line 1, in <module>
 string[14]
IndexError: string index out of range

```

在上面的 python 数据类型示例中，最后一个索引是`13`。用索引`14`执行的切片操作将导致一个错误`IndexError`，表明我们正在寻找的索引不存在。

> 我们在下面列出了字符串文字的一些要点:
> 
> *   在 Python 3.x 中，默认情况下所有字符串都是 *Unicode* 。
> *   可以在`''`或`""`中写入字符串。两者都工作正常。
> *   字符串是不可变的。(尽管您可以修改变量)
> *   在字符串中使用转义序列来标记新的一行，提供制表符空间，写入`\`字符等。

### 字符串上的操作

在 python 数据类型的这一节中，我们讨论一些最常见的字符串方法。一个方法就像一个函数，但是它在一个对象上运行*。如果变量`sample_string`是一个字符串，那么代码`sample_string.upper()`在该字符串对象上运行`upper()`方法并返回结果(这种在对象上运行方法的思想是组成面向对象编程(OOP)的基本思想之一)。有些方法还将参数作为参数。我们给方法提供一个参数，作为圆括号内的自变量。*

*   `upper()`方法:该方法返回字符串的大写版本。python 数据类型示例如下:

    ```py
    In [37]: sample_string.upper()
    Out[37]: 'EPAT HANDBOOK!'

    ```

*   方法:这个方法返回字符串的小写版本。python 数据类型示例如下:

    ```py
    In [38]: sample_string.lower()
    Out[38]: 'epat handbook!'

    ```

*   方法:这个方法返回一个从开始和结束都去掉了空格的字符串。python 数据类型示例如下:

    ```py
    In [39]: ' A string with whitespace at both the ends. '.strip()
    Out[39]: 'A string with whitespace at both the ends.'

    ```

*   `isalpha()`方法:如果字符串中的所有字符都是字母，这个方法返回布尔值`True`，否则返回`False`。python 数据类型示例如下:

```py
In [40]: 'Alphabets'.isalpha()
Out[40]: True
In [41]: 'This string contains only alphabets'.isalpha()
Out[41]: False # The string under evaluation contains whitespace.

```

*   `isdigit()`方法:如果字符串中的所有字符都是数字，这个方法返回布尔值`True`，否则返回`False`。python 数据类型示例如下:

    ```py
    In [42]: '12345'.isdigit()
    Out[42]: True

    ```

*   `startswith(argument)`方法:如果字符串的第一个字符以作为参数提供的字符开始，该方法返回布尔值`True`，否则返回`False`。python 数据类型示例如下:

    ```py
    In [43]: 'EPAT Handbook!'.startswith('E')
    Out[43]: True

    ```

*   `endswith(argument)`方法:如果字符串的最后一个字符以作为参数提供的字符结尾，该方法返回布尔值`True`，否则返回`False`。python 数据类型示例如下:

    ```py
    In [44]: 'EPAT Handbook!'.startswith('k')
    Out[44]: False # String ends with the '!' character.

    ```

*   `find(sub, start, end)`方法:该方法返回子串`sub`在片`[start:end]`中找到的字符串中的最低索引。这里，参数`start`和`end`是可选的。如果没有找到`sub`，则返回`-1`。python 数据类型示例如下:

```py
In [45]: 'EPAT Handbook!'.find('EPAT')
Out[45]: 0
In [46]: 'EPAT Handbook!'.find('A')
Out[46]: 2 # First occurrence of 'A' is at index 2.
In [47]: 'EPAT Handbook!'.find('Z')
Out[47]: -1 # We do not have 'Z' in the string.

```

*   `replace(old, new)`方法:该方法返回一个字符串的副本，其中所有出现的`old`都被替换为`new`。python 数据类型示例如下:

```py
Out[48]: '00 01 10 11'.replace('0', '1')
Out[48]: '11 11 11 11' # Replace 0 with 1
In [49]: '00 01 10 11'.replace('1', '0')
Out[49]: '00 00 00 00' # Replace 1 with 0

```

*   `split(delim)`方法:该方法用于根据`delim`参数将一个字符串拆分成多个字符串。python 数据类型示例如下:

```py
In [50]: 'AAPL MSFT GOOG'.split(' ')
Out[50]: ['AAPL', 'MSFT', 'GOOG']

```

这里，Python 在一个名为 *List* 的数据结构中输出三个字符串。python 数据类型示例如下:

*   `index(character)`方法:该方法返回第一次出现的`character`的索引。python 数据类型示例如下:

```py
In [51]: 'EPAT Handbook!'.index('P')
Out[51]: 1

```

如果在字符串中找不到作为参数提供的字符，Python 将提供一个错误。

```py
In [52]: 'EPAT Handbook!'.index('Z')
Traceback (most recent call last):
 File "<ipython-input-52-d1b3e87f78be>", line 1, in <module>
 'EPAT Handbook!'.index('Z')
ValueError: substring not found

```

*   方法:这个方法返回一个大写的字符串。python 数据类型示例如下:

```py
In [53]: 'python is amazing!'.capitalize()
Out[53]: 'Python is amazing!'

```

*   `count(character)`方法:该方法返回由`character`提供的参数的计数。python 数据类型示例如下:

```py
In [54]: 'EPAT Handbook'.count('o')
Out[54]: 2
In [55]: 'EPAT Handbook'.count('a')
Out[55]: 1

```

### type()函数

内置的`type(argument)`函数用于评估 python 数据类型，并返回作为参数传递的`argument`的类类型。该功能主要用于调试。

```py
In [56]: type('EPAT Handbook')
Out[56]: str # A string is represented by the class 'str'.
In [57]: type(224.61)
Out[57]: float # A float literal is represented by the class 'float'.
In [58]: type(224)
Out[58]: int # An integer literal is represented by the class 'int'.
In [59]: type('0')
Out[59]: str # An argument provided is within quotation marks. Hence, it is considered as a string object represented by the class 'str'.
In [60]: type(True)
Out[60]: bool # A boolean value is represented by the class 'bool'.
In [61]: type(False)
Out[61]: bool
In [62]: type('False')
Out[62]: str # An argument is provided within a quotation mark.
In [63]: type([1, 2, 3])
Out[63]: list # An object passed as an argument belongs to the class 'list'.
In [64]: type({'key':'value'})
Out[64]: dict # An object passed as an argument belongs to the class 'dict'.
In [65]: type((1, 2, 3))
Out[65]: tuple # An object passed as an argument belongs to the class 'tuple'.
In [66]: type({1, 2, 3})
Out[66]: set # An object passed as an argument belongs to the class 'set'.

```

A `list`、`dict`、`tuple`、`set`是 Python 内部的原生数据结构。

## Python 数据类型转换

我们经常会遇到需要改变底层数据的 python 数据类型的情况。或者我们发现我们一直在使用一个整数，而我们真正需要的是一个浮点数。在这种情况下，我们可以转换变量的 python 数据类型。如上所示，我们可以使用`type()`函数检查变量的数据类型。

可能有两种类型的转换:*隐式*称为强制，以及*显式*通常称为强制转换。当我们将一个变量的类型从一种改变为另一种时，这被称为*类型转换*。

隐式转换:这是一个自动的类型转换，Python 解释器会为我们动态处理。我们不需要为此指定任何命令或函数。看看下面的 python 数据类型示例:

```py
In [67]: 8 / 2
Out[67]: 4.0

```

在作为被除数的两个整数`8`和作为除数的两个整数`2`之间执行的除法运算。数学上，我们期望输出是`4`——一个整数值，但是 Python 返回的输出是`4.0`——一个浮点值。也就是 Python 内部把一个整数`4`转换成浮点数`4.0`。

**显式转换**:这种类型的转换是用户自定义的。我们需要显式地更改某些文字的 python 数据类型，以使其与数据操作兼容。让我们尝试使用`+`操作符连接一个字符串和一个整数。

```py
In [68]: 'This is the year ' + 2019
Traceback (most recent call last):
 File "<ipython-input-68-2bccd8d1d6de>", line 1, in <module>
 'This is the year ' + 2019
TypeError: must be str, not int

```

这里我们试图连接一个字符串`'This is the year '`和一个整数`2019`。这样做的时候，python 抛出了一个错误`TypeError`，指出不兼容的 Python 数据类型。执行两者之间连接的一种方法是将 python 数据类型`2019`显式转换为 string，然后执行操作。我们使用`str()`将整数转换成字符串。

```py
In [68]: 'This is the year ' + str(2019)
Out[68]: 'This is the year 2019'

```

类似地，我们可以通过以下方式显式更改文本的 python 数据类型。

```py
# Integer to Float conversion
In [69]: float(4)
Out[69]: 4.0
# String to Float conversion
In [70]: float('4.2')
Out[70]: 4.2
In [71]: float('4.0')
Out[71]: 4.0
# Float to Integer conversion
In [72]: int(4.0)
Out[72]: 4 # Python will drop the fractional part.
In [73]: int(4.2)
Out[73]: 4
# String to Integer conversion
In [74]: int('4')
Out[74]: 4
# Python does not convert a string literal with a fractional part, and instead, it will throw an error.
In [75]: int('4.0')
Traceback (most recent call last):
 File "<ipython-input-75-a6536d9312a9>", line 1, in <module>
 int('4.0')
ValueError: invalid literal for int() with base 10: '4.0'
# Float to String conversion
In [76]: str(4.2)
Out[76]: '4.2'
# Integer to String conversion
In [77]: str(4)
Out[77]: '4'

```

在上面的例子中，我们看到了如何将 python 数据类型从一种文字改变为另一种文字。同样，`bool`所代表的布尔型 python 数据类型也没有什么不同。我们可以将`bool`定型为`int`，就像我们对其余部分所做的那样。事实上，Python 内部将布尔值`False`视为`0`，将`True`视为`1`。

```py
# Boolean to Integer conversion
In [64]: int(False)
Out[64]: 0
In [65]: int(True)
Out[65]: 1

```

也可以将整数值转换为布尔值。Python 将`0`转换为`False`，剩余的所有整数被转换为`True`。

```py
# Integer to Boolean conversion
In [78]: bool(0)
Out[78]: False
In [79]: bool(1)
Out[79]: True
In [80]: bool(-1)
Out[80]: True
In [81]: bool(125)
Out[81]: True

```

## 结论

因此，我们已经熟悉了 python 变量，然后继续定义它们，理解 python 数据类型、它们的内部工作方式和类型转换。

重申一下，Python 数据类型和变量教程是从为两者创建的 [Python 基础手册](https://www.quantinsti.com/python-basics-handbook)中摘录的；刚开始使用 [Python 的初学者以及有成就的交易者可以在编写策略时将它用作方便的参考。](https://quantra.quantinsti.com/course/python-for-trading)

请在下面的评论中告诉我们你是否喜欢这篇文章和任何其他反馈。

*免责声明:股票市场的所有投资和交易都涉及风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。T3】*
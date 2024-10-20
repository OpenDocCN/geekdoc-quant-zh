# Julia 编程的基本要点

> 原文：<https://blog.quantinsti.com/julia-syntax/>

安舒尔·塔亚尔

这是我在 Julia 编程系列中的第二篇文章。在我之前的博客中，我向你介绍了 [Julia 编程](/julia-programming/)，并讨论了它的起源和特性。在这里，我将使用 Julia 编程的基本语法。

我将本文分为以下几个部分:

*   [基本算术运算](#basic-arithmetic-operations)
*   [一般操作](#general-operations)
*   [琴弦](#strings)
*   [数据结构](#data-structures)
*   [使用矩阵](#working-with-matrices)
*   [循环](#loops)
*   [条件语句](#conditional-statements)
*   [功能](#functions)
*   [在 Julia 中使用 R 和 Python 代码](#using-r-and-python-code-in-julia)
*   [Python vs Julia——基本操作的语法比较](#python-vs-julia-comparison-of-syntax-for-basic-operations)

* * *

让我们从学习任何新的编程语言的最传统的方法开始。

![Julia hello world](img/edcb3b0acdff7d573c7cc1b56d118cc9.png)

对于前几个代码片段，我特意使用了我的 Julia 控制台中的屏幕截图，以便您更好地了解它。

* * *

## 基本算术运算

让我们用 Julia 做一些基本的算术运算。执行同一操作有多种方式。

![Julia addition](img/3f1cb9b5ab3af49135aeff8d0ff1781b.png)

以下是如何编写复数并对其进行基本运算的方法。

![Julia complex numbers](img/7cbc7135a511e9d3a4c8c2a360454201.png)

当你将一个浮点数加到一个整数上时，它返回一个浮点数。

```py
 ## Returns a float 
1.0 + 2 
```

```py
Output: 3.0

```

让我们看看组织。

```py
## Division 
1/2

```

```py
Output: 0.5

```

指数运算可以使用“^”符号来完成。

```py
5^2

```

```py
Output: 25
```

朱莉娅也能对分数进行运算。

```py
## Fractional numbers
1//2
## Adding fractional numbers
1//12 + 3//29

```

```py
 Output: 65//348
```

* * *

## 常规操作

编程时，查看变量的类型至关重要。以下是在 Julia 中可以做到的方法。

```py
typeof(1)
typeof(1.0)
typeof('a')
typeof("Test")

```

```py
Output:

Int64
Float64
Char
String

```

这里需要注意的一点是，字符是用单引号定义的，而字符串是用双引号定义的。单引号中的字符串将返回错误。

让我们看看如何将一种变量类型转换成另一种类型。

将浮点数转换为整数。

```py
# Method 1
convert(Int32, 1.0)

# Method 2
Int64(4.0)

```

```py
Output:
1
4

```

以下示例显示了在 Julia 中注释多行代码的方法。

```py
#=
Your comments here
Your comments here
Your comments here
=#

```

单行注释可以写在“#”之后。

当您遇到困难时，这些文档会派上用场。以下是你如何找到任何函数的细节-

```py
? log
Output: log(b,x) Compute the base blogarithm of x. Throws DomainError for negative Real arguments.
Examples
julia> log(4,8)
1.5
julia> log(4,2)
0.5

```

* * *

## 用线串

现在，让我们看看如何在 Julia 中使用字符串。

```py
 "This is a string."
```

```py
Output: This is a string.
```

可以使用""或""" ""来定义字符串。第二个版本的用例是当你需要在字符串中使用'时。比如说-

```py
 """ This is the use case for "triple-quote" string definition method.""" 
```

```py
Output: This is the use case for \"triple-quote\" string definition method.

```

下面是我们如何使用类似字符串的变量。

```py
variable = "Julia"
"This is how variables can be used inside strings in $variable."

```

```py
Output: This is how variables can be used inside strings in Julia.

```

也可以对字符串执行求幂运算。这里有一个例子-

```py
 variable^3 
```

```py
Output: JuliaJuliaJulia
```

让我们继续讨论操作字符串的方法。做同一件事有多种方法。让我们看看如何添加 2 个字符串。

```py
# Method 1

string("This is how we", " merge strings")
string("This is how we merge ", 2,  " strings with a number in-between")

# Method 2

var_1 = "This is method 2"
var_2 = "of concatenating strings in Julia"
var_1 * " " * var_2

# Method 3

var_3 = "This is method 3"
"$var_3 $var_2"

```

```py
Output: 
This is how we merge strings 
This is how we merge 2 strings with a number in-between 
This is method 2 of concatenating strings in Julia 
This is method 3 of concatenating strings in Julia

```

* * *

## 数据结构

数据结构是任何编程语言的组成部分。它们提供了不同的方法来组织数据，以便有效地使用它们。

### 元组

元组是一种不能修改的数据结构。下面是定义元组的方法。

```py
tuples = (1, 2, 3)
typeof(tuples)

```

```py
Output:
(1, 2, 3)
Tuple{Int64, Int64, Int64}

```

Julia 中的索引从 1 开始。以下是在 Julia 中访问任何数据结构的第一个和最后一个元素的方法。

```py
# Accessing the first element
tuples[1]

# Accessing the last element
tuples[end]

# [10] [11] Negative indexing doesn't work in Julia
tuples[-1]

# Tuples can't be modified
push!(tuples, 2)

```

```py
Output:

1
3

BoundsError: attempt to access Tuple{Int64, Int64, Int64} at index [-1]
Stacktrace:
[1] getindex(t::Tuple, i::Int64)
@ Base ./tuple.jl:29
[2] top-level scope
@ In[30]:2
[3] eval
@ ./boot.jl:360 [inlined]
[4] include_string(mapexpr::typeof(REPL.softscope), mod::Module, code::String, filename::String)
@ Base ./loading.jl:1116
MethodError: no method matching push!(::Tuple{Int64, Int64, Int64}, ::Int64)
Closest candidates are:
push!(::Any, ::Any, ::Any) at abstractarray.jl:2387
push!(::Any, ::Any, ::Any, ::Any...) at abstractarray.jl:2388
push!(::AbstractChannel, ::Any) at channels.jl:10
...
Stacktrace:
[1] top-level scope
@ In[33]:2
[2] eval
@ ./boot.jl:360 [inlined]
[3] include_string(mapexpr::typeof(REPL.softscope), mod::Module, code::String, filename::String)
@ Base ./loading.jl:1116

```

你可以这样合并元组-

```py
# Concatenating tuples
(tuples..., tuples...)

# This method of adding "..." after any variable can be used to merge any two datatypes

```

```py
Output:

(1, 2, 3, 1, 2, 3)

```

### 向量

向量是一种可以修改的数据结构。这是你如何使用向量的方法。

```py
# Method 1
vector = [8, 1, 9, 12]

# Method 2
vector_2 = [8 ; 1 ; 9 ; 12]

```

```py
Output:

4-element Vector{Int64}:

8
1
9
12

```

这就是在朱莉娅身上突变是如何实现的。使用“！”符号，将更改写入原始变量。这相当于 Python 中的“inplace=True”。

```py
# Mutation in Julia
sort(vector)

# The original vector doesn't change
sort!(vector)

# The original vector changes
vector

```

```py
Output:

4-element Vector{Int64}:
1
8
9
12

```

若要执行基于元素的操作，请使用“.”接线员。

vector + 1 #这个不行

```py
vector .+ 1

# Adding vectors
vector + vector_2

```

```py
Output: 

4-element Vector{Int64}:
2
9
10
13

4-element Vector{Int64}:
2
16
18
24

```

现在，向量可以包含不同数据类型的变量。这里有一个例子-

```py
vector_3 = [1, 5, "foo", 1+3im]

```

```py
Output:

4-element Vector{Any}:
1
5
"foo"
1 + 3im

```

请注意，vector 类型被假定为“Any ”,因为存在不同数据类型的变量。

我们来看看数列的生成方法。下面是一个生成从 1 到 10、间距为 2 的序列的示例。

```py
seq = [1:2:10;]

```

这是输出的样子。

```py
Output:

5-element Vector{Int64}:
1
3
5
7
9

```

### 字典

现在我们继续创建字典。在编程语言中，字典用于存储关于唯一变量的信息。

就像人类语言词典中的每个单词都有一个相关的含义一样，在 Julia 中，每个键都有一个相关的值。这在您想要查找与特定键相关联的值的情况下非常有用。

以下是如何在 Julia 中创建字典的方法。

```py
dictionary = Dict('A' => 1, 'B' => 2)

```

这是输出的样子-

```py
Output:

Dict{Char, Int64} with 2 entries:
'A' => 1
'B' => 2

```

既然我们已经创建了一个字典，我们想访问它的各种元素。我们可以这样做。

```py
# Accessing the keys
keys(dictionary)

# Accessing the values associated with each key
values(dictionary)

```

```py
Output:

KeySet for a Dict{Char, Int64} with 2 entries. Keys:
'A'
'B'

ValueIterator for a Dict{Char, Int64} with 2 entries. Values:
1
2

```

让我们给字典增加一个新条目。

```py
# Adding a new entry

merge!(dictionary, Dict('J' => 23))

```

```py
Output:

Dict{Char, Int64} with 3 entries:
'J' => 23
'A' => 1
'B' => 2

```

请注意“！”符号使改变永久化。

现在让我们删除一个条目。

```py
## Removing an entry permanently from a dictionary
pop!(dictionary, 'J')

dictionary

```

```py
Output:

Dict{Char, Int64} with 2 entries:
'A' => 1
'B' => 2

```

* * *

## 使用矩阵

矩阵是用向量的向量表示的一组数字。以下是创建矩阵的方法。

```py
matrix_1 = [[1 2 3 ]; [4 5 6]]

```

它看起来是这样的:

```py
Output:

2×3 Matrix{Int64}:
1 2  3
4 5  6

```

让我们看看矩阵中的其他各种运算。

```py

# Size of a matrix
print("This size of the matrix is" , size(matrix_1))

# Matrix
matrix_2 = [[2 2 0 ]; [2 7 9]]

#Transpose of a matrix
matrix_2'

# Accessing matrix elements
matrix_2[2,3]
matrix_2[1:4]

```

```py
Output:

The size of the matrix is (2, 3)

2×3 Matrix{Int64}:
2 2  0
2 7  9

9

4-element Vector{Int64}:
2
2
2
7

```

现在让我们来做矩阵的加法和乘法。

```py
# Adding matrices
matrix_2 + matrix_1
matrix_3 = [[2 3] ; [5 6] ; [4 5]]

# Multiplying matrices
matrix_1 * matrix_3

```

```py
The output of addition is -
2×3 Matrix{Int64}:
3 4   3
6 12  15

The output of multiplication is -
2×2 Matrix{Int64}:
24  30
57  72

```

使用“.”在 Julia 中执行 elementwise 操作符号。任何后跟“.”的操作会表演。这里有一个取矩阵中每个元素的对数的例子。它相当于 Python 中的 map()函数

```py
# element wise operation.

log.(matrix_1)

```

```py
Output:

2×3 Matrix{Float64}:
0.0 0.693147  1.09861
1.38629 1.60944   1.79176

```

让我们创建一个 0 和 1 的矩阵。您可以使用函数 0()和 1()来实现这一点。

```py
zero = zeros(3,4)
one = ones(2,3)

```

```py
Output:

3×4 Matrix{Float64}:
0.0 0.0  0.0  0.0
0.0 0.0  0.0  0.0
0.0 0.0  0.0  0.0

2×3 Matrix{Float64}:
1.0 1.0  1.0
1.0 1.0  1.0

```

让我们看看如何生成随机值。

```py
rand_1 = rand(5)

# Random values in 2D
rand_2 = rand(5, 2)

# Random values in 3D
rand_3 = rand(3, 2, 2)

```

```py
Output:

5-element Vector{Float64}:
0.24942793903668203
0.8454642816997531
0.8538602946052574
0.21154126925067507
0.07873330355017316

5×2 Matrix{Float64}:
0.706975 0.935989
0.494324 0.988657
0.994824 0.943832
0.44183 0.404011
0.802337 0.124313

3×2×2 Array{Float64, 3}:
[:, :, 1] =
0.443337 0.813706
0.958816 0.53124
0.203751 0.951473

[:, :, 2] =
0.125259 0.761672
0.440907 0.0505402
0.161741 0.672215

```

* * *

## 环

循环有助于重复执行相同的任务。编程中使用了多种类型的循环。大多数情况下，它们是:

*   **For loop** -当要运行的迭代次数事先已知时，使用这种类型的循环。
*   **While loop** -当迭代次数取决于条件时，使用这种类型的循环。

让我们看看如何在 Julia 中创建它们。

```py
## While loop

var = 0
while var < 10
var += 1
println(var)
end

```

```py
Output:

1
2
3
4
5
6
7
8
9
10

```

```py
## For loop

# Method 1
for i in 1:10
println(i)
end

# Method 2
colleagues = ["Vivek", "Jay", "Mario", "Udisha"]
for colleague in colleagues
println(colleague)
end

# Method 3
c = [i+j for i in 1:3, j in 1:5]

```

```py
Output:

The output of method 1 -
1
2
3
4
5
6
7
8
9
10

The output of method 2 -
Vivek
Jay
Mario
Udisha

The output of method 3 -
3×5 Matrix{Int64}:
2 3  4  5  6
3 4  5  6  7
4 5  6  7  8

```

在任何编程语言中，都有多种方法来执行相同的操作。请随意采取自己的方法。

* * *

## 条件语句

让我们继续讨论条件语句。这些是 if-else 条件语句，您希望在某个事件发生时执行某个操作。下面是控制流程。

语法是这样的

```py
if condition 1
println(“Statements if condition 1 is true”)
else
println(“Statements if condition 1 is false”)
end
```

这是你可以做到的。

```py
var_1 = 31
var_2 = 45

# Method 1
if var_1 > var_2
println("$var_1 is larger than $var_2")
elseif var_2 > var_1
println("$var_2 is larger than $var_1")
else
println("None")
end

# Method 2
# condition ? True:False
(var_1 > var_2) ? var_1 : var_2

# Method 3
# && is logical "and" operator
(var_1 > var_2) && [22] println("$var_1 is larger than $var_2")
(var_2 > var_1) && println("$var_2 is larger than $var_1")

```

```py
Output:

45 is larger than 31

45

false

45 is larger than 31

```

* * *

## 功能

函数是一组编写在一起的指令，这样它们就可以多次使用，而无需重复编写代码。

创建函数还有助于轻松调试代码，因为您可以查看单个块(函数)并找出有错误的块。

下面是我们如何在 Julia 中编写函数:

```py

# Method 1
function power_5(var_1)
return var_1^5
end

# Calling the function
power_5(4)

# Method 2
power_5(x) = x^5
power_5(4)

```

```py
Output:

1024
1024

```

* * *

## 在 Julia 中使用 R 和 Python 代码

有时，您可能希望使用 R 或 Python 代码，因为在 Julia 中可能没有执行某些操作的库。

然而，使用两种语言来执行某个操作可能是一个挑战。因此，Julia 通过使用“PyCall”和“RCall”包提供了使用 R 和 Python 代码的选项。

### 如何在 Julia 中使用 Python 代码

以下是如何在 Julia 中使用 Python 代码的方法。

```py

# Install the "PyCall" package for Python
using Pkg
Pkg.add("PyCall")
using PyCall

## Importing numpy package from Python
np = pyimport("numpy")

## Using numpy package in Julia
np.array([1,2,3])

```

```py
Output:

3-element Vector{Int64}:
1
2
3

```

### 如何在 Julia 中使用 R 代码

让我们看一个在 Julia 中使用 R 的例子。

```py
# Install "RCall" package for R
Pkg.add("RCall")
using RCall

# There are several ways to call R code

# Method 1
# Calling the mean() function from R
rcall(:mean, [1,2,3])

# Method 2 for user-defined functions
R"""
power_4 <- function(x)
{
return(x^4)
}"""

## Calling the defined function
rcall(:power_4, 5)

```

```py
Output:

RObject{RealSxp}
[1] 2
RObject{RealSxp}
[1] 625

```

关于使用 RCall 包的更多细节，你可以参考这里的[。](https://juliainterop.github.io/RCall.jl/stable/gettingstarted/)

* * *

## Python 与 Julia——基本操作的语法比较

| **功能** | **Python** | 朱莉娅 |
| 列向量 | [1, 2, 3] | [1,2,3] |
| 单行矩阵 | [[1], [2], [3]] | [1 2 3] |
| 数字序列 | 范围(1，10，2) | [1:2:10; ] |
| [数]矩阵 | [[1,2] , [3,4]] | [1 2; 3 4] |
| 随机数 | 随机的 | 兰特(4.5) |
| 变化 | 原地=真 | ！ |
| 矩阵到向量 | 扁平() | 一个[:] |
| 矩阵的共轭 | A.conj() | 一个 |
| 元素式操作 | 地图() | 。 |
| 力量 | var**2 | var^2 |
| 索引 | 从 0 开始 | 从 1 开始 |
| 最大值 | 最大值(A) | 最大(A) |
| 最小值 | 最小(A) | 最低(A) |
| For 循环 | 对于 i in 范围(n):
#命令 | 对于 i in 1:n
#命令
结束 |
| While 循环 | 当 i <=n 时: | 当 i <=n 时 |
| 如果-否则 | 如果我<=m:
#命令
否则:
#命令 | 如果我<=m
#命令
否则
#命令
结束 |
| 临时功能 | y =λx:x * * 5 | Y = x -> x^5 |
| 功能 | def func(y，x):
返回 y + 3*x | func(y，x) = y + 3x
或
函数 func(y，x)
返回 y + 3x
结束 |

* * *

## 结论

在本文中，我们从代码片段开始。这个想法是向您介绍这种编程语言的基本语法和可能性。

下一篇文章将向您介绍 Julia 中的数据可视化技术。在那之前，你可以自由探索和创造你自己的朱莉娅之旅！

然而，如果你想从事算法交易，那么我们由行业专家、交易从业者和中坚分子如 E. P. Chan 博士、Euan Sinclair 博士等教授的综合[算法交易课程](https://www.quantinsti.com/)正适合你。立即注册！

* * *

<small>*免责声明:本文提供的所有数据和信息仅供参考。QuantInsti 对本文中任何信息的准确性、完整性、现时性、适用性或有效性不做任何陈述，也不对这些信息中的任何错误、遗漏或延迟或因其显示或使用而导致的任何损失、伤害或损害负责。所有信息均按原样提供。*</small>
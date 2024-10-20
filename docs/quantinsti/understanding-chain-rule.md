# 理解链式法则

> 原文：<https://blog.quantinsti.com/understanding-chain-rule/>

由[瓦伦·迪瓦卡](https://www.linkedin.com/in/varun-divakar-b862a667/)

在这篇关于“理解链式法则”的博客中，我们将借助一个例子来学习链式法则背后的数学原理。

#### **目录**

*   [什么是衍生品？](#derivative)
*   [什么是链式法则？](#chainrule)
*   [理解链式法则](#understand)
*   [链式法则示例](#example)

对于那些对[神经网络和深度学习](https://blog.quantinsti.com/introduction-deep-learning-neural-network)感兴趣的人来说，[反向传播](https://blog.quantinsti.com/backpropagation)的过程是一个非常重要的概念，在创建这些高级模型时被广泛使用。在执行反向传播时，我们使用链式法则的概念反向传播预测中的误差值来调整权重。

为了能够理解这个单位，你应该知道什么是导数。

## **![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")什么是导数？**

不要多心，万一不知道或者不记得一样，可以去 Quantra 网站的[词汇表版块了解一下。](https://quantra.quantinsti.com/glossary)

## **![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")什么是链式法则？**

链式法则基本上是一个计算两个或多个函数合成的导数的公式。

## **![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")理解链式法则**

假设 f 和 g 是函数，那么链式法则将它们合成的导数表示为 *f ∘ g* (将 *x* 映射到 *f(g(x))* 的函数)。如下所述计算该组成的导数。

![derivative](img/b47e9426b55a363fa9423b9eb1c2961b.png)

这里 *f* 是 *g* 的函数 *g* 是变量 *x* 的函数。

上述规则的另一种写法是:

![derivative](img/9495a145a792daa53566bf9c0745e4a4.png)

其中函数 *F* 代表复合函数 *f(g(x))*

假设我们有三个变量 *x，y* 和 *z* ，这样，变量 *z* 取决于变量 *y* ，而变量*y*又取决于变量 *x* 。所以 *y* 和 *z* 是因变量， *z* 通过中间变量 *y* 依赖于 *x* 。那么用于微分变量 *z* 的链式法则可以以下面的方式书写。

![differentiate](img/9116cb507d82376e1bafceec76598f10.png)

这是我们在反向传播中使用的最后一个公式。

这里 *z* 是 *y* 的函数，

***z = f(y)***

并且 *y* 是 *x* 的函数，

***y= g(x)***

使用前面的公式，我们可以将微分方程改写如下:

![differential equation](img/3ea50ff07654ddd4268cad5f02c44438.png)

让我们借助一个例子来更好地理解这一点。

## **![Anchor](img/4765334125b448ec4c4bdf8285a1da72.png "Anchor")链式法则的例子**

让我们借助维基百科的一个众所周知的例子来理解链式法则。假设你是从天上掉下来的，在下落的过程中，大气压一直在变化。查看下图，了解这一变化。

![chain rule example](img/35db125b610c61032a96c1cc41187da2.png)

在你坠落的时候，海拔 4000 米，初速度为零，重力是 9.8 米每秒平方。现在将这种情况与之前的链式法则方程进行比较。假设方程中的变量 *x* 是变量 *t* ，或者时间。

那么变量 *y* 或 *g(t)* ，也就是你从下落开始所走的距离，由下式给出

***g(t)= 0.5 * 9.8t<sup>2</sup>**T5】*

因此，平均海平面的高度可由变量 *h* 给出，即

***h = 4000g(t)***

假设我们也知道，基于模型，高度 *h* 处的大气压力为:

***f(h)= 101325 e<sup>—0.0001h</sup>***

这两个方程可以通过它们各自的变量来区分，以获得以下信息:

***g′(t)= 9.8t***，

其中，***g′(t)***是你在时间 *t* 的速度

***f′(h)=-10.1325<sup>e-0.0001h</sup>***

其中，***f′(h)***是大气压相对于高度的变化率 *h*

现在让我们来理解如何把这两个方程结合起来，得出

在跳伞者跳伞后的 *t* 秒，大气压力相对于时间的变化率，使用链式法则:

![chain rule](img/90d6d55b91ef98c93aec184ce96b28c4.png)

![chain rule calculation](img/c37613af2b403e7bdcb82b5fe450f9d0.png)

这个方程给出了自秋季以来大气压力随时间的变化率。在神经网络中，我们需要计算每个神经元的权重相对于预测误差的变化。现在你可能已经想到了，链式法则有助于相应地调整这些权重。

## **结论**

如果我们想应用链式法则来反向传播神经网络中的误差，那么我们将使用这样一个方程。

![chain rule to backpropagate](img/bd9064f50deef82e1f1e1512ed8b0a80.png)

在与 E. P. Chan 博士合作的 Quantra 关于 [交易中的深度学习的课程中，我们不仅会帮助您理解深度学习等先进概念，还会将它们应用到交易的背景中。](https://quantra.quantinsti.com/course/neural-networks-deep-learning-trading-ernest-chan)

*免责声明:股票市场的所有投资和交易都涉及风险。在金融市场进行交易的任何决定，包括股票或期权或其他金融工具的交易，都是个人决定，只能在彻底研究后做出，包括个人风险和财务评估以及在您认为必要的范围内寻求专业帮助。本文提到的交易策略或相关信息仅供参考。T3】*

**建议阅读:**

*   [神经网络中的前向传播](https://blog.quantinsti.com/forward-propagation-neural-networks)
*   [理解反向传播](https://blog.quantinsti.com/backpropagation)
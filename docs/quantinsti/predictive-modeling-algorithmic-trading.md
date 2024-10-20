# 算法交易的 R 语言预测建模

> 原文：<https://blog.quantinsti.com/predictive-modeling-algorithmic-trading/>

*由[米林德帕拉德卡](https://www.linkedin.com/in/milind-paradkar-b37292107)T3】*

![Predictive modeling in R](img/b3c788eec7484b156e6372b337e85f44.png)

### 什么是预测建模？

> ***预测建模*** *是在**预测**分析中使用的过程，用于创建未来行为的统计**模型**。**预测**分析是数据挖掘的一个领域，涉及预测概率和趋势*[*<sup>1</sup>*](http://searchdatamanagement.techtarget.com/definition/predictive-modeling)

[算法交易](https://quantra.quantinsti.com/course/getting-started-with-algorithmic-trading) 中的**预测建模是一个建模过程，其中我们使用一组**预测变量**来预测结果的概率。在这篇文章中，我们将展示 r。**

### 谁应该使用它？

可以为不同的资产建立预测模型，如股票、期货、货币、商品等。例如，我们可以建立一个模型来预测股票第二天的价格变化，或者建立一个模型来预测外汇汇率。

### 我们应该如何/为什么使用它？

预测建模的力量可以用来做出正确的投资决策，并建立有利可图的投资组合。

### 本文的目的

在这篇文章中，我们将详细介绍在 R 中使用不同的技术指标进行交易的预测建模的一步一步的过程。该模型试图使用这些指标和机器学习算法来预测第二天的价格变化(上涨/下跌)。

#### 步骤 1:特征构建

我们的过程从构建数据集开始，该数据集包含用于进行预测的特征和输出变量。

首先，我们使用由股票和指数的 5 年价格序列组成的原始数据构建数据集。该股票和指数数据由**日期、开盘、最高、最低、最后**和**成交量**组成。使用这些数据，我们根据各种技术指标(如下所列)计算我们的特征。

| **否** | **技术指标名称** |
| one | 力指数 |
| Two | 威廉%R |
| three | 相对强度指数 |
| four | 变化率 |
| five | 动量(MOM) |
| six | 平均真实范围 |

**注意:**在开始之前，请确保您已经在 RStudio 上安装并选择了以下软件包: ***Quantmode、* *PRoc、* *TTR、* *Caret、* *Corrplot、* *FSelector、* *rJava、* *kLar、* *randomforest、* *kernlab、***

##### r 代码:

![Predictive Modeling for Algorithmic Trading 1](img/07ca8802bd4f3864dec7bc0199c29e7c.png) ![Predictive Modeling for Algorithmic Trading 1](img/70d8816644f3659ffe6205c813f7de75.png)

计算出的技术指标与价格变化类别(上涨/下跌)相结合，形成一个数据集。

#### 步骤 2:使用数字和图像理解数据集

预测建模最重要的先决条件是对数据集有很好的理解。这种理解有助于:

*   数据转换
*   选择正确的机器学习算法
*   解释从模型中获得的结果
*   提高其准确性

为了获得对数据集的这种理解，您可以使用描述性统计，如标准差、均值、偏斜度，以及对数据的图形化理解。

##### r 代码:

![Predictive Modeling for Algorithmic Trading 1](img/e2f906d8a35f92959258b3a6e21a3b9c.png)

**相关矩阵![Predictive Modeling for Algorithmic Trading 1](img/4505ee9443bd82c5d279fd5289447b7f.png)**

#### 步骤 3:特征选择

特征选择是选择与模型构建最相关的特征子集的过程，有助于创建准确的预测模型。有各种各样的特征选择算法，这些算法主要属于以下三类之一:

1.  过滤方法-通过使用某种统计方法给特征分配分数来选择特征。
2.  包装方法–评估不同的功能子集，并确定最佳子集。
3.  嵌入式方法–这种方法在训练模型时计算出哪个特征的精确度最高。

在我们的模型中，我们将使用过滤方法，利用**f 选择器**包中的 **random.forest.importance** 函数。 **random.forest.importance** 函数评定每个特征在结果分类中的重要性，即类别变量。该函数返回一个数据框，其中包含每个属性的名称以及基于精度平均下降值的重要性值。

##### r 代码:

![Predictive Modeling for Algorithmic Trading 1](img/46b602cd6b40fae789f5f000b0abfbc2.png)

##### 输出:

![Predictive Modeling for Algorithmic Trading 1](img/3b0140dfb38ac4e3dd5792d7fa4acb90.png)

现在，为了使用由 **random.forest.importance** 返回的重要性值选择最佳特征，我们使用 **cutoff.k** 函数，该函数提供 k 个具有最高重要性值的特征。

在我们的模型中，我们从最初从价格数据序列中提取的 17 个特征中选择了 10 个。使用这十个特征，我们创建了一个将用于机器学习算法的数据集。

#### 步骤 4:设置重采样方法

在预测建模中，我们需要数据有两个原因:

*   来训练模型
*   测试数据以确定模型所做预测的准确性。

当数据有限时，我们可以使用重采样方法，将数据分成训练和测试部分。R 中有不同的重采样方法，如数据分裂、bootstrap 方法、k-fold 交叉验证、重复 k-fold 交叉验证等。

在我们的例子中，我们使用了 **k 重交叉验证方法**，该方法将数据集分成 **k 个子集**。当模型在所有剩余的子集上训练时，我们将每个子集放在一边。重复此过程，直到确定数据集中每个实例的准确性。最后，该函数确定总体精度估计值。

##### 代码: **![Predictive Modeling for Algorithmic Trading 1](img/9d20791662adfc9ed8e7c18ae3afd768.png)**

#### 第五步:训练不同的算法

R 中有数百种可用的机器学习算法，对于初学者来说，确定使用哪种模型可能会很困惑。建模者应该根据手头的问题尝试不同的算法，随着经验和实践的增加，你将能够确定正确的集合。

**几种问题:**

*   分类
*   回归
*   使聚集
*   规则提取

在我们的例子中，我们正在处理一个分类问题，因此我们将探索一些适合解决这类问题的算法。我们将使用以下内容:

*   k-最近邻(KNN)
*   分类和回归树
*   朴素贝叶斯
*   基于径向基函数(SVM)算法的支持向量机。

我们不会详述这些算法的工作，因为这篇文章的目的是详述建模过程中的步骤，而不是这些算法的底层工作。

我们使用 caret 包中的 train 函数，它使用调整参数网格来拟合不同的预测模型。例如:

![predictive-modeling-for-algorithmic-trading-8](img/eb18e2f60d0106256bad0fc5f313d930.png)

在上面的例子中，我们使用的是通过方法参数指定的 **KNN** 算法。**类**是输出变量，**数据集 _rf** 是用于训练和测试模型的数据集。 **preProc** 参数定义数据转换方法，而 **trControl** 参数定义训练函数的计算细节。

![Predictive Modeling for Algorithmic Trading 1](img/c8c77eff02020baeb09b6b498e683906.png)

#### 步骤 6:评估模型

使用不同的度量标准，如准确度、Kappa、均方根误差(RMSE)、R <sup>2</sup> 等，评估训练的模型在预测结果中的准确度。

我们使用“准确性”指标来评估我们训练的模型。准确性是正确分类的实例占测试数据集中所有实例的百分比。我们已经使用了 caret 包中的 resamples 函数，它接受经过训练的对象，并使用 summary 函数生成一个摘要。

![Predictive Modeling for Algorithmic Trading 1](img/dd9cd707d7afb7de496f170ae1a0644b.png)

![Predictive Modeling for Algorithmic Trading 1](img/2a5b84caf123ed8ba65f70db00595327.png)

![Predictive Modeling for Algorithmic Trading 1](img/a1c1682b2d4e72de8b6791af354f4f62.png)

#### 步骤 7:调整入围模型

正如我们可以从精确度指标中观察到的，所有模型的精确度都在 50-54%之间。理想情况下，我们应该尝试以最高的精度调整模型。然而，出于示例的原因，我们将选择 KNN 算法，并尝试通过调整参数来提高其精度。

##### 调整参数

我们将在 1 到 10 的范围内调整 KNN 算法(参数 k)。训练函数中的 **tuneGrid** 参数有助于在评估模型时确定该范围内的精度。

![Predictive Modeling for Algorithmic Trading 1](img/65cafbc3865943c7d1a247658cdf6ee8.png)

##### 输出:

![Predictive Modeling for Algorithmic Trading 1](img/3363575334492b61a27284cc6b5e7ebb.png)

从调整过程中可以看出，KNN 算法的精度没有增加，它与早先获得的精度相似。您也可以尝试根据其他算法各自的调整参数来调整它们，并选择精确度最高的算法。

### 结论:

在初始阶段，建模人员可以尝试使用不同的技术指标，基于其他资产类别创建模型，并尝试不同的预测建模问题。有一些非常好的软件包可以使 R 中的预测建模变得容易，有了经验和实践，你将开始构建健壮的模型，在市场中交易获利。

### 下一步

学习一个简单的实践和实施期权交易策略，一个容易跟随的例子。您还可以学习如何使用 Python 编程来设计这种策略的收益图。[点击此处](/long-strangle-option-strategy-in-python/)进入战略。

### **下载数据文件**

*   预测建模 program.rar
    *   BAJAJ-汽车 5 年数据. csv
    *   NIFTY 5 年数据. csv
    *   r 代码-预测建模 program.rar
# 整体方法——装袋和增压

> 原文：<https://blog.quantinsti.com/ensemble-methods-bagging-boosting/>

由马里奥·皮萨·培尼亚和 T2 主持

在这篇 **[帖子](/decision-tree)** 中，我们已经简单地看到了什么是决策树，以及如何为分类和回归问题构建决策树。我们还看到，它们对于进行定性或定量预测非常有用，而且构建它们并没有太大的困难。

但是，有必要了解决策树通常存在的问题，因为算法构建决策树的贪婪方法并不总是提供最佳输出，预测的精度和稳健性也不像我们希望的那样稳定。

通常，决策树有以下已知问题:

*   噪音
*   欠拟合(偏差)
*   过度拟合(方差)

在本帖中，我们将重点关注 Bagging 和 Boosting，以分别并行和顺序地[构建决策树](https://quantra.quantinsti.com/course/decision-trees-analysis-trading-ernest-chan)，并集成输出以提高预测精度和减少方差。

### **什么是装袋？**

**Bagging** ，也称为 **bootstrapping，**是一种减少预测方差的集成方法。

Bagging 算法与 N 个随机生成的数据集并行构建 N 棵树，并替换以训练模型，最终结果是在树上获得的所有结果的平均值(对于回归树)或最高评级(对于分类树)。

因此，**打包**或**自举**算法执行的步骤很简单:

1.  用训练数据集的替换生成 N 个随机数据集。
2.  并行拟合每个随机训练数据集的 N 个预测值，每棵树一组。
3.  对回归树的结果进行平均，或者对分类树进行最多投票。

我们必须考虑到，这种方法并不总是改进我们的决策树的最佳算法，因为它只适用于当我们有一个复杂的树，它的预测显示出很大的差异。

我们使用 sklearn.ensemble 库中的函数 BaggingRegressor 和 BaggingClassifier 来实现 bagging 算法。

### **用 Python 构建决策树**

让我们记住用 Python 构建决策树的主要步骤:

1.  检索和整理金融工具的市场数据。
2.  引入预测变量(即技术指标、[情绪指标](https://quantra.quantinsti.com/course/trading-using-options-sentiment-indicators)、广度指标等)。)
3.  设置目标变量或所需输出。
4.  在训练数据和测试数据之间拆分数据。
5.  生成训练模型的决策树。
6.  测试和分析模型。

你可以参考[这篇博客](/decision-tree)来了解更多关于如何构建决策树、决策树分类器等等。

### **用 Bagging 增强决策树**

我们几乎可以重用上面提到的关于决策树的所有步骤。虽然当我们到达第五步时，我们必须用 Bagging 算法替换它。

### **增压**

与并行集成技术 bagging 不同，boosting 按顺序工作。它的目的是通过顺序改进先前的分类，将弱学习者转换为强学习者，从而随着我们的前进将偏差误差最小化。

### 增压是如何工作的？

最初，通过从训练数据集中随机选择数据集，Boosting 开始类似于 bagging。它使用这些特征创建分类模型，并在现有的“训练数据集”上测试该模型。

训练数据集中的一些数据点被正确分类。现在，为了构建下一个随机数据集，在前一个数据集中被错误分类的实例或数据点将被给予更高的优先级，这仅仅意味着这些实例或数据点将具有在下一个数据集中被选择的更高可能性。

通过这种方式，boosting 使用从先前选择的实例中获得的数据来顺序构建 N 个随机数据集。

### **升压算法的类型**

*   #### **AdaBoost**

自适应增强技术迭代地工作，以改进在某一阶段发生的分类。它使用决策树桩。

**什么是决策树桩？**

决策树桩基本上是基于单个特征做出决策的一级决策树。

决策树桩用于对数据点进行分类，并通过增加误分类数据点的优先级来迭代改进。不同的决策树桩也可以组合起来，以创建一个更好的决策树桩，这将确保数据没有任何错误。

我们可以使用 sklearn.ensemble 库中的 AdaBoostRegressor 和 AdaBoostClassifier 来实现 AdaBoost 算法。

*   #### **Gradient propulsion**

就像 AdaBoost 专注于最小化错误分类的点一样，梯度提升专注于最小化模型内的损失函数。

一旦为特定模型定义了损失函数，就使用梯度提升来最小化该函数的值，从而通过修改与数据点相关联的权重来最小化构建另一棵树时的误差。

通过使用库 sklearn.ensemble，GradientBoostingRegressor 和 GradientBoostingClassifier 可用于在 Python 中实现此方法。

*   #### **XGBoost**T3】

XGBoost 或极端梯度增强模型是梯度增强的一种实现。这是一个可用于实现梯度推进算法的库。

你可以在 R [这里](/forecasting-markets-using-extreme-gradient-boosting-xgboost)详细阅读并学习如何实现。

### **结论**

In the fabulous world of ML, this enhancement method for our decision trees helps us to reduce the variance and increase the accuracy but it is necessary to know when to apply it because if our decision trees have other problems it will be more convenient to know and apply other serial or parallel enhancement methods.

在本课程中，您可以了解更多关于决策树和集成方法在 Python 中的实现。

*免责声明:本文提供的所有数据和信息仅供参考。QuantInsti 对本文中任何信息的准确性、完整性、现时性、适用性或有效性不做任何陈述，也不对这些信息中的任何错误、遗漏或延迟或因其显示或使用而导致的任何损失、伤害或损害承担任何责任。所有信息均按原样提供。T3】*
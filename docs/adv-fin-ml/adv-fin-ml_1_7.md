# 第九章：交叉验证下的超参数调优

## 9.1 动机

超参数调优是拟合机器学习算法的重要步骤。如果这一步没有做好，算法可能会过拟合，实际表现会令人失望。机器学习文献特别关注对任何调优超参数进行交叉验证。正如我们在第七章中看到的，金融领域的交叉验证（CV）是一个特别困难的问题，其他领域的解决方案可能会失败。在本章中，我们将讨论如何使用清除的 k 折 CV 方法进行超参数调优。参考文献部分列出了提出可能在特定问题中有用的替代方法的研究。

## 9.2 网格搜索交叉验证

网格搜索交叉验证根据用户定义的得分函数对最大化 CV 性能的参数组合进行彻底搜索。当我们对数据的底层结构了解不多时，这是一种合理的初步方法。Scikit-learn 在`GridSearchCV`函数中实现了这一逻辑，该函数接受 CV 生成器作为参数。由于第七章中解释的原因，我们需要传递`PurgedKFold`类（代码片段 7.3），以防止`GridSearchCV`对泄漏信息过拟合 ML 估计器。

> **代码片段 9.1 使用清除的 K 折交叉验证的网格搜索**
> 
> ![](img/Image00387.jpg)

代码片段 9.1 列出了函数`clfHyperFit`，该函数实现了清除的`GridSearchCV`。参数`fit_params`可用于传递`sample_weight`，而`param_grid`包含将组合成网格的值。此外，该函数允许对调优的估计器进行集成。对估计器进行集成通常是个好主意，原因在第六章中已解释，上述函数包含了为此目的的逻辑。

我建议你在元标签应用的上下文中使用`scoring=‘f1’`，原因如下。假设样本中有大量负面（即，标签为‘0’）案例。一个将所有案例预测为负面的分类器将获得高`‘accuracy’`或`‘neg_log_loss’`，尽管它并未从特征中学习如何区分案例。实际上，这种模型的召回率为零，精确度未定义（见第三章第 3.7 节）。`‘f1’`分数通过从精确度和召回率的角度评分分类器来纠正这种性能膨胀（见第十四章第 14.8 节）。

对于其他（非元标签）应用，使用`‘accuracy’`或`‘neg_log_loss’`是可以的，因为我们对所有案例的预测都同样感兴趣。请注意，对案例的重新标记对`‘accuracy’`或`‘neg_log_loss’`没有影响，但会对`‘f1’`产生影响。

此示例很好地引入了 sklearn 的`Pipelines`的一个限制：它们的拟合方法不期望`sample_weight`参数，而是期望一个带关键字的`fit_params`参数。这是一个已在 GitHub 上报告的错误；不过，修复可能需要一些时间，因为这涉及到重写和测试大量功能。在那之前，可以自由使用代码片段 9.2 中的解决方法。它创建了一个新类，称为`MyPipeline`，该类继承了 sklearn 的`Pipeline`中的所有方法。它用一个新的方法覆盖继承的`fit`方法，该方法处理参数`sample_weight`，然后重定向到父类。

> **代码片段 9.2 增强型管道类**
> 
> ![](img/Image00389.jpg)

如果你不熟悉扩展类的这种技术，建议阅读这个入门的 Stackoverflow 文章：[`stackoverflow.com/questions/ 576169/understanding-python-super-with-init-methods`](http://stackoverflow.com/questions/576169/understanding-python-super-with-init-methods)。

## 9.3 随机搜索交叉验证

对于参数数量较多的机器学习算法，网格搜索交叉验证 (CV) 变得计算上不可行。在这种情况下，一个具有良好统计特性的替代方案是从一个分布中抽样每个参数（Begstra 等人 [2011, 2012]）。这有两个好处：首先，我们可以控制搜索的组合数量，而不考虑问题的维度（相当于计算预算）。其次，性能上相对无关的参数不会显著增加我们的搜索时间，这与网格搜索 CV 的情况相反。

与其编写一个新的函数来处理 `RandomizedSearchCV`，不如扩展代码片段 9.1，加入一个选项。一个可能的实现是代码片段 9.3。

> **代码片段 9.3 使用清除 K 折交叉验证的随机搜索**
> 
> ![](img/Image00391.jpg)

**9.3.1 对数均匀分布**

一些机器学习算法通常仅接受非负超参数。这就是一些非常流行的参数的情况，例如 SVC 分类器中的 `C` 和 RBF 核中的 `gamma`。^(1) 我们可以从一个界定在 0 和某个大值（例如 100）的均匀分布中抽取随机数。这意味着 99% 的值预计会大于 1。这并不一定是探索非线性响应参数的可行区域的最有效方法。例如，SVC 对于将 `C` 从 0.01 增加到 1 的反应与将 `C` 从 1 增加到 100 的反应是一样的。^(2) 因此，从 *U* [0, 100]（均匀）分布中抽样 `C` 将是低效的。在这种情况下，似乎从对数分布均匀抽取值更为有效。我称之为“对数均匀分布”，由于在文献中找不到这个定义，我必须对其进行恰当的定义。

随机变量 *x* 在 *a* > 0 和 *b* > *a* 之间遵循对数均匀分布，当且仅当 log [ *x* ] ∼ *U* [log [ *a* ], log [ *b* ]]。该分布的累积分布函数 (CDF) 为：

![](img/Image00394.jpg)

从中，我们得出一个 PDF：

![](img/Image00569.jpg)

![](img/Image00401.jpg)

**图 9.1** 测试 `logUniform_gen` 类的结果

请注意，CDF 对对数的底数是不变的，因为！[](Image00403.jpg)，对任何底数 *c* 都是如此，因此随机变量不是 *c* 的函数。Snippet 9.4 在 `scipy.stats` 中实现（并测试）了一个随机变量，其中 [ *a* , *b* ] = [1 *E* − 3, 1 *E* 3]，因此 log [ *x* ] ∼ *U* [log [1 *E* − 3], log [1 *E* 3]]。  图 9.1  显示了样本在对数尺度上的均匀性。

> **SNIPPET 9.4 THE** `**LOGUNIFORM_GEN**` **CLASS**
> 
> ![](img/Image00406.jpg)

## 9.4 评分与超参数调优

片段 9.1 和 9.3 为元标签应用设置了 `scoring=‘f1’`。对于其他应用，它们设置了 `scoring=`neg_log_loss`` 而不是标准的 `scoring=‘accuracy’`。尽管准确度有更直观的解释，我建议你在调整投资策略的超参数时使用 `neg_log_loss`。让我解释一下我的理由。

假设你的机器学习投资策略预测你应该以高概率购买某个证券。你将根据策略的信心进入一个较大的多头头寸。如果预测是错误的，而市场反而下跌，你将会损失很多钱。然而，准确度对高概率的错误买入预测和低概率的错误买入预测一视同仁。此外，准确度可以用低概率的命中来弥补高概率的漏掉。

投资策略通过以高信心预测正确标签而获利。低信心的良好预测所带来的收益不足以弥补高信心的错误预测带来的损失。因此，准确度无法真实反映分类器的性能。相反，日志损失 ^(3)（也称交叉熵损失）计算分类器在给定真实标签时的对数似然，考虑了预测的概率。日志损失可以如下估计：

![](img/Image00409.jpg)

其中

+   *p [*n* , *k*]* 是与标签 *k* 的预测 *n* 相关的概率。

+   *Y* 是一个 1-of-*K* 的二元指示矩阵，当观察 *n* 被分配标签 *k*（从 *K* 个可能标签中）时，*y [*n* , *k*]* = 1，否则为 0。

假设分类器预测两个 1，其中真实标签分别为 1 和 0。第一个预测是命中，第二个预测是漏掉，因此准确度为 50%。图 9.2 绘制了这些预测来自于概率范围 [0.5, 0.9] 时的交叉熵损失。可以观察到在图的右侧，由于高概率的漏掉，日志损失很大，尽管所有情况下的准确度都是 50%。

![](img/Image00411.jpg)

**图 9.2** 日志损失与命中和漏掉的预测概率的关系

偏好交叉熵损失而不是准确度的第二个原因是，交叉验证通过应用样本权重来评估分类器（见第七章，第 7.5 节）。正如您在第四章中回忆的那样，观察权重是根据观察的绝对收益确定的。这意味着，样本加权的交叉熵损失在 PNL（市值损益）计算中估计了分类器的表现：它使用正确的标签来表示方向，概率来表示头寸规模，样本权重来表示观察的收益/结果。这是金融应用中超参数调整的正确机器学习性能指标，而不是准确度。

当我们使用对数损失作为评分统计时，通常更喜欢改变其符号，因此称之为“负对数损失 *.* ”。这种变化的原因是出于美观，基于直觉：高的负对数损失值优于低的负对数损失值，这与准确度类似。在使用`neg_log_loss`时，请记住这个 sklearn 的 bug：[`github.com/scikit-learn/scikit-learn/issues/9144`](https://github.com/scikit-learn/scikit-learn/issues/9144)。为了规避此 bug，您应该使用第七章中介绍的`cvScore`函数。

**练习**

1.  > > 使用第八章中的`getTestData`函数，形成一个包含 10,000 个观测值和 10 个特征的合成数据集，其中 5 个是信息性特征，5 个是噪声特征。

    1.  在 10 折交叉验证中使用`GridSearchCV`来寻找具有 RBF 内核的 SVC 的`C`和`gamma`最优超参数，其中`param_grid = {'C':[1E-2,1E-1,1,10,100],'gamma':[1E-2,1E-1,1,10,100]}`，评分函数为`neg_log_loss`。

    1.  网格中有多少个节点？

    1.  找到最优解决方案花了多少次拟合？

    1.  找到这个解决方案花了多长时间？

    1.  如何访问最优结果？

    1.  最优参数组合的 CV 评分是多少？

    1.  如何将样本权重传递给 SVC？

1.  > > 使用练习 1 中的相同数据集，

    1.  在 10 折交叉验证中使用`RandomizedSearchCV`来寻找具有 RBF 内核的 SVC 的`C`和`gamma`最优超参数，其中`param_distributions = {`C`:logUniform(a = 1E-2,b = 1E2),`gamma`:logUniform(a = 1E-2,b = 1E2)},n_iter = 25`，评分函数为`neg_log_loss`。

    1.  找到这个解决方案花了多长时间？

    1.  最优参数组合是否与练习 1 中找到的类似？

    1.  最优参数组合的 CV 评分是多少？与练习 1 中的 CV 评分相比如何？

1.  > > 来自练习 1，

    1.  计算从 1.a 中得出的样本内预测的夏普比率（有关夏普比率的定义，请参见第十四章）。

    1.  重复 1.a，这次使用`accuracy`作为评分函数。计算由超参数调整得出的样本内预测。

    1.  哪种评分方法导致更高的（样本内）夏普比率？

1.  > > 来自练习 2，

    1.  计算从 2.a 中得出的样本内预测的夏普比率。

    1.  重复第 2.a 点，这次用 `accuracy` 作为评分函数。计算基于超调参数的样本内预测。

    1.  什么评分方法会导致更高的（样本内）Sharpe 比率？

1.  > > 阅读日志损失的定义，*L* [*Y* , *P*]。

    1.  为什么评分函数 `neg_log_loss` 被定义为负日志损失，− *L* [*Y* , *P*]？

    1.  最大化日志损失而不是负日志损失的结果会是什么？

1.  > > 考虑一种投资策略，无论预测的置信度如何，均等地调整赌注。在这种情况下，进行超参数调整时，更合适的评分函数是准确性还是交叉熵损失？

**参考文献**

1.  Bergstra, J., R. Bardenet, Y. Bengio 和 B. Kegl (2011): “超参数优化的算法。” *神经信息处理系统进展*，页 2546–2554。

1.  Bergstra, J. 和 Y. Bengio (2012): “超参数优化的随机搜索。” *机器学习研究期刊*，第 13 卷，页 281–305。

**参考书目**

1.  Chapelle, O., V. Vapnik, O. Bousquet 和 S. Mukherjee (2002): “为支持向量机选择多个参数。” *机器学习*，第 46 卷，页 131–159。

1.  Chuong, B., C. Foo 和 A. Ng (2008): “对数线性模型的高效多超参数学习。” *神经信息处理系统进展*，第 20 卷。可在 [`ai.stanford.edu/∼chuongdo/papers/learn_reg.pdf`](http://ai.stanford.edu/~chuongdo/papers/learn_reg.pdf) 查阅。

1.  Gorissen, D., K. Crombecq, I. Couckuyt, P. Demeester 和 T. Dhaene (2010): “用于计算机设计的替代建模和自适应采样工具箱。” *机器学习研究期刊*，第 11 卷，页 2051–2055。

1.  Hsu, C., C. Chang 和 C. Lin (2010): “支持向量分类的实用指南。” 技术报告，国立台湾大学。

1.  Hutter, F., H. Hoos 和 K. Leyton-Brown (2011): “通用算法配置的顺序模型优化。” 第五届国际学习与智能优化会议论文集，页 507–523。

1.  Larsen, J., L. Hansen, C. Svarer 和 M. Ohlsson (1996): “神经网络的设计与正则化：验证集的最佳使用。” 1996 年 IEEE 信号处理学会研讨会论文集。

1.  Maclaurin, D., D. Duvenaud 和 R. Adams (2015): “通过可逆学习进行基于梯度的超参数优化。” 工作论文。可在 [`arxiv.org/abs/1502.03492`](https://arxiv.org/abs/1502.03492) 查阅。

1.  Martinez-Cantin, R. (2014): “BayesOpt：用于非线性优化、实验设计和赌博的贝叶斯优化库。” *机器学习研究期刊*，第 15 卷，页 3915–3919。

**注释**

^(1)     [`scikit-learn.org/stable/modules/metrics.html.`](http://scikit-learn.org/stable/modules/metrics.html.)

^(2)     [`scikit-learn.org/stable/auto_examples/svm/plot_rbf_parameters.html.`](http://scikit-learn.org/stable/auto_examples/svm/plot_rbf_parameters.html.)

^(3)     [`scikit-learn.org/stable/modules/model_evaluation.html#log-loss`](http://scikit-learn.org/stable/modules/model_evaluation.html#log-loss) .


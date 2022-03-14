---
title: "ML 1: 基础"
categories: 
- Programming
- ML
tags:
- Programming
- ML
language: zh-CN
katex: true
---

<div>

$\gdef\vect{\boldsymbol} \gdef\sspace{\mathcal} \gdef\P{\mathbb{P}} \gdef\ind#1{\mathbf{1} \\{ #1 \\}} \gdef\E{\mathbb{E}} \gdef\Var{\mathrm{Var}} \gdef\vx{\vect x}$

</div>

## 数学符号解释

- $x$: 标量
- $\vect x$: 向量
- $\vect X$: 矩阵
- $\sspace X$: 一个集合，一般表示输入输出空间
- $\R$: 实数集
- $\N$: 自然数集
- $\E$: 数学期望
- $\Var$: 方差

## 甚么是机器学习

机器学习本质是预测在一个未知的函数上某个输入的输出。

- 输入：$\vect x \in \sspace X$，在入门时一般假设 $\sspace X = \R^d$。
- 输出：$y \in \sspace Y$
- 学习目标：一个函数 $f: \sspace X \to \sspace Y$。一般需要该函数是可测的。

## 基础

- 数据：$(\vect x_1, y_1), (\vect x_2, y_2), \dots \in \sspace{X} \times \sspace{Y}$，其中 $y_i$ 称为**标签** (label)
- 假设：存在一个（相对简单的）函数 $f^*: \sspace{X} \to \sspace{Y}$ 使得对大多数 $i$ 而言，$f^*(\vect x_i) = y_i$
- 学习任务：给定 $n$ 个总体中的数据，需要找到一个近似函数 $\hat f \approx f^*$.
- 目标：$\hat f$ 能给出最准确的对于还没有观测到的样本的预测

一个十分合理的 $\hat f$ 实际是对于观测到的数据 $(\vect x_i, y_i)$，$\hat f(\vect x_i) = f(y_i)$；对于其它数据，返回随机值。然而，这个函数是没有意义的，因为这对我们的目标根本没有价值。换而言之，我们的目标事实上是去**通用化** (generalize) 这个函数，使得它对任意数据都能有准确的预测。

观测到的数据叫做已做标签的**训练数据** (labeled training data)，$\hat f$ 叫做**分类器** (classifier)。在测试阶段，未做标签的用于测试的数据叫做**测试数据** (test data)，最终通过分类器获得对于测试数据的**预测** (prediction)。

这种学习方式叫做**监督学习** (supervised learning)。

对于非监督学习，

- 数据：$\vect x_i \in \sspace X$
- 假设：在 $\sspace X$ 中存在一个潜在的规律或结构
- 学习任务：从 $n$ 个样本中发现规律
- 目标：使用发现的规律，给出对数据的总结

## 监督学习

我们来看一个统计建模的方法。

假设我们现在有从**同一个且潜在的分布**中抽取的**独立**样本 $(\vect x_i, y_i), i \in \\{ 1, 2, ..., n \\}$（称为 i.i.d. 假设）。称这个分布为 $\mathscr D (\sspace X \times \sspace Y)$，有 $(\vect x_i, y_i) \sim \mathscr D$。现在，令 $\sspace F$ 为模型的集合，我们需要从 $\sspace F$ 中选出一个 $\hat f$ 使得对于训练集，它给出的标签最一致。选出 $\hat f$ 的统计方法有：

- 极大似然 (maximum likelihood)（最能拟合数据）
- 最大后验 (maximum a posteriori)（最能拟合数据，但需要有先验假设）
- 最优损失 (loss) 标准（最能分辨标签）

### 极大似然估计 (MLE)

我们先忽略标签。给定一些 i.i.d. 数据 $\vect x_i \in \sspace X$，并假设我们有一个模型集合 $\sspace P = \\{ p_\theta \ | \ \theta \in \Theta \\}$（即，每一个模型 $p$ 能用一系列参数 $\theta$ 表示）。举例而言，如果是一个正态分布，那我们的 $\Theta = \R \times \R^+$，因为参数是 $\theta = (\mu, \sigma^2)$。对正态分布而言，模型是一个从实数数据到概率密度的函数 $p_\theta: \R \to \R$，即它的 PDF $p_\theta(x) = \phi(x)$。我们是在将 $\Theta$ 与 $\mathscr D$ 联系起来。

给定这些条件，我们的目标是找到参数设置 $\theta$ 使得这个模型**最能**产生给定的数据。我们能用似然估计来找到最优模型。

定义似然函数为 $$\begin{align*} \mathcal L (\theta|X) &:= \P(X|\theta) = \P(\vect x_1, \dots, \vect x_n|\theta) \\\\ &\overset{\text{\tiny i.i.d.}}{=} \prod_{i=1}^n \P(\vect x_i|\theta) = \prod_{i=1}^n p_\theta(\vect x_i). \end{align*}$$ 似然函数表示了如果我们选择模型 $p_\theta$，那有多大的概率能出现这些数据 $X$。所以，我们需要选择能最大化 $\mathcal L(\theta|X)$ 的 $\theta$，即 $ \theta = \argmax_\theta \mathcal L$。这个 $\theta$ 是一个估计，称为**最大似然估计** (MLE)。

<div class="success">

> 例 1：假设有身高数据 $x_i$，假设模型类为在 $\R$ 中的正态分布模型 $$p_{ \\{ \mu, \sigma^2 \\} } (x) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp \left ( -\frac{(x - \mu)^2}{2\sigma^2} \right ),$$ 我们的最大似然估计是 $\argmax_\theta \mathcal L(\theta | X)$。

</div>

有一些方法能能简化 MLE 的计算。首先，我们能看出 $\argmax_\theta \mathcal L = \argmax_\theta \log \mathcal L$（因为自然对数函数是严格单调递增的）。至于为什么选择自然对数函数，是因为 $\mathcal L$ 是由**积**组成的，而使用对数函数可以将其转化为**和**。其次，想要找到函数的极值，我们只需要找到一些驻点，即导数为 0 的点。在这里，我们就看到了转化为和的意义，即简化求导过程。

<div class="success">

> 例 1（续）：我们现在可以计算正态分布的 MLE：$$\argmax_\theta \mathcal L(\theta|X) = \argmax_{\mu, \sigma^2} \sum_{i=1}^n \left [ -\frac{1}{2}\log(2\pi \sigma^2) - \frac{(x_i - \mu)^2}{2\sigma^2} \right ].$$ 令求和的那一部分为 $g_i(\mu, \sigma^2)$，那么我们如果想要对 $\mu$ 求最大值，则 $\nabla_\mu \left ( \sum_{i=1}^n g_i(\mu, \sigma^2) \right ) = 0$。我们会得到 $\widehat \mu_\mathrm{ML} = \frac{1}{n} \sum_{i=1}^n x_i$。我们发现这个估计很合理，就是样本的均值。对方差进行一样的计算，我们发现 $\widehat \sigma^2_\mathrm{ML} = \frac{1}{n} \sum_{i=1}^n (x_i - \mu)^2$。

</div>

### 多元正态分布

我们对一元正态分布很熟悉，但是在机器学习中，大多数数据都是向量，即多元的。于是，我们的概率密度函数会变成 $p: \R^d \to \R$。这里，$\sspace X = \R^d$。于是，期望 $\vect \mu$ 也会有 $d$ 维，而方差现在变成了一个协方差矩阵 $\vect \Sigma$（因为有更多的空间关系，包括大小，方向等）。我们定义多元正态分布密度函数为 $$p_{\\{\vect \mu, \vect \Sigma \\}}(\vect x) = \frac{1}{\sqrt{(2\pi)^d \det(\vect \Sigma)}} \exp \left ( -\frac{1}{2}(\vect x - \vect \mu)^\top \vect \Sigma^{-1} (\vect x - \vect \mu) \right ),$$ 其中 $\Sigma$ 是正定的（对于任意 $\vect a$，$\vect a^\top \vect \Sigma \vect a > 0$）。

### 从 MLE 到分类

我们能用 MLE 进行分类吗？首先，我们需要同意分类器 $\hat f(\vect x) = \argmax_y \P(Y = y | X = \vect x)$ 是**最**好的分类器。我们能发现 $\hat f: \sspace X \to \sspace Y$，则 $\hat f$ 是一个分类器。然后使用贝叶斯法则，有 $$\hat f(\vect x) = \argmax_y \frac{\P(X = \vect x|Y = y) \P(Y = y)}{\P(X = \vect x)} = \argmax_y \P(X = \vect x|Y = y) \P(Y = y),$$ 其中第二步是因为 $\P(X = x)$ 与 $y$ 无关。我们将 $\P(X = \vect x|Y = y)$ 称为**类条件模型** (class conditional probability model)，$\P(Y = y)$ 称为**类先验** (class prior)。我们将这个分类器称为**贝叶斯分类器** (Bayes classifier)。

类先验是我们观测到的标签是 $y$ 的数据的占比。我们可以通过找到一个分布后计算参数的 MLE，然后获得一个分布的估计 $\widehat \P(Y = y)$。这个估计事实上就是标签为 $y$ 的数据出现的概率。相似地，我们也对类条件进行建模预估。我们对每一个标签/分类分别使用概率模型并用 MLE 找到参数的估计。

<div class="success">

> 例 2：假设我们现在需要基于身高体重数据学习一个分辨男 (M) 女 (F) 的分类器。所以，$\sspace X = \R^2, \sspace Y = \{M, F\}$。我们的分类器是 $$\hat f (\vect x) = \argmax_{y \in \sspace Y} \P(X = \vect x | Y = y) \P(Y = y).$$ 使用有标签的训练集，我们可以学习这些参数：$\P(Y = M) \approx$ 训练集标签为 M 的数据占比，$\P(Y = F) \approx$ 训练集中标签为 F 的数据占比。对于类条件，$\P(X|Y = M) = p(X; \theta(M)), \P(X|Y = F) = p(X; \theta(F))$，其中 $\theta(x)$ 是只适用标签为 $x$ 的数据的 MLE 估计。

</div>

由此，我们创造出了我们的第一个分类器！但是为什么是这个函数 $\argmax_y \P(Y|X)$ 呢？

### 贝叶斯分类器

假设有两个分类器 $f, g: \sspace X \to \sspace Y$。对于同一个 $(\vect x, y) \sim \mathscr D(\sspace X \times \sspace Y)$，我们想知道 $f(\vect x)$ 和 $g(\vect x)$ 是否都能等于真实标签 $y$。

<div class="primary">

> 定义：**指示函数** (indicator function)
> 指示函数 $\ind{x}$ 当满足条件 $x$ 时值为 1，否则为 0。

</div>

我们可以发现给定 $(\vect x, y) \sim \mathscr D$，准确率 $\P_{(\vect x, y)} (f(\vect x) = y) = \E_{(\vect x, y)} [\ind{ f(\vect x_i) = y_i}]$。

假设 $\sspace Y = \\{0, 1\\}$ 且 $f(\vect x) = \argmax_y \P(Y = y|X = \vect x)$ 为贝叶斯分类器，并假设 $g(\vect x)$ 为任意分类器。我们有以下定理：$$ \P_{(\vect x, y)} (g(\vect x) = y) \leq \P_{(\vect x, y)} (f(\vect x) = y),$$ 即贝叶斯分类器是最优的。

首先，可以发现对于任意的分类器 $h$，$$\begin{align*}\P(h(\vect x) = y | X = \vect x) &= \P(h(\vect x) = 0, Y = 0|X = \vect x) + \P(h(\vect x) = 1, Y = 1|X = \vect x) \\\\ &= \ind{h(\vect x) = 1} \P(Y = 1|X = \vect x) + \ind{h(\vect x) = 0} \P(Y = 0|X = \vect x) \end{align*}$$ 令 $\eta(\vect x) = \P(Y = 1|X = \vect x)$，则上式等于 $\ind{h(\vect x) = 1} \eta(\vect x) + \ind{h(\vect x) = 0} (1 - \eta(\vect x))$。于是有 $$\begin{equation*} \begin{split} \P(f & (\vx) = y|X = \vx) - \P(g(\vx) = y|X = \vx) \\\\ &= \eta(\vx)\left ( \ind{f(\vx) = 1} - \ind{g(\vx) = 1} \right ) + (1 - \eta(\vx)) \left ( \ind{f(\vx) = 0} - \ind{g(\vx) = 0} \right ) \\\\ &= (2\eta(\vx) - 1) \left ( \ind{f(\vx) = 1} - \ind{g(\vx) = 1} \right ) \\\\ &\geq 0 \end{split} \end{equation*}$$ 最后的非负可以通过分类讨论得出。然后对上式进行对 $\vx$ 的积分，我们就能得到非条件性的结论，即 $\P(f(\vx) = y) \geq \P(g(\vx) = y)$。

<div class="primary">

> 这是因为 $$\E_{X, Y}[\alpha(x, y)] = \E_X \left [ \E_{Y|X} [\alpha(x, y) | X = x] \right ],$$ 并且这里 $\P(f(\vx) = y) = \E_{X, Y} [\ind{f(\vx) = y}]$。

</div>

那既然贝叶斯分类器是最佳的，它能用来解决所有分类问题了吗？答案是否定的，因为现实中的数据不可能来源于常规的分布，例如正态分布与指数分布。数据的分布可以有非常多隐藏参数，所以我们需要非参数密度估计 (nonparametric density estimation)。假设有 $n$ 个样本，参数有 $d$ 维，那么参数估计 $\widehat P_n$ 对非参分布 $p$ 的误差是 $$\int_{\R^d} (p(\vx) - \widehat P_n (\vx))^2 dx \leq n^{-\frac{4}{4+d}}.$$

### 朴素贝叶斯分类器

朴素贝叶斯分类器 (Naive Bayes classifier) 需要一个假设：给定标签，每一个属性/特征之间相互独立。于是，$$\begin{align*} \hat f(\vx) &= \argmax_y \P(X = \vx | Y = y) \P(Y = y) \\\\ &= \argmax_{y} \prod_{j=1}^d \P(X^{(j)} = \vx^{(j)}|Y = y) \P(Y = y) \end{align*}$$ 朴素贝叶斯是非常简单的模型，但是它可能不能准确描述属性之间的关系，导致预测不准确。

### 分类器的评判标准

给定分类器 $f$，如何评判它的好坏？我们需要计算 $\P(f(\vx) = y) = \E [\ind{f(\vx) = y}]$。然而，我们不知道潜在的分布，无法计算这个期望。我们可以用训练集的均值计算：$\frac{1}{n} \sum_{i=1}^n \ind{f(\vx_i) = y_i}$，但是它不是无偏估计，因为训练集是用于构建分类器 $f$ 的。我们需要使用不在训练集中的数据（即测试集）进行评判。

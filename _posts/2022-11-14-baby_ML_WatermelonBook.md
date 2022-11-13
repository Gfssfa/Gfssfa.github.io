---
layout:     post
title:      "机器学习基础"
subtitle:   ""
date:       2022-11-14 2:00:00
author:     "Gfssfa"
header-img: "img/bg-post-2022-11-14.jpg"
catalog: true
mathjax: true
tags:
    - baby系列
    - 西瓜书
    - 机器学习
    - 笔记

---

状态：更新中

参考书籍：机器学习-周志华（西瓜书），南瓜书

参考教学资源：学堂在线-机器学习初步（2022年秋）

## ch00 前言

> zzh推荐西瓜书读两到三遍：

> 第一遍一个月左右的时间，侧重思想，机器学习涉及的问题，其中第一二章的数学公式的推导初读可以跳一跳

> 第二遍几个月后

> 第三遍一年甚至几年后有了相当的机器学习的经历再读

课程学习需要有一定的数理基础

只是入门书籍课程:train:



## ch03 线性模型

### 3.1基本形式：

线性模型（linear model）

向量形式：

$f(\boldsymbol{x})=\boldsymbol{w}^{\mathrm{T}} \boldsymbol{x}+b$

特点：

* 形式简单，易于建模
* 基本
* 可解释性（comprehensibility）好

### 3.2 线性回归

线性回归形式：

$f\left(x_i\right)=w x_i+b \text { 使得 } f\left(x_i\right) \simeq y_i$

==对离散属性的处理：==
对于离散属性，若属性之存在“序”（order）关系，可通过连续化将其转化为连续值。
若属性值间不存在序关系，假定有k个属性值，则通常转化为k维向量。例如属性“瓜类”的取值“西瓜”“南瓜”“黄瓜”，可以转化成`(0,0,1)`,`(0,1,0)`,`(1,0,0)`



==最小二乘法：==
基于均方误差最小化来进行模型求解的方法

对应欧式距离。线性回归中，最小二乘法试图找到一条直线，使所有样本到直线上的欧氏距离之和最小。

$\begin{aligned}
\left(w^*, b^*\right) &=\underset{(w, b)}{\arg \min } \sum_{i=1}^m\left(f\left(x_i\right)-y_i\right)^2 \\
&=\underset{(w, b)}{\arg \min } \sum_{i=1}^m\left(y_i-w x_i-b\right)^2
\end{aligned}$

对$w$和$b$求导：

$\frac{\partial E_{(w, b)}}{\partial w}=2\left(w \sum_{i=1}^m x_i^2-\sum_{i=1}^m\left(y_i-b\right) x_i\right)$

$\frac{\partial E_{(w, b)}}{\partial b}=2\left(m b-\sum_{i=1}^m\left(y_i-w x_i\right)\right)$

然后令等于零得到闭式解（closed- form，解析解）

$w=\frac{\sum_{i=1}^m y_i\left(x_i-\bar{x}\right)}{\sum_{i=1}^m x_i^2-\frac{1}{m}\left(\sum_{i=1}^m x_i\right)^2}$

$b=\frac{1}{m} \sum_{i=1}^m\left(y_i-w x_i\right)$



==多元线性回归（multivariate linear regression）== 

公式推导 公式3.9-3.12

样本有$d$个属性描述，先对$w$,$b$扩充：

$\mathbf{X}=\left(\begin{array}{ccccc}x_{11} & x_{12} & \cdots & x_{1 d} & 1 \\ x_{21} & x_{22} & \cdots & x_{2 d} & 1 \\ \vdots & \vdots & \ddots & \vdots & \vdots \\ x_{m 1} & x_{m 2} & \cdots & x_{m d} & 1\end{array}\right)=\left(\begin{array}{cc}\boldsymbol{x}_1^{\mathrm{T}} & 1 \\ \boldsymbol{x}_2^{\mathrm{T}} & 1 \\ \vdots & \vdots \\ \boldsymbol{x}_m^{\mathrm{T}} & 1\end{array}\right) \quad \boldsymbol{y}=\left(y_1 ; y_2 ; \ldots ; y_m\right)$

然后就有：

$\hat{\boldsymbol{w}}^*=\underset{\hat{\boldsymbol{w}}}{\arg \min }(\boldsymbol{y}-\mathbf{X} \hat{\boldsymbol{w}})^{\mathrm{T}}(\boldsymbol{y}-\mathbf{X} \hat{\boldsymbol{w}})$

令$E_{\hat{\boldsymbol{w}}}=(\boldsymbol{y}-\mathbf{X} \hat{\boldsymbol{w}})^{\mathrm{T}}(\boldsymbol{y}-\mathbf{X} \hat{\boldsymbol{w}})$对$\hat{\boldsymbol{w}}$求导：

$\frac{\partial E_{\hat{\boldsymbol{w}}}}{\partial \hat{\boldsymbol{w}}}=2 \mathbf{X}^{\mathrm{T}}(\mathbf{X} \hat{\boldsymbol{w}}-\boldsymbol{y})$

令上式令可得$\hat{\boldsymbol{w}}$最优解的闭式解，但是涉及==矩阵逆==：

当$\mathbf{X}^{\mathrm{T}} \mathbf{X}$满秩或者正定：$\hat{\boldsymbol{w}}^*=\left(\mathbf{X}^{\mathrm{T}} \mathbf{X}\right)^{-1} \mathbf{X}^{\mathrm{T}} \boldsymbol{y}$

最终学到的多元线性回归模型为：$f\left(\hat{\boldsymbol{x}}_i\right)=\hat{\boldsymbol{x}}_i^{\mathrm{T}}\left(\mathbf{X}^{\mathrm{T}} \mathbf{X}\right)^{-1} \mathbf{X}^{\mathrm{T}} \boldsymbol{y}$

而当$\mathbf{X}^{\mathrm{T}} \mathbf{X}$不满秩，即==许多任务中大量的变量，其数目甚至超过样例数，导致$\mathbf{X}$列数大于行数==，此时可以解出多个$\hat{\boldsymbol{w}}$，具体是哪个由学习算法的归纳偏好决定。常见方法是引入正则化。



对数线性回归（log-linear regression）：$\ln y=\boldsymbol{w}^{\mathrm{T}} \boldsymbol{x}+b$

==广义（generalized）线性模型：==

$y=g^{-1}\left(\boldsymbol{w}^{\mathrm{T}} \boldsymbol{x}+b\right)$

$g(\cdot)$称之为==联系函数==，单调可微



### 3.3 对数几率回归

如何做分类任务：找一个单调可微函数讲分类任务的真实标记$y$与线性回归模型的预测值联系起来

从二分类到多分类

单位阶跃函数（unit-step function）：数学性质差

所以要找替代函数，替代函数性质：单调可微，任意阶可导
sigmoid函数：S型函数  对数几率（对率）函数是其中的一种：

$y=\frac{1}{1+e^{-z}}$

对数几率回归模型 注意：对数几率回归是一种==分类==学习方法

将$y$看做类后验概率估计$p(y=1 \mid \boldsymbol{x})$

$\ln \frac{p(y=1 \mid \boldsymbol{x})}{p(y=0 \mid \boldsymbol{x})}=\boldsymbol{w}^{\mathrm{T}} \boldsymbol{x}+b$

可以用对率回归模型用极大似然法（maximum likelihood method）来估计$w$，$b$：

最大化对数似然函数：$\ell(\boldsymbol{w}, b)=\sum_{i=1}^m \ln p\left(y_i \mid \boldsymbol{x}_i ; \boldsymbol{w}, b\right)$

> 极大似然的想法：

> $max {P(真的是正类)P(预测是正类)+P(真的是负类)P(预测是负类)}$

> 取对数是为了缓解浮点数下溢出

$\boldsymbol{w}^{\mathrm{T}} \boldsymbol{x}+b$ 可简写为 $\boldsymbol{\beta}^{\mathrm{T}} \hat{\boldsymbol{x}}$

$p_1(\hat{\boldsymbol{x}} ; \boldsymbol{\beta})=p(y=1 \mid \hat{\boldsymbol{x}} ; \boldsymbol{\beta})$

$p_0(\hat{\boldsymbol{x}} ; \boldsymbol{\beta})=p(y=0 \mid \hat{\boldsymbol{x}} ; \boldsymbol{\beta})=1-p_1(\hat{\boldsymbol{x}} ; \boldsymbol{\beta})$

则最大化对数似然函数$\ell(\boldsymbol{w}, b)$中的似然项可以重写为：

$p\left(y_i \mid \boldsymbol{x}_i ; \boldsymbol{w}, b\right)=y_i p_1\left(\hat{\boldsymbol{x}}_i ; \boldsymbol{\beta}\right)+\left(1-y_i\right) p_0\left(\hat{\boldsymbol{x}}_i ; \boldsymbol{\beta}\right)$

最大化$\ell(\boldsymbol{w}, b)$等价于最小化：

$\ell(\boldsymbol{\beta})=\sum_{i=1}^m\left(-y_i \boldsymbol{\beta}^{\mathrm{T}} \hat{\boldsymbol{x}}_i+\ln \left(1+e^{\boldsymbol{\beta}^{\mathrm{T}} \hat{\boldsymbol{x}}_i}\right)\right)$

这式是关于$\beta$的高阶可导连续函数，然后就可以利用凸优化理论中的方法例如梯度下降算法，牛顿法等等，可以求最优解：

$\boldsymbol{\beta}^*=\underset{\boldsymbol{\beta}}{\arg \min \ell(\boldsymbol{\beta})}$

注意点：

*  凸函数$\ln \frac{1+e^{f(x)}}{e^y}$能用直接求导令其为零得到最优解
* $w=w_{i y}+\Delta w$迭代解法，易并行化



### 3.6 类别不平衡问题

理想/假设：训练集是真实样本总体的无偏采样，因此观测几率代表真实几率

再缩放（rescaling）:

$m^{+}$表示正例数目，$m^{-}$表示反例数目

原来$m^{+}=m^{-}$ ，那么若 $\frac{y}{1-y}>1$ 则预测为正例，

现在$\frac{y^{\prime}}{1-y^{\prime}}=\frac{y}{1-y} \times \frac{m^{-}}{m^{+}}$

==缺陷==：未必能有效地给予选联机观测几率来范推断出真实几率

“再缩放”是“代价敏感学习”（cost-sensitive learning）的基础

三种方法：（假设正例偏少）

* 欠采样（undersampling）：去除一些反例，使正反例数目接近然后学习

注意随意丢弃反例可能会确实重要信息。 

* 过采样（oversampling）：增加一些正例，使正反例数目接近然后学习

注意不能简单重复采样，否则会导致严重的过拟合。SMOTE（Chawla et al.）算法通过对正例插值产生正例

* 阈值移动（threshold-moving）：直接基于原始训练集进行学习，但是在用训练好的分类器进行预测是，将再缩放嵌入到决策过程中

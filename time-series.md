---
description: 时间序列数据上的机器学习方法
---

# 时间序列（Time Series）

## 时间序列：[WIKI](https://zh.wikipedia.org/wiki/%E6%99%82%E9%96%93%E5%BA%8F%E5%88%97)

**时间序列**（英语：time series）是一组按照时间发生先后顺序进行排列的数据点[序列](https://zh.wikipedia.org/wiki/%E5%BA%8F%E5%88%97)。通常一组时间序列的时间间隔为一恒定值（如1秒，5分钟，12小时，7天，1年），因此时间序列可以作为离散时间数据进行分析处理。

时间序列内容非常丰富，内容很多也很难；算是大学时比较难的几门数学课之一，不过这里不打算详细介绍这些冗长枯燥的理论，而是打算以一个例子介绍时间序列的建模

### 时间系列数据

说起时间序列的数据，最大名鼎鼎也最令人魂牵梦绕的数据就是量化交易的数据（股票、期货、数字货币等）

![](.gitbook/assets/image.png)

![](.gitbook/assets/image%20%281%29.png)

接下来的会利用上面的数据建立时间序列模型，第一步先从最简单的线性模型（AR，MA，ARMA）开始，下一节的主要目的是使用python实现ARMA和ARCH模型，本节的原理部分主要摘抄自[这里](https://zhuanlan.zhihu.com/p/21962996)

## 线性模型

很多时间序列具有线性性，即是线性时间序列，相应的有很多线性时间序列模型

### **自回归\(AR\)模型**

这里不做过多的平稳性等讨论，纯粹从技术的角度讨论其实现

#### 一阶自回归模型AR\(1\)

![](.gitbook/assets/image%20%283%29.png)

其中$${a_t}$$是**白噪声序列**

#### $$p$$阶自回归模型AR\(p\)

![](.gitbook/assets/image%20%2810%29.png)

关于AR模型的定阶也是一个重要的问题，比价常用的方法有：

* 第一种：利用**偏相关函数\(Partial Auto Correlation Function,PACF\)**
* 第二种：利用**信息准则函数**
  * AIC = -2 ln\(L\) + 2 k \# 中文名字：赤池信息量 akaike information criterion
  * BIC = -2 ln\(L\) + ln\(n\)\*k \# 中文名字：贝叶斯信息量 bayesian information criterion
  * HQ = -2 ln\(L\) + ln\(ln\(n\)\)\*k \# hannan-quinn criterion

但是这里不对定阶做详细讨论，**原因是这些都只是准则，实际使用还是要从数据出**

### **MA模型**

MA模型和AR大同小异，它并非是历史时序值的线性组合而是历史白噪声的线性组合。与AR最大的不同之处在于，AR模型中历史白噪声的影响是间接影响当前预测值的（通过影响历史时序值）。  


## ARCH模型

### ARCH的基本原理

在传统计量经济学模型中，干扰项的方差被假设为常数。但是许多经济时间序列呈现出波动的集聚性，在这种情况下假设方差为常数是不恰当的。

ARCH模型将当前一切可利用信息作为条件，并采用某种自回归形式来刻划方差的变异，对于一个时间序列而言，在不同时刻可利用的信息不同，而相应的条件方差也不同，**利用ARCH 模型，可以刻划出随时间而变异的条件方差**。

#### ARCH模型思想

* 资产收益率序列的扰动 {![a\_{t} ](http://www.zhihu.com/equation?tex=a_%7Bt%7D+)} 是序列不相关的，但是不独立。
* {![a\_{t} ](http://www.zhihu.com/equation?tex=a_%7Bt%7D+)}的不独立性可以用其延迟值的简单二次函数来描述。具体而言，一个ARCH\(m\)模型为：

![](.gitbook/assets/image%20%2821%29.png)

* 其中，{![\varepsilon \_{t} ](http://www.zhihu.com/equation?tex=%5Cvarepsilon+_%7Bt%7D+)}为 **均值为0，方差为1的独立同分布（iid）随机变量序列。**通常假定其服从标准正态分布。![\sigma \_{t}^{2} ](http://www.zhihu.com/equation?tex=%5Csigma+_%7Bt%7D%5E%7B2%7D+)为条件异方差。（注意区分：$$a_{t}$$和$$\alpha_t$$）

#### ARCH模型效应

从上面模型的结构看，大的过去的平方“扰动”会导致信息![a\_{t} ](http://www.zhihu.com/equation?tex=a_%7Bt%7D+)大的条件异方差。从而$$a_t$$有取绝对值较大的值的倾向。这意味着：**在ARCH的框架下，大的"扰动"会倾向于紧接着出现另一个大的"扰动"。这与波动率聚集的现象相似。**

所谓ARCH模型效应，也就是**条件异方差序列的序列相关性**


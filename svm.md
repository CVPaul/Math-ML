---
description: 支持向量机
---

# 支持向量机（Support Vector Machine）

## libsvm在MATLAB中的使用

### 系统环境

* Windows 10， Matlab 2018b
* 参考链接：[https://zhuanlan.zhihu.com/p/30485050](https://zhuanlan.zhihu.com/p/30485050), [https://blog.csdn.net/u012824097/article/details/61195288](https://blog.csdn.net/u012824097/article/details/61195288)

### 实验环境搭建

该小节逐步介绍libsvm的环境搭建过程

#### Step 1: libsvm

 在支持向量机的众多程序包中，最著名的当属台湾大学林智仁老师开发的 libsvm 了，由于libsvm是C++实现的是的，所以需要安装C++编译环境（TDM-GCC，下载地址：[http://tdm-gcc.tdragon.net/download](http://tdm-gcc.tdragon.net/download)，也可以使用VS的环境：mex -setup c++\)，这里直接使用了mex：

![](.gitbook/assets/image%20%285%29.png)

接下来下载libsvm（[https://www.csie.ntu.edu.tw/~cjlin/libsvm/](https://www.csie.ntu.edu.tw/~cjlin/libsvm/)，[https://github.com/cjlin1/libsvm](https://github.com/cjlin1/libsvm)）到任意目录，推荐目录：matlab根目录\MATLAB\R2018b\toolbox： 下载后解压：得到一个libsvm-master文件夹，将其所在的位置添加到MATLAB的路径中，并将里面的Windows文件夹添加到MATLAB的路径中，matlab添加路径的方式：【设置路径】—【添加并包含子文件夹】选择上述 libsvm-master 文件夹：

![](.gitbook/assets/image%20%288%29.png)

 Matlab 当前路径切换到 libsvm-3.22\matlab 下：

![](.gitbook/assets/image%20%2810%29.png)

输入make命令，生成mex文件

![](.gitbook/assets/image%20%289%29.png)

![](.gitbook/assets/image%20%284%29.png)

将上步生成的 4 个 .mexw64 文件，拷贝粘贴到 libsvm-master\windows 路径下  
替换原有文件，接下来就可以用了，输入svmtrain测试：

![](.gitbook/assets/image%20%2811%29.png)

上面表示成功了，在libsvm的根目录下有个heart\_scale的数据文件，切换在该目录下依次输入如下，命令

```text
[heart_scale_label,heart_scale_inst]=libsvmread('heart_scale');
model = svmtrain(heart_scale_label,heart_scale_inst, '-c 1 -g 0.07');
[predict_label, accuracy, dec_values] =svmpredict(heart_scale_label,heart_scale_inst, model);
```

### 实验：MINIST分类

* 使用支持向量机对 mnists 数据集进行二分类实验，记录实验数据组成，训练数据，交叉校验数据集，测试数据集的大小。实验分类的错误率。
* 对 minists 数据集的 0 到 9 个手写体数字，两两放在一起，作为二分类数据源，例如 0 和 9,2 和 7 等。 
* 介绍 SVM 的原理，求解算法用MATLAB和libsvm做。

### 试验结果

由于考虑2分类问题，所以这里有$$10\times(10-1)/2=45$$个模型的结果，结果太多下面仅展示两个，更多详细的信息附到文件尾部共查阅（或者查看试验记录experiment\_records.txt）

![mnist&#x4E0A;class-0 VS class1&#x7684;&#x7ED3;&#x679C;](.gitbook/assets/image.png)

#### 小结如下：

* mnist数据集上，0 VS 1的二分类问题（SVM）,训练集大小:12665\(其中0的样本数5923,1的样本数6742\),测试集大小:2115\(其中0的样本数980,1的样本数1135\)
* 0 VS 1的二分类交叉验证选取的最终参数：C=0.031250，分类准确度为99.91%,错误率为0.09%,每折的详细信息如上\(前几折样本数：2533,最后一折样本数：2533\)
* mnist数据集上，0 VS 1的二分类问题（SVM）,5折交叉验证选取最优参数C=0.031250,在此参数下训练模型，训练集分类错误率：0.05%,测试集分类错误率：0.05%

####  

![mnist&#x4E0A;class-0 VS class1&#x7684;&#x7ED3;&#x679C;](.gitbook/assets/image%20%281%29.png)

#### 小结如下：

* mnist数据集上，2 VS 7的二分类问题（SVM）,训练集大小:12223\(其中2的样本数5958,7的样本数6265\),测试集大小:2060\(其中2的样本数1032,7的样本数1028\)
* 2 VS 7的二分类交叉验证选取的最终参数：C=0.031250，分类准确度为98.74%,错误率为1.26%,每折的详细信息如上\(前几折样本数：2444,最后一折样本数：2447\)
* 2 VS 7的二分类交叉验证选取的最终参数：C=0.031250，分类准确度为98.74%,错误率为1.26%,每折的详细信息如上\(前几折样本数：2444,最后一折样本数：2447\)

#### 多分类问题的结果比较多，这里直接列出结论：

* 训练集：Accuracy = 96.0217% \(57613/60000\) \(classification\) 
* 测试集：Accuracy = 94.59% \(9459/10000\) \(classification\) 
* mnist数据集上多分类（SVM）,训练集分类错误率：3.98%,测试集分类错误率：5.41%

### SVM的原理

#### **用一句话解释SVM的核心思想就是：最大化分类间距，如下图所示：**

![&#x6700;&#x5927;&#x5316;&#x5206;&#x7C7B;&#x95F4;&#x8DDD;&#x793A;&#x610F;&#x56FE;](.gitbook/assets/image%20%283%29.png)

将最大化分类间距用数学形表达出来我们就得到了SVM的数学表达形式，下面一步一步介绍如何推导出该公式，这里假设两类且正样本的label=1,负样本的label=-1,并用$$n$$表示样本数，即：

$$y_{i}=\left\{ \begin{aligned} 1, &\text{for positive samples}\\ -1,&\text{for negative samples} \end{aligned}, i=1,2,...,n \right.$$

接下了假设分类面表示为：$$0=w^{T}x+b$$, 且根据基本的几何知识已知任意一点到直线/分类面的几何距离的表示为：$$\frac{|(w^{T}x+ b)|}{||w||}$$，$$(w^{T}x+ b)  $$的正负表示了在分类面的两侧，下面分情况讨论一下

#### 最大化分类间距的约束条件

* 对于**正样本**：我们已知正样本的$$y_i=1,i=1,2,...n $$, 那么我们要求，正样本被分到$$(w^{T}x+ b)\geq 0 $$的一侧，即：$$y_i(w^{T}x_i+ b) = \gamma_i, \gamma_i \geq \gamma, \gamma > 0$$
* 对于**负样本**：我们已知正样本的$$y_i=-1,i=1,2,...n $$, 那么我们要求，正样本被分到$$(w^{T}x+ b)\leq 0$$的一侧，即：$$y_i(w^{T}x_i+ b) = \gamma_i, \gamma_i \geq \gamma, \gamma > 0$$
* 正负样本最后都得到了相同的表现形式：$$y_i(w^{T}x_i+ b) = \gamma_i, \gamma_i \geq \gamma, \gamma > 0$$；约束两个类的样本在分界面的不同侧

#### 最大化分类间距的目标函数

根据前面的介绍这里的目标函数是：$$\frac{|(w^{T}x+ b)|}{||w||}$$，且约束条件要求所有的样本满足$$y_i(w^{T}x_i+ b) = \gamma_i, \gamma_i \geq \gamma, \gamma > 0$$，而最大化目标为：$$\max\arg min_{i=1,2,...n}\frac{\gamma_i}{||w||}$$等价于$$\max\frac{\gamma}{||w||}$$,故有如下的优化目标

$$\left\{  \begin{aligned} &\max\frac{\gamma}{||w||}\\ &s.t. y_{i}(w^{T}x_{i}+b）\geq \gamma, i=1,2,...,n  \end{aligned}  \right.$$

一般化的我们令$$\gamma=1$$（这不会影响目标的优化），于是有：

$$
\left\{ 
\begin{aligned}
&\max\frac{1.0}{||w||}\\
&s.t. y_{i}(w^{T}x_{i}+b）\geq 1.0, i=1,2,...,n

\end{aligned} 
\right.
$$




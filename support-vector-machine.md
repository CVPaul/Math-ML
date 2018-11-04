---
description: 支持向量机
---

# Support Vector Machine

## libsvm在MATLAB中的使用

### 系统环境

* Windows 10， Matlab 2018b
* 参考链接：[https://zhuanlan.zhihu.com/p/30485050](https://zhuanlan.zhihu.com/p/30485050), [https://blog.csdn.net/u012824097/article/details/61195288](https://blog.csdn.net/u012824097/article/details/61195288)

### 实验环境搭建

该小节逐步介绍libsvm的环境搭建过程

#### Step 1: libsvm

 在支持向量机的众多程序包中，最著名的当属台湾大学林智仁老师开发的 libsvm 了，由于libsvm是C++实现的是的，所以需要安装C++编译环境（TDM-GCC，下载地址：[http://tdm-gcc.tdragon.net/download](http://tdm-gcc.tdragon.net/download)，也可以使用VS的环境：mex -setup c++\)，这里直接使用了mex：

![](.gitbook/assets/image.png)

接下来下载libsvm（[https://www.csie.ntu.edu.tw/~cjlin/libsvm/](https://www.csie.ntu.edu.tw/~cjlin/libsvm/)，[https://github.com/cjlin1/libsvm](https://github.com/cjlin1/libsvm)）到任意目录，推荐目录：matlab根目录\MATLAB\R2018b\toolbox： 下载后解压：得到一个libsvm-master文件夹，将其所在的位置添加到MATLAB的路径中，并将里面的Windows文件夹添加到MATLAB的路径中，matlab添加路径的方式：【设置路径】—【添加并包含子文件夹】选择上述 libsvm-master 文件夹：

![](.gitbook/assets/image%20%281%29.png)

 Matlab 当前路径切换到 libsvm-3.22\matlab 下：

![](.gitbook/assets/image%20%282%29.png)

输入make命令，生成mex文件

![](.gitbook/assets/image%20%284%29.png)

![](.gitbook/assets/image%20%283%29.png)

将上步生成的 4 个 .mexw64 文件，拷贝粘贴到 libsvm-master\windows 路径下  
替换原有文件，接下来就可以用了，测试：

```text
load heart_scale.mat  %加载测试数据集
model = svmtrain(heart_scale_label, heart_scale_inst, '-c 1 -g 0.07');  %训练模型
```




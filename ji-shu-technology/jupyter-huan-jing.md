---
description: 为Jupyter添加kernel，扩展，外网访问，import notebook等
---

# Jupyter环境搭建

## Kernel的添加

要在jupyter下支持不同的环境，如：Python2, Python3, Golang, Julia, R, Matlab的支持的话都需要创建对用的kernel，最近在折腾MATLAB，所以下面以添加matlab为例，简单说明一下，下面的内容只是[官网的教程](https://am111.readthedocs.io/en/latest/jmatlab_use.html)直接翻译（我在Win10+python 3.6+Matlab R2018b下测试成功）：

###  安装 Jupyter-MATLAB

* 第一步：安装[Anaconda](https://www.anaconda.com/)
* 第二步：创建一个新的环境并激活
  * ​创建: `conda create -vv -n jmatlab python=3.6 jupyter`
  * 激活：`activate jmatlab # 这里 Windows下不需要 source`
  * **后面的命令都需要在这个激活的环境下执行，现在已经激活**
* 第三步：安装matlab\_kernel:
  * `pip install matlab_kernel # 如果不成功的话加上-U选项试试`
  * `python -m matlab_kernel install`
  * `jupyter kernelspec list # 查看是否安装成功`
* 第四步：配置MATLAB（[安装用于 Python 的 MATLAB 引擎 API](https://ww2.mathworks.cn/help/matlab/matlab_external/install-the-matlab-engine-for-python.html?requestedDomain=zh)）
  * 进入MATALB安装目录：`cd "MATLAB安装目录/extern/engines/python"`
  * 执行：`python setup.py install`
* 最后启动Jupyter： `jupyter notebook`

![](../.gitbook/assets/image%20%284%29.png)

### 测试Jupyter-MATLAB

![](../.gitbook/assets/image%20%2819%29.png)

上面的运行结果是图片，没办法缩放，旋转啥的，这时候需要**%plot native**来启动MATLAB自带的窗口

![](../.gitbook/assets/image%20%2812%29.png)


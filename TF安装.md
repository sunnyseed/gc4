## 0. 环境说明

硬件：Xeon E5-1620v2 3.7g + GTX 1080Ti

系统：Windows 10 Enterprise Version >1809

NVIDIA >419.35 驱动

Visual Studio 2017 （只需要C++部分）



1、安装 Anaconda3-5.2.0-Windows-x86_64（Python 3.6.5 x64）

​	https://repo.continuum.io/archive/

​	https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/ （推荐，清华大学开源软件镜像站进行下载并配置镜像）

问题描述：在win10下安装Anaconda 5.2.0时，最后有一步是要安装VSCode，但是在联网正常的情况下提示失败。解决办法：在anaconda\pkg目录下，找到vscode_inst.py文档，第110行原为：

VSCODE_ENDPOINT = '[https://vscode-update.azurewebsites.net/api/update/{}/stable/version'.format(VSCODE_SUBDIR)](https://vscode-update.azurewebsites.net/api/update/{}/stable/version' rel=) # NOQA

修改为：

VSCODE_ENDPOINT = '[https://update.code.visualstudio.com/api/update/{}/stable/version'.format(VSCODE_SUBDIR)](https://update.code.visualstudio.com/api/update/{}/stable/version' rel=) # NOQA

2、在 anaconda prompt 中测试

pip list

python

3、[Win10 x64 + CUDA 10.0 + cuDNN v7.5 + TensorFlow GPU 1.13 安装指南](https://www.cnblogs.com/sorex/p/7615185.html)

对应版本：

https://www.tensorflow.org/install/source#linux

（1）CUDA 10.0	（据说只要安装第一项，未试验）建议安装在默认目录

（2）cuDNN7.5		拷贝到 C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0

（3）到`C:\ProgramData\NVIDIA Corporation\CUDA Samples\v10.0`中打开项目。

一共161个，都编译成功即可。（打开目录中的vs2017，并保存）

（4）pip install tensorflow-gpu==1.13.1 -i https://pypi.tuna.tsinghua.edu.cn/simple

出现：

distributed 1.21.8 requires msgpack

pip install msgpack -i https://pypi.tuna.tsinghua.edu.cn/simple

（5）更新常见库

pip install --upgrade numpy -i https://pypi.tuna.tsinghua.edu.cn/simple

pip install --upgrade scipy -i https://pypi.tuna.tsinghua.edu.cn/simple

pip install --upgrade pandas -i https://pypi.tuna.tsinghua.edu.cn/simple

pip install --upgrade keras -i https://pypi.tuna.tsinghua.edu.cn/simple

pip install --upgrade matplotlib -i https://pypi.tuna.tsinghua.edu.cn/simple

（6）测试安装正确性：

\>>> import tensorflow as tf 

\>>> hello = tf.constant('Hello, TensorFlow!') 

\>>> sess = tf.Session() 

\>>> print(sess.run(hello))
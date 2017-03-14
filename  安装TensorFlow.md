#MAC上基于VirtualEnv安装TensorFlow

> TensorFlow是一个采用数据流图（data flow graphs），用于数值计算的开源软件库，一个用于人工智能的开源神器。

1,首先，安装所有必备工具：

```
$ sudo easy_install pip  # 如果还没有安装 pip
$ sudo pip install --upgrade virtualenv

```
2,接下来, 建立一个全新的 virtualenv 环境. 为了将环境建在 ~/tensorflow 目录下, 执行:

```
$ virtualenv --system-site-packages ~/tensorflow
$ cd ~/tensorflow

```
3,激活virtualenv：

```
$ source bin/activate  # 如果使用 bash
$ source bin/activate.csh  # 如果使用 csh
(tensorflow)$  # 终端提示符应该发生变化，以(tensorflow)开头

```
4,在virtualenv内，安装TensorFlow：

```
# Mac OS X, CPU only, Python 2.7:
(tensorflow)$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.0.0-py2-none-any.whl

# Mac OS X, GPU enabled, Python 2.7:
(tensorflow)$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/gpu/tensorflow_gpu-1.0.0-py2-none-any.whl

# Mac OS X, CPU only, Python 3.4 or 3.5:
(tensorflow)$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.0.0-py3-none-any.whl

# Mac OS X, GPU enabled, Python 3.4 or 3.5:
(tensorflow)$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/mac/gpu/tensorflow_gpu-1.0.0-py3-none-any.whl

安装TensorFlow:
# Python 2
(tensorflow)$ pip install --upgrade $TF_BINARY_URL

# Python 3
(tensorflow)$ pip3 install --upgrade $TF_BINARY_URL

```
此步骤可能会遇到错误：

**Operation not permitted**

如果你用sudo,你应该会遇到下面的错误提示：
```
Installing collected packages: setuptools, protobuf, wheel, numpy, tensorflow
Found existing installation: setuptools 1.1.6
Uninstalling setuptools-1.1.6:
Exception:
...
[Errno 1] Operation not permitted:
```

解决方法：

pip install --ignore-installed --upgrade $TF_BINARY_URL


**SSLError: SSL_VERIFY_FAILED**

```
SSLError: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed

```
解决方法：
此时需要手工在[这个链接](https://github.com/tensorflow/tensorflow)中下载安装whl文件，然后用sudo pip install tensorflow-0.9.0-cp27-none-linux_x86_64.whl，即可安装

5,运行TensorFlow程序：

```
(tensorflow)$ cd tensorflow/models/image/mnist
(tensorflow)$ python convolutional.py

# 当使用完 TensorFlow
(tensorflow)$ deactivate  # 停用 virtualenv

$  # 你的命令提示符会恢复原样
```
6,尝试你的第一个TensorFlow程序：

```
打开一个python终端：
$ python

>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print sess.run(hello)
Hello, TensorFlow!
>>> a = tf.constant(10)
>>> b = tf.constant(32)
>>> print sess.run(a+b)
42
>>>

```
此步骤可能遇到错误：

**No module named protobuf**

安装完以后，在Python环境中，运行import tensorflow as tf，如果出现ImportError: No module named protobuf错误

解决方法：请先卸载pip uninstall protobuf，然后重新装一遍既可以使用。

##总结
至此你就成功安装了TensorFlow,开启你的TensorFlow研究学习之旅吧。
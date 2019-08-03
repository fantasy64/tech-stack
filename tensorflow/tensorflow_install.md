[https://www.tensorflow.org/tutorials/images/image\_recognition?hl=zh-cn](https://www.tensorflow.org/tutorials/images/image_recognition?hl=zh-cn)

一：创建虚拟环境

创建一个新的虚拟环境，方法是选择 Python 解析器并创建一个./venv目录来存放它：

```python
virtualenv --system-site-packages -p python3 ./venv
```

使用特定于 shell 的命令激活该虚拟环境：

```python
source ./venv/bin/activate  # sh, bash, ksh, or zsh
```

当 virtualenv 处于有效状态时，shell 提示符带有\(_**venv**_\)前缀。

在不影响主机系统设置的情况下，在虚拟环境中安装软件包。首先升级pip：

```python
pip install --upgrade pip

pip list  # show packages installed within the virtual environment
```

之后要退出 virtualenv，请使用以下命令：

```python
deactivate  # don't exit until you're done using TensorFlow
```

二、在虚拟环境中安装tensorflow

再虚拟环境中安装：

```py
(venv) ➜  /Users/fantasy >pip install --upgrade tensorflow
```

通过下面的语句验证：

```py
python -c "import tensorflow as tf;print(tf.reduce_sum(tf.random.normal([1000,1000])))"
```

三、试验教程

[https://www.tensorflow.org/tutorials/keras/basic\_classification](https://www.tensorflow.org/tutorials/keras/basic_classification)

1、matplotlib 没有安装的问题

```Python
(venv) ➜  /Users/fantasy/venv/src >pip install matplotlib
```

2、安装好matplotlib运行还有报错，但是已经出结果了

```
(venv) ➜  /Users/fantasy/venv/src > python fashion_mnist.py
Unable to revert mtime: /Library/Fonts
1.14.0
```

上面这个错误的原因：暂时没找到

3、keras可以自动下载数据，下载的数据保存在哪里？

```Python
#在用户目录下.keras目录下
➜  /Users/fantasy/.keras/datasets > ls
fashion-mnist mnist.npz
```

4、模块训练好了，如何保存和恢复。

Keras 使用[HDF5](https://en.wikipedia.org/wiki/Hierarchical_Data_Format)标准提供基本的保存格式。对于我们来说，可将保存的模型视为一个二进制 blob。

理论上把这个模型拷贝到其它机器也是可以加载起来运行的。

```Python
#先安装依赖
pip install -q h5py pyyaml

#训练好模型后保存整个模型：
>>> model.save('my_model.h5')

#重新加载模型
>>> new_model = keras.models.load_model('my_model.h5')
```




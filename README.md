# TibetanMNIST：藏文手写数字数据集

> TibetanMNIST：国产MNIST数据集

这个Repo主要包括了：
- [TibetanMNIST：藏文手写数字数据集](#tibetanmnist藏文手写数字数据集)
  - [1. 数据集描述](#1-数据集描述)
  - [2. 不同方法与框架实现各种脑洞](#2-不同方法与框架实现各种脑洞)


## 1. 数据集描述

> 详细请见：[数据集文档](https://github.com/bat67/TibetanMNIST/tree/master/Datasets)


* 数据文化

	藏区按方言划分为卫藏、康巴、安多三大藏区，东接汉地九州。藏区有典：“法域卫藏、人域康巴、马域安多”即“卫藏的宗教、康巴的人、安多的马”。而藏文主要有楷体和形体两种文字，我们本次的TibetanMNIST正是形体藏文中的数字，也就是图片中连笔书写更加简洁的那种

	![pic1](https://github.com/bat67/TibetanMNIST/blob/master/assets/1.png)

	
* 文件列表

	i.TibetanMNIST.tfrecords（每张图像存储为28x28x3的三通道图像矩阵）

	ii.TibetanMNIST.npz（每张图像存储为28x28的单通道图像矩阵）

	iii.TibetanMNIST（原始图像文件，图像文件名的第一个数字为数字类别标签，第二个数字为数字所在纸张标签，第三个数字为纸张标签内的数字序列）

* 数据特征及属性

	![pic2](https://github.com/bat67/TibetanMNIST/blob/master/assets/2.jpg)

* 数据分布

	![pic3](https://github.com/bat67/TibetanMNIST/blob/master/assets/3.jpg)

* 藏文数字与阿拉伯数字对照表

	![pic4](https://github.com/bat67/TibetanMNIST/blob/master/assets/4.jpg)

* 数据示例

	![pic5](https://github.com/bat67/TibetanMNIST/blob/master/assets/5.jpg)

* 数据使用

	* TFReords文件使用
	
	```python
	import tensorflow as tf

	def _parse_function(example_proto):
		features = {
			'label':tf.FixedLenFeature([], tf.int64),
			'img_raw':tf.FixedLenFeature([], tf.string)
		}

		parsed_features = tf.parse_single_example(example_proto, features)
		img = tf.decode_raw(parsed_features['img_raw'], tf.uint8)
		img = tf.reshape(img, [28, 28, 3])
		# 在流中抛出img张量和label张量
		img = tf.cast(img, tf.float32) / 255
		label = tf.cast(parsed_features['label'], tf.int32)
		return img, label

	filenames = ["要读取的文件序列"]
	dataset = tf.data.TFRecordDataset(filenames)
	dataset = dataset.map(_parse_function)
	# 创建单次迭代器
	iterator = dataset.make_one_shot_iterator()
	# 读取图像数据、标签值
	image, label = iterator.get_next()
	
	```

	* NPZ文件读取
	
	```python
	import numpy as np

	data = np.load('文件')
	x_train = data['image'].reshape(17768, 784)
	y_train = utils.to_categorical(data['label'], 10)
	```

* 数据来源
	
	中央民族大学创业团队巨神人工智能科技
	
* 使用注意

	本数据集版权归中央民族大学所有，使用该数据请务必注明数据出处，否则我们将追究相应的法律责任！

## 2. 不同方法与框架实现各种脑洞

> 除了自己写的，剩余皆来自[此网站](https://www.kesci.com/home/dataset/5bfe734a954d6e0010683839/document)，若下面链接打不开可自行下载根目录中文件本地打开。

* [【刷榜】训练集 99.9799%，测试集 99.3467%](https://github.com/bat67/TibetanMNIST/blob/master/【刷榜】训练集%2099.9799%25%EF%BC%8C测试集%2099.3467%25.ipynb)
* [【官方示例】手写藏文MNIST数据集的图像分类](https://github.com/bat67/TibetanMNIST/blob/master/【官方示例】手写藏文MNIST数据集的图像分类.ipynb)
* [[深度思考]TibetanMNIST藏文手写数字数据集识别](https://github.com/bat67/TibetanMNIST/blob/master/%5B深度思考%5DTibetanMNIST藏文手写数字数据集识别.ipynb)
* [准确率99.3%——Keras进行藏文手写数字识别](https://github.com/bat67/TibetanMNIST/blob/master/准确率99.3%25——Keras进行藏文手写数字识别.ipynb)
* [【牛刀小试】2018快过去了，你会写藏文了吗](https://github.com/bat67/TibetanMNIST/blob/master/【牛刀小试】2018快过去了%EF%BC%8C你会写藏文了吗.ipynb)
* [不要怂，就是GAN！AI学藏文](https://github.com/bat67/TibetanMNIST/blob/master/不要怂%EF%BC%8C就是GAN%EF%BC%81AI学藏文.ipynb)
* [简单的BP神经网络](https://github.com/bat67/TibetanMNIST/blob/master/简单的BP神经网络.ipynb)
* [利用Keras识别TibetanMNIST数据集](https://github.com/bat67/TibetanMNIST/blob/master/利用Keras识别TibetanMNIST数据集.ipynb)
* [自定义图片数据集识别(使用PaddlePaddle)](https://github.com/bat67/TibetanMNIST/blob/master/额外篇一%20%20自定义图片数据集识别.ipynb)




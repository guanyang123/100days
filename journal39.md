2019/7/16
===========  
1、`什么是tensorflow?`  
Tensorflow 支持异构设备分布式计算。`异构设备`: 指CPU、GPU 等核心进行有效地协同合作。与只依靠CPU相比，性能更高，功耗更低。
`分布式`: 分布式架构的目的在于帮助我们调度和分配计算资源, 使得上千万、上亿数据量的模型能够有效地利用机器资源进行计算。TensorFlow的数据中央控制单元是`tensor`(张量)，一个tensor由一系列的原始值组成，这些值被形成一个`任意维数的数组`。  

2、`mnist = tf.keras.datasets.mnist  
(x_train, y_train),(x_test, y_test) = mnist.load_data()`  为keras自带的MNIST数据集加载方法。MNIST，是一个收录了许多 28 x 28 像素手写数字图片（以灰度值矩阵存储）及其对应的数字的数据集。

3、`plt.imshow()`函数负责对图像进行处理，并显示其格式，但是不能显示。其后跟着plt.show()才能显示出来

4、`imshow()`函数格式为：matplotlib.pyplot.imshow(X, cmap=None)，X: 要绘制的图像或数组。cmap: 颜色图谱（colormap), 默认绘制为RGB(A)颜色空间。例如：matplotlib.pyplot.imshow(img, cmap=jet)

5、#`tf.keras.utils.normalize()函数`，对数据进行归一化处理，1表示横轴，方向从左到右；0表示纵轴，方向从上到下。当axis=1时，数组的变化是横向的，而体现出来的是列的增加或者减少。

6、`Keras`是一个搭积木式的深度学习框架，用它可以很方便且直观地搭建一些常见的深度学习模型。

7、`kears  model.compile()函数`用来配置模型
！[image text](https://github.com/guanyang123/100days/blob/master/image/39.3.PNG)

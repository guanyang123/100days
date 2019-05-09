2019/5/9
===========
1、[SVM简介](http://www.360doc.com/content/18/1223/21/2005961_803872797.shtml)

2、[SVC模块简介](https://blog.csdn.net/aq_cainiao_aq/article/details/76025601)

3、`matplotlib`画图时颜色不够用，用`colormap`实现颜色列表,可以使用其他的颜色

4、`meshgrid`为绘图创建了某种坐标网格,根据输入的坐标向量生成对应的坐标矩阵，可以接受两个一维数组生成两个二维矩阵，对应两个数组中所有的(x,y)对。
以0.01的步伐在X轴上取点：np.arange(start=X_set[:,0].min()-1, stop=X_set[:,0].max()+1, step=0.01)
以0.01的步伐在Y轴上取点：np.arange(start=X_set[:,1].min()-1, stop=X_set[:,1].max()+1, step = 0.01)
    [meshgrid介绍](https://www.cnblogs.com/black-mamba/p/9186965.html)
    [机器学习第13天代码及解释](https://blog.csdn.net/STILLxjy/article/details/86515408)

5、假设A是一个 m 行 n 列的矩阵；
   `A.min(0) `: 返回A每一列最小值组成的一维数组；
   `A.min(1)`：返回A每一行最小值组成的一维数组；
   `A.max(0)`：返回A每一列最大值组成的一维数组；
   `A.max(1)`：返回A每一行最大值组成的一维数组；  
 
6、`arange()`是Numpy库中的函数，其返回值是数组对象，常用于循环；
 [numpy.arange()用法](https://blog.csdn.net/eurus_/article/details/82215877)

7、[plt.contourf()用法](https://blog.csdn.net/lens___/article/details/83960810)

8、`numpy.array()`用来创建一维数组或多维数组。在numpy模块中，我们经常会使用resize 和 reshape,在具体使用中，通常是使用`resize`改变数组的尺寸大小，使用`reshape`用来增加数组的维度。`shape`函数是numpy.core.fromnumeric中的函数，它的功能是`读取矩阵的长度`，比如shape[0]就是读取矩阵第一维度的长度。它的输入参数可以使一个整数表示维度，也可以是一个矩阵。

9、[enumerate()说明](https://www.cnblogs.com/dylancao/p/7871558.html)

10、对于一维数组或者列表，`unique`函数去除其中重复的元素，并按元素由大到小返回一个新的无元素重复的元组或者列表
[元组介绍](https://www.runoob.com/python/python-tuples.html)

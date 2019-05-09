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
   

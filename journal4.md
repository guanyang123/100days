2019/4/25
===========  
1、`KNeighborsClassifier算法`简称`KNN算法`：K最近邻分类算法的核心思想是如果一个样本在特征空间中的k个最相似（即特征空间中最邻近）的样本中的大多数属于某一个类别，则该样本也属于这个类别。KNN算法可以用于多分类，KNN算法不仅可以用于分类，还可以用于回归。通过找出一个样本的K个最近邻居，将这些邻居的属性的平均值赋给该样本，作为预测值。  

2、KNeighborsClassifier在`sklearn.neighbors`包之中，KNeighborsClassifier使用很简单，散步：（1）创建KNeighborsClassifier对象，（2）调用fit函数,(3)调用predict函数进行预测。  

![KNN用法](https://blog.csdn.net/hjh00/article/details/63808075)  
![KNN算法的参数](https://blog.csdn.net/d12340555hf/article/details/80075150)



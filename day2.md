100days
===========
day2 简单线性回归模型
___________
```python
  #第一步 数据预处理
  #matplotlib.pyplot是一个命令型函数集合，它可以让我们像使用MATLAB一样使用matplotlib，用来绘图。
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  
  #导入数据库;读取csv文件  read_csv()方法： 从文件，url，文件型对象中加载带分隔符的数据。默认分隔符为逗号  
  dataset = pd.read_csv('studentscores.csv') 
  #全部行or列；[a]第a行or列  iloc[前闭后开]方法：通过行号获取行数据，不能是字符；输出所有行第0列的内容
  X = dataset.iloc[:,:1].values      
  #print("X为: " + str(X))
  #输出所有行第1列的内容
  Y = dataset.iloc[:,1].values       
  #print("Y为: " + str(Y))
  
  #拆分数据集为训练集合和测试集合
  from sklearn.model_selection import train_test_split
  #train_test_split函数用于将矩阵随机划分为训练子集和测试子集，并返回划分好的训练集测试集样本和训练集测试集标签。
  X_train, X_test, Y_train, Y_test=train_test_split(X, Y, test_size=1/4, random_state=0)
  #print("X_train为: "+str(X_train))
  #print("X_test为: "+str(X_test))
  
  #第二步 对训练集应用简单的线性回归模型
  #LinerRegression:线性回归，线性回归是最典型的回归问题，其目标值与所有的特征之间存在线性关系。
  from sklearn.linear_model import LinearRegression
  regressor = LinearRegression()
  #fit():求得训练集X_train,Y_train的均值,方差，最大值，最小值为训练集固有的属性
  regressor = regressor.fit(X_train, Y_train)
  #coef_存放回归系数，intercept_存放截距
  #print("regressor.coef_为："+str(regressor.coef_))
  #print("regressor.intercept_为："+str(regressor.intercept_))

  #第三步 预测结果
  #predict():预测测试集类别,参数为测试集。
  Y_pred = regressor.predict(X_test)
  #print("Y_pred为："+str(Y_pred))

  #第四步 绘图
  #可视化训练集结果
  plt.figure(1)
  plt.xlabel('Hours')
  plt.ylabel('Scores')
  plt.title('machine')
  #scatter():绘制散点图，格式:scatter(x, y, s, color，marker)
  plt.scatter(X_train, Y_train, color='red')
  #绘制(实线、破折线、点划线、虚线、无线条)图，格式:plt.plot(x, y, data, format_string, **kwargs)。
  plt.plot(X_train, regressor.predict(X_train), color='blue')
  #可视化测试集结果
  plt.figure(2)
  plt.scatter(X_test, Y_test, color='red')
  plt.plot(X_test, regressor.predict(X_test), color='blue')
  #显示图形
  plt.show() 
```
figure 1
===========
  ![image text](https://github.com/guanyang123/100days/blob/master/image/2.6.png)  
figure 2
===========
  ![image text](https://github.com/guanyang123/100days/blob/master/image/2.7.PNG)

  
  
  
  

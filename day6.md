100days
===========
day6 逻辑回归
___________
 ```python
# 第一步 数据预处理
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# 导入数据库
df = pd.read_csv('Social_Network_Ads.csv')
# print("表格为：\n"+str(df))
# 取所有行的第2行到第三行的数据
X = df.iloc[:, 2:4].values
# print("X：\n"+str(X))
# 取所有行第4列的数据
Y = df.iloc[:, 4].values
# print("Y：\n"+str(Y))

# 拆分数据集为训练集合和测试集合
from sklearn.model_selection import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split(
    X, Y, test_size=0.25, random_state=0)

# 特征量化，标准化数据
from sklearn.preprocessing import StandardScaler
# StandardScaler()函数用来标准化数据，计算训练集的平均值和标准差，一遍测试数据集使用相同的变换
scaler = StandardScaler()
# fit_transform(trainData)方法对部分数据先拟合，找到整体指标，然后对数据进行转换，实现数据的标准化、归一化
X_train = scaler.fit_transform(X_train)
X_test = scaler.fit_transform(X_test)

# 第二步 训练
from sklearn.linear_model import LogisticRegression
lr = LogisticRegression()
# fit():求得训练集的均值为训练集的固有属性
lr = lr.fit(X_train, Y_train)
# print("lr：\n"+str(lr))

# 第三步 预测
# predict():预测测试集类别，参数为测试集
Y_pred = lr.predict(X_test)
# print("Y_pred：\n"+str(Y_pred))

# 第四步 评估预测结果
from sklearn.metrics import confusion_matrix
confusion_matrix(Y_test, Y_pred)
# print("confusion_matrix(Y_test,Y_pred)：\n"+str(confusion_matrix(Y_test,Y_pred)))
 
 
 
 
 
 
 
 
 
 ```

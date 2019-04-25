100days
===========
day11 KNN
___________
 ```python
 # 第一步数据预处理
import pandas as pd
import numpy as np

# 导入数据库
df = pd.read_csv('Social_Network_Ads.csv')
# print("df=\n"+str(df))
# 取所有行的第二列第三列的数据
X = df.iloc[:, 2:4].values
# 取所有行第四列的数据
Y = df.iloc[:, 4].values
# print("X=\n"+str(X))
# print("Y=\n"+str(Y))

# 把数据集分为训练集和测试集
from sklearn.model_selection import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split(
    X, Y, test_size=0.25, random_state=0)

# 特征量化，标准化数据
from sklearn.preprocessing import StandardScaler
# StandardScaler()函数用来标准化数据，计算训练集的平均值和标准差，以便测试数据集使用相同的变换
scaler = StandardScaler()
# fit_transform(trainData)方法对部分数据先拟合，找到整体指标，然后对数据进行转换，实现数据的标准化、归一化
X_train = scaler.fit_transform(X_train)
X_test = scaler.fit_transform(X_test)

# 第二步 将KNN应用于训练集
from sklearn.neighbors import KNeighborsClassifier
# n_neighbors(k)是最近邻居的数目,metric是矩阵，默认为minkowski,p是用于Minkowski
# metric(闵可夫斯基空间)的超参数
k = 5
neigh = KNeighborsClassifier(n_neighbors=k, metric='minkowski', p=2)
neigh.fit(X_train, Y_train)

# 第三步 预测结果
# predict():预测测试集类别，参数为测试集。
Y_pred = neigh.predict(X_test)
# print("X_test=\n"+str(X_test))

# 评估预测结果
from sklearn.metrics import confusion_matrix
# confusion_matrix是混淆矩阵函数
cm = confusion_matrix(Y_test, Y_pred)
print("confusion_matrix(Y_test,Y_pred)：\n" +
      str(confusion_matrix(Y_test, Y_pred)))
 
 ```

# 100days
===========
##数据预处理
___________
#第一步 导入库
import numpy as np
import pandas as pd

#第二步 导入数据库
dataset=pd.read_csv('Data.csv')   #读取csv文件
X=dataset.iloc[:,:-1].values      #:全部行 or 列；[a]第a行or列

#第三步 处理丢失数据
from sklearn.preprocessing import Imputer
imputer=Imputer(missing_values="NaN",strategy="mean",axls=0)
imputer=imputer.fit(X[:1,1:3])

#第四步 解决分类数据
from sklearn.preprocessing import LabelEncoder
labelencoder_X=LabelEncoder()
X[:,0]=labelencoder_X.fit_transform(X[:,0])
#创建虚拟变量
onehotencoder=OneHotEncoder(categorical_features=[0])
X=onehotencoder.fit_transform(X).toarray()
labelencoder_Y=LabelEncoder()
Y=labelencoder_Y.fit_transform(Y)

#第五步 拆分数据集为训练集合和测试集合
from sklearn.model_selection import train_test_split
X_train,X_test,Y_train,Y_test=train_test_split(X,Y,test_size=0.2,random_state=0)

#第六步 特征量化
from sklearn.preprocessing import StandardScaler
sc_X=StandardScaler()
X_train=sc_X.fit_transform(X_train)
X_test=sc_X.transform(X_test)

100days
===========
day3
___________
```python
    # 第一步 数据预处理
    import pandas as pd
    import numpy as np

    dataset = pd.read_csv('50_Startups.csv')
    # print("dataset为：\n"+str(dataset))
    # 输出所有行第0列到倒数第二列的内容
    X = dataset.iloc[:, :-1].values
    # print("X为：\n"+str(X))
    # 输出所有行第四列的内容
    Y = dataset.iloc[:, 4].values
    # print("Y为：\n"+str(Y))

    # LabelEncoder()是标签编码，即是对不连续的数字或者文本进行编号，转换成连续的数值型变量，从0开始编码。
    # OneHotEncoder()即独热编码，直观的来看就是有几个需要编码的状态就有几个比特；categorical_features是需要独热编码的列索引
    from sklearn.preprocessing import LabelEncoder, OneHotEncoder
    labelencoder = LabelEncoder()
    # fit_transform(trainData)对部分数据先拟合fit，然后对该trainData进行转换transform，从而实现数据的标准化、归一化等等。
    # X[:,0]即取数组X所有行第0列的数据
    X[:, 3] = labelencoder.fit_transform(X[:, 3])
    # print("X[:,3]为："+str(X[:,3]))
    onehotencoder = OneHotEncoder(categorical_features=[3])
    # toarray():按适当顺序（从第一个到最后一个元素）返回包含此列表中所有元素的数组。
    X = onehotencoder.fit_transform(X).toarray()
    # print("X为(toarray之后打印的）：\n"+str(X))
    Y = onehotencoder.fit_transform(X)
    # print("Y为(toarray之前打印的）：\n"+str(Y))

    # 躲避虚拟变量陷阱，取X的所有行的第一列到最后一列的数据
    X = X[:, 1:]
    # print("X(躲避)为：\n"+str(X))

    from sklearn.model_selection import train_test_split
    X_train, X_test, Y_train, Y_test = train_test_split(
      X, Y, test_size=0.2, random_state=0)

    # 第二步 在训练集上训练多元线性回归模型
    # LinerRegression:线性回归，线性回归是最典型的回归问题，其目标值与所有的特征之间存在线性关系。
    from sklearn.linear_model import LinearRegression
    regressor = LinearRegression()
    regressor.fit(X_train, Y_train)
    # coef_存放回归系数，intercept_存放截距
    # print("regressor.coef_为："+str(regressor.coef_))
    # print("regressor.intercept_为："+str(regressor.intercept_))

    # 第三步 预测
    # predict():预测测试集类别,参数为测试集。
    Y_pred = regressor.predict(X_test)
    # print("Y_pred为："+str(Y_pred))


```

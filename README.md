100days
===========
数据预处理
___________
    #第一步 导入库  
    import numpy as np        #numpy:以矩阵为基础的数学计算模块，纯数学。  
    import pandas as pd       #Pandas:属于一款很适合做数据分析的框架，可以理解成表格+时间戳,即表格容器。  
    #第二步 导入数据库  
    dataset=pd.read_csv('Data.csv')   #读取csv文件  read_csv()方法： 从文件，url，文件型对象中加载带分隔符的数据。默认分隔符为逗号  
    X=dataset.iloc[:,:-1].values      #全部行or列；[a]第a行or列  iloc[前闭后开]方法：通过行号获取行数据，不能是字符(输出所有行第0列到倒数第二列的内容)
    #print("X为: "+str(X))
    Y=dataset.iloc[:,3].values        #(输出所有行第三列的内容）
    print("Y为: "+str(Y))

    #第三步 处理丢失数据
    from sklearn.preprocessing import Imputer     #从sklearn.preprocessing模块中导入Imputer函数
    imputer=Imputer(missing_values="NaN",strategy="mean",axis=0)    #使用字符串'nan'来代替数据集中的缺失值;strategy采用均值策略,填补第0列;axis = 0指第0列，axis后面的值是指定一个轴做运算
    imputer=imputer.fit(X[:1,1:3])      #fit():求得训练集X的均值为训练集X固有的属性

    #第四步 解决分类数据
    from sklearn.preprocessing import LabelEncoder       #LabelEncoder()是标签编码，即是对不连续的数字或者文本进行编号，转换成连续的数值型变量
    labelencoder_X=LabelEncoder()
    X[:,0]=labelencoder_X.fit_transform(X[:,0])          #fit_transform(trainData)对部分数据先拟合fit，找到该part的整体指标，如均值、方差、最大值最小值等等（根据具体转换的目的），然后对该trainData进行转换transform，从而实现数据的标准化、归一化等等。
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

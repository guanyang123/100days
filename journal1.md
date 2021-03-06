2019/4/18
===========
把前三天里面的一些词汇，着重理解了一下。同时对这些词汇进行了比较细致的分析和解释。
___________
1、`train_test_split`函数用于将矩阵随机划分为训练子集和测试子集，并返回划分好的训练集测试集样本和训练集测试集标签。格式：
    `X_train,X_test, Y_train, Y_test=train_test_split(train_data,train_target,test_size=0.3, random_state=0)`；
    `random_state`:random_state：是随机数的种子。随机数种子：其实就是该组随机数的编号，在需要重复试验的时候，保证得到一组一样的随机数。当random_state=none、0、1、2、3等，是不同的划分规则。随机数的产生取决于种子，随机数和种子之间的关系遵从以下两个规则：种子不同，产生不同的随机数；种子相同，即使实例不同也产生相同的随机数；`train_data`：被划分的样本特征集,样本特征集就是包含样本特征的数据集`train_target`：被划分的样本标签;`test_size`：如果是浮点数，在0-1之间，表示样本占比；如果是整数的话就是样本的数量。
    
2、`scatter()`:绘制散点图，格式:scatter(x, y, s, color，marker)，这是最主要的几个用法,x和y是同为训练集或测试集，即`X_train,Y_train`(X_test,Y_test)。 如果括号中不写s=  c=则按默认顺序，写了则按规定的来，不考虑顺序；s(点的大小)默认为20；marker(标记)默认为`'o'`;`'o'`(英文状态下)。`scatter()`格式如图所示：
![image text](https://github.com/guanyang123/100days/blob/master/image/4.1.jpg)  
![image text](https://github.com/guanyang123/100days/blob/master/image/4.2.jpg)
    
3、`plot()`:绘制(实线、破折线、点划线、虚线、无线条)图，格式:plt.plot(x,y,data,format_string,**kwargs),
    x轴数据，y轴数据，`format_string`控制曲线的格式字串 ,format_string 由颜色字符，风格字符，和标记字符组成。`**kwargs`是键值参数, 相当于一个字典。[plot用法](https://blog.csdn.net/cjcrxzz/article/details/79627483)
   
4、`OneHotEncoder()`即[独热编码](https://zhuanlan.zhihu.com/p/39012149)，直观的来看就是有几个需要编码的状态就有几个比特；`categorical_features`是需要独热编码的列索引。首先`onehot`会增加三个虚拟变量，里面好多0导致矩阵使用稀疏矩阵存储，存储方式为`(x,y) value`的格式，`(x,y)`表示坐标，`value`表示值。不一定三个，这个`day`里的数据是三个
`toarray`之后就是换回原来的行列存储方式。toarray之前的结果
![image text](https://github.com/guanyang123/100days/blob/master/image/3.61.PNG)  
![image text](https://github.com/guanyang123/100days/blob/master/image/3.62.PNG)

5、`fit_transform(trainData)`对部分数据先拟合fit，找到该part的整体指标，如均值、方差、最大值最小值等等（根据具体转换的目的），
然后对该trainData进行转换transform，从而实现数据的标准化、归一化等等。`X[:,0]`即取数组X所有行第0列的数据

6、`虚拟变量陷阱 `:state只有三种取值，理论上2位二进制就可以表示，而这里用100,010,001三种表示。其实若把第一位统一去掉，变为00,10,01也是可以区分的。所以这里需要做一个处理：躲避虚拟变量陷阱，把第0列去掉了，如果不去除的话，多列之间有很强的相关性，可能对做分析有影响。如果有四个状态，也要去除一列，任何一列都可以。有个截距的问题，比如这去除第一个量之后的俩变量x1,x2，我们的线性回归模型是y=a*x1+b*x2+d，因为d的存在使得哪怕x1与x2都为0，预测值依然不会出问题


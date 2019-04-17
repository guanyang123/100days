2019/4/16
===========
1、`train_test_split`函数用于将矩阵随机划分为训练子集和测试子集，并返回划分好的训练集测试集样本和训练集测试集标签。格式：
    X_train,X_test, y_train, y_test=cross_validation.train_test_split(train_data,train_target,test_size=0.3, random_state=0)；
    `random_state`:其他参数一样的情况下你得到的随机数组每次都是不一样的；`train_data`：被划分的样本特征集；
    `train_target`：被划分的样本标签;`test_size`：如果是浮点数，在0-1之间，表示样本占比；如果是整数的话就是样本的数量。
    
2、`scatter()`:绘制散点图，格式:scatter(x, y, s, color，marker)，这是最主要的几个用法，
    如果括号中不写s=  c=则按默认顺序，写了则按规定的来，不考虑顺序；s(点的大小)默认为20；marker(标记)默认为`'o'`;`'o'`(英文状态下)。
    
3、`plot()`:绘制(实线、破折线、点划线、虚线、无线条)图，格式:plt.plot(x,y,data,format_string,**kwargs),
    x轴数据，y轴数据，`format_string`控制曲线的格式字串 ,format_string 由颜色字符，风格字符，和标记字符组成。`**kwargs`是键值参数，
    相当于一个字典。
    
4、`OneHotEncoder()`即独热编码，直观的来看就是有几个需要编码的状态就有几个比特；`categorical_features`是需要独热编码的列索引。首先onehot会增加三个虚拟变量，里面好多0导致矩阵使用稀疏矩阵存储，存储方式为(x,y) value的格式，(x,y)表示坐标，value表示值。不一定三个，这个day里的数据是三个
toarray之后就是换回原来的行列存储方式

 

5、`fit_transform(trainData)`对部分数据先拟合fit，找到该part的整体指标，如均值、方差、最大值最小值等等（根据具体转换的目的），
然后对该trainData进行转换transform，从而实现数据的标准化、归一化等等。`X[:,0]`即取数组X所有行第0列的数据

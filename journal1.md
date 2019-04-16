    `train_test_split`函数用于将矩阵随机划分为训练子集和测试子集，并返回划分好的训练集测试集样本和训练集测试集标签。格式：
        X_train,X_test, y_train, y_test=cross_validation.train_test_split(train_data,train_target,test_size=0.3, random_state=0)；
        random_state:其他参数一样的情况下你得到的随机数组每次都是不一样的；train_data：被划分的样本特征集；
        train_target：被划分的样本标签；test_size：如果是浮点数，在0-1之间，表示样本占比；如果是整数的话就是样本的数量

2019/7/17
=========== 
1、`cifar10` 是一个包含60000张图片的数据集。其中每张照片为32*32的彩色照片，每个像素点包括RGB三个数值，数值范围 0 ~ 255。所有照片分属10个不同的类别，分别是 'airplane', 'automobile', 'bird', 'cat', 'deer', 'dog', 'frog', 'horse', 'ship', 'truck',其中五万张图片被划分为训练集，剩下的一万张图片属于测试集。

2、`ImageDataGenerator()`是keras.preprocessing.image模块中的图片生成器，同时也可以在batch中对数据进行增强，扩充数据集大小，增强模型的泛化能力。比如进行旋转，变形，归一化等等。

3、`Sequential`序列惯性模型，序贯模型是函数式模型的简略版，为最简单的线性、从头到尾的结构顺序，不分叉。

4、`Dense`是全连接层，`Flatten`层用来将输入“压平”，即把多维的输入一维化，常用在从卷积层到全连接层的过渡。Flatten不影响batch的大小。`Activation` 是激活函数。`dropout`顾名思义就是丢弃，丢弃的是每一层的某些神经元。有什么作用呢？在DNN深度网络中过拟合问题一直存在，dropout技术可以在一定程度上防止网络的过拟合。`Conv2D` （卷积层）,`MaxPooling2D`（池化层）

5、[激活函数类型](https://blog.csdn.net/u012969412/article/details/70882296)

6、`pool_size`：整数或长为2的整数tuple，代表在两个方向（竖直，水平）上的下采样因子，如取（2，2）将使图片在两个维度上均变为原长的一半。为整数意为各个维度值相同且为该数字。

7、[model.fit](https://blog.csdn.net/a1111h/article/details/82148497)

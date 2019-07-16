2019/7/16
===========  
1、`什么是tensorflow?`  
Tensorflow 支持异构设备分布式计算。`异构设备`: 指CPU、GPU 等核心进行有效地协同合作。与只依靠CPU相比，性能更高，功耗更低。
`分布式`: 分布式架构的目的在于帮助我们调度和分配计算资源, 使得上千万、上亿数据量的模型能够有效地利用机器资源进行计算。TensorFlow的数据中央控制单元是`tensor`(张量)，一个tensor由一系列的原始值组成，这些值被形成一个`任意维数的数组`。  

2、mnist = tf.keras.datasets.mnist  
(x_train, y_train),(x_test, y_test) = mnist.load_data()  为keras自带的MNIST数据集加载方法



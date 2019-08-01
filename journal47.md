2019/7/24
# day47 深入研究Numpy2
## 花哨的索引
花哨的索引和前面那些简单的索引非常类 似，但是传递的是索引数组，而不是单个标量。
花哨的索引让我们能够快速获得并修改复 杂的数组值的子数据集。

### 1.花哨的索引在概念上非常简单，它意味着传递一个索引数组来一次性获得多个数组元素。
例如以下数组：
```python
In[1]: import numpy as np        
rand = np.random.RandomState(42) 
 
       x = rand.randint(100, size=10)
       print(x) 
 
[51 92 14 71 60 20 82 86 74 74]
```
假设我们希望获得三个不同的元素，可以用以下方式实现：
```python
In[2]: [x[3], x[7], x[2]] 
 
Out[2]: [71, 86, 14]
```
另外一种方法是通过传递索引的单个列表或数组来获得同样的结果：
```python
In[3]: ind = [3, 7, 4]
x[ind] 
 
Out[3]: array([71, 86, 60])
```
利用花哨的索引，结果的形状与索引数组的形状一致，而不是与被索引数组的形状一致：
```python
In[4]: ind = np.array([[3, 7],
[4, 5]])        
x[ind] 
 
Out[4]: array([[71, 86], 
[60, 20]])
```
花哨的索引也对多个维度适用。假设我们有以下数组：
```python
In[5]: X = np.arange(12).reshape((3, 4)) 
X 
 
Out[5]: array([[ 0,  1,  2,  3],
[ 4,  5,  6,  7],               
[ 8,  9, 10, 11]])
```
和标准的索引方式一样，第一个索引指的是行，第二个索引指的是列：
```python
In[6]: row = np.array([0, 1, 2])      
col = np.array([2, 1, 3])    
X[row, col] 
 
Out[6]: array([ 2,  5, 11])
```
这里需要注意，结果的第一个值是 X[0, 2]，第二个值是 X[1, 1]，第三个值是 X[2, 3]。 在花哨的索引中，
索引值的配对遵循 2.5 节介绍过的广播的规则。因此当我们将一个列向 量和一个行向量组合在一个索引中时，会得到一个二维的结果：
```python
In[7]: X[row[:, np.newaxis], col] 
 
Out[7]: array([[ 2,  1,  3],              
[ 6,  5,  7],               
[10,  9, 11]])
```
这里，每一行的值都与每一列的向量配对，正如我们看到的广播的算术运算：
```python
In[8]: row[:, np.newaxis] * col 
 
Out[8]: array([[0, 0, 0],             
[2, 1, 3],              
[4, 2, 6]])
```
这里特别需要记住的是，花哨的索引返回的值反映的是广播后的索引数组的形状，而不是 被索引的数组的形状。
### 2.　组合索引 
花哨的索引可以和其他索引方案结合起来形成更强大的索引操作：
```python
In[9]: print(X) 
 
[[ 0  1  2  3]  [ 4  5  6  7]  [ 8  9 10 11]]
```
可以将花哨的索引和简单的索引组合使用：
```python
In[10]: X[2, [2, 0, 1]] 
 
Out[10]: array([10,  8,  9])
```
也可以将花哨的索引和切片组合使用：
```python
In[11]: X[1:, [2, 0, 1]] 
 
Out[11]: array([[ 6,  4,  5],            
[10,  8,  9]])
```
更可以将花哨的索引和掩码组合使用：
```python
In[12]: mask = np.array([1, 0, 1, 0], dtype=bool)     
X[row[:, np.newaxis], mask] 
 

Out[12]: array([[ 0,  2],               
[ 4,  6],
[ 8, 10]])
```
索引选项的组合可以实现非常灵活的获取和修改数组元素的操作。
### 3.　示例：选择随机点 
花哨的索引的一个常见用途是从一个矩阵中选择行的子集。例如我们有一个 N×D 的矩阵，
表示在 D 个维度的 N 个点。以下是一个二维正态分布的点组成的数组：
```python
In[13]: mean = [0, 0]      
cov = [[1, 2],             
[2, 5]]        
X = rand.multivariate_normal(mean, cov, 100)   
X.shape 
 
Out[13]: (100, 2)
```

我们将利用花哨的索引随机选取 20 个点——选择 20 个随机的、不重复的索引值，并利用 这些索引值选取到原始数组对应的值：
```python
In[15]: indices = np.random.choice(X.shape[0], 20, replace=False)     
indices 
 
Out[15]: array([93, 45, 73, 81, 50, 10, 98, 94,  4, 64, 65, 89, 47, 84, 82,    
80, 25, 90, 63, 20]) 
 
In[16]: selection = X[indices]  # 花哨的索引      
selection.shape 
 
Out[16]: (20, 2)
```

这种方法通常用于快速分割数据，即需要分割训练 / 测试数据集以验证统计模型（详情请 参见 5.3 节）时，
以及在解答统计问题时的抽样方法中使用。
### 4.　用花哨的索引修改值
正如花哨的索引可以被用于获取部分数组，它也可以被用于修改部分数组。例如，假设我
们有一个索引数组，并且希望设置数组中对应的值：
```python
In[18]: x = np.arange(10)    
i = np.array([2, 1, 8, 4])       
x[i] = 99         
print(x) 
 
[ 0 99 99  3 99  5  6  7 99  9]
```
可以用任何的赋值操作来实现，例如：
```python
In[19]: x[i] -= 10      
print(x) 
 
[ 0 89 89  3 89  5  6  7 89  9]
```
不过需要注意，操作中重复的索引会导致一些出乎意料的结果产生，如以下例子所示：
```python
In[20]: x = np.zeros(10)        
x[[0, 0]] = [4, 6]      
print(x) 
 
[ 6.  0.  0.  0.  0.  0.  0.  0.  0.  0.]
```
4 去哪里了呢？这个操作首先赋值 x[0] = 4，然后赋值 x[0] = 6，因此当然 x[0] 的值为 6。
以上还算合理，但是设想以下操作：
```python
In[21]: i = [2, 3, 3, 4, 4, 4]     
x[i] += 1       
x 
 
Out[21]: array([ 6.,  0.,  1.,  1.,  1.,  0.,  0.,  0.,  0.,  0.])
```
你可能期望 x[3] 的值为 2，x[4] 的值为 3，因为这是这些索引值重复的次数。但是为什么 结果不同于我们的预想呢？从概念的角度理解，
这是因为 x[i] += 1 是 x[i] = x[i] + 1 的 简写。x[i] + 1 计算后，这个结果被赋值给了 x 相应的索引值。记住这个原理后，我们却 
发现数组并没有发生多次累加，而是发生了赋值，显然这不是我们希望的结果。
因此，如果你希望累加，该怎么做呢？你可以借助通用函数中的 at() 方法（在 NumPy 1.8 以后的版本中可以使用）来实现。进行如下操作：
```python
In[22]: x = np.zeros(10)
np.add.at(x, i, 1)
print(x) 
 
[ 0.  0.  1.  2.  3.  0.  0.  0.  0.  0.]
```
at() 函数在这里对给定的操作、给定的索引（这里是 i）以及给定的值（这里是 1）执行 的是就地操作。
另一个可以实现该功能的类似方法是通用函数中的 reduceat() 函数，你可 以在 NumPy 
文档中找到关于该函数的更多信息。
### 5.　示例：数据区间划分 
你可以用这些方法有效地将数据进行区间划分并手动创建直方图。例如，假定我们有 1000 个值，
希望快速统计分布在每个区间中的数据频次，可以用 ufunc.at 来计算：
```python
In[23]: np.random.seed(42)        
x = np.random.randn(100) 
 
        # 手动计算直方图      
        bins = np.linspace(-5, 5, 20)    
        counts = np.zeros_like(bins) 
 
        # 为每个x找到合适的区间      
        i = np.searchsorted(bins, x) 
 
        # 为每个区间加上1         
        np.add.at(counts, i, 1)
```        
计数数组 counts 反映的是在每个区间中的点的个数，即直方图分布：
```python
In[24]: # 画出结果        
plt.plot(bins, counts, linestyle='steps');
```
![图2-9 手动计算的直方图](https://github.com/liangju1996/100-days-of-ml-code/blob/master/%E5%9B%BE%E7%89%87/day47.png)
当然，如果每次需要画直方图你都这么做的话，也是很不明智的。这就是为什么 Matplotlib 提供了
plt.hist() 方法，该方法仅用一行代码就实现了上述功能：
```python
plt.hist(x, bins, histtype='step');
```
这个函数将生成一个和图2-9 几乎一模一样的图。为了计算区间，Matplotlib 将使用 np.histogram 函数，该函数的计算功能也和上面执行的计算类似。
接下来比较一下这两种 方法：
```python
In[25]: print("NumPy routine:")      
%timeit counts, edges = np.histogram(x, bins) 
 
        print("Custom routine:")        
        %timeit np.add.at(counts, np.searchsorted(bins, x), 1) 
 
NumPy routine: 10000 loops, best of 3: 97.6 µs per loop 
Custom routine: 10000 loops, best of 3: 19.5 µs per loop
```
可以看到，我们一行代码的算法比 NumPy 优化过的算法快好几倍！这是如何做到的呢？ 如果你深入np.histogram 
源代码（可以在IPython 中输入np.histogram?? 查看源代码）， 就会看到它比我们前面用过的简单的搜索和计数方法更复杂。
这是由于 NumPy 的算法更 灵活（需要适应不同场景），因此在数据点比较大时更能显示出其良好性能：
```python
In[26]: x = np.random.randn(1000000)         
print("NumPy routine:")        
%timeit counts, edges = np.histogram(x, bins) 
 
        print("Custom routine:") 

        %timeit np.add.at(counts, np.searchsorted(bins, x), 1) 
 
NumPy routine: 10 loops, best of 3: 68.7 ms per loop
Custom routine: 10 loops, best of 3: 135 ms per loop
```
以上比较表明，算法效率并不是一个简单的问题。一个对大数据集非常有效的算法并不总 是小数据集的最佳选择，反之同理（详情请参见 2.8.3 节）。但是自己编写这个算法的好处 是可以理解这些基本方法。你可以利用这些编写好的模块去扩展，以实现一些有意思的自 定义操作。将 Python 有效地用于数据密集型应用中的关键是，当应用场景合适时知道使用 np.histogram 这样的现成函数，当需要执行更多指定的操作时也知道如何利用更低级的功 能来实现。
## 数组的排序

### 1.　NumPy中的快速排序：np.sort和np.argsort 
尽管 Python 有内置的 sort 和 sorted 函数可以对列表进行排序，但是 NumPy 的 np.sort 函数实际上效率更高。默认情况下，np.sort 的排序算法是 快速排序，其算法复杂度为 [N log N ]，另外也可以选择归并排序和堆排序。对于大多数 应用场景，默认的快速排序已经足够高效了。
如果想在不修改原始输入数组的基础上返回一个排好序的数组，可以使用 np.sort：
```python
In[5]: x = np.array([2, 1, 4, 3, 5])     
np.sort(x) 
 
Out[5]: array([1, 2, 3, 4, 5])
```
如果希望用排好序的数组替代原始数组，可以使用数组的 sort 方法：
```python
In[6]: x.sort()       
print(x) 
 
[1 2 3 4 5]
```
另外一个相关的函数是 argsort，该函数返回的是原始数组排好序的索引值：
```python
In[7]: x = np.array([2, 1, 4, 3, 5])    
i = np.argsort(x)      
print(i) 
 
[1 0 3 2 4]
```
以上结果的第一个元素是数组中最小元素的索引值，第二个值给出的是次小元素的索引 值，以此类推。这些索引值可以被用于（通过花哨的索引）创建有序的数组：
```python
In[8]: x[i] 
 
Out[8]: array([1, 2, 3, 4, 5])
```
沿着行或列排序 
NumPy 排序算法的一个有用的功能是通过 axis 参数，沿着多维数组的行或列进行排序， 例如：
```python
In[9]: rand = np.random.RandomState(42)     
X = rand.randint(0, 10, (4, 6))      
print(X) 
 
[[6 3 7 4 6 9]  [2 6 7 4 3 7]  [7 2 5 4 1 7]  [5 1 4 0 9 5]] 
 
In[10]: 
# 对X的每一列排序       
np.sort(X, axis=0) 
 
Out[10]: array([[2, 1, 4, 0, 1, 5],       
[5, 2, 5, 4, 3, 7],            
[6, 3, 7, 4, 6, 7],            
[7, 6, 7, 4, 9, 9]]) 
 
In[11]:
# 对X每一行排序    
np.sort(X, axis=1) 
 
Out[11]: array([[3, 4, 6, 6, 7, 9],      
[2, 3, 4, 6, 7, 7],              
[1, 2, 4, 5, 7, 7],              
[0, 1, 4, 5, 5, 9]])
```
需要记住的是，这种处理方式是将行或列当作独立的数组，任何行或列的值之间的关系将 会丢失！
### 2.　部分排序：分隔 
有时候我们不希望对整个数组进行排序，仅仅希望找到数组中第K 小的值，NumPy 的 
np.partition 函数提供了该功能。np.partition 函数的输入是数组和数字 K，输出结果是 一个新数组，最左边是第 K 小的值，往右是任意顺序的其他值：
```python
In[12]: x = np.array([7, 2, 3, 1, 6, 5, 4])      
np.partition(x, 3) 
 
Out[12]: array([2, 1, 3, 4, 6, 5, 7])
```
请注意，结果数组中前三个值是数组中最小的三个值，剩下的位置是原始数组剩下的值。 在这两个分隔区间中，元素都是任意排列的。
与排序类似，也可以沿着多维数组任意的轴进行分隔：
```python
In[13]: np.partition(X, 2, axis=1) 
 
Out[13]: array([[3, 4, 6, 7, 6, 9],              
[2, 3, 4, 7, 6, 7],                
[1, 2, 4, 5, 7, 7],               
[0, 1, 4, 5, 9, 5]])
```
输出结果是一个数组，该数组每一行的前两个元素是该行最小的两个值，每行的其他值分 布在剩下的位置。
最后，正如 np.argsort 函数计算的是排序的索引值，也有一个 np.argpartition 函数计算 的是分隔的索引值，我们将在下一节中举例介绍它。
### 3.　示例：K个最近邻 
以下示例展示的是如何利用 argsort 函数沿着多个轴快速找到集合中每个点的最近邻。
首先，在二维平面上创建一个有10 个随机点的集合。按照惯例，将这些数据点放在一个 10×2 的数组中：
```python
In[14]: X = rand.rand(10, 2)
```

现在来计算两两数据点对间的距离。我们学过两点间距离的平方等于每个维度的距离差的 平方的和。
利用 NumPy 的广播（详情请参见 2.5 节）和聚合（详情请参见 2.4 节）功能， 可以用一行代码计算矩阵的平方距离：
```python
In[16]: dist_sq = np.sum((X[:,np.newaxis,:] - X[np.newaxis,:,:]) ** 2, axis=-1)
```
这个操作由很多部分组成。如果你对 NumPy 的广播规则不熟悉的话，可能这行代码看起 
来有些令人困惑。当你遇到这种代码时，将其各组件分解后再分析是非常有用的：
```python
In[17]:
# 在坐标系中计算每对点的差值      
differences = X[:, np.newaxis, :] - X[np.newaxis, :, :]     
differences.shape 
 
Out[17]: (10, 10, 2) 
 
In[18]: 
# 求出差值的平方        
sq_differences = differences ** 2     
sq_differences.shape 
 
Out[18]: (10, 10, 2) 
 
In[19]: 
# 将差值求和获得平方距离
dist_sq = sq_differences.sum(-1)   
dist_sq.shape 
 
Out[19]: (10, 10)
```
请再次确认以上步骤，应该看到该矩阵的对角线（也就是每个点到其自身的距离）的值 都是 0：
```python
In[20]: dist_sq.diagonal() 
 
Out[20]: array([ 0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.])
```
结果确实是这样的！当我们有了这样一个转化为两点间的平方距离的矩阵后，就可以使用 np.argsort
函数沿着每行进行排序了。最左边的列给出的索引值就是最近邻：
```python
In[21]: nearest = np.argsort(dist_sq, axis=1)       
print(nearest) 
 
[[0 3 9 7 1 4 2 5 6 8] 
[1 4 7 9 3 6 8 5 0 2] 
[2 1 4 6 3 0 8 9 7 5] 
[3 9 7 0 1 4 5 8 6 2]
[4 1 8 5 6 7 9 3 0 2]
[5 8 6 4 1 7 9 3 2 0] 
[6 8 5 4 1 7 9 3 2 0] 
[7 9 3 1 4 0 5 8 6 2] 
[8 5 6 4 1 7 9 3 2 0] 
[9 7 3 0 1 4 5 8 6 2]]
```
需要注意的是，第一列是按 0~9 从小到大排列的。这是因为每个点的最近邻是其自身，所 
以结果也正如我们所想。 如果使用全排序，我们实际上可以实现的比这个例子展示的更多。
如果我们仅仅关心 k 个 最近邻，那么唯一需要做的是分隔每一行，这样最小的k + 1的平方距离将排在
最前面， 其他更长的距离占据矩阵该行的其他位置。可以用 np.argpartition 函数实现：
```python
In[22]: K = 2    
nearest_partition = np.argpartition(dist_sq, K + 1, axis=1)
```
为了将邻节点网络可视化，我们将每个点和其最近的两个最近邻连接（如图 2-11 所示）：
```python
In[23]: plt.scatter(X[:, 0], X[:, 1], s=100) 
 
        # 将每个点与它的两个最近邻连接    
        K = 2 
 
        for i in range(X.shape[0]):     
        for j in nearest_partition[i, :K+1]:  
        # 画一条从X[i]到X[j]的线段           
        # 用zip方法实现：              
        plt.plot(*zip(X[j], X[i]), color='black')
```     
图 2-11：每个点的邻节点的可视化
图中每个点和离它最近的两个节点用连线连接。乍一看，你可能会奇怪为什么有些点的连 线多于两条，这是因为点
A 是点 B 最邻近的两个节点之一，但是并不意味着点 B 一定是 点 A 的最邻近的两个节点之一。
尽管本例中的广播和按行排序可能看起来不如循环直观，但是在实际运行中，Python 中 这类数据的操作会更高效。
你可能会尝试通过手动循环数据并对每一组邻节点单独进行排 序来实现同样的功能，但是这种方法和我们使用的向量化操作相比，
肯定在算法执行上效 率更低。并且向量化操作的优美之处在于，它的实现方式决定了它对输入数据的数据量并 不敏感。也就是说，
我们可以非常轻松地计算任意维度空间的 100 或 1 000 000 个邻节点， 而代码看起来是一样的。
最后还想提醒一点，做大数据量的最近邻搜索时，有几种基于树的算法的算法复杂度可 以实现接近 [N log N ]，
或者比暴力搜索法的 [N 2] 更好。其中一种就是KD-Tree，在 Scikit-Learn（http://bit.ly/2fSpdxI）中实现。

大 O 标记 
大 O 标记是一种描述一个算法对于相应的输入数据的大小需要执行的操作步骤数。要 
想正确使用它，需要深入理解计算机科学理论，并且将其和小 o 标记、大 θ 标记、大 Ω 标记以及其他混合变体区分开。
虽然区分这些概念可以提高算法复杂度计量的准确 性，但是除了在计算机科学理论和学究的博客评论外，实际中很少有这种区分。
在数 据科学中，更常见的还是不太严谨的大 O 标记——一种通用的（或许是不准确的）算 法复杂度的度量描述。
在这里要向相关的理论学家和学者致歉，本书中都会使用这种 表述方式。
如果不用太严谨的眼光看待大O 标记，那么它其实是告诉你：随着输入数据量的增 长，你的算法将花费多少时间。
如果你有一个 [N]（读作“N 阶”）复杂度的算法， 该算法花费1 秒钟来执行一个长度为N = 1000 的列表，那么它执行一个长度为N = 5000
的列表花费的时间大约是 5 秒钟。如果你有一个算法复杂度为 [N 2]（读作“N 的平方阶”），且该算法花费 1 秒钟来执行一个长度为 N = 1000 的列表
那么它执行一 个长度为 N = 5000 的列表花费的时间大约是 25 秒钟。 在计算算法复杂度时，N 通常表示数据集的大小（数据点的个数、维度的数目等）。
当 我们试图分析数十亿或数百万亿的数据时，算法复杂度为 [N] 和算法复杂度为 [N 2] 会有非常明显的差别！ 需要注意的是，
大 O 标记并没有告诉你计算的实际时间，而仅仅告诉你改变N 的值 时，运行时间的相应变化。通常情况下， [N] 复杂度的算法比 [N 2] 复杂度的算法更 高效。
但是对于小数据集，算法复杂度更优的算法可能未必更快。例如对于给定的问 题， [N 2] 复杂度的算法可能会花费 0.01 秒，而更“优异”的 [N] 复杂度的算法可
能会花费 1 秒。按照 1000 的因子将 N 倍增，那么 [N] 复杂度的算法将胜出。
即使是这个非严格版本的大 O 标记对于比较算法的性能也是非常有用的。我们将在本 书中用这个标记来测量算法复杂度。
## 　结构化数据：NumPy的结构化数组
大多数时候，我们的数据可以通过一个异构类型值组成的数组表示，但有时却并非如此。 本节介绍NumPy 的结构化数组和记录数组，它们为复合的、异构的数据提供了非常有 效的存储。尽管这里列举的模式对于简单的操作非常有用，但是这些场景通常也可以用 Pandas 的 DataFrame 来实现（将在第三章详细介绍）。
假定现在有关于一些人的分类数据（如姓名、年龄和体重），我们需要存储这些数据用于 Python 项目，那么一种可行的方法是将它们存在三个单独的数组中：
```python
In[2]: name = ['Alice', 'Bob', 'Cathy', 'Doug']  
age = [25, 45, 37, 19]       
weight = [55.0, 85.5, 68.0, 61.5]
```
但是这种方法有点笨，因为并没有任何信息告诉我们这三个数组是相关联的。如果可以用

一种单一结构来存储所有的数据，那么看起来会更自然。NumPy 可以用结构化数组实现这 种存储，这些结构化数组是复合数据类型的。
前面介绍过，利用以下表达式可以生成一个简单的数组：
```python
In[3]: x = np.zeros(4, dtype=int)
```
与之类似，通过指定复合数据类型，可以构造一个结构化数组：
```python
In[4]:
# 使用复合数据结构的结构化数组     
data = np.zeros(4, dtype={'names':('name', 'age', 'weight'),       
'formats':('U10', 'i4', 'f8')})      
print(data.dtype) 
 
[('name', '<U10'), ('age', '<i4'), ('weight', '<f8')]
```
这里 U10 表示“长度不超过 10 的 Unicode 字符串”，i4 表示“4 字节（即 32 比特）整型”， f8 表示“8 字节（即 64 比特）浮点型”。
后续的小节中将介绍更多的数据类型代码。
现在生成了一个空的数组容器，可以将列表数据放入数组中：
```python
In[5]: data['name'] = name     
data['age'] = age    
data['weight'] = weight 
print(data) 
 
[('Alice', 25, 55.0) ('Bob', 45, 85.5) ('Cathy', 37, 68.0)  ('Doug', 19, 61.5)]
```
正如我们希望的，所有的数据被安排在一个内存块中。
结构化数组的方便之处在于，你可以通过索引或名称查看相应的值：
```python
In[6]: 
# 获取所有名字     
data['name'] 
 
Out[6]: array(['Alice', 'Bob', 'Cathy', 'Doug'],      
dtype='<U10') 
 
In[7]: 
# 获取数据第一行  
data[0] 
 
Out[7]: ('Alice', 25, 55.0) 
 
In[8]: 
# 获取最后一行的名字   
data[-1]['name'] 
 
Out[8]: 'Doug'
```
利用布尔掩码，还可以做一些更复杂的操作，如按照年龄进行筛选：
```python
In[9]: 
# 获取年龄小于30岁的人的名字      
data[data['age'] < 30]['name'] 
 
Out[9]: array(['Alice', 'Doug'],    
dtype='<U10')
```
请注意，如果你希望实现比上面更复杂的操作，那么你应该考虑使用 Pandas 包，我们将在 下一章中详细介绍它。正如你将会看到的，Pandas 提供了一个 DataFrame 对象，该结构是 构建于 NumPy 数组之上的，提供了很多有用的数据操作功能，其中有些与前面介绍的类 似，当然也有更多没提过并且非常实用的功能。
### 1.　生成结构化数组 
结构化数组的数据类型有多种制定方式。此前我们看过了采用字典的方法：
```python
In[10]: np.dtype({'names':('name', 'age', 'weight'),          
'formats':('U10', 'i4', 'f8')}) 
 
Out[10]: dtype([('name', '<U10'), ('age', '<i4'), ('weight', '<f8')])
```
为了简明起见，数值数据类型可以用 Python 类型或 NumPy 的 dtype 类型指定：
```python
In[11]: np.dtype({'names':('name', 'age', 'weight'),               
'formats':((np.str_, 10), int, np.float32)}) 
 
Out[11]: dtype([('name', '<U10'), ('age', '<i8'), ('weight', '<f4')])
```
复合类型也可以是元组列表：
```python
In[12]: np.dtype([('name', 'S10'), ('age', 'i4'), ('weight', 'f8')]) 
 
Out[12]: dtype([('name', 'S10'), ('age', '<i4'), ('weight', '<f8')])
```
如果类型的名称对你来说并不重要，那你可以仅仅用一个字符串来指定它。在该字符串中 数据类型用逗号分隔：
```python
In[13]: np.dtype('S10,i4,f8') 
 
Out[13]: dtype([('f0', 'S10'), ('f1', '<i4'), ('f2', '<f8')])
```
简写的字符串格式的代码可能看起来令人困惑，但是它们其实基于非常简单的规则。
第 一个（可选）字符是 < 或者 >，分别表示“低字节序”（little endian）和“高字节序”（bid endian），
表示字节（bytes）类型的数据在内存中存放顺序的习惯用法。后一个字符指定的 是数据的类型：字符、字节、整型、浮点型，
等等。最后一个字符表示该 对象的字节大小。 

### 2.　更高级的复合类型
NumPy 中也可以定义更高级的复合数据类型。例如，你可以创建一种类型，其中每个元素 
都包含一个数组或矩阵。我们会创建一个数据类型，该数据类型用 mat 组件包含一个 3×3 的浮点矩阵：
```python
In[14]: tp = np.dtype([('id', 'i8'), ('mat', 'f8', (3, 3))])   
X = np.zeros(1, dtype=tp)      
print(X[0])       
print(X['mat'][0]) 
 
(0, [[0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0]]) 
[[ 0.  0.  0.]
[ 0.  0.  0.] 
[ 0.  0.  0.]]
```
现在 X 数组的每个元素都包含一个 id 和一个 3×3 的矩阵。为什么我们宁愿用这种方法存 储数据，也不用简单的多维数组，
或者 Python 字典呢？原因是 NumPy 的 dtype 直接映射 到 C 结构的定义，因此包含数组内容的缓存可以直接在 C 程序中使用。
如果你想写一个 Python 接口与一个遗留的 C 语言或 Fortran 库交互，从而操作结构化数据，你将会发现结 构化数组非常有用！
### 3.　记录数组：结构化数组的扭转 
NumPy 还提供了 np.recarray 类。它和前面介绍的结构化数组几乎相同，但是它有一个独 
特的特征：域可以像属性一样获取，而不是像字典的键那样获取。前面的例子通过以下代 码获取年龄：
```python
In[15]: data['age'] 
 
Out[15]: array([25, 45, 37, 19], dtype=int32)
```
如果将这些数据当作一个记录数组，我们可以用很少的按键来获取这个结果：
```python
In[16]: data_rec = data.view(np.recarray)      
data_rec.age 
 
Out[16]: array([25, 45, 37, 19], dtype=int32)
```
记录数组的不好的地方在于，即使使用同样的语法，在获取域时也会有一些额外的开销， 如以下示例所示：
```python
In[17]: %timeit data['age']      
%timeit data_rec['age']       
%timeit data_rec.age 
 
1000000 loops, best of 3: 241 ns per loop
100000 loops, best of 3: 4.61 µs per loop 
100000 loops, best of 3: 7.27 µs per loop
```
是否值得为更简便的标记方式花费额外的开销，这将取决于你的实际应用




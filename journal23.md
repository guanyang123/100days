2019/7/2
===========
  1、决策树是一种监督学习算法，主要用于声类问题，适用于分类和连续输入以及输出变量。决策树是一棵树，其中每个分支节点表示多个备选项之间的选择，每个叶节点表示一个决策。[什么是决策树]（https://blog.csdn.net/leiting_imecas/article/details/52950663##s1）  
  
  2、`ID3算法`： ID3算法将初始集合S作为根节点,在算法的每一步迭代中，其遍历集合中的每个为使用的属性，计算该属性的熵或信息增益。从中选择具有最小熵H(S)或最大信息增益IG(A)的属性。再用选定的属性将集合S分为不同的数据子集（例如年龄小于50岁，年龄在50~100岁之间，年龄大于50岁）。算法继续对每个子集进行递归处理，每次只考虑之前没有选定的属性。
   子集的递归过程在下述情况中会停止：
   1.子集中的每个元素属于同一类（+或-），则这个节点为叶节点并标记为实例所属的类；
   2.子集中没有更多的属性可以选择，而其中的实例仍不相同（有些为+，有些为-），则这个节点为叶节点并标记为子集中大部分实例所属的类；
   3.子集中没有实例，这种情况发生在父集中没有实例全符合选定属性的特殊值，例如，如果没有实例的年龄大于100岁。这时叶节点；被创建，并标记为父集中实例最常见的类。
   `整个算法中，决策树中的分支节点表示分割数据的选定数据，终端节点表示此分支最终子集的类标签。`
 
  3、[信息增益、熵的解释]（https://baike.sogou.com/v10807448.htm?fromTitle=id3%E7%AE%97%E6%B3%95）  
  
  4、`DecisionTreeClassifier用法`
    ![image text](https://github.com/guanyang123/100days/blob/master/image/25.1.PNG)
  
  